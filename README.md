# zenkaku2hankaku
Apexを使って全角のカタカナ数字テキストが入ってきたときに半角にします

手順
1. 全角カタカナ数字を～　とテスト用のApex～ を各自環境のApexクラスに作成。
2. テスト用のApex～をテスト実行。
3. 何事もなければフロー作成。
   レコードトリガーフローで条件を以下のように設定
3-1. 条件：レコードの作成・更新
   　　　数式がTrueになったら
   -*-*-数式-*-*-
      AND(
      NOT(ISBLANK($Record.対象項目__c)),
      OR(ISNEW(), ISCHANGED($Record.対象項目__c))
     )

3-2. テキスト型変数でvarNormalizedTextの作成
   
3-3. フローにアクションコンポーネントを追加し、Convert Full-width to Half-widthを追加。
inputtextを該当の項目
outputtextをvarNormalizedTextに設定

3-4.フローに決定コンポーネントを追加し、以下のように設定
   空でない場合　varNormalizedTex null false
   空である場合　varNormalizedTex null true

3-5. 空でない場合の遷移にレコードを更新コンポーネントを追加
   フローをトリガーしたレコードを使用
   対象項目　→　varNormalizedText

3-6. フローを新規で保存

4. きちんとフローが走るかテストする
