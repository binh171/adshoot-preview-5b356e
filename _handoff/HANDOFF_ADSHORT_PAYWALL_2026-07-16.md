# HANDOFF — AdShort Paywall (2026-07-16, sang máy khác)

## TL;DR
Paywall web AdShort **HOÀN THIỆN + đã lên link chính**. 3 gói Creator/Studio/Agency: hero màu theo persona, CTA green-neo, ★ trial, copy App-Store-safe. Costing credit đã tính tỉ mỉ từ model thật. **Còn 1 việc chặn: BE khóa số credit** (dưới).

---

## 1. REPO & CHẠY LOCAL
- **Repo paywall (RIÊNG, KHÁC claude-creative)**: `binh171/adshoot-preview-5b356e`
- **Folder local**: `C:\Users\ADMIN\Downloads\Claude Creative\_preview_v2_work`
- File chính: **`index.html`** (1 file, static — HTML+CSS+JS inline)
- **main HEAD**: `04f7eda` (Merge PR #3) · branch `feat/paywall-store-ui` đã merge hết
- **LIVE**: https://binh171.github.io/adshoot-preview-5b356e/ (GitHub Pages deploy từ `main`)
- Chạy local: `cd _preview_v2_work && python -m http.server 8971` → mở `http://localhost:8971/index.html`
- Mở paywall: trong app bấm nút mở paywall, hoặc console `openPaywall(); p2setTier('creator'|'studio'|'agency'); p2setBilling('yearly'|'monthly')`

## 2. ĐÃ SHIP HÔM NAY (3 PR vào main)
- **PR #1**: paywall 3-tier store-ready + fix landmine "unlimited upscale" (upscale chưa Live → bỏ)
- **PR #2**: persona colors (green/gold/blue) + Agency CTA "Continue"
- **PR #3**: benefits final (ghi dồn, ★ star, App-Store-safe) + hero cutout perfume + tick green-chỉ-Creator

## 3. PAYWALL FINAL — text 3 gói (đang live)
**Chung**: giá Creator $19.99/$13.99yr · Studio $29.99/$20.99yr (POPULAR) · Agency $69.99/$48.99yr. Creator+Studio trial 3d, Agency "Continue".

**Creator** 🟢 (hero: đầm xanh `onboarding/_aha_onmodel/dress_cutout.png`, tick GREEN):
★ Get 3 days free · Video ads from a photo — all ad formats · Keeps your product true — no warped logos or colors · Full AI photo studio · Unlimited background removal · Auto-sized for Meta·TikTok·Shopify·Amazon · No watermark — photos & videos · AI credit allowance

**Studio** 🟡 (hero: perfume gold `store/_card/perfume_cut.png`, tick trung tính):
★ Get 3 days free · Higher AI credit allowance — more ads every month · Ad template library — proven layouts to start fast · [+ full list như Creator]

**Agency** 🔵 (hero: vòng cổ `store/_card/necklace_cut.png`, tick trung tính):
★ Most AI credit allowance — highest monthly volume · ★ Multiple ads in one run · Ad template library · [+ full list]

**Design tokens** (trong `#paywall` CSS): `--tacc` (accent tier) · `--tglow` · `--tink` (chữ pill: creator dark, agency white) · `--tbg` (backdrop radial). Tick vars `--tickbg/tickbd/tickfg` set trong render() (green creator / neutral khác). Star = `.ck.st` dùng `--tacc`. Green `--g #1FD177` neo CTA+billing+trial-tag.

## 4. COSTING CREDIT (đã tính tỉ mỉ)
📄 **`research/ADSHORT_CREDIT_COSTING_2026-07-16.md`** (mục 0-FINAL) — đọc trước khi động credit.
- **Anchor: 1 credit = $0.10 COGS** (engine mới). Giá model verified fal MCP 2026-07-16.
- Video: **Light 12cr** (ugc/commercial/tryon/review $0.68–1.13) · **Standard 18cr** (ugc-full/editorial/demo $1.21–1.63) · **Premium 28cr** (motion/unboxing $2.01–2.62).
- Ảnh: photo edit **1cr** ($0.04) · Remove BG **FREE** ($0 in-house) · on-device FREE.
- **Budget đề xuất: Creator 60 / Studio 100 / Agency 220 cr/tháng** → margin net **52–57%** sau Apple 30%.
- 1 credit: COGS $0.10 · bán ~$0.30 list · net ~$0.21.

## 5. ⚠️ CÒN TREO — BE PHẢI KHÓA (chặn hiện số credit lên paywall)
1. **Photo-edit credit 6 → 1** (đồng bộ anchor $0.10; hiện file Excel ghi 6cr = thang cũ lệch 15×).
2. **Remove BG = free unlimited** (in-house $0).
3. **Budget/gói = 60/100/220** (hay số BE chốt).
4. **Re-quote 5 format** (ugc/demo/review/motion/unboxing) theo recipe experiential 07-07 — hoặc engine đã fix (2 ảnh engine-final anhvd gửi cho thấy đã có bucket 12/18/28).
- Khi có số → có thể đổi paywall từ "AI credit allowance" (vague) sang hiện SỐ kiểu Pixelcut ("600 credits/mo · ~5 ad videos").

## 6. FILE MAP
| File | Vai trò |
|---|---|
| `_preview_v2_work/index.html` | Paywall (+ cả app). `#paywall` block, TIERS obj + render() ~dòng 2830-2870 |
| `_preview_v2_work/store/_card/{perfume,necklace,dress,shoes,tote}_cut.png` | Hero cutout (perfume tôi tách rembg $0) |
| `_preview_v2_work/onboarding/_aha_onmodel/dress_cutout.png` | Đầm xanh Creator |
| `research/ADSHORT_CREDIT_COSTING_2026-07-16.md` | Costing đầy đủ |
| `C:\Users\ADMIN\Downloads\AdShort_paywall_3tier_final.png` | Ảnh 3 tier side-by-side |
| `C:\Users\ADMIN\Downloads\AdShort features check (1).xlsx` | Feature/COGS từ anhvd (free/sub gating) |
| `C:\Users\ADMIN\Downloads\adshoot-engine-handoff\handoff_2026-06-29\{cost_model,format_recipes}.v1.json` | Recipe model + cost engine |

## 7. GOTCHAS (render/verify)
- **Browser pane (mcp__Claude_Browser) screenshot TIMEOUT** với app này (nặng) → dùng **Playwright MCP** (`file:` bị chặn → serve `python -m http.server`).
- Chụp full paywall: isolate `document.body.replaceChildren(pw)` + set `#paywall position:relative` + `.p2wrap position:relative height:auto overflow:visible` → `browser_take_screenshot fullPage:true scale:css`. Ghép PIL hstack + crop black bottom bằng numpy.
- Deploy: merge PR → Actions "pages" ~25s → check `gh run view <id> --json status,conclusion`.
- Verify live: `gh` xong navigate playwright tới live URL, chạy `p2setTier` + đọc DOM (đừng tin cache — reload).

## 8. NEXT (nếu tối làm tiếp)
- Chờ/nhận số credit BE → wire số thật vào paywall (thay "allowance" vague).
- (Tùy) muốn tier dày hơn thật: BE gate format theo tier (Creator 6 → Studio/Agency 8; Editorial Try-on chỉ Agency).
- Nếu build 4K/priority/best-models → mới được thêm dòng đó (giờ chưa Live, cấm ghi).
