Gas kita kerjain ini DES yang mumet itu.


# Tugas <img width="1246" height="193" alt="image" src="https://github.com/user-attachments/assets/46b0aeb1-9c41-45e2-9ed9-15058c09f51b" />
Nama: Jofanka Al-Kautsar Pangestu Abady

NRP: 5027241107

## Step Awal
Konversi ke biner
| Heksadesimal | Biner |
|---|---|
| 0 | 0000 |
| 1 | 0001 |
| 2 | 0010 |
| 3 | 0011 |
| 4 | 0100 |
| 5 | 0101 |
| 6 | 0110 |
| 7 | 0111 |
| 8 | 1000 |
| 9 | 1001 |
| A | 1010 |
| B | 1011 |
| C | 1100 |
| D | 1101 |
| E | 1110 |
| F | 1111 |

Plaintext
```
M = 0123456789ABCDEF -> 0000 0001 0010 0011 0100 0101 0110 0111 1000 1001 1010 1011 1100 1101 1110 1111
K = 133457799BBCDFF1 -> 0001 0011 0011 0100 0101 0111 0111 1001 1001 1011 1011 1100 1101 1111 1111 0001
```

## Proses Membuat Sub-key
```
K 64-bit = 0001 0011 0011 0100 0101 0111 0111 1001 1001 1011 1011 1100 1101 1111 1111 0001
```

<img width="541" height="315" alt="image" src="https://github.com/user-attachments/assets/99d4f8f3-8d89-427a-8665-efe28554d24a" />

Mengubah key yang sebelumnya berformat 64-bit menjadi 56-bit menggunakan PC-1. Setiap bit urutan kelipatan 8 (8, 16, 32, dst) akan dihapus. Kita ambil contoh bit ke-7 (bernilai 1) menjadi urutan ke9 di 56-bit, sehingga didapat hasil K sebegai berikut.
```
K 56-bit = 1111000 0110011 0010101 0101111 0101010 1011001 1001111 0001111
```

Selanjutnya, nilai K ini dibagi menjadi dua bagian kiri dan kanan, yaitu c0 dan d0 dengan masing-masing 28-bit
```
C0 = 1111000011001100101010101111
D0 = 0101010101100110011110001111
```
