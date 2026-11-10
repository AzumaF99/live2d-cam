# Live2D Cam

iPhoneのカメラで顔を追跡し、PC上のLive2Dモデルを動かしてOBSで配信するためのWebアプリです。

- `index.html` … PC用ビューア（モデル表示・OBS取り込み）
- `tracker.html` … iPhone用トラッカー（Safariで開く）

映像はiPhone内で処理され、PCへ送られるのは顔の向き・目・口などの数値だけです（WebRTC / PeerJS経由）。

## セットアップ（GitHub Pages）

1. GitHubで新しい**公開**リポジトリを作る（例: `live2d-cam`）
2. `index.html` と `tracker.html` をアップロードする
3. モデルをURLから読み込みたい場合は、`model/` フォルダにモデル一式（`.model3.json` / `.moc3` / テクスチャ等）を入れる
4. Settings → Pages → Branch を `main` / `(root)` にして保存
5. 数分後、`https://<ユーザー名>.github.io/live2d-cam/` をPCのChromeで開く

> 注意: 公開リポジトリに置いたモデルは誰でもダウンロードできます。
> 公開したくない場合は `model/` を置かず、ビューアの「PCのフォルダから選ぶ」を使い、
> OBSでは「ウィンドウキャプチャ」＋背景グリーンのクロマキーで取り込んでください。

## 使い方

1. PCでビューアを開き、モデルを読み込む（`model/xxxx.model3.json` を入力、またはフォルダ選択）
2. 画面のQRコードをiPhoneで読み、Safariで開いて「開始」→ カメラを許可
3. まっすぐ前を向いて「正面をリセット」
4. ビューアで位置・大きさ・動きの大きさ・左右反転などを調整
5. 「OBS用URLをコピー」→ OBSのソース追加「ブラウザ」にURLを貼る（幅1920 / 高さ1080など）
6. OBSに入れたら、Chromeのビューアのタブは閉じる（同じルームコードは同時に1つだけ）

## うまくいかないとき

- **モデルが出ない**: `.model3.json` のパスの大文字小文字を確認。Cubism 2（`.model.json`）のモデルは非対応です。
- **向きが逆**: 「鏡のように動かす」「左右を逆に」「上下を逆に」「傾きを逆に」を切り替えてください。
- **つながらない**: PCとiPhoneを同じWi-Fiにすると安定します。両方のページを再読み込みしてください。
- **口や眉が動かない**: モデルのパラメータIDが標準名（`ParamMouthOpenY` など）でない場合は対応付けの追加が必要です。

## 使用ライブラリ

PixiJS 6 / pixi-live2d-display 0.4 / Live2D Cubism Core（Live2D社サイトから読み込み）/ MediaPipe Face Landmarker / PeerJS / qrcodejs

Live2D Cubism Core の利用には Live2D社のライセンスが適用されます。
