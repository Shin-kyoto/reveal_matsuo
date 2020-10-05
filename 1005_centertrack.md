---
theme : "white"
transition : "default"
---

# 1005_center track

疑問点

---

## 構成
1. Intro
2. Related Work
3. Preliminaries
4. Tracking objects as points
5. Experiments

---

## 3.Preliminaries_p4
- 入力：画像（W,H,3）
- 出力：(中心点 $p$,BBのサイズ $s$)    
--

中心点の低解像度ヒートマップ Y   $$ \hat{Y} \in [0,1]^{\frac{W}{R}\times \frac{H}{R}\times C} $$  
サイズマップ（矢印）
$$ \hat{S} \in \mathbb{R}^{\frac{W}{R}\times \frac{H}{R}\times 2} $$

--

- 教師：pがアノテーションされた画像
- オブジェクト数N,`downsampling factor` Rはハイパラ？
- $Y_{xyc}$:ヒートマップYにおける、(x,y)においてクラスcである確率

---

## 4.1_p6
- objectの位置 $\hat{p}$    
- 別フレームのobject同士をoffsetにより関連づける
- $\kappa$ 内にunmatched prior detection がなければ、新しいtrackletを生成

--

## 4.2_p6
- フレーム $t-1$ と $t$ とのずれ $\hat{D}^{(t)}$    
- サイズ $\hat{s}$
- confidence $\hat{w} = \hat{Y_{\hat{p}}}$

--

## 4.4_p6

- 画像とpointだけで、直前のフレームを生成できるらしい
- ランダムにスケーリング、変換させて直前のフレームを生成する
- コードのどのモジュール？

--


### まだちゃんと理解していないこと_4章
- 出力は $ \hat{Y} $, $ \hat{S} $,  $\hat{D}^{(t)}$ ?
- コードとの対応
- どこにRNNを追加するか？
- モデルの構造

---

### まだちゃんと理解していないこと_5章
- MOTA
- Ablation study

---

### 相談したい
- 出力、教師データ：$p$,$s$,$c$をアノテーションしてもらえば十分か？

--

### 相談したい
- center trackモジュールの前にCNN+LSTMをくっつけてやるのが一番簡単そう
- center trackモジュール内に矛盾なく実装