# Version Control and Branch Management (Git)

## Daftar isi
- [Resume](#resume)
- [Praktikum](#praktikum)

# Resume

# Praktikum

## 1. Membuat github repository ✅

Pembuatan repositori github kurang lebih mengikuti panduan [berikut](https://docs.github.com/en/get-started/quickstart/create-a-repo), hal yang berbeda adalah **membiarkan repository kosong (tanpa inisialisasi `readme.md`)**

Kemudian _clone_ `remote repo` atau hubungkan `local repo` dengan `remote repo`, pada bahasan ini yang dilakukan adalah menghubungkan `local repo`. Cara yang dilakukan adalah memasukan perintah berikut di terminal yang berjalan di `local repo`.

```
git remote add origin <remote repository URL>
```

lakukan verifikasi dengan printah
```
git remote -v
```

Sekarang, `local repo` sudah terhubung dengan `remote repo`.

## 2. Membuat brancing **main**, development, featureA, dan featureB ✅

_[Why not `master` ?](https://github.com/github/renaming)_

Pada branch master, dibuat file `index.html` kemudian masukan code berikut.
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
</body>
</html>
```
### **Git Push**
kemudian `save` lalu lakukan `add` `commit` dan `push`

```
git add .
git commit -m "initial commit"
git push origin main
```

---
### **Git Pull**
Untuk mengkonfirmasi keberhasilan push lakukan,
```
git pull origin main
```
Akan muncul pesan bahwa `HEAD` pada `local repo` sudah sama dengen `HEAD` pada `remote repo`

---
### **Git stash**
Misal kita menambahkan data berikut dalam tag `body` pada html

```html
</head>
<body>
    <h1>Ini main</h1> <!-- perubahan baru -->
</body>
</html>
```
Namun, kita ragu bahwa perubahan tersebut layak untuk di-`commit` di-`main` pada saat ini. Maka dilakukan `stash` guna menyimpan perubahan tersebut sementara

```
git stash push 
```
Perubahan tersebut akan hilang seolah tidak pernah terjadi, namun sebenarnya tersimpan. Untuk melihat seluruh simpanan `stash` jalankan perintah berikut.

```
git stash list
```

kemudian jika ingin mengembalikan perubahan yang tersimpan dalam `stash`, lakukan

```
git stash apply --index <indeks stash pada stash list>
```

---

Kemudian dibuat branch `development` **terhadap branch `main`**. lalu pindah ke branch `development`.

```
git branch development
git switch development
```
Maka akan didapat file-file yang ada dan isinya sama dengan branch `main`

---
Pada branch `development`, edit file `index.html` menjadi seperti berikut.
```html
...
</head>
<body>
    <h1>featureA</h1>
    <p>

    </p>
    <h1>featureB</h1>
    <p>

    </p>
</body>
</html>
```
lakukan `commit` pada branch `development`.

---
Kemudian saatnya kita membuat branch `featureA` dan `featureB`. **Pembuatan branch ini harus dilakukan ketika kita berada pada branch `development`.**
```c
// pada branch `development`
git branch featureA
git branch featuerB
```
## 3. Penanganan konflik ketika `featureB` di merge setelah `featureA` merge ke `development`

Kita pergi ke branch `featureA` dan edit `index.html` menjadi seperti berikut

```html
<!--index.html pada branch `featureA`-->
...
</head>
<body>
    <h1>featureA</h1>
    <p>
        some featureA
    </p>
...
```
### **Git merge**
Lakukan `commit` pada branch `featureA`. Kemudian, ke branch `development` lalu lakukan `merge`.
```
git merge featureA --no-ff
```
Argumen `--no-ff` pada `merge` berarti `pointer` tracker pada branch `development` tidak berpindah ke `pointer` branch `featureA` namun mereka membuat sebuah `snapshot` baru.

---
Jika sudah, pergi ke branch `featureB` lalu edit `index.html` menjadi seperti berikut.

```html
    <h1>featureA</h1>
    <p>
        oops mistakenly edited this line
    </p>
    <h1>featureB</h1>
    <p>
        some featureB
    </p>
```
Perhatikan dalam sekenario diatas, kita mengisi tag paragraph dari _featureA_, hal ini sengaja guna memancing conflict nantinya.

Simpan perubahan tersebut lalu lakukan `commit`.

Kemudian pergi ke branch `development` lalu jalankan printah berikut
```
git merge featureB --no-ff
```
Maka akan muncul conflict, untuk melakukan penyelesaian, buka `VSCODE` (karna penulis menggunakan IDE ini) lalu pergi ke line code dimana terjadi conflict. Akan terlihat tampilan berikut:

-- gambar conflict

Pilih opsi yang ada di atas sesuai kebutuhan, untuk saat ini kita pilih `accept current changes`

# 4. Implementasi push, pull, stash, dan merge ✅
Terlaksanakan sembari mengerjakan [nomer 2](#2-membuat-brancing-main-development-featurea-dan-featureb-%E2%9C%85) dan [nomer3](#3-penanganan-konflik-ketika-featureb-di-merge-setelah-featurea-merge-ke-development).

# 5. Merge no fast forward ✅

Pergi ke branch `main`, lalu jalankan
```
git merge development --no-ff
```
Maka ketika kita buka `log` dengan perintah
```
git log --oneline --graph --all
```
terbukti bahwa `snapshot` yang dihasilkan adalah baru alias non liner merge.

-- gambar log