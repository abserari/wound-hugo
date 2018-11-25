+++
author = "Abser Ari"
categories = ["Algorithm"]
date = "2018-11-25"
description = "HyperLogLog"
featured = "pic03.jpg"
featuredalt = "Pic 3"
featuredpath = "date"
linktitle = ""
title = "HyperLogLog"
type = "post"

+++



## 基数计数基本概念

__基数计数(cardinality counting)__通常用来统计一个集合中不重复的元素个数，例如统计某个网站的UV，或者用户搜索网站的关键词数量。数据分析、网络监控及数据库优化等领域都会涉及到基数计数的需求。 要实现基数计数，最简单的做法是记录集合中所有不重复的元素集合<div id="gcbhoa" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/b203891c74e924db0c6b5e07fe602d11.svg" data-text="S%E2%80%8B_u%E2%80%8B" data-width="22" data-height="24"><img src="https://cdn.nlark.com/__latex/b203891c74e924db0c6b5e07fe602d11.svg" width="22"/></div>，当新来一个元素<div id="b0umcs" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/1ba8aaab47179b3d3e24b0ccea9f4e30.svg" data-text="x_i" data-width="16" data-height="24"><img src="https://cdn.nlark.com/__latex/1ba8aaab47179b3d3e24b0ccea9f4e30.svg" width="16"/></div>，若<div id="408umz" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/b203891c74e924db0c6b5e07fe602d11.svg" data-text="S%E2%80%8B_u%E2%80%8B" data-width="22" data-height="24"><img src="https://cdn.nlark.com/__latex/b203891c74e924db0c6b5e07fe602d11.svg" width="22"/></div>中不包含元素<div id="50u1nf" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/1ba8aaab47179b3d3e24b0ccea9f4e30.svg" data-text="x_i" data-width="16" data-height="24"><img src="https://cdn.nlark.com/__latex/1ba8aaab47179b3d3e24b0ccea9f4e30.svg" width="16"/></div>​，则将<div id="dhwtwt" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/1ba8aaab47179b3d3e24b0ccea9f4e30.svg" data-text="x_i" data-width="16" data-height="24"><img src="https://cdn.nlark.com/__latex/1ba8aaab47179b3d3e24b0ccea9f4e30.svg" width="16"/></div>加入<div id="cvovnf" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/b203891c74e924db0c6b5e07fe602d11.svg" data-text="S%E2%80%8B_u%E2%80%8B" data-width="22" data-height="24"><img src="https://cdn.nlark.com/__latex/b203891c74e924db0c6b5e07fe602d11.svg" width="22"/></div>，否则不加入，计数值就是<div id="s2nwaz" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/b203891c74e924db0c6b5e07fe602d11.svg" data-text="S%E2%80%8B_u%E2%80%8B" data-width="22" data-height="24"><img src="https://cdn.nlark.com/__latex/b203891c74e924db0c6b5e07fe602d11.svg" width="22"/></div>​的元素数量。这种做法存在两个问题：

1. 当统计的数据量变大时，相应的存储内存也会线性增长
2. 当集合<div id="s2nwaz" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/b203891c74e924db0c6b5e07fe602d11.svg" data-text="S%E2%80%8B_u%E2%80%8B" data-width="22" data-height="24"><img src="https://cdn.nlark.com/__latex/b203891c74e924db0c6b5e07fe602d11.svg" width="22"/></div>变大，判断其是否包含新加入元素<div id="b0umcs" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/1ba8aaab47179b3d3e24b0ccea9f4e30.svg" data-text="x_i" data-width="16" data-height="24"><img src="https://cdn.nlark.com/__latex/1ba8aaab47179b3d3e24b0ccea9f4e30.svg" width="16"/></div>​的成本变大

### 概率算法

实际上目前还没有发现更好的在大数据场景中准确计算基数的高效算法，因此在不追求绝对准确的情况下，使用概率算法算是一个不错的解决方案。概率算法不直接存储数据集合本身，通过一定的概率统计方法预估基数值，这种方法可以大大节省内存，同时保证误差控制在一定范围内。目前用于基数计数的概率算法包括:

* __*Linear Counting(LC)*__：早期的基数估计算法，LC在空间复杂度方面并不算优秀，实际上LC的空间复杂度与简单bitmap方法是一样的（但是有个常数项级别的降低），都是O(N​max​​)；
* __*LogLog Counting(LLC)*__：LogLog Counting相比于LC更加节省内存，空间复杂度只有O(log​2​​(log​2​​(N​max​​)))
* __*HyperLogLog Counting(HLL)*__：HyperLogLog Counting是基于LLC的优化和改进，在同样空间复杂度情况下，能够比LLC的基数估计误差更小。

