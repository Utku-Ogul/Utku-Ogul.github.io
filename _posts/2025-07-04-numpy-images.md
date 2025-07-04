---
title: NumPy ile Görsel İşleme
date: 2025-07-04 15:00:00 +0300
categories: [NumPy, OpenCV, Python]
tags: [numpy, görüntü işleme, python, pil]
description: NumPy, PIL ve matplotlib kullanarak bir görselin kırmızı kanal ayrıştırması ve görselleştirilmesi işlemleri.
---

## 🐶 Görsel Yükleme (PIL ile)

```python
from PIL import Image

pic = Image.open('00-puppy.jpg')
```

**Açıklama:**  
- `Image.open(...)`: JPEG görsel dosyasını açar ve `pic` nesnesine atar.

![Köpek görseli](/assets/img/00-puppy.jpg)
_Kaynak: momswhothink.com — [Orijinal Sayfa](https://www.momswhothink.com/male-dog-names-j/)_

---

## 🧪 Görseli NumPy Dizisine Çevirme

```python
import numpy as np

pic_arr = np.asarray(pic)
pic_arr.shape
```

**Açıklama:**  
- `np.asarray(pic)`: Görseli NumPy dizisine çevirir.
- `.shape`: Dizi boyutu → (yükseklik, genişlik, kanal sayısı)

---

## 🎨 Kırmızı Kanal Görselleştirmesi (colormap ile)

```python
import matplotlib.pyplot as plt

plt.imshow(pic_arr[:,:,0])
plt.show()
```

![Kırmızı Kanal - Normal Colormap](/assets/img/Figure_1.png)  
_Kırmızı kanalın `viridis` (default) colormap ile görselleştirilmiş hali_

---

## 🖤 Kırmızı Kanalı Gri Tonlamayla Görselleştirme

```python
plt.imshow(pic_arr[:,:,0], cmap='gray')
plt.show()
```

![Kırmızı Kanal - Gri Ton](/assets/img/Figure_2.png)  
_Kırmızı kanalın grayscale olarak görselleştirilmiş hali_

---

## 🔴 Sadece Kırmızı Kanalın Gösterilmesi

```python
pic_red = pic_arr.copy()
pic_red[:, :, 1] = 0
pic_red[:, :, 2] = 0

plt.imshow(pic_red)
plt.show()
```

![Yalnızca Kırmızı Kanal](/assets/img/Figure_3.png)  
_Yalnızca kırmızı kanal verisi ile yeniden oluşturulmuş görsel_

---

Bu çalışma, renk kanalları üzerinde işlem yapmayı öğrenmek için temel bir örnektir. NumPy ve matplotlib ile farklı renk filtreleri ve efektler uygulanabilir.
