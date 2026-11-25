# SümerMenu — Akıllı QR & NFC Restoran Menü ve Masa Operasyon Platformu

[![Live Demo](https://img.shields.io/badge/Canlı_Demo-sumermenu.vercel.app-0EA5E9?style=for-the-badge&logo=vercel&logoColor=white)](https://sumermenu.vercel.app)
[![Next.js](https://img.shields.io/badge/Next.js-App_Router-000000?style=for-the-badge&logo=nextdotjs&logoColor=white)](https://nextjs.org/)
[![Supabase](https://img.shields.io/badge/Supabase-PostgreSQL_%26_Realtime-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white)](https://supabase.com/)

Restoran ve kafeler için geliştirilmiş, çok kiracılı (multi-tenant) **QR & NFC dijital menü, masa aksiyonları ve yapay zeka destekli menü danışmanı** platformunun mimari vitrin deposudur *(Aktif Geliştirme — ana uygulama kaynak kodu özel depoda tutulmaktadır)*.

## Temel Özellikler

- **Nisaba AI (Menü Danışmanı):** Google Gemini API (`POST /api/ai/advisor`) üzerinden müşteri tercihine ve 14 temel alerjen/diyet filtresine (*Glütensiz, Vegan, Vejetaryen vb.*) göre yemek önerisi sunan yapay zeka asistanı.
- **Hammurabi İstemci Koruma Katmanı (`useHammurabiShield`):** Kötüye kullanımı önlemek için istemci telemetrisi, bekleme süresi (15 sn cooldown), oturum başı çağrı limiti (3 çağrı), dwell/burst algılama ve kaydırarak onaylama (*slide-to-confirm*) UX kapısı.
- **Masa İşlemleri & KDS / Garson Konsolu:** Supabase Realtime üzerinden anlık **Garson Çağır** ve **Hesap İste** (*POS / Kredi Kartı vs. Nakit*) akışları.

## Teknoloji Yığını

- **Frontend:** Next.js (App Router), TypeScript, Tailwind CSS
- **Backend & Veritabanı:** Supabase (PostgreSQL, Auth, Realtime, REST API)
- **Yapay Zeka & Güvenlik Başlıkları:** Google Gemini API (`Nisaba AI`), CSP, HSTS, `X-Frame-Options`
- **Dağıtım:** Vercel

## Mimari Akış

```text
[Müşteri QR/NFC Tarama]
        │
        ▼
[Next.js App Router UI] ──► [Hammurabi UX Katmanı (Cooldown / Telemetry / Slide Gate)]
        │                                       │
        ├──► POST /api/ai/advisor ──► [Google Gemini (Nisaba AI)]
        │
        └──► Supabase Realtime ─────► [Garson & Mutfak (KDS) Konsolu]
```
