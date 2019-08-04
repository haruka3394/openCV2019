# ディジタル信号処理と画像処理　OpenCvを用いた画像処理

B173394 

- OpenCVを用いてカメラ画像を取得し, 毎フレームの輝度の平均値を出力する. またその値をグラフにプロットする. 

以下にソースコードを示す. まずAnacondaをインストールし, JupyterにてOpenCVをインストールした. 

``` Python
!pip install opencv-python
```

``` Python
import cv2
import numpy as np
import matplotlib.pyplot as plt

y=[]

capture = cv2.VideoCapture(0)

while(True):
    ret, frame = capture.read()
    gray = cv2.cvtColor(frame, cv2.COLOR_RGB2GRAY)
    avr = np.average(gray)
    print(avr)
    y.append(avr)
    cv2.imshow('frame',gray)
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break


print(len(y))
x=np.linspace(1,100,len(y))
capture.release()
cv2.destroyAllWindows()
plt.plot(x, y, label="test")
plt.show()
```
- コードの説明
  - cv2 (openCVを使用する), numpy as np (array型の変数を使用する),  matplotlib.pyplot as plt (グラフを表示させる)ライブラリをインポートする. 
  
  - `y = []` : 配列を得ている
  - `capture = cv2.VideoCapture(0)` : カメラのキャプチャを開始させる. 
  ``` Phython
    while(True):
    ret, frame = capture.read()
    gray = cv2.cvtColor(frame, cv2.COLOR_RGB2GRAY)
    avr = np.average(gray)
    print(avr)
    y.append(avr)
    cv2.imshow('frame',gray)
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break
    ```
  - このwhile文でキーボードからqを入力されるまで画像を取得して基礎値の平均を取っている. これは毎フレームごとに行われる. 
    - `capture.read()` : カメラから画像を取得する. それをframeに入れている. 
    - `gray = cv2.cvtColor(frame, cv2.COLOR_RGB2GRAY)` : 画像をグレースケールに変換している. 
    - `avr = np.average(gray)` : グレースケールに変換した画像の輝度値の平均値を取っている.  
    - `print(avr)` : 輝度値の平均値を表示させている. 
    - `y.append(avr)` : yに輝度値の平均値の値を入れて行っている. 
    - `cv2.imshow('frame',gray)` : カメラの画像をウィンドウに出力している. 
    
  - `print(len(y))` : 輝度値の平均値がいくつあるかを表示させている. 
  - `x=np.linspace(1,100,len(y))` : xを定義している. 1から100までを輝度値の平均値の個数で割っている. 
  - `capture.release(), cv2.destroyAllWindows()` : カメラから得ているキャプチャを終了し, ウィンドウを閉じる. 
  - `plt.plot(x, y, label="test"), plt.show()` : w,yの値を表示させている. 
  
  
- 実行結果  
今回の課題は, カメラに指を押し当て脈拍を図るというものだった. これは指に光をあてることで指を透過し, 光の微量な変化を読み込み, 輝度値の平均としてグラフに表示している. 以下にグラフを表示する. 

![](opencv-2.pdf)

これにより脈拍をグラフの一定の変化により確認することができる. また, 輝度値の値をkidoti.txtに示し, ウィンドウの画像の変化をGIFに示す. GIFファイルからも光の微量な変化を見ることができる. 

![](openCV.gif)

- バージョン
    - macOS Mojave 10.14.5
    - Pyhton 3.7

- 参考文献
  - [matplotlibでのプロットの基本](https://qiita.com/KntKnk0328/items/5ef40d9e77308dd0d0a40)  
  matplotでグラフをプロットする方法
  
  - [Pythonでリストサイズを取得](https://note.nkmk.me/python-list-len/)  
  リストサイズの取得
  
  - [配列の要素の平均を求めるNumPyのaverage関数とmean関数の使い方](https://deepage.net/features/numpy-average.html)  
  配列(画像)の要素の平均を求める
  
  - [OpenCV 接続したカメラから動画を取得しよう (Python)](https://weblabo.oscasierra.net/python/opencv-videocapture-camera.html)  
  ビデオからの画像取得
  
  - [PythonとOpenCVで画像をグレースケールに変換してみた](https://water2litter.net/gin/?p=1757)  
  画像をグレースケールに変換 
