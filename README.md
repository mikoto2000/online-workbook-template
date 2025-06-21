# データベーススペシャリスト試験 問題集

DBスペシャリスト受験対策用のWeb問題集です。

## ファイル構成

- `index.html` - メインの問題集Webページ
- `questions.json` - 問題データファイル
- `questions-schema.json` - JSONスキーマ定義
- `README.md` - このファイル

## 対応問題形式

### 1. 単一選択問題（single_choice）
ラジオボタンで1つの選択肢を選ぶ形式

### 2. 複数選択問題（multiple_choice）  
チェックボックスで複数の選択肢を選ぶ形式

### 3. 記述式問題（essay）
テキストエリアで自由記述する形式

## questions.json の構造

### 基本構造
```json
{
  "sections": [
    {
      "id": "section-id",
      "title": "セクションタイトル", 
      "questions": [...]
    }
  ]
}
```

### 問題の定義

#### 単一選択問題の例
```json
{
  "id": "q1-1",
  "number": "問題 1-1",
  "type": "single_choice",
  "question": "問題文をここに記述",
  "choices": [
    { "value": "a", "text": "選択肢A" },
    { "value": "b", "text": "選択肢B" },
    { "value": "c", "text": "選択肢C" },
    { "value": "d", "text": "選択肢D" }
  ],
  "correct": "b",
  "explanation": "解説文をここに記述"
}
```

#### 複数選択問題の例
```json
{
  "id": "q1-2", 
  "number": "問題 1-2",
  "type": "multiple_choice",
  "question": "適切なものをすべて選択せよ",
  "choices": [
    { "value": "a", "text": "選択肢A" },
    { "value": "b", "text": "選択肢B" },
    { "value": "c", "text": "選択肢C" },
    { "value": "d", "text": "選択肢D" }
  ],
  "correct": ["a", "c", "d"],
  "explanation": "解説文をここに記述"
}
```

#### 記述式問題の例
```json
{
  "id": "q1-3",
  "number": "問題 1-3", 
  "type": "essay",
  "question": "○○について300字以内で説明せよ",
  "correct": "",
  "explanation": "【解答例】解答例をここに記述"
}
```

## 問題追加・編集方法

### 手動編集
1. `questions.json`ファイルを編集
2. スキーマに従って問題データを追加・修正
3. ブラウザでページを再読み込み

### ChatGPTを使用した自動生成

ChatGPTを使って効率的に問題を生成できます。詳細は[prompt-templates.md](prompt-templates.md)を参照してください。

#### 簡単な手順

1. **ChatGPTに初期設定を送信**
   ```
   あなたはデータベーススペシャリスト試験の問題作成者です。
   以下のJSONスキーマに従って、高品質な試験問題を作成してください。
   [スキーマの内容をコピー]
   ```

2. **分野別に問題を生成**
   ```
   データベース設計分野の問題を5問作成してください。
   【含めるべき内容】
   - 概念設計（E-R図、エンティティ、リレーションシップ）
   - 論理設計（正規化、テーブル設計）
   [詳細はprompt-templates.mdを参照]
   ```

3. **生成されたJSONを検証・配置**
   - JSONスキーマで検証
   - `questions.json`に配置
   - ブラウザで動作確認

**利点：**
- 大量の問題を短時間で生成
- 一定の品質を保った問題作成
- 多様な出題パターンの実現

## JSONスキーマ検証

`questions-schema.json`を使用してJSONファイルの妥当性を検証できます。

### VS Code での検証設定
`.vscode/settings.json`に以下を追加：

```json
{
  "json.schemas": [
    {
      "fileMatch": ["questions.json"],
      "url": "./questions-schema.json"
    }
  ]
}
```

### コマンドラインでの検証
Node.jsのajvパッケージを使用：

```bash
npm install -g ajv-cli
ajv validate -s questions-schema.json -d questions.json
```

## 機能

- レスポンシブデザイン（PC・タブレット・スマートフォン対応）
- セクション間のスムーズスクロール
- 解答表示/非表示切り替え
- 記述式問題の文字数カウンター
- 問題タイプの視覚的表示

## ブラウザ対応

- Chrome 60+
- Firefox 60+ 
- Safari 12+
- Edge 79+

## カスタマイズ

### スタイルの変更
`index.html`内の`<style>`セクションを編集してデザインをカスタマイズできます。

### 問題分野の追加
`questions.json`の`sections`配列に新しいセクションを追加するだけで新しい分野を追加できます。

### 選択肢数の変更
選択肢は最大8個（a-h）まで対応しています。

## ライセンス

このプロジェクトはMITライセンスの下で公開されています。詳細は[LICENSE](LICENSE)ファイルを参照してください。

### コンテンツライセンス
問題文・解説等のコンテンツは教育目的での利用を想定しています。実際の試験問題とは異なる独自作成の問題です。

## 免責事項

- このツールは学習支援を目的としており、試験の合格を保証するものではありません
- 実際の試験内容や出題傾向と異なる場合があります
- 利用者の責任において使用してください

## 貢献

問題の追加・修正・機能改善のプルリクエストを歓迎します。

1. このリポジトリをフォーク
2. 機能ブランチを作成 (`git checkout -b feature/amazing-feature`)
3. 変更をコミット (`git commit -m 'Add some amazing feature'`)
4. ブランチにプッシュ (`git push origin feature/amazing-feature`)
5. プルリクエストを作成