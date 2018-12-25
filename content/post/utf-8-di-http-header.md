---
title: "Utf 8 Di Http Header"
date: 2018-12-25T11:46:56+07:00
draft: false
---
Ketika bekerja dengan UTF-8, kita dapat menggunakan pengkodean yang dijelaskan dalam RFC 6266 untuk "Content-Disposition" dan menerjemahkannya ke bahasa Latin dalam kasus lain.

HTTP 1.1 adalah protokol hiperteks yang terkenal untuk transfer data. Pesan HTTP dikodekan dengan ISO-8859-1 (yang secara nominal dapat dianggap sebagai versi ASCII yang disempurnakan, berisi umlaut, diakritik dan karakter lain dari bahasa Eropa Barat). Pada saat yang sama, isi pesan dapat menggunakan pengodean lain yang ditugaskan di header "Tipe Konten". Tapi apa yang harus kita lakukan jika kita perlu menetapkan karakter non-ASCII bukan di badan pesan, tetapi di header? Mungkin kasus yang paling terkenal adalah menetapkan nama file di header "Content-Disposition". Sepertinya ini tugas bersama, tetapi implementasinya tidak jelas

TL; DR: Gunakan penyandian yang dijelaskan dalam RFC 6266 untuk "Disposisi Konten" dan transliterasikan ke dalam bahasa Latin dalam kasus lain.

** Pengantar Encodings **
Artikel itu menyebutkan US-ASCII (biasanya dinamai ASCII), ISO-8859-1, dan pengkodean UTF-8. Berikut ini adalah pengantar kecil untuk pengkodean ini. Paragraf ini untuk pengembang yang jarang bekerja dengan penyandian ini atau tidak menggunakannya sama sekali, dan sebagian telah melupakannya.

ASCII adalah penyandian sederhana dengan 128 karakter, termasuk alfabet Latin, digit, tanda baca, dan karakter utilitas.

7 bit sudah cukup untuk mewakili karakter ASCII. Kata "test" dalam representasi HEX akan terlihat seperti: 0x74 0x65 0x73 0x74. Bit pertama dari setiap karakter akan selalu 0, karena encoding memiliki 128 karakter, dan gigitan memberikan 2 ^ 8 = 256 varian.

ISO-8859-1 adalah penyandian yang ditujukan untuk bahasa-bahasa Eropa Barat. Ini memiliki diakritik, umlaut Jerman, dll.

Pengkodean memiliki 256 karakter, dengan demikian, dapat direpresentasikan dengan 1 byte. Paruh pertama (128 karakter) sepenuhnya cocok dengan ASCII. Karenanya, jika bit pertama = 0, itu adalah karakter ASCII yang biasa. Jika ini 1, kami mengenali karakter ISO-8859-1 tertentu.

UTF-8 adalah salah satu pengkodean paling terkenal bersama dengan ASCII. Ia mampu meng-encode 1.112.064 karakter. Setiap ukuran karakter bervariasi dari 1 hingga 4 gigitan (sebelumnya nilainya bisa hingga 6 gigitan).

Program yang memproses pengkodean ini memeriksa bit pertama dan memperkirakan ukuran karakter dalam byte. Jika oktet dimulai dengan 0, karakter diwakili oleh 1 byte. 110 - 2 byte, 1110 - 3 byte, 11110 - 4 byte.

Seperti halnya dengan ISO-8859-1, 128 pertama akan cocok dengan ASCII. Itulah sebabnya teks yang menggunakan karakter ASCII akan terlihat sama persis dalam representasi biner, terlepas dari pengkodean yang digunakan: US-ASCII, ISO-8859-1 atau UTF-8.

** UTF-8 in the Message Body **
Sebelum kita melanjutkan ke tajuk, mari kita lihat bagaimana UTF-8 digunakan dalam badan pesan. Untuk tujuan itu, kami akan menggunakan tajuk "Tipe Konten".

Jika "Tipe Konten" tidak ditetapkan, browser harus memproses pesan seolah-olah mereka berada di ISO-8859-1. Peramban seharusnya tidak mencoba menebak penyandian, dan tentu saja tidak boleh mengabaikan "Jenis-Konten." Jadi, jika kita mentransfer pesan UTF-8, tetapi tidak menetapkan pengkodean di header, mereka akan dibaca seolah-olah mereka dikodekan dengan ISO-8859-1.

Diterjemahkan dari https://dzone.com/articles/utf-8-in-http-headers