# AdShort Preview — UI Roadmap (map hoàn chỉnh)

> Repo: `binh171/adshoot-preview-5b356e` · Live: https://binh171.github.io/adshoot-preview-5b356e/
> Bản gốc đối chiếu: https://binh171.github.io/adshoot-preview-f5bbdd/
> Cập nhật: 2026-07-06. Nguồn: CEO feedback "UI xấu" + research App Store/HIG iOS 26 + Liquid Glass + trends 2026.

## ĐÃ SHIP (v2 → v4, 2026-07-06)

- **v2**: palette iOS (bỏ giấy be), serif → chỉ logo, capsule buttons, floating glass tab bar + minimize-on-scroll
- **v3**: quét sạch màu be hardcode, glass-chip/badge system, active đen→green, sticky glass header + large-title shrink, **AdVideo dark mode** + hero tràn mép + feed card 210px, **Editor full-bleed** + toolbar/dock kính + Done, Product card 4:5 tên đè gradient, gen sheet = bottom sheet + nút Generate gradient AI + shimmer sweep, paywall timeline Today/Day5/Day7, Apply row "✦ Suggested"
- **v4**: before/after drag slider (Store), search island kính cạnh tab bar, dark contrast fixes
- **v5**: chip lọc Store + Apply — ký tự text 🏷♡◫✎ → SVG stroke icon đồng bộ tab bar (feedback trực tiếp từ user)
- **v6 (P1+P2 trọn gói)**: AHA chips glass · tab icon duotone fill active · logo Meta/TikTok · hero chips glass · Q1 chips ảnh sản phẩm thật · ✦ tool AI editor · concentric gen sheet · **feed High-impression card 262px snap-center + Ken Burns live** · **Switch → bottom sheet** (scrim + handle) · gen sheet kéo-để-đóng thật · generating skeleton 9:16 · result slide-up · **search island → search sheet** (Recent/Trending) · reduced-motion đủ bộ

- **v7 (feedback user)**: All tools bỏ hộp-lồng-hộp → icon squircle trắng 60px trên nền, 4 cột × 2 hàng; search island bỏ khỏi khu tab bar → nút tròn glass trên header Store (cạnh ◆40), tab bar về giữa

