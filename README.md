# modul-tampilan

Render view/template HTML untuk bahasa [Tenun](https://github.com/TenunLang/Tenun). Placeholder `{{kunci}}` diganti nilai, otomatis di-escape (cegah XSS).

## Pasang

```
tenun add tampilan
```

## Pakai

```tenun
impor "tampilan";

biar t: teks = tampilan("publik/halaman.html");   // baca berkas template
t = isi(t, "judul", "Beranda");
t = isi(t, "nama", "Budi");
// t sekarang HTML siap kirim
```

Template `publik/halaman.html`:

```html
<h1>{{judul}}</h1>
<p>Halo {{nama}}</p>
```

## Fungsi

- `tampilan(berkas: teks): teks` — baca berkas template.
- `isi(tmpl: teks, kunci: teks, nilai: teks): teks` — ganti `{{kunci}}` dengan nilai (di-escape HTML). Bisa dirantai.
- `isi_mentah(tmpl, kunci, nilai): teks` — sama, tanpa escape (untuk HTML terpercaya).
- `tampilan_escape(s: teks): teks` — escape `& < > " '`.

## Contoh dengan server

```tenun
impor "tampilan";

fungsi tangani(metode: teks, jalur: teks, badan: teks): teks {
    headerKan("Content-Type", "text/html; charset=utf-8");
    biar t: teks = tampilan("publik/index.html");
    kembali isi(t, "nama", "Dunia");
}
layani(8080);
```

## Catatan

- Placeholder ditulis tanpa spasi: `{{nama}}` (bukan `{{ nama }}`).
- Perulangan/objek bersarang menyusul (memerlukan map/struct di bahasa inti).

## Lisensi

MIT.
