# **Richardson Extrapolation**

> Dalam analisis numerik, Richardson Extrapolation adalah metode percepatan urutan, yang digunakan untuk meningkatkan laju konvergensi suatu urutan. 
>
> Richardson Extrapolation termasuk integrasi Romberg, yang menerapkan ekstrapolasi Richardson pada aturan trapesium, dan algoritma Bulirsch-Stoer untuk menyelesaikan persamaan diferensial biasa.



### **Teori**

Dalam rumus :

***( f (x + h) - f (x - h) ) / (2 h)***

untuk nilai h yang sangat kecil, dua fungsi evaluasi *f (x + h)* dan *f (x - h)* akan menjadi kira-kira sama, dan oleh karena itu pembatalan subtraktif akan terjadi. Oleh karena itu, tidak disarankan untuk menggunakan nilai h yang semakin kecil.

Kita dapat mencoba untuk memperkirakan nilai tepat *e* dengan perkiraan *a(h)*. Dalam hal ini, *e* adalah turunan dari *f (1) (x)* dan perkiraannya adalah *( h ) = (f (x + h) - f (x - h)) / (2 h)*. Misalkan sekarang bahwa kesalahan aproksimasi didefinisikan oleh serangkaian bentuk Taylor :

<p align = "center"><i>e = a(h) + K h<sup>n</sup> + o(h<sup>n</sup>)</i></p>

Apabila menggunakan *h / 2* :

<p align = "center"><i>e = a(h/2) + K (h/2)n + o((h/2)n)</i>
<br><i>= a(h/2) + K/2n h<sup>n</sup> + o(h<sup>n</sup>)</i></p>

Mengalikan kedua ekspresi ini dengan 2*n* dan mengurangi hasil persamaan pertama

<p align = "center"><i>2n<sup>e</sup> − e = 2na(h/2) − a(h) + K/2n h<sup>n</sup> − K h<sup>n</sup> + o(h<sup>n</sup>)</i></p>

Perhatikan bahwa istilah h<sup>n</sup> dibatalkan dan kita dibiarkan dengan

<p align = "center"><i>(2n − 1)e = 2na(h/2) − a(h) + o(h<sup>n</sup>)</i></p>

Jika kita melihat seri Taylor lengkap untuk rumus perbedaan-terpusat yang terpusat, kita perhatikan bahwa istilah kesalahannya dalam bentuk Knh<sup>n</sup>. Dapat kita tulis dengan :

<p align = center><i>K1 = −1/6 f(3)(x)h<sup>2</sup>, etc.</i></p>

### **Contoh Program**

```python
from math import *
def zeros(n,m):
    Z=[]
    for i in range(n):
        Z.append([0]*m)
    return Z

def D(Func,a,h):
        return (Func(a+h)-Func(a-h))/(2*h)

def Richardson_dif(func,a):
    k=9 
    L=zeros(k,k)
    for I in range(k):
        L[I][0]=D(func,a,1/(2**(I+1)))
    for j in range(1,k):
        for i in range(k-j):
            L[i][j]=((4**(j))*L[i+1][j-1]-L[i][j-1])/(4**(j)-1)
    return L[0][k-1]
    
print('f(x) = -0.1*x**4-0.15*x**3-0.5*x**2-0.25*x+1.2 dengan x = 0.5')
print('Hasil Diferensiasi Numerik= '+'%04.20f'%Richardson_dif(lambda x: -0.1*x**4-0.15*x**3-0.5*x**2-0.25*x+1.2 ,0.5))
print('diff(2**cos(pi+sin(x)) dengan x = pi/2 adalah = %04.20f'%Richardson_dif(lambda x: 2**cos(pi+sin(x)),pi/3))

```

### **Hasil Running**

```python
f(x) = -0.1*x**4-0.15*x**3-0.5*x**2-0.25*x+1.2 dengan x = 0.5
Hasil Diferensiasi Numerik= -0.91250000000000530687
diff(2**cos(pi+sin(x)) dengan x = pi/2 adalah = 0.16849558398154249050
```

