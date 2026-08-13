# Fresh Design Sources

Folder ini menyimpan referensi dan keputusan visual yang tidak boleh otomatis menjadi resource aplikasi.

## App icon

- `AppIcon/AppIcon_Foreground_Official.png` adalah master foreground resmi Sprout & Slice yang dipilih pemilik; jangan mengubah, meregangkan, atau memecahnya.
- `AppIcon/Fresh_App_Icon_Concept_02.png` tetap disimpan sebagai referensi historis yang mengarahkan proses generasi.
- `AppIcon/APP_ICON_SPEC.md` mendokumentasikan artwork final dan hubungan sumbernya.
- `AppIcon/APP_ICON_COMPOSER_SPEC.md` mendokumentasikan konfigurasi appearance dan Liquid Glass yang aktif di `../Fresh/AppIcon.icon`.
- Ikon final sudah dibuat dengan Icon Composer dan menjadi sumber app icon bernama `AppIcon` untuk build Fresh.
- Tiga layer lama sengaja tidak disimpan sebagai master karena tidak sama dengan konsep.

## UI concepts

- `UIConcepts/fresh_ui_visual_direction.png` adalah katalog arah visual, bukan screen spec final.
- `UIConcepts/VISUAL_DIRECTION_RECONCILIATION.md` menjelaskan bagian yang boleh dan tidak boleh diwarisi.
- `UI_SCREEN_GENERATION_PROMPTS.md` berisi prompt berurutan untuk satu chat image-generation: style lock, delapan halaman, ilustrasi transparan yang diperlukan, Markdown implementasi, dan audit lintas layar.

Jika terjadi konflik, ikuti screen spec terkait, Design System, panduan visual, reconciliation, lalu gambar konsep.
