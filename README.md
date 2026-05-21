[README.md](https://github.com/user-attachments/files/28125650/README.md)
# AR サイズ確認ツール

スマートフォンのブラウザ（Safari / Chrome）から、専用アプリ不要で商品の実物大設置イメージをARで確認・比較できるWebアプリです。

## 機能

| 機能 | 説明 |
|------|------|
| AR表示 | カメラ映像に実物大の商品画像を重ねて表示 |
| 2商品比較 | 商品A・Bを同時配置してサイズ比較が可能 |
| タップ配置 | 画面タップで任意の位置に商品を設置 |
| 即時切替 | 機種・カラーを変更すると配置済み商品も即反映 |
| 撮影保存 | 撮影ボタンでAR映像をJPEGとして保存 |

## 対応環境

- **iOS Safari** 13以上（DeviceOrientation APIでジャイロ対応）
- **Android Chrome** 最新版
- カメラアクセス許可が必要

## ディレクトリ構成

```
/
├── index.html          # アプリ本体（1ファイル完結）
├── AR_image/           # 商品画像フォルダ（背景透過PNG）
│   ├── FS-2214SF_CG.png
│   ├── FS-2214SF_JG.png
│   ├── FS-2214SF_PS.png
│   ├── FS-2614HF_PS.png
│   ├── FS-3018H_JB.png
│   ├── FS-3626H_CG.png
│   ├── MJX-139EF_FG.png
│   ├── MJX-177C_PS.png
│   └── MJX-157E_JG.png
└── README.md
```

## 画像ファイルの命名規則

```
{品番}_{カラーコード}.png
例: FS-2214SF_CG.png
```

- 背景透過PNGを推奨
- 推奨解像度: 幅 800px 以上

## マスタデータ（index.html 内の `MASTER` 配列）

| 機種名 | 品番 | カラー | 幅mm | 奥行mm | 高さmm |
|--------|------|--------|------|--------|--------|
| FORTA | FS-2214SF | CG/JG/PS | 2210 | 1370 | 2030 |
| FORTA | FS-2614HF | PS | 2630 | 1370 | 2330 |
| FORTA | FS-3018H | JB | 3050 | 1790 | 2330 |
| FORTA | FS-3626H | CG | 3580 | 2630 | 2330 |
| シンプリー | MJX-139EF | FG | 1320 | 905 | 1903 |
| シンプリー | MJX-177C | PS | 1740 | 755 | 1303 |
| シンプリー | MJX-157E | JG | 1520 | 755 | 1903 |

商品を追加する場合は `index.html` の `MASTER` 配列に行を追加し、`AR_image/` に対応する画像ファイルを置くだけです。

## GitHub Pages でのホスティング

1. このリポジトリを GitHub に push
2. Settings → Pages → Source: `main` ブランチの `/（root）`
3. 発行されたURLをスマートフォンで開く

> **注意**: カメラAPIは **HTTPS** 環境でのみ動作します。GitHub Pages は自動的にHTTPSになります。

## ローカル開発

```bash
# python 3
python3 -m http.server 8080
# または Node.js
npx serve .
```

`http://localhost:8080` をブラウザで開く（localhostはHTTPS不要）。

## 商品データのカスタマイズ

`index.html` 内の `MASTER` 配列を編集します：

```javascript
const MASTER = [
  {
    model: '機種名グループ',   // セレクタの第1階層
    code:  '品番',             // セレクタの第2階層
    color: 'カラーコード',     // セレクタの第3階層
    file:  '品番_カラー.png',  // AR_image/ 内のファイル名
    w: 2210,                   // 幅 mm
    d: 1370,                   // 奥行 mm
    h: 2030,                   // 高さ mm
  },
  // ...
];
```

## iOS 撮影について

iOS Safari では WebGL Canvas のピクセル読み取りに制限がある場合があります。  
その場合は **スクリーンショット（サイドボタン＋音量ボタン）** での保存をご案内ください。

## ライセンス

社内利用専用
