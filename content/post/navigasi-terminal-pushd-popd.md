---
title: "Navigasi Terminal Pushd Popd"
date: 2018-12-25T11:35:36+07:00
draft: false
---
# Menavigasi Terminal melalui perintah `pushd` dan` popd`

Dalam beberapa kasus yang jarang terjadi, setidaknya bagi saya, kita mungkin perlu mengubah ke direktori home pengguna kami, melalui cd ~, dan kemudian kembali ke apa yang kami lakukan di folder proyek. Masalahnya adalah bahwa kembali ke folder proyek kami mungkin berarti berjalan ke dalamnya.

Untungnya, banyak sistem * nix datang dengan perintah pushd dan popd built-in (AFAIK), yang membangun dan menyimpan tumpukan direktori. Sementara pushd menambahkan jalur direktori ke bagian atas tumpukan direktori, popd menghapusnya dari tumpukan.

Anda dapat memperoleh informasi lebih lanjut tentang perintah-perintah ini dengan mengetik help pushd dan help popd di terminal prompt Anda. Saya akan meninggalkan Anda dengan sebuah contoh sehingga Anda bisa mendapatkan ide yang lebih baik tentang bagaimana dan kapan kedua perintah ini dapat bermanfaat.

Saya harap Anda mendapatkan idenya. Anda dapat menggali lebih dalam perintah-perintah ini melalui help pushd, help popd, atau bahkan help dirs. Mereka berguna dalam kasus lain.

Diterjemahkan dari https://dev.to/avocadoras/navigating-the-terminal-via-pushd-and-popd-commands-13c9
