# P2_Probstat_F_5025201051
## Muhammad Fath Mushaffa Azhar - 5025201051

## Soal 1
### Soal 1.a
Memasukkan semua data ke sebuah variabel
```
before <- c(78, 75, 67, 77, 70, 72, 28, 74, 77)
after <- c(100, 95, 70, 90, 90, 90, 89, 90, 100)
```
Setelah itu hitung standart deviasi before dan after
```
sd_sebelum <- sd(before)
sd_sesudah <- sd(after)
```
### Soal 1.b
Menggunakan t.test 
```
t.test(before, after, alternative = "greater", var.equal = FALSE)
```
### Soal 1.c
Untuk melihat pengaruh jika tingkat signifikasi 5% dan tidak ada pengaruh yang signifikan secara statistika
```
t.test(before, after, mu = 0, alternative = "two.sided", var.equal = TRUE)
```

## Soal 2
### Soal 2.a
Setuju, karena uji z menolak H0

### Soal 2.b
Diketahui n = 100, Rata-Rata (X̄) = 23500, dan standar deviasi(σ) = 3900
```
tsum.test(mean.x=23500, sd(3900), n.x=100)
```
### Soal 2.c
Dari hasil perhitungan dapat disimpulkan bahwa mobil dikemudikan rata-rata lebih dari 20.000 kilometer per tahun

## Soal 3
### Soal 3.a
H0 = 9.50
H1 = 10.98
### Soal 3.b
Menggunakan fungsi `tsum.test` 
```
tsum.test(mean.x=3.64, s.x = 1.67, n.x = 19, 
          mean.y =2.79 , s.y = 1.32, n.y = 27, 
          alternative = "greater", var.equal = TRUE)
```
### Soal 3.c
Menggunakan bantuan library `mosaic`
```

```
