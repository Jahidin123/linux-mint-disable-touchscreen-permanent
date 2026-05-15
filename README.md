# Disable Touchscreen Permanently on Linux Mint

Tutorial lengkap mematikan touchscreen permanen di Linux Mint menggunakan `libinput` dan `nano`.

Metode ini:
- Aman
- Tidak menghapus driver
- Bisa dikembalikan kapan saja
- Cocok untuk touchscreen error / ghost touch

---

# 1. Open Terminal

Tekan:

```text
CTRL + ALT + T
```

atau buka:

```text
Menu -> Terminal
```

---

# 2. Check Touchscreen Device Name

Jalankan:

```bash
xinput list
```

Contoh output:

```text
Virtual core pointer
⎜   ↳ ELAN Touchscreen                     id=12
⎜   ↳ USB Optical Mouse                   id=13
```

Cari device yang ada tulisan:

```text
Touchscreen
```

Contoh nama touchscreen:

```text
ELAN Touchscreen
```

Catat nama tersebut.

---

# 3. Open libinput Config File

Jalankan:

```bash
sudo nano /usr/share/X11/xorg.conf.d/40-libinput.conf
```

Masukkan password jika diminta.

Catatan:
- Password tidak akan terlihat saat diketik
- Tetap ketik lalu tekan Enter

---

# 4. Add Touchscreen OFF Configuration

Scroll ke bagian paling bawah file.

Tambahkan konfigurasi berikut:

```text
Section "InputClass"
    Identifier "Touchscreen OFF"
    MatchProduct "ELAN Touchscreen"
    Option "Ignore" "true"
EndSection
```

---

# 5. Change Touchscreen Name

Bagian ini:

```text
MatchProduct "ELAN Touchscreen"
```

harus sama persis dengan hasil dari:

```bash
xinput list
```

Contoh lain:

```text
MatchProduct "Goodix Capacitive TouchScreen"
```

atau:

```text
MatchProduct "Wacom HID 5289 Finger"
```

Nama harus sesuai huruf besar dan kecil.

---

# 6. Save File in Nano

Tekan:

```text
CTRL + O
```

Lalu tekan:

```text
Enter
```

untuk menyimpan file.

---

# 7. Exit Nano

Tekan:

```text
CTRL + X
```

---

# 8. Reboot System

Jalankan:

```bash
sudo reboot
```

---

# 9. Finished

Setelah restart:
- Touchscreen akan nonaktif permanen
- Touchpad dan mouse tetap normal

---

# Re-Enable Touchscreen

Buka kembali file konfigurasi:

```bash
sudo nano /usr/share/X11/xorg.conf.d/40-libinput.conf
```

Cari dan hapus bagian ini:

```text
Section "InputClass"
    Identifier "Touchscreen OFF"
    MatchProduct "ELAN Touchscreen"
    Option "Ignore" "true"
EndSection
```

---

# Save Again

Tekan:

```text
CTRL + O
Enter
CTRL + X
```

Lalu reboot:

```bash
sudo reboot
```

Touchscreen akan aktif kembali.

---

# Troubleshooting

## Check Device Again

```bash
xinput list
```

---

## Find More Detailed Touchscreen Name

```bash
libinput list-devices
```

atau:

```bash
grep -i touch /proc/bus/input/devices
```

---

# Notes

File:

```text
/usr/share/X11/xorg.conf.d/40-libinput.conf
```

dapat tertimpa update sistem.

Metode lebih aman sebenarnya menggunakan file custom di:

```text
/etc/X11/xorg.conf.d/
```

tetapi edit langsung lebih mudah untuk penggunaan cepat.

---

# Tested On

- Linux Mint Cinnamon
- Linux Mint XFCE
- Linux Mint MATE

---

# License

MIT
