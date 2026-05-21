# zenkaku2hankaku
Apexを使って全角のカタカナ数字テキストが入ってきたときに半角にします

手順
1. 全角カタカナ数字を～　とテスト用のApex～ を各自環境のApexクラスに作成。
2. テスト用のApex～をテスト実行。
3. 何事もなければフロー作成。
4. レコードトリガーフローで条件を以下のように設定
5. 条件：レコードの作成・更新
   　　　数式がTrueになったら
   -*-*-数式-*-*-
      AND(
      NOT(ISBLANK($Record.対象項目__c)),
      OR(ISNEW(), ISCHANGED($Record.対象項目__c))
     )

6. テキスト型変数でvarNormalizedTextの作成
   
7. フローにアクションコンポーネントを追加し、Convert Full-width to Half-widthを追加。
＊inputtextを該当の項目
＊outputtextをvarNormalizedTextに設定

8.フローに決定コンポーネントを追加し、以下のように設定
＊空でない場合　varNormalizedTex null false
＊空である場合　varNormalizedTex null true

9. 空でない場合の遷移にレコードを更新コンポーネントを追加
＊フローをトリガーしたレコードを使用
＊対象項目　→　varNormalizedText

10. フローを新規で保存

11. きちんとフローが走るかテストする
