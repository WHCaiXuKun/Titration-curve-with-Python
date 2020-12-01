# matplotlib
Pytonのmatplotlibモジュールを使って化学における中和滴定曲線を描く。

![](https://github.com/Xiong-yinghao/Titration-curve-with-Python/blob/main/%E4%B8%AD%E5%92%8C%E6%BB%B4%E5%AE%9A.png?raw=true)

- [PH滴定分析](https://github.com/Xiong-yinghao/Titration-curve-with-Python/blob/main/PH%E6%BB%B4%E5%AE%9A%E6%9B%B2%E7%B7%9A.ipynb)
- [図１ 中和滴定曲線](https://github.com/Xiong-yinghao/Titration-curve-with-Python/blob/main/%E4%B8%AD%E5%92%8C%E6%BB%B4%E5%AE%9A.png)

### 概要
水素イオン濃度の異なる二種の溶液をガラスの薄膜でへだてると水素イオンに関する一種の濃淡電池が形成され、薄膜の両側のポテンシャル差は両液のpH差と関係づけられ、ガラス薄膜はプロトンセンサ一として利用できる。
pHは厳密には、(1)式に示すように定義される(aH+は水素イオンの活量) が、この量を実験的に測定することは困難である。それゆえに測定に用いたセル(電池)の起電カによってpHを定義するのが好ましい。   
![](https://latex.codecogs.com/gif.latex?pH%3Dlog%5Cfrac%7B1%7D%7Ba_%7BH%5E&plus;%7D%7D%3D-loga_%7BH%5E&plus;%7D) ....(1)  
弱酸または弱塩基の中和反応で当量点でのpHが急変するので、pH変化からいずれか一方の既知濃度の標準液を用いて他方の濃度を求めることができる。
強酸による弱塩基(B)の滴定における溶液内平衡には次のようなものがある。  
![][1]  
これらの平衡定数は次のようになる。  
![][2]　　
ここで、Ka・Kb=kwとなることがわかる。  

- 滴定開始前(弱塩基Bの水溶液)には    　
![][3]C:Bの濃度   

- 当量点前では   
![][4]  

- 当量点(強酸ー弱塩基の水溶液)では    
![][5]C:塩[BH+]の濃度  

- 当量点後(BH+の解離は無視できる)  
![][6]C:酸の濃度  
と近所的に水素イオンまたは水酸化イオンが求められる。滴定曲線は図1のようになり、生成する塩が加水分解を受けて酸性を呈するので指示薬は酸性側で変色するものを用いなければならない。


```
x = [i for i in range(21)]
for j in range(1,41):
    a = j/5
    a = a + 20
    x.append(a)

for i in range(28,36):
    x.append(i)
```  

x[ml]を滴下量とする、以上でxをリストを作った。最初0mlから20mlまで１mlずつ滴下した。その後20mlから２８mlまで0.2mlずつ滴下した。
yをPHとする、PHの値はPH電極(プロントセンサー)により測定できる。

```
DataSet = list(zip(x, y))
```

得られたxとyのリストをセットし、list(zip(x, y))でセットを含むリストにした。これをdf.to_csv("滴定曲線.csv", index=False)により、csvファイルとして保存した。何故かローカルファイルに保存するという、データの完全性を保つからだ。続いて、保存されたファイルを一度読み込んだ。見やすため、図の色をrainbowにした。
x軸を滴下量[ml]、y軸をPH、plt.scatter(x, y, cmap='rainbow', marker='o', c=y, alpha=.5, s=100)を用いてPHと滴下量[ml]に関する散布図を描いた。

```
plt.figure(figsize=(20,8), dpi=80)
plt.title("滴定曲線", fontproperties=my_font, size=24)
plt.xlabel("滴下量[ml]", fontproperties=my_font, size=24)
plt.ylabel("PH", size=24)
plt.scatter(x, y, cmap='rainbow', marker='o', c=y, alpha=.5, s=100)
plt.grid(True)
plt.figure(figsize=(20,8), dpi=80)
plt.savefig("滴定曲線.jpg")
plt.show()
```

[1]:https://latex.codecogs.com/gif.latex?H_2O%20%5Crightleftharpoons%20H%5E&plus;%20&plus;%20OH%5E-%5C%5C%20B%20&plus;%20H%5E&plus;%20%5Crightleftharpoons%20BH%5E&plus;%5C%5C%20B%20&plus;%20H_2O%20%5Crightleftharpoons%20BH%5E&plus;%20&plus;%20OH%5E-
[2]:https://latex.codecogs.com/gif.latex?%5BH%5E&plus;%5D%5BOH%5E-%5D%20%3D%20K_w%5C%5C%20%5Cfrac%7B%5BB%5D%5BH%5E&plus;%5D%7D%7B%5BBH%5E&plus;%5D%7D%20%3D%20K_a%5C%5C%20%5Cfrac%7B%5BBH%5E&plus;%5D%5BOH%5E-%5D%7D%7B%5BB%5D%7D%20%3D%20K_b
[3]:https://latex.codecogs.com/gif.latex?%5BOH%5E-%5D%20%3D%20%5Csqrt%7BC%5Ccdot%20K_b%7D
[4]:https://latex.codecogs.com/gif.latex?%5BOH%5E-%5D%20%3D%20%28%5BB%5D/%5BBH%5E&plus;%5D%29%20%5Ccdot%20K_b
[5]:https://latex.codecogs.com/gif.latex?%5BH%5E&plus;%5D%20%3D%20%5Csqrt%7B%28K_w/K_b%29%5Ccdot%20C%7D
[6]:https://latex.codecogs.com/gif.latex?%5BH%5E&plus;%5D%20%5Capprox%20C
