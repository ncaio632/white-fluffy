# アーキテクチャと状態遷移

**実行可能な要約。完全なインターフェースは[英語版](architecture.en.md)。稼働中のサーバーではない。**

一覧取得、秘密参照解決、資産権限照会、効果分類、境界評価、承認台帳、送信、監査を別モジュールにする。評価器は証拠とポリシーから判断だけを返し、送信しない。効果分類はレビュー済みローカル表と記述子ハッシュを使う。リモートの「読取り専用」というヒントを唯一の根拠にしない。

```text
NEW -> INVENTORY_CHECKED -> AUTHENTICATED -> ASSET_AUTHORIZED -> CLASSIFIED
CLASSIFIED -> READY (read)
CLASSIFIED -> AWAITING_APPROVAL -> APPROVED -> READY (write)
READY -> AUDIT_RECORDED -> DISPATCHING -> SUCCEEDED | FAILED | INDETERMINATE
pre-dispatch failure -> BLOCKED
```

送信直前にセッション、主体、期限、権限改訂を再確認する。書込み承認の消費と送信意図の記録を原子的に行う。監査記録に失敗したら送信前に停止する。意図記録後のクラッシュは効果の証明にならず、再起動時に読取りで照合する。

送信後のタイムアウトは `DISPATCH_UNKNOWN` とし、自動再送しない。対象やペイロードの変更は新しい承認を要する。認証失敗と権限拒否を混同せず、境界順で最初のエラーを返す。公開記録は秘密や実資産の対応表を含めない。
