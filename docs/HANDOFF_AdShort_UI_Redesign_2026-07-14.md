# 🎨 HANDOFF — AdShort UI Redesign (Glass Depth 2-tier)

> Ngày: 2026-07-14 · Cho session MỚI đọc trước khi làm tiếp · TỰ-CHỨA

## 📋 TÓM TẮT (TLDR)
- **Việc:** Redesign toàn bộ UI app **AdShort** (mobile prototype) vì bị chê xấu. Đã qua **rất nhiều vòng iterate** với PO (BinhNT).
- **Đã CHỐT kiến trúc:** **2 tầng** — `STORY` (cinematic Glass Depth) cho onboarding/paywall/result · `WORK` (surface đặc sạch, kính chỉ ở nav) cho store/product/advideo/editor.
- **Đã khoá `DESIGN.md`** (single source of truth) tại repo root.
- **Đã DONE (preview, chưa merge):** Onboarding Story-tier (glassdeep_ob.html) + hệ nút locked + Store Work-tier v2 (store_work.html).
- **CÒN LẠI:** dựng Product/AdVideo/Editor tầng Work → **merge tất cả vào `index.html` gốc** (giữ engine, chỉ thay vỏ CSS/markup) → deploy.
- **⚠️ Bản gốc `index.html` CHƯA đụng** — chỉ mới làm file preview riêng. Merge là bước cuối, làm cẩn thận.

---

## 1. Repo & cách chạy
- **Repo GitHub:** `binh171/adshoot-preview-5b356e` (app trong 1 file `index.html`, ~2621 dòng, có engine/animation thật). Live: https://binh171.github.io/adshoot-preview-5b356e/ · push `main` → GitHub Actions auto-deploy ~1 phút.
- **Local:** đã clone tại `~/Downloads/adshoot-preview-5b356e/`.
- **Chạy preview:** `cd ~/Downloads/adshoot-preview-5b356e && python3 -m http.server 8777` → mở `http://localhost:8777/<file>.html` (dùng lệnh `open` để mở trên browser thật; browser-pane MCP chụp trang dài hay bị đen).

## 2. Files trong repo (trạng thái)
| File | Là gì | Trạng thái |
|---|---|---|
| `index.html` | **BẢN GỐC** prototype (engine thật) | ⚠️ **NGUYÊN VẸN, chưa đụng** |
| `DESIGN.md` | Design system 2-tier **đã khoá** | ✅ Dùng làm chuẩn |
| `glassdeep_ob.html` | **Onboarding Story-tier** (welcome/aha/q1/q2/paywall) + hệ nút | ✅ DONE (bản tốt nhất cho OB) |
| `store_work.html` | **Store Work-tier v2** (surface sạch, bento, glass nav) | ✅ DONE (bản tốt nhất cho Store) |
| `buttons.html`→`buttons4.html` | Board thử nút (10 mẫu mỗi loại) | Tham khảo |
| `concepts.html`,`concepts10.html`,`concepts_full.html`,`concept06.html`,`editorial.html`,`pro.html`,`minimal.html`,`trendy.html`,`glassdeep.html`,`glassdeep_store.html`,`icons.html` | Board khám phá hướng | Tham khảo (đã bị thay bởi 2-tier) |
| `index_d1.html`,`index_v2.html` | Reskin full-app thử nghiệm sớm | Bỏ (superseded) |

## 3. Docs liên quan (Desktop/PO SPM)
- `AUDIT_AdShort_UI_2026-07-13.md` — audit hiện trạng gốc (lưu ý: nhiều "bug" ban đầu là FALSE POSITIVE do letterbox/transition).
- `AdShort_UI_REBUILD_CHECKLIST_2026-07-13.md` — checklist ~76 mục component.
- `AdShort_DESIGN_2tier_2026-07-14.md` — copy của DESIGN.md.

---

## 4. ✅ QUYẾT ĐỊNH ĐÃ CHỐT (không làm lại)

