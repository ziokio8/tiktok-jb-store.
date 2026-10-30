# TIKTOK JB STORE — Admin + Server Authentication

Project ini adalah template deploy untuk Netlify. Password tidak disimpan di HTML atau source code.

## Yang tersedia
- Halaman toko publik dan katalog produk.
- `/admin.html` login admin.
- Dashboard untuk tambah, edit, hapus produk.
- Data katalog disimpan di Netlify Blobs.
- Password diverifikasi di server dengan bcrypt.
- Session cookie HttpOnly, Secure, SameSite=Strict, bertanda tangan HMAC, masa berlaku 8 jam.
- Pemeriksaan Origin untuk POST dan header keamanan dasar.

## Setup di HP / komputer
1. Upload folder project ini ke GitHub sebagai repository baru.
2. Hubungkan repository ke Netlify: https://app.netlify.com/
3. Di Netlify buka Site configuration → Environment variables, lalu buat:
   - `ADMIN_USERNAME` = username admin yang kamu pilih
   - `ADMIN_PASSWORD_HASH` = hash bcrypt, lihat langkah berikut
   - `ADMIN_SESSION_SECRET` = string acak rahasia minimal 32 karakter
4. Buat hash bcrypt secara lokal:
   - Jalankan `npm install`
   - Jalankan `npm run hash-password`
   - Ketik password admin ketika diminta. Salin hash hasilnya ke `ADMIN_PASSWORD_HASH`.
   - Jangan kirim password atau hash ke orang lain dan jangan taruh di file frontend.
5. Deploy ulang (trigger deploy) setelah mengatur environment variables.
6. Buka `https://ALAMAT-SITUS/admin.html`.

## Catatan keamanan penting
- Jangan gunakan password yang sama dengan email, bank, atau akun pribadi.
- Password yang pernah dikirim melalui chat sebaiknya diganti sebelum dipakai di produksi.
- Gunakan Netlify environment variables; jangan commit `.env`.
- Untuk pemakaian publik berskala besar, tambahkan rate limiting/WAF di depan endpoint login dan aktifkan notifikasi keamanan.
- Netlify Blobs akan menyimpan data produk setelah site terhubung dan function dijalankan.
- Ganti nomor WhatsApp contoh di `public/index.html` dan `public/admin.html` jika perlu.
- Template ini tidak mengotomatisasi pemindahan kepemilikan akun TikTok; pastikan setiap transaksi mematuhi ketentuan platform dan hukum yang berlaku.
