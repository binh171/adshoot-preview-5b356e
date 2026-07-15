# AdShort — Bàn giao thay đổi UI (2026-07-08) · cho anhvd triển khai

## 📋 TÓM TẮT
Phiên này chỉnh 8 vùng UI trong `index.html` (1 file, dark = class `.phone.dark`). Trọng tâm lớn nhất: **REBUILD bước 4 "Export formats"** thành danh sách **1 dòng/nền tảng** với dropdown **tỉ lệ + kích thước** (đổi tỉ lệ → size nạp lại), logo brand thật, gọn mặc định + "More platforms". Tất cả làm **cả light + dark**, đã verify, đã live.

- **Commit**: `v12` = `1b06796`, `v13` = `a1b478e` (branch `main`).
- **Live**: https://binh171.github.io/adshoot-preview-5b356e/ (push `main` → GitHub Actions auto-deploy ~1 phút).
- **Toàn app = 1 file** `index.html`. Theme: mặc định light; dark bật bằng class `.phone.dark` (toggle ☾ header Store, nhớ localStorage).

---

## 1. Thay đổi theo vùng (grep class/id trong index.html)

| Vùng | Class / id | Thay đổi |
|---|---|---|
| Head | `<link tabler-icons>` | Thêm Tabler icons webfont (cho brand-logo). |
| FAB AdVideo | `.fabMake` | Thanh full-width → **pill gọn "✦ Create ad"** canh giữa, tách khỏi tab bar kính. |
| FAB Store | `.storefab` | "Create & edit" **thu nhỏ = size FAB AdVideo** (padding 12×20, font 14px). |
| Gen sheet title | `.gtt` | "Make ad" → **"Create your ad"**. |
| Gen chip (direct) | `openGen` else | "New ad" → **"Custom"**. |
| **Bước 4 Export** | `#stepFmt` | **REBUILD** (xem §2). |
| Result: gợi ý | `.fmsug` `.fmtrack` `renderSug()` `FMT_LOGIC` | Dải tỉ lệ chạy → **format creative đề xuất theo category** (marquee phải→trái, clip live). |
| Result: nút | `.gract` `#grDownload` `#grSend` `.admenu` | 3 nút dọc → **Download + Send to ad platform** (chia đôi) + menu Meta/TikTok/Google Ads. |
| Result: save | `.grnote` `#grSave` | Nút to → **dòng note** "Find it anytime in the Product tab". |
| Store All tools | `.toolc .ic` | Ô trắng đặc → **glass frosted** (light + dark). |
| Thương hiệu | `.as-mk` `.as-tg` `.hbrand` | Wordmark + tagline → **Fraunces serif** (sửa bug bị ép sans). |
| Welcome | `.wfoot .cta` `@keyframes ctaglare` | Nút "Begin" → **sheen + vệt sáng chạy**. |

---

## 2. Bước 4 "Export formats" — chi tiết (phần backend cần map)

**UI**: mỗi nền tảng = 1 `.fmtrow` gồm: logo chip + tên + `<select class="ra">` (tỉ lệ) + `<select class="sz">` (kích thước) + `.ck` (vòng tròn chọn xuất).
- Mặc định hiện: **Meta Ads (#1) · TikTok Ads (#2)** (đã chọn) + **Shopify**. Phần còn lại (Instagram / Facebook / YouTube / Amazon / Etsy) ẩn trong nút **`.fmtmore` "More platforms"** → bấm mở (`#stepFmt.exp`, hiện `.fmtrow.sec`).
- **Ratio đổi → size nạp lại**: `ra.change` → `sz.innerHTML = opts(f.map[ra.value])`.

**Data model** (`var FMTS` trong `<script>`):
```js
{ g:'ad'|'mk', pri:1?, id, name, ic:'ti-brand-*', c:'#hex',
  svg?:'<svg>…', // dùng khi Tabler thiếu logo (Shopify)
  map:{ '9:16':['1080×1920','720×1280'], '4:5':['1080×1350'], … } }
```
- `map` = **tỉ lệ → mảng kích thước chuẩn**. Backend map thẳng: platform + ratio chọn + size chọn.
- Chọn xuất = `fmtSel[id]` (bool). `fmtCount()` = số platform bật.

**Kích thước native theo MODEL (anhvd map resolution thật)**:
- Seedance 1.0 **Pro** (ProFast, default): **480/720/1080p** native (Lite chỉ 720). Endpoint mặc định đang `...seedance-pro-720p...` ⇒ pipeline **đang cap 720p** dù Pro làm được 1080 (chỉ cần set param resolution).
- Seedance 2.0: 1080p / tối đa 2K. Veo 3: 1080p. **Veo 3.1: tới 4K native**.
- 4K trên Seedance = phải **upscale** (Topaz…) = tốn compute.
- ⇒ **Luật**: `sz` cho chọn phải khớp res model đang gen. Đề xuất tier: 720 (draft) · 1080 Full HD (chuẩn ad Meta) · 4K (Veo3.1/upscale = Premium).

**Logo**: `ti-brand-{meta,tiktok,instagram,facebook,youtube,amazon,etsy}` (Tabler). **Shopify** dùng inline SVG bag (Tabler bản này thiếu `ti-brand-shopify`).

---

## 3. Ghi chú
- Mọi thay đổi verify **cả light + dark** (screenshot 2 mode).
- Asset ảnh/clip: cấu trúc thư mục thật trong repo (`advideo/`, `store/`, `product/`, `onboarding/`).
- **CHƯA làm (strategy, để sau)**: gating free/paid (free = chỉ sửa ảnh, video gen = paid) + res-tier paywall (720/1080/4K theo tier). Xem `project_adshort_monetize_resolution` (memory) khi triển khai.
