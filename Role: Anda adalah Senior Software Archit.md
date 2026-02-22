Role: Anda adalah Senior Software Architect dengan keahlian mendalam di Go (Fiber framework), Svelte, dan Supabase. Anda sangat mengutamakan Clean Architecture dan skalabilitas sistem multi-tenant.

Tujuan: Membangun MVP SaaS Manajemen Keuangan Keluarga.

Tech Stack Utama:

Backend: Go dengan framework Fiber.

Frontend: Svelte (Web-first).

Database & Auth: Supabase (PostgreSQL).

Deployment: Docker & Easypanel (VPS).

Integrasi: Webhook support untuk n8n dan Telegram Bot sebagai entry point data.

Spesifikasi MVP:

Multi-tenancy: Struktur data berbasis family_id. Setiap user terikat pada satu keluarga.

Fitur Inti: Management Budget, Pencatatan Pengeluaran, Dashboard Monitoring, dan Notification Engine (Alert saat budget menipis).

Input Fleksibel: Mendukung input dari Web UI dan Webhook (untuk Telegram/n8n).

Tugas Anda:

Berikan rekomendasi Skema Database (ERD) di Supabase yang mendukung multi-tenancy dan pelacakan budget vs pengeluaran secara efisien.

Buat Arsitektur Folder Project untuk Go Fiber yang mengikuti prinsip Clean Architecture (Repository, Service, Controller).

Tuliskan boilerplate Go Fiber Middleware untuk validasi family_id dari JWT Supabase.

Berikan contoh Svelte Store untuk mengelola state budget dan pengeluaran secara real-time.

Sebelum memberikan kode, tolong berikan analisis singkat mengenai strategi terbaik untuk implementasi "Budget Alert" (apakah lewat database trigger atau worker di Go).