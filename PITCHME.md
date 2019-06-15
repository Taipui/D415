# D415を使ってみた

D415を用いた3Dスキャン

---

## D415とは

<img src="realsense.png" width=50%>

Intel RealSense Depth Camera D400シリーズの一種

デプスカメラ

---

## D400シリーズは3種類ある

D415、D435、D435i

---

### それぞれの違い

|  |D415  |D435  |D435i  |
|:---:|:---:|:---:|:---:|
|<span style="font-size: 80%;">FoV</span>  |<span style="font-size: 80%;">65°</span>  |<span style="font-size: 80%;">85°</span>  |<span style="font-size: 80%;">85°</span>  |
|<span style="font-size: 80%;">シャッタータイプ</span>  |<span style="font-size: 80%;">ローリング</span>  |<span style="font-size: 80%;">グローバル</span>  |<span style="font-size: 80%;">グローバル</span>  |
|<span style="font-size: 80%;">モジュール</span>  |<span style="font-size: 80%;">Intel RealSense D415 module</span>  |<span style="font-size: 80%;">Intel RealSense D430 module</span>  |<span style="font-size: 80%;">Intel RealSense D430 module</span>  |
|<span style="font-size: 80%;">Imager</span>  |<span style="font-size: 80%;">2メガピクセル</span>  |<span style="font-size: 80%;">1メガピクセル</span>  |<span style="font-size: 80%;">1メガピクセル</span>  |

---

### それぞれの違い

D415は精度が高いため、3Dスキャンに向いている

D435は視野が広いため、トラッキングに向いている

D435iはD435にIMU(深度データと同期して装置そのものの動きが測定できる)が搭載されている

今回は3Dスキャンをするため、D415を選択

---

T265というカメラも存在する

<img src="t265.webp" width=50%>

より高精度でトラッキングしたい時用

デプスカメラではない

---

## 購入

<img src="d415_package.jpg" width=40%>

[Amazon](https://www.amazon.co.jp/gp/product/B07BJ1KKTV/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1)で購入

22,670円(2019年6月7日)

お急ぎ便で1日で届いた

---

## 同梱物

<img src="d415_bundled.jpg" width=40%>

D415

三脚

USB3.1 C to A

---

## PCとつなぐ

<img src="set.jpg" width=40%>

最初USBをどこに挿すか分からなかった

三脚が割とチープ

三脚が軽くケーブルが固めなのであまり安定しない

---

## サイトに行き、ツールをダウンロード

https://www.intelrealsense.com/get-started-depth-camera/

<img src="site1.png" width=40%>

全部英語です

---

## Viewer

<img src="viewer1.png" width=50%>

インストール不要で、デプスカメラの機能を一通り試すことができます。

---

## Unity SDK

[Github](https://github.com/IntelRealSense/librealsense/releases/tag/v2.21.0)にUnity用のSDKがあります。

<img src="unitySdk.png" width=50%>

---

## データ化

<img src="viewer2.png" width=50%>

ViewerでポイントクラウドをPLYに変換できます。

---

## MeshLabを用いて変換

PLY形式を扱えるのであれば、これでよいのですが、

Unity等の一部のソフトではPLY形式に対応していないことがあります。

MeshLabというフリーソフトを使えば、obj等の形式に変換できます。

<img src="meshLab.png" width=40%>

---

色は点群に保存されており、Unityではこれをインポートできないため、

今回はdae形式で保存します。

---

## Unityへ読み込む

<span style="font-size: 70%;">dae形式は読み込めますが、色情報はありません。</span>

<span style="font-size: 70%;">頂点単位のカラーをサポートするシェーダーが必要になります。</span>

<span style="font-size: 70%;">HoloLens向けのSDKにこのシェーダーが含まれているので、</span>

<span style="font-size: 70%;">[MRTK](https://github.com/Microsoft/MixedRealityToolkit-Unity/releases)を導入します。</span>

<img src="mrtk.png" width=40%>

「HoloToolkit-Unity-2017.4.3.0-Refresh.unitypackage」をインポートします。

---

「Fast Configurable 2 Sided」というシェーダーのマテリアルを適用し、

「Vertex Color Enabled」にチェックを入れると、色が乗ります。

<img src="unity.png" width=50%>

---

## まとめ

「カメラに映ったものをポイントクラウド化できる」ということなので、

フル3Dモデル化するには一工夫必要

表面的なものでよいのであれば、無料ですぐに立体化出来るのでお手軽

カメラの電源はPCから供給できるので、

モバイルPCと組み合わせれば、割とポータブル

リアルタイム処理も可能！？

---

# 参考文献

[インテル® RealSense™ テクノロジー](https://www.intel.co.jp/content/www/jp/ja/architecture-and-technology/realsense-overview.html)

[スイッチサイエンス](https://www.switch-science.com/)

[【記事】RealSense D415とD435 および D435iとT265の比較と選び方｜新着情報｜テガラ株式会社](https://www.tegara.com/news/2019/04/realsense-compare.html)

[Capturing a 3D Point Cloud with Intel RealSense and Converting to a Mesh with MeshLab](https://www.andreasjakl.com/capturing-3d-point-cloud-intel-realsense-converting-mesh-meshlab/)

[MRTK](https://github.com/IntelRealSense/librealsense/releases/tag/v2.21.0)
