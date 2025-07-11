---
title: OpenCV ile Görsel Açma ve İşleme
date: 2025-07-04 18:00:00 +0300
categories: [OpenCV, Python]
tags: [opencv, görüntü işleme, python]
description: Bu yazıda OpenCV ile görsel okuma, RGB dönüşümü, colormap uygulamaları ve yeniden boyutlandırma işlemleri ele alınmıştır.
---

## 🖼️ Görseli OpenCV ile Okuma

```python
import cv2

img = cv2.imread('00-puppy.jpg')
print(type(img))
print(img.shape)
```

**Açıklama:**  
- `cv2.imread(...)`: Görsel dosyasını okur.  
- `type(img)` → `numpy.ndarray` türünde bir çıktı verir.  
- `.shape` → (yükseklik, genişlik, kanal sayısı)

![Orijinal Görsel (OpenCV BGR)](/assets/img/ImageBasicsWithOpenCV/Figure_1.png)  
_Kaynak: [momswhothink.com - Dog Names Starting with J](https://www.momswhothink.com/male-dog-names-j/)_

---

## 🔁 BGR'den RGB'ye Dönüşüm

```python
fix_img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
plt.imshow(fix_img)
plt.show()
```

![RGB'ye Dönüştürülmüş Görsel](/assets/img/ImageBasicsWithOpenCV/Figure_2.png)  
_Matplotlib ile doğru gösterim için RGB formatına çevrilmiş hali_

---

## ⚫ Görseli Grayscale Olarak Okuma

```python
img_gray = cv2.imread('00-puppy.jpg', cv2.IMREAD_GRAYSCALE)
plt.imshow(img_gray, cmap='gray')
```

![Gri Tonlamalı Görsel](/assets/img/ImageBasicsWithOpenCV/Figure_3.png)  
_Görsel grayscale olarak okunup gösterildi_

---

## 🔥 Magma Colormap ile Görselleştirme

```python
plt.imshow(img_gray, cmap='magma')
```

![Magma Colormap](/assets/img/ImageBasicsWithOpenCV/Figure_4.png)  
_Grayscale görsel üzerine magma colormap uygulanmış hali_

---

## 📏 Görseli Sabit Boyuta Yeniden Boyutlandırma

```python
new_img = cv2.resize(fix_img, (1000, 400))
plt.imshow(new_img)
```

![1000x400 Boyutlu Görsel](/assets/img/ImageBasicsWithOpenCV/Figure_5.png)  
_Görsel 1000x400 boyutuna yeniden ölçeklendi_

---

## 📐 Görseli Yüzde 50 Ölçekleme

```python
w_ratio = 0.5
h_ratio = 0.5
new_img = cv2.resize(fix_img, (0, 0), fx=w_ratio, fy=h_ratio)
plt.imshow(new_img)
```

![%50 Ölçekli Görsel](/assets/img/ImageBasicsWithOpenCV/Figure_6.png)  
_Görsel orijinal boyutunun %50’sine küçültüldü_

---

## 🔃 Görseli Dikey Olarak Çevirme

```python
new_img = cv2.flip(new_img, 0)
```

![Dikey Flip](/assets/img/ImageBasicsWithOpenCV/Figure_7.png)  
_Görsel dikey olarak çevrildi (flip vertical)_

---

## 🔄 Görseli Yatay Olarak Çevirme

```python
new_img = cv2.flip(new_img, 1)
```

![Yatay Flip](/assets/img/ImageBasicsWithOpenCV/Figure_8.png)  
_Görsel yatay olarak çevrildi (flip horizontal)_

---

## 🔁 Görseli Hem Dikey Hem Yatay Çevirme

```python
new_img = cv2.flip(new_img, -1)
```

![Çift Flip](/assets/img/ImageBasicsWithOpenCV/Figure_9.png)  
_Görsel hem dikey hem yatay çevrildi_

---

## 💾 Yeni Görseli Kaydetme

```python
cv2.imwrite('my_new_picture.jpg', new_img)
```

![Kaydedilen Yeni Görsel](/assets/img/ImageBasicsWithOpenCV/Figure_10.png)  
_Değişiklik yapılmış haliyle yeni görsel dosyaya yazıldı_

---

## 🧩 Matplotlib ile Subplot Üzerinde Gösterme

```python
fig = plt.figure(figsize=(10, 8))
ax = fig.add_subplot(111)
ax.imshow(fix_img)
plt.show()
```

![Subplot ile Görsel](/assets/img/ImageBasicsWithOpenCV/my_new_picture.jpg)  
_Renk uzayı düzeltilmiş görsel subplot ile gösterildi_