### Kiến trúc 2 tầng
- **STORY** (welcome, aha, q1, q2, paywall, result): ảnh sản phẩm full-bleed + scrim + grain, kính phủ tự do, Fraunces display trắng + accent mint. Cinematic.
- **WORK** (store, product, advideo, editor, picker): **surface đặc sạch** (light/dark), theme có chiều sâu (gradient + ambient glow emerald + grain — KHÔNG phẳng lì), **kính CHỈ ở header + nav + FAB**, KHÔNG phủ kính lên content.
- Lý do: kính-phủ-content làm đục màn nhiều tool. (Đúng research iOS 26: glass chỉ ở lớp chrome.)

### Brand / Fonts
- Wordmark **"AdShort" LUÔN viết liền** (không hở). Logo play-ring (vòng emerald + gold + tam giác), làm **to**.
- Fonts: **Fraunces** (display + wordmark, dùng ít, không italic <16px) + **Geist** (UI/body/sans). Geist Mono cho số.
- Màu: `--em #0E5C43` · mint `#2EC494 / #5FD3A9 / #8FE9C8` · gold `#C9A254` (HIẾM, chỉ Pro/score). Xem token đầy đủ trong DESIGN.md §2.

### Icons
- **Phosphor Icons** (CDN `https://unpkg.com/@phosphor-icons/web@2.1.1`, class `ph ph-<name>`). KHÔNG vẽ tay, **KHÔNG emoji**.
- Marketplace logo: **logo brand thật** qua Simple Icons (`https://cdn.simpleicons.org/<slug>/white`) + `onerror` fallback về chữ-cái-màu-brand (vài brand nhỏ Temu/Mercari/Poshmark/Faire/Depop thiếu slug → fallback).

### Hệ NÚT (đã khoá)
- **Story primary** (Begin/Continue/Remove…): **Bright liquid glass + tia sáng quét động** (sweep 4.2s). Bo pill 999. `background:linear-gradient(180deg,rgba(255,255,255,.68),rgba(255,255,255,.5)); backdrop-filter:blur(26px) saturate(140%) brightness(1.15); border:1px solid rgba(255,255,255,.85); color:#0a3a2c`. KHÔNG mũi tên.
- **Paywall CTA**: bright liquid glass + **breathing glow** (3s). Cùng chất, khác hiệu ứng.
- **Work primary**: solid **emerald gradient** (`#0E5C43→#2EC494`), chữ trắng, pill.
- **Work secondary**: outline `--line`. **Tertiary**: soft `--em-soft`.
- (Đã thử & BỊ LOẠI: nút mũi-tên-badge tròn, nút kính tối/đục, pill trắng phẳng, gradient arrow-badge.)

### Paywall (giữ nội dung gốc, chỉ đổi skin)
- **Trial 3 ngày**: timeline **Today → Day 2 (remind) → Day 3 (plan starts)**. CTA "**Try 3 days free**", sub "remind you **on day 2**".
- Bỏ badge "AdShort Pro" → dùng wordmark AdShort viết liền.
- Neo nội dung xuống đáy (ảnh trên, text+plan+CTA gói dưới). Giữ: 3 feature check + 3 plan (Creator $14.99 / Studio $29 POPULAR / Agency $69) + Restore·Terms·Privacy.

### Store Work-tier v2 (store_work.html)
- Theme depth (gradient + emerald glow + grain 3.5%). Header + nav = glass. **Nav = liquid glass PILL floating** (Store/AdVideo/Product, mint active) — PO chốt "giữ, không sửa".
- **Popular tools = BENTO**: 1 card featured "Remove background" (ảnh + gradient icon tile) + 3 card compact (Resize/Retouch/Upscale, gradient icon emerald→mint). Chip filter active = emerald gradient. Card bo lớn (18-22), shadow tinh.
- **Giữ ĐỦ tool** (bắt buộc theo engine): filter All/Listing/Social/Marketing/Edit · Popular tools · All tools grid · hero showcase · Marketplace formats (Shopify/Amazon/Etsy/TikTok + logo) · Shopify templates (On-model/Studio hero/Editorial/Lifestyle) · FAB Create&edit · nav.

