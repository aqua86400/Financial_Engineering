# 作業二：債券報價中的 YTM、Spot Rate、Forward Rate
> 0403更新歷程；
0404更新程式、程式流程圖 (抱歉滿晚才寫得完整，因為實在不是很理解這些利率內部的流程。)

## 學習歷程
一、 這次的作業對非財務相關的我挺困難的......除了看老師的投影片([1](https://docs.google.com/presentation/d/e/2PACX-1vT0uWPmTezKky8GLD_fkmfuJjXCLRuVkQWNuHmeogeMpY21cbwQurn7CsaVWRZDSZcZTvXjjpvY4lwE/pub?start=false&loop=false&delayms=3000&slide=id.p)、[2](https://docs.google.com/presentation/d/e/2PACX-1vSVL0BfN9ddvwhYgAX3PDQzzy864wCQflg9G1-1J7g-t7Rw8bXg1iicVBmgN0HSarVZSFs35Pxv1gA3/pub?start=false&loop=false&delayms=3000&slide=id.p))和相關連結，還有去旁聽一門課([財務演算法](https://github.com/andydong1209/NTU_FinAlgo))，剛好也有提到YTM、Spot Rate與Forward Rate，不過還不是很了解，因此還有求助一位朋友也是修課同學。


二、**到期收益率**(Yield to Maturity, YTM)：

* 一項債券的[內部報酬率](https://zh.wikipedia.org/wiki/%E5%85%A7%E9%83%A8%E5%A0%B1%E9%85%AC%E7%8E%87)(Internal Rate of Return)，如果 PV 是現值，CF_i 是第i期的現金流，n 是總期數，則即期利率y有以下方程式：
<img src="https://render.githubusercontent.com/render/math?math=PV = \sum_{i=1}^n\dfrac{CF_i}{(1 %2By)^i}">

我使用了Python的`sympy`套件來求 y，由於他會把所有的的解包括實數、虛數算出來，而這邊的 YTM 是要正的實數，所以我有另外建一個判別一個數字是正實數與否的函數。


三、**即期利率**(Spot Rate, SR)：

* 零息債券(Zero-Coupon Bond)的到期收益率就是它的即期利率。

如果今天是一個有配息的債券，我們可以把它切割成總期數個數(n)個的零息債券來看，然後去算最後一期的折現率也就是這邊的 SR(n)，所以要先在市場上找到其他年期是小於總年期的零息債的 YTM 當作前面的 SR(i) 才能計算。


四、**遠期利率**(Forward Rate, FR)
* 未來 i 時點開始，到 i+n(=j) 時點的即期利率，稱為 i 時點之 n 期遠期利率。

建立在[無套利理論](https://wiki.mbalib.com/zh-tw/%E6%97%A0%E5%A5%97%E5%88%A9%E5%AE%9A%E4%BB%B7%E5%8E%9F%E7%90%86)上，一次買 一年到期的債券的利益 要等於 先買半年到期後再續買半年的。

故有關係式：

<img src="https://render.githubusercontent.com/render/math?math=(1 %2B SR(j))^j=(1 %2B SR(i))^i(1 %2B f_{i,j})^{j-i}">，

<img src="https://render.githubusercontent.com/render/math?math=f_{i,j}"> 就是第i時點到第j時點的遠期利率。

## 程式流程圖
以下為[`Hw2.ipynb`](https://github.com/aqua86400/Financial_Engineering/blob/master/Hw2/Hw2.ipynb)的程式流程圖(使用了[draw.io線上圖表軟體](https://app.diagrams.net/))：<br />

![flowchart_hw2](https://github.com/aqua86400/Financial_Engineering/blob/master/Hw2/hw2_flowchart.png)
