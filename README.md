# matplotlib-
Pytonのmatplotlibモジュールを使って化学における中和滴定曲線を描く  
![](https://github.com/Xiong-yinghao/Titration-curve-with-Python/blob/main/%E4%B8%AD%E5%92%8C%E6%BB%B4%E5%AE%9A.png?raw=true)
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
得られたxとyのリストをセットし、list(zip(x, y))でセットを含むリストにした。これをdf.to_csv("滴定曲線.csv", index=False)により、csvファイルとして保存した。何故かローカルファイルに保存するという、データの完全性を保つからだ。続いて、保存されたファイルを一度読み込んだ。  
x軸を滴下量[ml]、y軸をPH、plt.scatter(x, y, cmap='rainbow', marker='o', c=y, alpha=.5, s=100)を用いてPHと滴下量[ml]に関する散布図を描いた。
