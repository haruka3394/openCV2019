

# ディジタル信号処理と画像処理　レポート課題

## B172170  北川大輝


- OpenCVを用いて，カメラ画像を取得し，毎フレームの輝度の平均値を出力，グラフにプロットするプログラムを作成する．

以下のソースコードのように実装した．

``` Python

%matplotlib nbagg

import numpy as np
import cv2
import matplotlib.pyplot as plt



y = [0] * 500
i = 0

cam = cv2.VideoCapture(0)
while True:
    _, img = cam.read()
    y[i] = img.mean()
    i += 1

    cv2.imshow('PUSH ENTER KEY', img)
    if cv2.waitKey(1) == 13: break

        cam.release()
cv2.destroyAllWindows()

ave_y = sum(y[20: i-20]) / len(y[20:i-20])
x = np.linspace(0, 500, 500)
plt.plot(x, y)
plt.xlabel("times")
plt.ylabel("mean of image")
plt.xlim([10, i-10])
plt.ylim([ave_y-5, ave_y +5])
plt.title("Finger blood flow")
plt.savefig('Finger.pdf')
plt.show()

```
- インポートしたライブラリは，numpy，cv2，matplotlibの３種類
    - numpy ：array型の変数を使用するため．
    - cv2：openCVを使用するため．
    - matplotlib.pyplot：グラフを表示させるため．

-
