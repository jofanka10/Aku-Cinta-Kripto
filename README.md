kita kerjain ini DES yang mumet itu.


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

Lalu, kita lakukan shift left sebanyak 16 sekali, sehingga menghasilkan c1d1 - c16d16. Untuk aturan jumlah biat yang digeser ke kiri, kita menggunakan tabel ini.

<img width="651" height="831" alt="image" src="https://github.com/user-attachments/assets/f83dc115-a8c4-44ae-bd81-9d74a5351179" />

Setelah dilakukan shift left, didapat hasilnya seperti ini. Shift left dilakukan per variabel, misalnya 

```
C1  = 1110000110011001010101011111
D1  = 1010101011001100111100011110

C2  = 1100001100110010101010111111
D2  = 0101010110011001111000111101

C3  = 0000110011001010101011111111
D3  = 0101011001100111100011110101

C4  = 0011001100101010101111111100
D4  = 0101100110011110001111010101

C5  = 1100110010101010111111110000
D5  = 0110011001111000111101010101

C6  = 0011001010101011111111000011
D6  = 1001100111100011110101010101

C7  = 1100101010101111111100001100
D7  = 0110011110001111010101010110

C8  = 0010101010111111110000110011
D8  = 1001111000111101010101011001

C9  = 0101010101111111100001100110
D9  = 0011110001111010101010110011

C10 = 0101010111111110000110011001
D10 = 1111000111101010101011001100

C11 = 0101011111111000011001100101
D11 = 1100011110101010101100110011

C12 = 0101111111100001100110010101
D12 = 0001111010101010110011001111

C13 = 0111111110000110011001010101
D13 = 0111101010101011001100111100

C14 = 1111111000011001100101010101
D14 = 1110101010101100110011110001

C15 = 1111100001100110010101010111
D15 = 1010101010110011001111000111

C16 = 1111000011001100101010101111
D16 = 0101010101100110011110001111
```

Setelah mendapatkan hasilnya, masing-masing variable c dan d dengna angka yang sama (misal c1 dan d1 digabung) lalu di-convert ke 48-bit menggunakan PC-2. Untuk Tabelnya seperti ini

<img width="634" height="446" alt="image" src="https://github.com/user-attachments/assets/6396aac2-eb21-436b-9f38-9faa694331d0" />

Untuk caranya sama seperti yang ada pada PC-1. Setelah itu didapat hasilnya seperti ini (Dari c1d1 akan menjadi k1 setelah menjalani proses ini)

```
K1  = 000110 110000 001011 101111 111111 000111 000001 110010
K2  = 011110 011010 111011 011001 110110 111100 100111 100101
K3  = 010101 011111 110010 001010 010000 101100 111110 011001
K4  = 011100 101010 110111 010110 110110 110011 010100 011101
K5  = 011111 001110 110000 000111 111010 110101 001110 101000
K6  = 011000 111010 010100 111110 010100 000111 101100 101111
K7  = 111011 001000 010010 110111 111101 100001 100010 111100
K8  = 111101 111000 101000 111010 110000 010011 101111 111011
K9  = 111000 001101 101111 101011 111011 011110 011110 000001
K10 = 101100 011111 001101 000111 101110 100100 011001 001111
K11 = 001000 010101 111111 010011 110111 101101 001110 000110
K12 = 011101 010111 000111 110101 100101 000110 011111 101001
K13 = 100101 111100 010111 010001 111110 101011 101001 000001
K14 = 010111 110100 001110 110111 111100 101110 011100 111010
K15 = 101111 111001 000110 001101 001111 010011 111100 001010
K16 = 110010 110011 110110 001011 000011 100001 011111 110101
```

## Proses Enkripsi Data
Untuk melakukan enkripsi, kita gunakan Feistel Cipher.

<img width="732" height="997" alt="image" src="https://github.com/user-attachments/assets/05cd7da2-3a27-4b71-8a2b-47cb1ddacf30" />

Untuk langkah-langkahnya seperti ini.

1. Pada bagian kanan (32-bit R0) melakukan serangkaian ... terhadap kunci pertama (K1) dengan proses sebagai berikut.
   
   a. Perlu diingat bahwa bentuk dari
      K1 = 48-bit
      R0 = 32-bit

   b. Lakukan Initial Permuataion (IP) pada Plaintext M menggunakan tabel IP.
   
      <img width="552" height="286" alt="image" src="https://github.com/user-attachments/assets/b88c84a5-586d-4f7c-b786-cf7343c2e35a" />

      Sehingga Plantext yang sebelumnya
      ```
      M = 0000 0001 0010 0011 0100 0101 0110 0111 1000 1001 1010 1011 1100 1101 1110 1111
      ```
      menjadi seperti ini
      ```
      L0 = 1100 1100 0000 0000 1100 1100 1111 1111
      R0 = 1111 0000 1010 1010 1111 0000 1010 1010
      ```
      Note: Setelah melakukan Initial Permutation, Plaintext M langsung dibagi dua kiri kanan (masing-masing 32-bit).


   c. Kita perlu udah R0 ini ke format 48-bit menggunakan E-Bits.
   
      <img width="765" height="533" alt="image" src="https://github.com/user-attachments/assets/c24b5291-9875-4d82-a6f2-305a2b4dec15" />

      Sehingga R0 yang sebelumnya
      ```
      R0 = 1111 0000 1010 1010 1111 0000 1010 1010
      ```
      menjadi
      ```
      R0 48-bit = 011110 100001 010101 010101 011110 100001 010101 010101
      ```

      Setelah itu, R0 di-XOR-kan dengan K1
      ```
      R0 48-bit      = 011110 100001 010101 010101 011110 100001 010101 010101
      K1             = 000110 110000 001011 101111 111111 000111 000001 110010
                       ——————————————————————————————————————————————————————— ⊕
      R0 48-bit ⊕ K1 = 011000 010001 011110 111010 100001 100110 010100 100111
      ```


      Hasil XOR tadi diubah dari 48-bit menjadi 32-bit menggunakan S-Box.

      <img width="1685" height="796" alt="image" src="https://github.com/user-attachments/assets/81dd24b9-1f32-43f4-9fa9-1bdd7936cf83" />



   