---

## 5. 🧠 GU CỦA PO — tránh lặp cái đã bị loại
- **CHÊ:** nền phẳng lì · màu nâu/warm · minimal quá khô · kính đục trên content · icon vẽ tay/emoji (trẻ con) · nút phẳng/tối/đục · "chưa sang" nếu chỉ dựa màu.
- **THÍCH:** "sang từ CRAFT không từ màu" (spacing/type/tiết chế) · **thời thượng** (bento, kính, chữ biểu cảm, motion) · cảm giác **pro tool cho seller** (không phải app consumer/tạp chí) · Glass Depth cinematic cho story · bright liquid glass buttons.
- **Cách làm việc PO thích:** đưa **nhiều mẫu (5-10) để chọn** rồi spin sâu cái được chọn · tự research để nâng bar · verify trước khi khẳng định · giữ đủ tool engine, chỉ đổi vỏ.
- **Ngôn ngữ:** giao tiếp tiếng Việt.

---

## 6. ▶️ VIỆC TIẾP THEO (thứ tự)
1. **Dựng Product tầng Work** (list sản phẩm + Make video/Export + readiness score) — như store_work.html, surface sạch + glass nav. Duyệt với PO.
2. **Dựng AdVideo tầng Work** (chọn product/Switch + format Reels/Shopify/IG/Story + High-impression trending + Make an ad).
3. **Dựng Editor tầng Work** (toolbar X/undo/redo/AI/preview/Done + Layers/Insert/Text/Background/Shadow/Resize + canvas).
4. **MERGE vào `index.html` gốc** — bước lớn nhất, làm surgical:
   - GIỮ nguyên engine/logic/JS/animation (hero 5-beat, filterTools, toggleSearch, openPaywall, buildGroups…).
   - Chỉ thay **CSS + markup vỏ**. Story screens → skin cinematic; Work screens → skin surface sạch + nav glass.
   - Map token vào `:root` + `.phone.dark` (override cuối stylesheet).
   - Đối chiếu DESIGN.md §10 Do/Don't.
5. **Test** 26 flow + dark/light. **Deploy** (push main).

## 7. ⚠️ GOTCHAS / vị trí trong index.html gốc
- Bộ tool Store thật: dòng **~1321–1456** (`data-s="store"`).
- Onboarding: welcome ~1262, aha ~1285, q1 ~1307, q2 ~1314.
- Paywall HTML: **~1932–1957** (`#paywall`).
- Data q1/q2: `CAT_GROUPS`/`MK_GROUPS`/`MK_LOGO`/`CAT_ICONS` ~dòng **2052–2067**. (MK_LOGO gốc dùng chữ-cái-màu; ta nâng lên logo brand thật.)
- Screens = `<section class="screen" data-s="...">`, chuyển màn bằng JS `go('<name>')`, `.screen{position:absolute;inset:0}` (đừng "sửa" dải trắng đáy — đó là letterbox, KHÔNG phải bug).
- Dark mode = class `.phone.dark` (toggle ☾, nhớ localStorage). Override phải đặt CUỐI stylesheet.

## 8. Trạng thái khác
- API keys: không cần cho preview (thuần front-end).
- Gen ảnh mới: KHÔNG cần — dùng ảnh sẵn trong `store/`, `onboarding/`.
- Chưa commit/push gì lên repo (mọi thứ là file preview local).

---
> Bắt đầu session mới: (1) đọc `DESIGN.md` + file này, (2) chạy server :8777, (3) mở `glassdeep_ob.html` + `store_work.html` để nắm chuẩn hiện tại, (4) làm tiếp Product tầng Work.
