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
install.packages("mosaic")
library(mosaic)

plotDist(dist='t', df=2, col="green")
```
### Soal 3.d
Untuk menghitung sampel statistik dapat menggunakan fungsi `qchisq` dengan `df=2
```
qchisq(p = 0.05, df = 2, lower.tail=FALSE)
```
### Soal 3.e
       Untuk mendapatkan keputusan diperlukan bantuan dengan Teori Keputusan
       Teori keputusan adalah teori formal pengambilan keputusan di bawah ketidakpastian. 
       Aksinya adalah : `({a}_{a∈A})`
       Kemungkinan konsekuensi : `({c}_{c∈C})` (tergantung pada keadaan dan tindakan)
       Maka keputusan dapat dibuat dengan `t.test`
### Soal 3.f
Kesimpulan yang didapatkan yaitu perbedaan rata-rata yang terjadi tidak ada jika dilihat dari uji statistik dan akan ada tetapi tidak signifikan jika dipengaruhi nilai kritikal.

## Soal 4
### Soal 4.a
mengambil data dari link yang telah disediadakan
```
myData  <- read.table(url("https://rstatisticsandresearch.weebly.com/uploads/1/0/2/6/1026585/onewayanova.txt")) 
dim(myData)
head(myData)
attach(myData)
```
Selanjutnya membuat myFile menjadi group 
```
myData$V1 <- as.factor(myData$V1)
myData$V1 = factor(myData$V1,labels = c("Kucing Oren","Kucing Hitam","Kucing Putih","Kucing Oren"))
```
Setelah itu, dicek apakah dia menyimpan nilai di groupnya
```
class(myData$V1)
```
Lalu bagi tiap valuer menjadi 3 bagian ke 3 grup
```
group1 <- subset(myData, V1=="Kucing Oren")
group2 <- subset(myData, V1=="Kucing Hitam")
group3 <- subset(myData, V1=="Kucing Putih")
```

## Soal 5
### Soal 5.a
Run semua library yang diperlukan 
```
install.packages("multcompView")
library(readr)
library(ggplot2)
library(multcompView)
library(dplyr)
```
Selanjutnya membaca file GTL.csv dari documents
```
GTL <- read_csv("C:/Users/azhar/Downloads/GTL.csv")
head(GTL)
```
Lakukan observasi pada data
```
str(GTL)
```
Selanjutnya lakukan viasualisasi menggunakan simple plot yaitu sebagai berikut
```
qplot(x = Temp, y = Light, geom = "point", data = GTL) +
  facet_grid(.~Glass, labeller = label_both)
```
### Soal 5.b
Langkah pertama adalah membuat variabel as factor sebagai ANOVA
```
GTL$Glass <- as.factor(GTL$Glass)
GTL$Temp_Factor <- as.factor(GTL$Temp)
str(GTL)
```
Selanjutnya melakukan analisis of variance (aov) yaitu sebagai berikut 
```
anova <- aov(Light ~ Glass*Temp_Factor, data = GTL)
summary(anova)
```
### Soal 5.c
Menggunakan `group_by` lalu melakukan `summarise` sesuai mean dan standar deviasi yang berlaku sehingga scriptnya adalah sebagai beriku
```
data_summary <- group_by(GTL, Glass, Temp) %>%
  summarise(mean=mean(Light), sd=sd(Light)) %>%
  arrange(desc(mean))
print(data_summary)
```
### Soal 5.d
Menggunakan fungsi `TukeyHSD` sebagai berikut
```
tukey <- TukeyHSD(anova)
print(tukey)
```
### Soal 5.e
membuat compact letter display sebagai berikut
```
tukey.cld <- multcompLetters4(anova, tukey)
print(tukey.cld)
```
Tambahkan compact letter display tersebut ke tabel dengan means(rata-rata) dan sd
```
cld <- as.data.frame.list(tukey.cld$`Glass:Temp_Factor`)
data_summary$Tukey <- cld$Letters
print(data_summary)
```
