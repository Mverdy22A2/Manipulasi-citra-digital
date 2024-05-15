# Manipulasi-citra-digital

# modul
```
import cv2
```

# original image
```
image = cv2.imread('many fruits.png')
imagecopy= image.copy()
cv2.imshow( 'Original image' , image )
cv2.waitKey(0)
cv2.destroyAllWindows()
```

![image](https://github.com/Mverdy22A2/Manipulasi-citra-digital/assets/115523263/9888dd71-fa01-4dac-8ada-80808440c6fe)

# Gray
```
gray_image = cv2.cvtColor(image,cv2.COLOR_BGR2GRAY)
cv2.imshow( 'gray' , gray_image )
cv2.waitKey(0)
cv2.destroyAllWindows()
```

![image](https://github.com/Mverdy22A2/Manipulasi-citra-digital/assets/115523263/a0e59ff3-ea7f-494c-8559-2ea3f4d9fff3)

# binary
```
ret,binary_im = cv2.threshold(gray_image,245,255,cv2.THRESH_BINARY)
cv2.imshow( 'binary' , binary_im )
cv2.waitKey(0)
cv2.destroyAllWindows()
```

![image](https://github.com/Mverdy22A2/Manipulasi-citra-digital/assets/115523263/fc7c7975-90cf-4c69-ba88-cf39bc7e8075)

# inverted binary
```
binary_im= ~binary_im
cv2.imshow( 'inverted binary' , binary_im )
cv2.waitKey(0)
cv2.destroyAllWindows()
```

![image](https://github.com/Mverdy22A2/Manipulasi-citra-digital/assets/115523263/7831bb11-387d-4c8d-bf8e-3a4fa44e3b34)

```
contours, hierarchy = cv2.findContours(binary_im,cv2.RETR_EXTERNAL,cv2.CHAIN_APPROX_SIMPLE)
```

# contours marked on RGB image
```
with_contours = cv2.drawContours(image,contours,-1,(0,0,255),3)
cv2.imshow( 'contours marked on RGB image' , with_contours )
cv2.waitKey(0)
cv2.destroyAllWindows()
```

![image](https://github.com/Mverdy22A2/Manipulasi-citra-digital/assets/115523263/88794889-9170-494b-a50d-a91eb6ee53e8)

# Refrence image
```
ref_image = cv2.imread('bananaref.png')
cv2.imshow( 'Reference image' , ref_image )
cv2.waitKey(0)
cv2.destroyAllWindows()
```

![image](https://github.com/Mverdy22A2/Manipulasi-citra-digital/assets/115523263/eccccc55-3679-4b81-bc7d-4944cd9871c6)

# Grayscale image
```
gray_image = cv2.cvtColor(ref_image,cv2.COLOR_BGR2GRAY)
cv2.imshow( 'Grayscale image' , gray_image )
cv2.waitKey(0)
cv2.destroyAllWindows()
```

![image](https://github.com/Mverdy22A2/Manipulasi-citra-digital/assets/115523263/a622b3a9-f6a0-4607-a17b-c48b1ae4c0cf)

# Binary image
```
ret,binary_im = cv2.threshold(gray_image,245,255,cv2.THRESH_BINARY)
cv2.imshow( 'Binary image' , binary_im )
cv2.waitKey(0)
cv2.destroyAllWindows()
```

![image](https://github.com/Mverdy22A2/Manipulasi-citra-digital/assets/115523263/0e2c6641-6cec-4696-86d5-3792a32562dd)

```
binary_im= binary_im
cv2.imshow( 'inverted binary image' , binary_im )
cv2.waitKey(0)
cv2.destroyAllWindows()
```

```
reference_contour = contours[0]
```

```
# Buat list kosong untuk menyimpan hasil perbandingan
dist_list = []

# Loop melalui setiap kontur dalam contours
for cnt in contours:
    # Hitung kesamaan bentuk antara kontur saat ini dan reference_contour
    retval = cv2.matchShapes(cnt, reference_contour, 1, 0)
    # Tambahkan hasil ke dalam list dist_list
    dist_list.append(retval)
```

```
sorted_list= dist_list.copy()
sorted_list.sort() # sorts the list from smallest to largest
ind1_dist= dist_list.index(sorted_list[0])
ind2_dist= dist_list.index(sorted_list[1])
```

```
banana_cnts= []
banana_cnts.append(contours[ind1_dist])
banana_cnts.append(contours[ind2_dist])
```

```
with_contours = cv2.drawContours(image,banana_cnts,-3,(255,2,0),3)
cv2.imshow( 'contours marked on RGB image' , with_contours )
cv2.waitKey(0)
cv2.destroyAllWindows()
```


```
for cnt in banana_cnts:
    x, y, w, h = cv2.boundingRect(cnt)
    if h > w:
        # Calculate the center and radius of the circle
        center = (x + w // 2, y + h // 2)
        radius = max(w, h) // 2
        # Draw the circle
        cv2.circle(imagecopy, center, radius, (255, 0, 0), 5)

cv2.imshow('Upright banana marked on RGB image', imagecopy)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

