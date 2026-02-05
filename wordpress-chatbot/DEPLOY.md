# WordPress更新サポートチャットボット - デプロイ手順

## 📋 準備したファイル

✅ `app_public.py` - 公開用（APIキーなし）
✅ `requirements.txt` - 必要なパッケージ
✅ `secrets.toml` - APIキー設定（Streamlit Cloud用）
✅ `.gitignore` - 秘密情報の除外設定

---

## 🚀 デプロイ手順（30分）

### ステップ1: GitHubリポジトリ作成（5分）

1. https://github.com/new にアクセス
2. 以下を入力：
   - Repository name: `wordpress-chatbot`
   - Public または Private（どちらでもOK）
3. 「Create repository」をクリック

---

### ステップ2: ファイルを準備（5分）

#### 2-1. ファイルの配置

```bash
cd ~/Desktop/wordpress-chatbot

# app_public.py を app.py にリネーム
cp app_public.py app.py

# .gitignoreをコピー
cp /path/to/.gitignore .

# 確認
ls -la
```

以下のファイルがあればOK：
- ✅ app.py（公開用）
- ✅ requirements.txt
- ✅ .gitignore

以下のファイルは**含めない**：
- ❌ secrets.toml（ローカルに保管）
- ❌ app_local.py
- ❌ app_fixed.py
- ❌ app_v2.py

---

### ステップ3: GitHubにプッシュ（10分）

```bash
cd ~/Desktop/wordpress-chatbot

# Git初期設定（初回のみ）
git config --global user.name "Katayama Yugo"
git config --global user.email "your-email@example.com"

# リポジトリ初期化
git init
git add app.py requirements.txt .gitignore
git commit -m "Initial commit - WordPress support chatbot"

# GitHubに接続
git remote add origin https://github.com/あなたのユーザー名/wordpress-chatbot.git
git branch -M main
git push -u origin main
```

**パスワードを聞かれたら：**
- Username: GitHubのユーザー名
- Password: GitHubのパスワード または Personal Access Token

---

### ステップ4: Streamlit Cloudにデプロイ（10分）

#### 4-1. Streamlit Cloudにログイン

1. https://streamlit.io/cloud にアクセス
2. 「Sign up」→「Continue with GitHub」
3. GitHubアカウントで連携

#### 4-2. アプリをデプロイ

1. 「New app」をクリック
2. 以下を選択：
   - **Repository**: `あなたのユーザー名/wordpress-chatbot`
   - **Branch**: `main`
   - **Main file path**: `app.py`

3. 「Advanced settings」をクリック

4. **「Secrets」に以下を入力：**

```toml
ANTHROPIC_API_KEY = "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"
```

5. 「Deploy!」をクリック

---

### ステップ5: 動作確認（5分）

デプロイ完了後（3〜5分）：

1. 自動で公開URLが発行される
   - 例：`https://wordpress-chatbot-xxxxx.streamlit.app/`

2. URLを開いて確認：
   - ✅ タイトルが表示される
   - ✅ サイドバーに使い方が表示される
   - ✅ 質問を入力できる

3. テスト質問：
   ```
   新しい記事を投稿したい
   ```
   
   回答が返ってくればOK！🎉

---

## 🎯 完成後にやること

### クライアントに共有

```
件名: WordPress更新サポートチャットのご案内

〇〇様

いつもお世話になっております。

WordPressの操作でわからないことがあったら、
いつでも質問できるチャットをご用意しました。

【URL】
https://wordpress-chatbot-xxxxx.streamlit.app/

使い方：
1. 上記URLを開く
2. 質問を入力
3. 回答が表示されます

例：「新しい記事を投稿したい」

24時間いつでも使えます。
何度質問しても無料です。

ご不明点があればお気軽にお問い合わせください。
```

---

## 🔧 マニュアル更新方法

### app.pyを編集

1. ローカルでapp.pyを編集
2. `WORDPRESS_MANUAL` の内容を変更
3. GitHubにプッシュ

```bash
cd ~/Desktop/wordpress-chatbot
git add app.py
git commit -m "マニュアル更新"
git push
```

4. Streamlit Cloudが自動で更新（3〜5分）

---

## 💰 コスト

- **Streamlit Cloud**: 無料
- **ホスティング**: 無料
- **ドメイン**: 無料（自動付与）
- **API使用料**: 約100〜300円/月

---

## ⚠️ トラブルシューティング

### デプロイが失敗する

**原因1:** requirements.txtが古い
```bash
# 最新版に更新
pip3 freeze > requirements.txt
```

**原因2:** Secretsの設定ミス
- Streamlit Cloudの「Secrets」を再確認
- APIキーが正しいか確認

### APIエラーが出る

- Streamlit Cloudの「Secrets」にAPIキーが設定されているか確認
- APIキーが正しいか確認（sk-ant- で始まる）

---

## 📞 サポート

わからないことがあれば、いつでも連絡してください！