- **v9 (feedback user — CEO không ưng dark)**: **theme toggle ☾ trên header Store, MẶC ĐỊNH LIGHT**, dark = opt-in class `.phone.dark` (var swap + toàn bộ override scoped), nhớ lựa chọn localStorage; AdVideo theo theme chung; Editor/Picker giữ dark cố định (chuẩn editor)
- **v8 (feedback user — đồng nhất)**: **DARK MODE TOÀN APP** (P3.1 — swap :root vars + block override cuối stylesheet; content tiles/product photos giữ nền trắng; nút nền trắng giữ chữ green đậm #0A4632); **bỏ card "See the difference"**; thêm sub-caption 4 section Store lấp khoảng trống. Bài học cascade: override theme PHẢI nằm cuối stylesheet.

> P1 ✅ xong · P2 ✅ xong · P3 xong 3.1+3.3 (còn 3.2 perf audit, 3.5 tokens doc) · P0.2/P0.3 chờ CEO + iPhone · Deck compare.html chụp bản LIGHT cũ — cần chụp lại sau khi CEO chốt dark

---

## P0 — REVIEW GATE (làm trước khi code tiếp)

| # | Việc | Effort | Ghi chú |
|---|---|---|---|
| 0.1 | Deck so sánh before/after từng màn (f5bbdd vs 5b356e) gửi CEO | S | Screenshot 6 màn × 2 bản, ghép side-by-side |
| 0.2 | Thu feedback CEO CÓ CẤU TRÚC theo từng màn (không thoại rời) | S | Template: màn → giữ/sửa/bỏ → lý do |
| 0.3 | Test trên iPhone thật (Safari) — glass, sticky, slider, safe-area | M | `-webkit-backdrop-filter` có rồi nhưng chưa verify máy thật |

**Nguyên tắc:** P1–P3 chỉ chạy sau khi P0.2 chốt scope. Feedback CEO có thể xoá/đổi hạng mục bên dưới.

## P1 — HOÀN THIỆN CONCEPT (visual, nợ từ spec)

| # | Việc | Effort | Impact | Chi tiết |
|---|---|---|---|---|
| 1.1 | AHA demo: chip/badge/score → glass-chip | S | M | `.achip .badge .cscore .skip` — skip làm rồi, 3 cái kia còn nền đặc |
| 1.2 | Icon tab bar: outline → filled khi active | M | M | Hiện fake bằng stroke-width 2.4; cần vẽ 3 filled variant |
| 1.3 | Post to Meta/TikTok: thêm logo platform vào nút | S | S | `.grbtns` result screen |
| 1.4 | Store hero: chip Remove BG/Retouch trên tile → glass thật | S | S | `.hc-chip` đang trắng đặc .95 |
| 1.5 | Q1/Q2: chip category kèm ảnh minh hoạ (Pinterest onboarding) | M | M | Cần chọn ảnh/emoji per category từ asset có sẵn |
| 1.6 | Editor: icon ✦ trên tool AI (Background/Shadow), checker khi transparent | S | S | |
| 1.7 | Concentric corners audit: radius con = cha − padding toàn app | M | M | Hero tile, gen sheet cards, paywall tiers |

## P2 — CHIỀU SÂU TƯƠNG TÁC (đổi hành vi, không chỉ skin)

| # | Việc | Effort | Impact | Chi tiết |
|---|---|---|---|---|
| 2.1 | High-impression → feed dọc 9:16 full-bleed vuốt kiểu Reels, autoplay muted | L | **XL** | Cái "3 tab chạy" CEO thích — bước nhảy lớn nhất còn lại. Cần video/poster sẵn trong `advideo/_pixelcut` |
| 2.2 | Switch sản phẩm → bottom sheet (thay dropdown web) | M | M | `.ctxdrop` → sheet có handle + scrim; vị trí trong .phone cần tính |
| 2.3 | Gen sheet: drag handle kéo được thật (detent 92% ↔ full ↔ dismiss) | M | M | Pointer events trên `#gen::before` vùng .gtop |
| 2.4 | Generating: shimmer skeleton ĐÚNG khung 9:16 kết quả (thay 2 ảnh pulse) | S | M | Spec gốc; hiện mới có sheen quét |
| 2.5 | Result: slide-up + scale reveal khi gen xong | S | S | 300ms ease-out |
| 2.6 | Search island → mở search sheet demo (recent + suggestions) thay toast | M | S | Chỉ làm nếu CEO khen island |

## P3 — HỆ THỐNG HOÁ (nền để scale)

| # | Việc | Effort | Impact | Chi tiết |
|---|---|---|---|---|
| 3.1 | Dark mode toàn app (Store/Product/onboarding) qua CSS vars | L | L | Đã có pattern từ AdVideo; đổi sang `light-dark()` hoặc class toggle |
| 3.2 | Perf audit backdrop-filter: đếm panel active/màn, archive off-screen | M | M | Rule ≤3 panel; Store scrolled đang có header+nav+island+chips |
| 3.3 | `prefers-reduced-motion` cho animation mới (aigrad, gpsheen, ba, navmin) | S | S | Media query đã có sẵn, thêm selector |
| 3.4 | FEED refactor: tách retitle khỏi reorder (bẫy data-grp đã ghi memory) | M | S | Chỉ làm khi cần thêm section mới vào Store |
| 3.5 | Design tokens doc cho dev iOS thật (radius/spacing/color/glass recipe) | M | L | Xuất từ :root — làm khi app thật bắt đầu build UI |

## P4 — HANDOFF

| # | Việc | Effort |
|---|---|---|
| 4.1 | Cập nhật handoff doc AdShoot (repo chính `adshoot-engine-handoff@main`) trỏ sang preview mới + learnings | S |
| 4.2 | Ghi SESSION_LESSONS: FEED trap, glass recipe, nav minimize pattern | S |

## KHÔNG LÀM (đã quyết, kèm lý do)

- **FAB gộp vào giữa tab bar** — 3 tab không có ô giữa tự nhiên; FAB nổi hiện không còn đè content. Chỉ mở lại nếu CEO yêu cầu.
- **Kính hoá content** (card ảnh, video) — vi phạm rule Liquid Glass của Apple, giảm độ đọc.
- **Đổi cấu trúc 3 tab / flow AHA / màu green brand** — IA và identity đang đúng.

## THÔNG SỐ CHUẨN (tham chiếu nhanh)

```
Glass bar:  rgba(255,255,255,.62) + blur(24px) saturate(180%) + border rgba(255,255,255,.55)
            + inset 0 1px 0 rgba(255,255,255,.65) + 0 8px 32px rgba(0,0,0,.16)
Glass chip: rgba(28,28,30,.45) trên ảnh / rgba(255,255,255,.72) trên nền sáng + blur(8-12px)
Dark set:   bg #0D0F0E · card #1C1C1E · text phụ #98989F · accent sáng #7FD4B3
Radius:     chip/nút 999 · card 12-16 · hero/sheet 24-30 · concentric = cha − padding
AI:         --ai: linear-gradient(135deg,#0E5C43,#2EC494) · icon ✦ · shimmer 1.8-3.5s
```