# HLL
### 直观演示
[HLLDEMO](http://content.research.neustar.biz/blog/hll.html)



![hyperloglog | left](http://static.zybuluo.com/rainybowe/rv2u7tl6xu15f54ozc6v5q5b/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202017-07-02%2017.22.55.png "")

### HLL的实际步骤
1. 通过hash函数计算输入值对应的比特串
2. 比特串的低 <div id="pe4mnd" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/996cfc927186db0ef2bed7d3890832c5.svg" data-text="t(t%3Dlog_2%5Em)" data-width="82" data-height="24"><img src="https://cdn.nlark.com/__latex/996cfc927186db0ef2bed7d3890832c5.svg" width="82"/></div>位对应的数字用来找到数组__S__中对应的位置 __i__
3. __t+1__位开始找到第一个1出现的位置 __k__，将 __k__ 记入数组<div id="gzqbhp" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/804f14414dab2297b600211a82c39fa8.svg" data-text="S_i" data-width="16" data-height="24"><img src="https://cdn.nlark.com/__latex/804f14414dab2297b600211a82c39fa8.svg" width="16"/></div>位置
4. 基于数组__S__记录的所有数据的统计值，计算整体的基数值，计算公式可以简单表示为：<div id="3oxkmy" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/263877c375517993b38d9f0dbf5effb6.svg" data-text="%5Chat%7Bn%7D%3Df(S)%E2%80%8B" data-width="67" data-height="24"><img src="https://cdn.nlark.com/__latex/263877c375517993b38d9f0dbf5effb6.svg" width="67"/></div>

__HLL__是__LLC__的误差改进，实际是基于__LLC__。

### 算法来源（N次伯努利过程）

下面非正式的从直观角度描述LLC算法的思想来源。

设__a__为待估集合（哈希后）中的一个元素，由上面对H的定义可知，__a__可以看做一个长度固定的比特串（也就是__a__的二进制表示），设H哈希后的结果长度为L比特，我们将这__L__个比特位从左到右分别编号为__1、2、…、L__：


![image | left](http://blog.codinglabs.org/uploads/pictures/algorithms-for-cardinality-estimation-part-iii/1.png "")

又因为__a__是从服从均与分布的样本空间中随机抽取的一个样本，因此__a__每个比特位服从如下分布且相互独立。

<div id="rchrhq" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/d41c76fd4769600b621b4edb68e66e55.svg" data-text="%20%20p(x%3Dk)%20%3D%0A%5Cbegin%7Bcases%7D%0A0.5%2C%20%20%26%20%5Ctext%7B%24k%24%20%3D%200%7D%20%5C%5C%0A0.5%2C%20%26%20%5Ctext%7B%24k%24%20%3D%201%7D%0A%5Cend%7Bcases%7D" data-width="187" data-height="45"><img src="https://cdn.nlark.com/__latex/d41c76fd4769600b621b4edb68e66e55.svg" width="187"/></div>
通俗说就是a的每个比特位为0和1的概率各为0.5，且相互之间是独立的。

设 ρ(a)为a的比特串中第一个“1”出现的位置，显然1≤ρ(a)≤L，这里我们忽略比特串全为0的情况（概率为<div id="0cfwyz" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/898a64131575f1dd2310578eaa024e49.svg" data-text="1%2F2L" data-width="37" data-height="24"><img src="https://cdn.nlark.com/__latex/898a64131575f1dd2310578eaa024e49.svg" width="37"/></div>）。如果我们遍历集合中所有元素的比特串，取<div id="it5wtg" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/50f1c9cecf88293f2d528300158704ab.svg" data-text="%CF%81_%7Bmax%7D%0A" data-width="34" data-height="24"><img src="https://cdn.nlark.com/__latex/50f1c9cecf88293f2d528300158704ab.svg" width="34"/></div>为所有__ρ(a)__的最大值。

此时我们可以将<div id="gk3vcl" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/2bc7592c5ee7f031c54ed7e0a0ace6a6.svg" data-text="2%CF%81_%7Bmax%7D" data-width="43" data-height="24"><img src="https://cdn.nlark.com/__latex/2bc7592c5ee7f031c54ed7e0a0ace6a6.svg" width="43"/></div>作为基数的一个粗糙估计，即：

<div id="ehtowt" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/d7e9bef80ecf0500e2c18e0b4c29e5ec.svg" data-text="n%3D2%5E%7B%CF%81_%7Bmax%7D%7D" data-width="70" data-height="24"><img src="https://cdn.nlark.com/__latex/d7e9bef80ecf0500e2c18e0b4c29e5ec.svg" width="70"/></div>

#### 解释
注意如下事实：

由于比特串每个比特都独立且服从0-1分布，因此从左到右扫描上述某个比特串寻找第一个“1”的过程从统计学角度看是一个伯努利过程，例如，可以等价看作不断投掷一个硬币（每次投掷正反面概率皆为0.5），直到得到一个正面的过程。在一次这样的过程中，投掷一次就得到正面的概率为1/2，投掷两次得到正面的概率是<div id="tehgte" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/1c30f976355d106be6c65ea27efdbcf6.svg" data-text="1%2F2%5E2" data-width="33" data-height="24"><img src="https://cdn.nlark.com/__latex/1c30f976355d106be6c65ea27efdbcf6.svg" width="33"/></div>，__…__，投掷__k__次才得到第一个正面的概率为<div id="a0ntrh" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/3b99ad226dc8916d35336785ba082276.svg" data-text="1%2F2%5Ek" data-width="34" data-height="24"><img src="https://cdn.nlark.com/__latex/3b99ad226dc8916d35336785ba082276.svg" width="34"/></div>。

现在考虑如下两个问题：

1、进行n次伯努利过程，所有投掷次数都不大于k的概率是多少？

2、进行n次伯努利过程，至少有一次投掷次数等于k的概率是多少？

首先看第一个问题，在一次伯努利过程中，投掷次数大于k的概率为<div id="gfgicc" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/3b99ad226dc8916d35336785ba082276.svg" data-text="1%2F2%5Ek" data-width="34" data-height="24"><img src="https://cdn.nlark.com/__latex/3b99ad226dc8916d35336785ba082276.svg" width="34"/></div>，即连续掷出k个反面的概率。因此，在一次过程中投掷次数不大于k的概率为<div id="mmcroy" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/dcac898d26731f27f342ab79696d5f01.svg" data-text="1-1%2F2%5Ek" data-width="63" data-height="24"><img src="https://cdn.nlark.com/__latex/dcac898d26731f27f342ab79696d5f01.svg" width="63"/></div>。因此，n次伯努利过程投掷次数均不大于k的概率为：

<div id="r190vr" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/87b855d089a473a664ff90e97e61e6a1.svg" data-text="P_n(X%E2%89%A4k)%3D(1%E2%88%921%2F2k)%5En" data-width="188" data-height="24"><img src="https://cdn.nlark.com/__latex/87b855d089a473a664ff90e97e61e6a1.svg" width="188"/></div>

显然第二个问题的答案是：

<div id="fck6km" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/9f103c40faf010b8af7341bc4ffe89c9.svg" data-text="P_n(X%E2%89%A5k)%3D1%E2%88%92(1%E2%88%921%2F2k%E2%88%921)%5En" data-width="247" data-height="24"><img src="https://cdn.nlark.com/__latex/9f103c40faf010b8af7341bc4ffe89c9.svg" width="247"/></div>

从以上分析可以看出，当<div id="8h2kfr" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/6158b1f234ebc7d3c76692c3ddd5270f.svg" data-text="n%E2%89%AA2%5Ek" data-width="53" data-height="24"><img src="https://cdn.nlark.com/__latex/6158b1f234ebc7d3c76692c3ddd5270f.svg" width="53"/></div>时，__Pn(X≥k)__的概率几乎为0，同时，当<div id="kz8xif" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/6158b1f234ebc7d3c76692c3ddd5270f.svg" data-text="n%E2%89%AA2%5Ek" data-width="53" data-height="24"><img src="https://cdn.nlark.com/__latex/6158b1f234ebc7d3c76692c3ddd5270f.svg" width="53"/></div>时，__Pn(X≤k)__的概率也几乎为0。用自然语言概括上述结论就是：当伯努利过程次数远远小于<div id="vbwfgz" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/fe401f62231ac24e3399751a415a4eaa.svg" data-text="2%5Ek" data-width="17" data-height="24"><img src="https://cdn.nlark.com/__latex/fe401f62231ac24e3399751a415a4eaa.svg" width="17"/></div>时，至少有一次过程投掷次数等于k的概率几乎为0；当伯努利过程次数远远大于<div id="vvoihd" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/fe401f62231ac24e3399751a415a4eaa.svg" data-text="2%5Ek" data-width="17" data-height="24"><img src="https://cdn.nlark.com/__latex/fe401f62231ac24e3399751a415a4eaa.svg" width="17"/></div>时，没有一次过程投掷次数大于k的概率也几乎为0。

如果将上面描述做一个对应：一次伯努利过程对应一个元素的比特串，反面对应0，正面对应1，投掷次数k对应第一个“1”出现的位置，我们就得到了下面结论：

设一个集合的基数为n，<div id="zxg2bg" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/50f1c9cecf88293f2d528300158704ab.svg" data-text="%CF%81_%7Bmax%7D" data-width="34" data-height="24"><img src="https://cdn.nlark.com/__latex/50f1c9cecf88293f2d528300158704ab.svg" width="34"/></div>为所有元素中首个“1”的位置最大的那个元素的“1”的位置，如果n远远小于<div id="rgndlp" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/aa208763a1096ea14b0177179aa651d5.svg" data-text="2%5E%7B%CF%81_%7Bmax%7D%7D" data-width="37" data-height="24"><img src="https://cdn.nlark.com/__latex/aa208763a1096ea14b0177179aa651d5.svg" width="37"/></div>，则我们得到<div id="gi0bbi" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/50f1c9cecf88293f2d528300158704ab.svg" data-text="%CF%81_%7Bmax%7D" data-width="34" data-height="24"><img src="https://cdn.nlark.com/__latex/50f1c9cecf88293f2d528300158704ab.svg" width="34"/></div>为当前值的概率几乎为0（它应该更小），同样的，如果n远远大于<div id="29amgv" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/aa208763a1096ea14b0177179aa651d5.svg" data-text="2%5E%7B%CF%81_%7Bmax%7D%7D" data-width="37" data-height="24"><img src="https://cdn.nlark.com/__latex/aa208763a1096ea14b0177179aa651d5.svg" width="37"/></div>，则我们得到<div id="c8qkgq" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/50f1c9cecf88293f2d528300158704ab.svg" data-text="%CF%81_%7Bmax%7D" data-width="34" data-height="24"><img src="https://cdn.nlark.com/__latex/50f1c9cecf88293f2d528300158704ab.svg" width="34"/></div>为当前值的概率也几乎为0（它应该更大），因此<div id="598wkb" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/aa208763a1096ea14b0177179aa651d5.svg" data-text="2%5E%7B%CF%81_%7Bmax%7D%7D" data-width="37" data-height="24"><img src="https://cdn.nlark.com/__latex/aa208763a1096ea14b0177179aa651d5.svg" width="37"/></div>可以作为基数n的一个粗糙估计。

__以上结论可以总结为__<span data-type="color" style="color:rgb(81, 81, 81)"><span data-type="background" style="background-color:rgb(255, 255, 255)">：进行了</span></span>n<span data-type="color" style="color:rgb(81, 81, 81)"><span data-type="background" style="background-color:rgb(255, 255, 255)">次进行抛硬币实验，每次分别记录下第一次抛到正面的抛掷次数k</span></span>k<span data-type="color" style="color:rgb(81, 81, 81)"><span data-type="background" style="background-color:rgb(255, 255, 255)">，那么可以用n次实验中最大的抛掷次数</span></span><div id="keungw" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/5e41a763a2c066b1f0f119d7c0874fa2.svg" data-text="k_%7Bmax%7D" data-width="35" data-height="24"><img src="https://cdn.nlark.com/__latex/5e41a763a2c066b1f0f119d7c0874fa2.svg" width="35"/></div><span data-type="color" style="color:rgb(81, 81, 81)"><span data-type="background" style="background-color:rgb(255, 255, 255)">来预估实验组数量</span></span>n<span data-type="color" style="color:rgb(81, 81, 81)"><span data-type="background" style="background-color:rgb(255, 255, 255)">： </span></span><div id="og16ug" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/55630d261e6562fce2c626d2c30cd28b.svg" data-text="%5Chat%7Bn%7D%20%3D%202%5E%7Bk_%7Bmax%7D%7D" data-width="70" data-height="24"><img src="https://cdn.nlark.com/__latex/55630d261e6562fce2c626d2c30cd28b.svg" width="70"/></div>


![原型图 (1).png-18.1kB | left](http://static.zybuluo.com/rainybowe/atnfc03t63r868n86f4amzae/%E5%8E%9F%E5%9E%8B%E5%9B%BE%20%281%29.png "")

<span data-type="color" style="color:rgb(81, 81, 81)"><span data-type="background" style="background-color:rgb(255, 255, 255)">回到基数统计的问题，我们需要统计一组数据中不重复元素的个数，集合中每个元素的经过hash函数后可以表示成0和1构成的二进制数串，一个二进制串可以类比为一次抛硬币实验，1是抛到正面，0是反面。二进制串中从低位开始第一个1出现的位置可以理解为抛硬币试验中第一次出现正面的抛掷次数</span></span>k<span data-type="color" style="color:rgb(81, 81, 81)"><span data-type="background" style="background-color:rgb(255, 255, 255)">，那么基于上面的结论，我们可以通过多次抛硬币实验的最大抛到正面的次数来预估总共进行了多少次实验，同样可以可以通过第一个1出现位置的最大值</span></span>​<span data-type="color" style="color:rgb(81, 81, 81)"><span data-type="background" style="background-color:rgb(255, 255, 255)">来</span></span><div id="4u5big" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/5e41a763a2c066b1f0f119d7c0874fa2.svg" data-text="k_%7Bmax%7D" data-width="35" data-height="24"><img src="https://cdn.nlark.com/__latex/5e41a763a2c066b1f0f119d7c0874fa2.svg" width="35"/></div><span data-type="color" style="color:rgb(81, 81, 81)"><span data-type="background" style="background-color:rgb(255, 255, 255)">预估总共有多少个不同的数字（整体基数）。</span></span>
## LogLogCounting

### 均匀随机化

与LC一样，在使用LLC之前需要选取一个哈希函数H应用于所有元素，然后对哈希值进行基数估计。H必须满足如下条件（定性的）：

1、H的结果具有很好的均匀性，也就是说无论原始集合元素的值分布如何，其哈希结果的值几乎服从均匀分布（完全服从均匀分布是不可能的，D. Knuth已经证明不可能通过一个哈希函数将一组不服从均匀分布的数据映射为绝对均匀分布，但是很多哈希函数可以生成几乎服从均匀分布的结果，这里我们忽略这种理论上的差异，认为哈希结果就是服从均匀分布）。

2、H的碰撞几乎可以忽略不计。也就是说我们认为对于不同的原始值，其哈希结果相同的概率非常小以至于可以忽略不计。

3、H的哈希结果是固定长度的。

以上对哈希函数的要求是随机化和后续概率分析的基础。后面的分析均认为是针对哈希后的均匀分布数据进行。

### 分桶平均

上述分析给出了LLC的基本思想，不过如果直接使用上面的单一估计量进行基数估计会由于偶然性而存在较大误差。因此，LLC采用了分桶平均的思想来消减误差。具体来说，就是将哈希空间平均分成m份，每份称之为一个桶（bucket）。对于每一个元素，其哈希值的前k比特作为桶编号，其中<div id="rqsdzv" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/9bfdddc438393f4f8c33b6015e451242.svg" data-text="2%5Ek%3Dm" data-width="54" data-height="24"><img src="https://cdn.nlark.com/__latex/9bfdddc438393f4f8c33b6015e451242.svg" width="54"/></div>，而后L-k个比特作为真正用于基数估计的比特串。桶编号相同的元素被分配到同一个桶，在进行基数估计时，首先计算每个桶内元素最大的第一个“1”的位置，设为M[i]，然后对这m个值取平均后再进行估计，即：

<div id="73iwio" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/d0b756c091ab82db7e4420be47c850cc.svg" data-text="%5Chat%20n%20%3D2%5E%7B1%2Fm%7D%E2%88%91M%5Bi%5D" data-width="130" data-height="28"><img src="https://cdn.nlark.com/__latex/d0b756c091ab82db7e4420be47c850cc.svg" width="130"/></div>

这相当于物理试验中经常使用的多次试验取平均的做法，可以有效消减因偶然性带来的误差。

下面举一个例子说明分桶平均怎么做。

假设H的哈希长度为16bit，分桶数m定为32。设一个元素哈希值的比特串为“0001001010001010”，由于m为32，因此前5个bit为桶编号，所以这个元素应该归入“00010”即2号桶（桶编号从0开始，最大编号为m-1），而剩下部分是“01010001010”且显然ρ(01010001010)=2，所以桶编号为“00010”的元素最大的ρ即为M[2]的值。

### 偏差修正

上述经过分桶平均后的估计量看似已经很不错了，不过通过数学分析可以知道这并不是基数n的无偏估计。因此需要修正成无偏估计。这部分的具体数学分析在“Loglog Counting of Large Cardinalities”中，过程过于艰涩这里不再具体详述，有兴趣的朋友可以参考原论文。这里只简要提一下分析框架：

首先上文已经得出：

<div id="bs2avv" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/87b855d089a473a664ff90e97e61e6a1.svg" data-text="P_n(X%E2%89%A4k)%3D(1%E2%88%921%2F2k)%5En" data-width="188" data-height="24"><img src="https://cdn.nlark.com/__latex/87b855d089a473a664ff90e97e61e6a1.svg" width="188"/></div>

因此：

<div id="q9ivyv" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/9f7011ab269c90f3b3236d3bef6a7807.svg" data-text="P_n(X%3Dk)%3D(1%E2%88%921%2F2k)%5En%E2%88%92(1%E2%88%921%2F2k%E2%88%921)%5En" data-width="325" data-height="24"><img src="https://cdn.nlark.com/__latex/9f7011ab269c90f3b3236d3bef6a7807.svg" width="325"/></div>

这是一个未知通项公式的递推数列，研究这种问题的常用方法是使用生成函数（generating function）。通过运用指数生成函数和poissonization得到上述估计量的Poisson期望和方差为：
<div id="a9cbyi" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/e0d9d689ba93e5965e596f74cc802a25.svg" data-text="%CE%B5n%E2%88%BC%5B(%CE%93(%E2%88%921%2Fm)%5Cfrac%7B1%E2%88%922%5E%7B1%2Fm%7D%7D%7Blog2%7D)%5Em%2B%CF%B5_n%5Dn" data-width="261" data-height="47"><img src="https://cdn.nlark.com/__latex/e0d9d689ba93e5965e596f74cc802a25.svg" width="261"/></div>

<div id="53v5tl" data-type="math" data-display="block" data-align="left" data-src="https://cdn.nlark.com/__latex/a8059ed576b9fc9eabeee8c9b1ceecb6.svg" data-text="%CE%BD_n%E2%88%BC%5B(%CE%93(%E2%88%922%2Fm)%5Cfrac%7B1%E2%88%922%5E%7B2%2Fm%7D%7D%7Blog_2m%7D)%5Em%E2%88%92(%CE%93(%E2%88%921%2Fm)1%E2%88%92%5Cfrac%7B2%5E%7B1%2Fm%7D%7D%7Blog_2m%7D)%5E%7B2m%7D%2B%CE%B7_n%5Dn%5E2" data-width="471" data-height="47"><img src="https://cdn.nlark.com/__latex/a8059ed576b9fc9eabeee8c9b1ceecb6.svg" width="471"/></div>
其中<div id="w43uiq" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/b37f31d1fbf544f67ac8ad275a980aa3.svg" data-text="%7C%CF%B5_n%7C" data-width="25" data-height="24"><img src="https://cdn.nlark.com/__latex/b37f31d1fbf544f67ac8ad275a980aa3.svg" width="25"/></div>和<div id="5opwkp" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/d9649cb69f9c1553fa37feca018b4c39.svg" data-text="%7C%CE%B7_n%7C" data-width="27" data-height="24"><img src="https://cdn.nlark.com/__latex/d9649cb69f9c1553fa37feca018b4c39.svg" width="27"/></div>不超过<div id="mbkhrr" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/7228baf1916540fe9a085048283ed14d.svg" data-text="10%5E%7B%E2%88%926%7D" data-width="34" data-height="24"><img src="https://cdn.nlark.com/__latex/7228baf1916540fe9a085048283ed14d.svg" width="34"/></div>。

最后通过depoissonization得到一个渐进无偏估计量：

<div id="0suput" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/dbdf5ecd276f02bdd57b91f9a636cd02.svg" data-text="%5Chat%20n%20%3D%CE%B1_m2%5E%7B1%2Fm%7D%E2%88%91M%5Bi%5D" data-width="153" data-height="28"><img src="https://cdn.nlark.com/__latex/dbdf5ecd276f02bdd57b91f9a636cd02.svg" width="153"/></div>

其中：

<div id="bne4gc" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/c3d2954dee1af62ea7a73fb2fa05a1d5.svg" data-text="%CE%B1_m%3D(%CE%93(%E2%88%921%2Fm)%5Cfrac%7B1%E2%88%922%5E%7B1%2Fm%7D%7D%7Blog2%7D)%E2%88%92m" data-width="233" data-height="47"><img src="https://cdn.nlark.com/__latex/c3d2954dee1af62ea7a73fb2fa05a1d5.svg" width="233"/></div>

<div id="pp44fv" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/66a4a1e5ccc124e304c6555acdd81cc5.svg" data-text="%CE%93(s)%3D%5Cfrac1s%20%E2%88%AB%5E%E2%88%9E_0e%5E%7B%E2%88%92t%7Dt%5Esdt" data-width="159" data-height="43"><img src="https://cdn.nlark.com/__latex/66a4a1e5ccc124e304c6555acdd81cc5.svg" width="159"/></div>

其中m是分桶数。这就是LLC最终使用的估计量。

### 误差分析

不加证明给出如下结论：

<div id="2fwnqd" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/eedf9833ca7f1277fd5a92e9b59a99cc.svg" data-text="StdError(%5Chat%20n%2Fn)%E2%89%88%5Cfrac%7B1.30%7D%7B%E2%88%9Am%7D" data-width="172" data-height="44"><img src="https://cdn.nlark.com/__latex/eedf9833ca7f1277fd5a92e9b59a99cc.svg" width="172"/></div>

## 算法应用

### 误差控制

在应用LLC时，主要需要考虑的是分桶数m，而这个m主要取决于误差。根据上面的误差分析，如果要将误差控制在__ϵ__之内，则：

<div id="ib33es" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/0ca0a961024756a88df245d08a29a67b.svg" data-text="m%3E(1.30%2F%CF%B5)%5E2" data-width="105" data-height="24"><img src="https://cdn.nlark.com/__latex/0ca0a961024756a88df245d08a29a67b.svg" width="105"/></div>

### 内存使用分析

内存使用与m的大小及哈希值得长度（或说基数上限）有关。假设H的值为32bit，由于<div id="f7b1ot" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/d4cbf5e99763c0a9b9066897c8781f5c.svg" data-text="%CF%81_%7Bmax%7D%E2%89%A432" data-width="74" data-height="24"><img src="https://cdn.nlark.com/__latex/d4cbf5e99763c0a9b9066897c8781f5c.svg" width="74"/></div>，因此每个桶需要5bit空间存储这个桶的<div id="1gv8gu" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/50f1c9cecf88293f2d528300158704ab.svg" data-text="%CF%81_%7Bmax%7D" data-width="34" data-height="24"><img src="https://cdn.nlark.com/__latex/50f1c9cecf88293f2d528300158704ab.svg" width="34"/></div>，m个桶就是5×m/8字节。例如基数上限为一亿（约<div id="uqc2qs" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/35dd254fcc92c59fb3a61f3fb0dcf3d5.svg" data-text="2%5E%7B27%7D" data-width="22" data-height="24"><img src="https://cdn.nlark.com/__latex/35dd254fcc92c59fb3a61f3fb0dcf3d5.svg" width="22"/></div>），当分桶数m为1024时，每个桶的基数上限约为<div id="lquyce" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/054fbb50164e57339335d442e5b35ee5.svg" data-text="2%5E%7B17%7D" data-width="22" data-height="24"><img src="https://cdn.nlark.com/__latex/054fbb50164e57339335d442e5b35ee5.svg" width="22"/></div>，而<div id="62cfqs" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/ab6752515605f1f83a8b97ee3f02986f.svg" data-text="log_2(log_2(2%5E%7B17%7D))%3D4.09" data-width="161" data-height="24"><img src="https://cdn.nlark.com/__latex/ab6752515605f1f83a8b97ee3f02986f.svg" width="161"/></div>，因此每个桶需要5bit，需要字节数就是5×1024/8=640，误差为<div id="l8nzng" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/59709319d309873ef67d15ecdda15f58.svg" data-text="1.30%20%2F%20%5Csqrt%7B1024%7D%20%3D%200.040625" data-width="175" data-height="24"><img src="https://cdn.nlark.com/__latex/59709319d309873ef67d15ecdda15f58.svg" width="175"/></div>，也就是约为4%。

### 合并

与__LC__不同，__LLC__的合并是以桶为单位而不是bit为单位，由于__LLC__只需记录桶的<div id="95vggu" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/50f1c9cecf88293f2d528300158704ab.svg" data-text="%CF%81_%7Bmax%7D" data-width="34" data-height="24"><img src="https://cdn.nlark.com/__latex/50f1c9cecf88293f2d528300158704ab.svg" width="34"/></div>，因此合并时取相同桶编号数值最大者为合并后此桶的数值即可。

# HyperLogLog Counting

__HyperLogLog Counting__（以下简称__HLLC__）的基本思想也是在__LLC__的基础上做改进，具体细节请参考“HyperLogLog: the analysis of a near-optimal cardinality estimation algorithm”这篇论文。

## 基本算法

HLLC的第一个改进是使用调和平均数替代几何平均数。注意LLC是对各个桶取算数平均数，而算数平均数最终被应用到2的指数上，所以总体来看LLC取得是几何平均数。由于几何平均数对于离群值（例如这里的0）特别敏感，因此当存在离群值时，LLC的偏差就会很大，这也从另一个角度解释了为什么n不太大时LLC的效果不太好。这是因为n较小时，可能存在较多空桶，而这些特殊的离群值强烈干扰了几何平均数的稳定性。

因此，HLLC使用调和平均数来代替几何平均数，调和平均数的定义如下：

<div id="thsbtn" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/1a546ae72c5c0a2078424c29e7fe229f.svg" data-text="H%20%3D%20%5Cfrac%7Bn%7D%7B%5Cfrac%7B1%7D%7Bx_1%7D%20%2B%20%5Cfrac%7B1%7D%7Bx_2%7D%20%2B%20...%20%2B%20%5Cfrac%7B1%7D%7Bx_n%7D%7D%20%3D%20%5Cfrac%7Bn%7D%7B%5Csum_%7Bi%3D1%7D%5En%20%5Cfrac%7B1%7D%7Bx_i%7D%7D" data-width="262" data-height="47"><img src="https://cdn.nlark.com/__latex/1a546ae72c5c0a2078424c29e7fe229f.svg" width="262"/></div>

调和平均数可以有效抵抗离群值的扰动。使用调和平均数代替几何平均数后，估计公式变为如下：
<div id="52gibr" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/57ba6207913030823f9b63062e857c73.svg" data-text="%5Chat%7Bn%7D%3D%5Cfrac%7B%5Calpha_m%20m%5E2%7D%7B%5Csum%7B2%5E%7B-M%7D%7D%7D" data-width="92" data-height="50"><img src="https://cdn.nlark.com/__latex/57ba6207913030823f9b63062e857c73.svg" width="92"/></div>

其中：
<div id="r5bvmc" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/00fe56224e63f9b36d1916eaee2e9436.svg" data-text="%5Calpha_m%3D(m%5Cint%20_0%5E%5Cinfty%20(log_2(%5Cfrac%7B2%2Bu%7D%7B1%2Bu%7D))%5Em%20du)%5E%7B-1%7D" data-width="258" data-height="43"><img src="https://cdn.nlark.com/__latex/00fe56224e63f9b36d1916eaee2e9436.svg" width="258"/></div>

## 偏差分析

根据论文中的分析结论，与LLC一样HLLC是渐近无偏估计，且其渐近标准差为：

<div id="ha7wah" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/9867f3c2097951bbd1aaf0df698bb281.svg" data-text="SE_%7Bhllc%7D(%5Chat%7Bn%7D%2Fn)%3D1.04%2F%5Csqrt%7Bm%7D" data-width="178" data-height="24"><img src="https://cdn.nlark.com/__latex/9867f3c2097951bbd1aaf0df698bb281.svg" width="178"/></div>

因此在存储空间相同的情况下，HLLC比LLC具有更高的精度。例如，对于分桶数m为2^13（8k字节）时，LLC的标准误差为1.4%，而HLLC为1.1%。

## 分段偏差修正

在HLLC的论文中，作者在实现建议部分还给出了在n相对于m较小或较大时的偏差修正方案。具体来说，设E为估计值：

当<div id="goggam" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/be90b52e69dad1ef3bf2c24d72f63ad9.svg" data-text="E%20%5Cleq%20%5Cfrac%7B5%7D%7B2%7Dm" data-width="65" data-height="38"><img src="https://cdn.nlark.com/__latex/be90b52e69dad1ef3bf2c24d72f63ad9.svg" width="65"/></div>时，使用LC进行估计。

当<div id="74yybg" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/671a9e591e2e36cdb400be85b96b6f55.svg" data-text="%5Cfrac%7B5%7D%7B2%7Dm%20%3C%20E%20%5Cleq%20%5Cfrac%7B1%7D%7B30%7D2%5E%7B32%7D" data-width="134" data-height="38"><img src="https://cdn.nlark.com/__latex/671a9e591e2e36cdb400be85b96b6f55.svg" width="134"/></div>是，使用上面给出的HLLC公式进行估计。

当<div id="691guk" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/28fa502941b68f854066d996df46044e.svg" data-text="E%20%3E%20%5Cfrac%7B1%7D%7B30%7D2%5E%7B32%7D" data-width="81" data-height="38"><img src="https://cdn.nlark.com/__latex/28fa502941b68f854066d996df46044e.svg" width="81"/></div>时，估计公式如为<div id="vlfqkb" data-type="math" data-display="inline" data-align="left" data-src="https://cdn.nlark.com/__latex/997e68b9acf46a672f43972856f0e9b6.svg" data-text="%5Chat%7Bn%7D%3D-2%5E%7B32%7Dlog(1-E%2F2%5E%7B32%7D)" data-width="177" data-height="24"><img src="https://cdn.nlark.com/__latex/997e68b9acf46a672f43972856f0e9b6.svg" width="177"/></div>。

关于分段偏差修正效果分析也可以在原论文中找到。

# 结论

### 并行化
这些基数估计算法的一个好处就是非常容易并行化。对于相同分桶数和相同哈希函数的情况，多台机器节点可以独立并行的执行这个算法；最后只要将各个节点计算的同一个桶的最大值做一个简单的合并就可以得到这个桶最终的值。而且这种并行计算的结果和单机计算结果是完全一致的，所需的额外消耗仅仅是小于1k的字节在不同节点间的传输。

### 应用场景
基数估计算法使用很少的资源给出数据集基数的一个良好估计，一般只要使用少于1k的空间存储状态。这个方法和数据本身的特征无关，而且可以高效的进行分布式并行计算。估计结果可以用于很多方面，例如流量监控（多少不同IP访问过一个服务器）以及数据库查询优化（例如我们是否需要排序和合并，或者是否需要构建哈希表）。

# 参考阅读

[Redis new data structure: the HyperLogLog](http://antirez.com/news/75)
[HyperLogLog — Cornerstone of a Big Data Infrastructure](https://research.neustar.biz/2012/10/25/sketch-of-the-day-hyperloglog-cornerstone-of-a-big-data-infrastructure/)
