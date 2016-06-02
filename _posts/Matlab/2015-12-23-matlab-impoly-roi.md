---
layout: post
title: "用 impoly 圈選 ROI - Matlab"
category: Matlab Note
tags: [Matlab]
---
{% include JB/setup %}

### [Matlab] 用impoly圈ROI

#### 定量分析

醫學影像最常使用到的定量分析，相信在實驗室待過得都對圈選ROI (Region of Interest) 很熟悉。不需要PMOD等套裝軟件，只要可以image到figure上，matlab也有內建的指令可以達到需求。

```
本次會使用到的重要指令：
* h = impoly(hparent, position)
* BW = createMask(h)
```

#### 首先你得先有個圖片
![phantom-env](/images/2015/12/non-comp-phantom-env.png)

這是一張5MHz單陣元探頭掃的玻璃珠仿體，未壓縮的包絡(envelope)影像

使用`image`或`imagesc`將影像display出來，如上圖，coding可參考：

```Matlab
>> imagesc(env);
>> colormap(gray(40));  % dynamic range = 40dB
>> axis off
```

此時注意目前開啟的figure是哪一張，不是你要圈選得可用，`figure(n)`去挑。n為正整數，這裡就是`figure(1)`。

此時要`impoly`要使用handle，因為後續需要使用。

```Matlab
>> figure(1);
>> h = impoly;
```

此時會跳出畫面像一般畫不規則線一樣點擊節點（此時為十字游標），最後繞一圈回到初始點（變成中空圓心游標），如下圖。

![using impoly](/images/2015/12/impoly-roi.png)

> 拍不出游標的樣子QQ

#### 產生mask

mask是什麼，跟字面上的意思一樣，0擋住、1露出來，所以他是一個`logical object`。
剛剛的handle,`h`代表的是在該父handle(也就是figure)上的某個位置的多邊形，所以產生mask要指定是依據哪個handle。

```Matlab
>> ROI = createMask(h);
```

產生的mask如下圖：

![createMask](/images/2015/12/createMask.png)

其大小會與影像大小一樣大，而被impoly圈出的多邊形則是其保留的部份(該處值均為1)。下圖辨識mask的樣子。

![mask](/images/2015/12/mask.png)

> 因為值只有0與1，所以是黑白的。

#### 定量就是算ROI內的intensity!

所以你需要的是mask中的值，怎麼取得呢？

剛剛說mask裡的是1，不要的地方是0，所以mask與原始檔案`.*`就可以取得要的值了！來試試吧！

```Matlab
>> pos_val = env2(find(env.*ROI)); % 變數中（這裡為env）以find找到的那幾個位置的總和
   % find加一個變數會找所有非0的*位置*
>> val = sum(pos_val(:)); % 若打算計算mask內值的總和
```

一行的寫法：

```Matlab
val = sum(sum(env(find(env.*ROI))));
% 因為env(_position_)依然是一個矩陣，所以要sum兩次
```

#### 要用同樣的mask?

若要在另一個figure使用同樣的mask，剛剛的mask那邊按右鍵點選，`copy position`，你就會得到一串座標，等一下要使用。

![copy-mask](/images/2015/12/copy-mask.png)

接著開另一個figure，這裡是figure(3)。

![other-img](/images/2015/12/other-img.png)

把剛剛複製的座標作為_position_這個`input`

```Matlab
h2 = impoly(gca(figure(3)), position );
% gca為抓取該軸的handle
```

就會變成：

![paste-mask](/images/2015/12/paste-mask.png)

最後用同樣的方法就可以算出這張圖同一個位置的intensity值啦!

#### 更好的方法？

當然，如果你覺得這個方法真是麻煩透了，歡迎您寄信來跟我們分享你的方法！

p.s. 還沒用回覆系統，所以只好請用別的管道跟我說囉！
