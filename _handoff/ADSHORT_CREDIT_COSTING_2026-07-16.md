# AdShort — Credit Costing từ model thật (2026-07-16)

> ⚠️ **UPDATE — ENGINE-FINAL (2 ảnh engine chưa-commit, 2026-07-16 chiều)**: bản dưới (mục 1-6) là recipe cũ tôi có; engine THẬT đã đổi. Dùng số ENGINE-FINAL dưới đây, phần cũ để tham chiếu.

## 0-FINAL. BẢNG COGS CHỐT (anchor 1 credit = $0.10 COGS)

**Video** (COLD + audio): ugc_ad-light $0.68 · commercial/ugc_tryon $0.93 · product_review $1.13 → **Light 12cr** · ugc_ad-full $1.21 · editorial_tryon $1.35 · demo $1.63 → **Standard 18cr** · motion_ad $2.01 · unboxing $2.62 → **Premium 28cr**.
**Ảnh**: Remove BG (in-house $0) = **FREE ∞** · AI photo edit (Flux Kontext $0.04) = **1cr** · on-device (Core Image $0) = FREE.
**Peg**: 1 credit = $0.10 COGS · bán ~$0.30 list · net ~$0.21 sau Apple 30%. Ảnh charge 1cr/$0.04 = đệm 2.5×. Cache L2 = margin bonus.

## 0. ENGINE-FINAL — GIÁ THẬT/CLIP (Recipe mode, fal COLD, +$0.06 audio)

| Bucket | Format | COGS thật | Credit/clip (1cr=$0.10, buffer) |
|---|---|---|---|
| **Light** | ugc_ad(nhẹ) $0.68 · commercial $0.93 · ugc_tryon $0.93 · product_review $1.13 | $0.68–1.13 | **12** |
| **Standard** | ugc_ad(đủ) $1.21 · editorial_tryon $1.35 · demo $1.63 | $1.21–1.63 | **18** |
| **Premium** | motion_ad $2.01 · unboxing $2.62 | $2.0–2.62 | **28** |

- **Anchor mới: 1 credit = $0.10 COGS** (khác peg $0.05-list cũ của tôi). Range clip ~$0.68–2.62, median ~$1.1–1.3.
- Công thức: `cost = compose×$0.15 + Σ(motion $/s × dur) + $0(native/card/label/assemble) + $0.06 audio`.
- $/s verified: kling 0.07 · veo 0.15 · omnihuman 0.14 · seedance_2_fast(_ref) 0.242 · seedance_2_ref 0.303.
- Composer mode (nếu bật flip#13) ĐẮT HƠN: demo $2.53 · motion_ad $3.92. → giữ Recipe mode default.
- **gen_store L2 cache** (vừa build): clip trùng nội dung → $0 lần sau. Tính giá theo COLD, coi cache = margin bonus.

## 0b. CÂN ĐỐI credit/gói — margin SAU Apple cut (điều engine note chưa trừ)

Anchor $0.10 COGS/cr. Sub bán theo giá list; Apple cắt 30% (năm1). Đề xuất giữ **~55% margin net**:

| Gói | Giá/mo list | Net (−30%) | **Credit/tháng** | COGS max | Margin net | ~Clip (L/S/P) |
|---|---|---|---|---|---|---|
| **Creator** | $19.99 | $13.99 | **60** | $6.00 | **57%** | 5 / 3 / 2 |
| **Studio** | $29.99 | $20.99 | **100** | $10.00 | **52%** | 8 / 5 / 3 |
| **Agency** | $69.99 | $48.99 | **220** | $22.00 | **55%** | 18 / 12 / 7 |

- Effective sell/cr: Creator $0.333 → net $0.233 → COGS $0.10 = **57% margin**. Dương khoẻ cả 3.
- ⚠️ **Gói YEARLY margin mỏng hơn** (Creator yearly $13.99/mo → net $9.79 → cùng 60cr = **~39%**). Chấp nhận (đổi lấy cam kết năm), nhưng đừng cho credit cao hơn ở yearly.
- Cache L2 + res thấp = margin thực CAO HƠN số này (buffer an toàn).
- Clip count ~5/8/18 KHỚP ước tính cũ (~6/10/24) — chỉ khác đơn vị credit do đổi anchor.

## 0c. 2 quyết định engine hỏi (ảnh hưởng credit)
1. **Tier→model?** Hiện Draft/Pro/Ultra cùng model/giá. → **Đề xuất PO: chưa map model theo tier** (giữ credit đơn giản); phân biệt gói bằng **volume credit + feature** (support/4K/priority). Map `apply_tier` (Ultra=veo/seedance-ref) để SAU khi cần "best models" cho Agency.
2. **Resolution lever?** → **Có**: base 1080p = credit chuẩn; **4K = +50% credit**, chỉ Agency/Premium (khớp Photoroom "4k+ resolution", vừa thêm đòn nâng cấp vừa bù cost Veo 4K).

---
### (Tham chiếu — recipe cũ tôi tự tính, engine đã đổi số một số format)


> Mục tiêu: từ **model engine gọi để tạo 1 video** → COGS → giá trị 1 credit → credit mỗi gói. Tính tỉ mỉ, có store-cut.
> Nguồn: `adshoot-engine-handoff/handoff_2026-06-29/format_recipes.v1.json` (recipe = model gọi thật, look_note update 07-07) + `cost_model.v1.json`. Giá fal **validate real-time qua fal MCP 2026-07-16 — khớp 100%**.

## 1. Giá model fal (VERIFIED 2026-07-16, khớp cost_model 06-30)

| Model | Vai trò | Giá |
|---|---|---|
| Nano Banana Pro (`gemini-3-pro-image/edit`) | composite | **$0.15 / ảnh** |
| Seedream v5 Lite (`bytedance/seedream/v5/lite/edit`) | scene/label | **$0.035 / ảnh** |
| Hailuo 02 Std (`minimax/hailuo-02/standard/i2v`) | motion người | **$0.045 / s** (6s=$0.27, 10s=$0.45) |
| Kling 2.5T (`kling-video/v2.5-turbo/pro/i2v`) | motion giữ-nhãn | **$0.07 / s** (5s=$0.35) |
| Veo 3.1 (`veo3.1/i2v`) | hero cao cấp | **$0.40 / s** (5s=$2.00, 8s=$3.20 ⚠️) |
| Veo 3.1 Fast | hero rẻ hơn | **$0.15 / s** |
| MiniMax Speech-02 HD | VO/TTS | **$0.10 / 1000 ký tự** |
| ffmpeg (ken-burns/caption/concat) | — | **$0** |

## 2. COGS mỗi format = tổng giá beat (từ recipe canonical)

| Format | Beats (model) | **COGS** | Credit @55% list* |
|---|---|---|---|
| before_after | seedream + hailuo6s + ffmpeg×2 | **$0.34** | 16 |
| split_screen | seedream + hailuo5s + ffmpeg×2 | **$0.34** | 16 |
| turntable | seedream + kling5s + ffmpeg×3 | **$0.385** | 18 |
| listicle | seedream×3(wan) + seedream + ffmpeg | **$0.44** | 20 |
| product_review | nbpro + kling5s + assemble + ffmpeg | **$0.50** | 23 |
| commercial_premium | nbpro + seedream+kling5s + ffmpeg | **$0.535** | 24 |
| commercial | nbpro + kling5s + seedream×2 + ffmpeg×2 | **$0.57** | 26 |
| editorial_tryon | nbpro + hailuo10s + seedream×2 + ffmpeg×2 | **$0.67** | 30 |
| founder | nbpro + hailuo-pro10s + seedream | **$0.665** | 30 |
| grwm | hailuo(2+6+3)s + seedream | **$0.725** | 33 |
| demo | nbpro + kling5s×2 + ffmpeg | **$0.85** | 38 |
| commercial_lite | nbpro + (seedream+kling5s)×2 + ffmpeg | **$0.92** | 41 |
| ugc_tryon | nbpro + hailuo6s + (seedream+hailuo10s) + ffmpeg | **$0.94** | 42 |
| **ugc_ad** | nbpro + hailuo6s + kling5s×2 + ffmpeg | **$1.12** | **50** |
| motion_ad | seedream + nbpro + veo5s + veo2s | **$1.235** | 55 |
| unboxing | nbpro×2 + kling(4×3+4)s + ffmpeg×2 | **$1.63** | 73 |
| unboxing_oneshot | nbpro×3 + veo8s + veo4s | **$2.25** | 100 |

*Credit @55% list = `ceil(COGS / 0.45 / $0.05)` — công thức engine (`credit_formula`), margin 55% GROSS trên giá list.

## 3. ⚠️ PHÁT HIỆN 1: recipe 07-07 ĐẮT HƠN credit đang charge (Excel/estimateCost)

| Format | COGS recipe | Credit ĐÚNG (55%) | Credit Excel đang charge | Lệch |
|---|---|---|---|---|
| ugc_ad | $1.12 | **50** | 20 | **thiếu 2.5×** |
| demo | $0.85 | 38 | 20 | thiếu ~2× |
| product_review | $0.50 | 23 | 19 | thiếu nhẹ |
| motion_ad | $1.235 | 55 | 40 | thiếu |
| unboxing | $1.63 | 73 | 54 | thiếu |
| commercial | $0.57 | 26 | 26 | ✓ khớp |
| ugc_tryon | $0.94 | 42 | 42 | ✓ khớp |
| editorial_tryon | $0.67 | 30 | 30 | ✓ khớp |

→ UGC/Demo/Review/Motion/Unboxing dùng recipe "experiential" 07-07 (thêm beat Kling product_use+react) → **đắt hơn** credit đang thu. Commercial/try-on thì khớp. **Cần BE re-quote 5 format này** hoặc số credit sẽ lỗ.

## 4. Giá trị 1 credit — CÓ store-cut (điểm mấu chốt)

- User trả **$0.05 / credit** (list, peg engine).
- **COGS / credit** (khi charge đúng công thức 55%) = `0.45 × $0.05` = **$0.0225 / credit** — ĐỒNG ĐỀU mọi format.
- Apple cắt: **năm 1 = 30%** → dev thực nhận **$0.035/cr**; **năm 2 = 15%** → **$0.0425/cr**.

| | Thu/credit (net) | COGS/credit | **Margin net/credit** |
|---|---|---|---|
| Năm 1 (cut 30%) | $0.035 | $0.0225 | **+36%** ✅ |
| Năm 2 (cut 15%) | $0.0425 | $0.0225 | **+47%** ✅ |

→ **Video KHÔNG lỗ SAU store-cut — miễn là charge đúng credit theo công thức 55%.** "Lỗ" chỉ xảy ra khi charge flat/cũ (vd UGC 20cr cho recipe $1.12: thu net $0.70 < COGS $1.12 = **lỗ $0.42**).

## 5. ✅ PHÁT HIỆN 2: số 50/83/216 CŨ thực ra GROUNDED (tôi rút lại nhận định "bịa")

50/83/216 "photo edits" (photo=6cr) ⇒ budget **300 / 500 / 1300 credit**. Đây CHÍNH LÀ mức credit giữ được ~50% margin sau cut 30%:
- Ngưỡng 50% margin: `N ≤ giá_list / $0.0643`.
- Creator $19.99 → ≤311cr · Studio $29.99 → ≤466cr · Agency $69.99 → ≤1088cr.

Khớp gần đúng 300/500/1300. Vậy con số cũ có cơ sở, không phải bịa — tôi nói lại cho đúng.

## 6. ĐỀ XUẤT credit/gói (giá hiện tại, giữ ~50% margin net sau cut 30%)

| Gói | Giá/mo (list) | **Credit/tháng** | ≈ UGC video (50cr) | ≈ format rẻ (18cr) | ≈ photo edit (6cr) |
|---|---|---|---|---|---|
| **Creator** | $19.99 | **300** | 6 | 16 | 50 |
| **Studio** | $29.99 | **500** | 10 | 27 | 83 |
| **Agency** | $69.99 | **1.200** | 24 | 66 | 200 |

- Margin net (cut 30%) khi user xài HẾT vào UGC đắt: Creator ~50%, Studio ~52%, Agency ~45%. Dương cả 3.
- Credit = van chặn cost (hết → mua thêm/nâng gói). Không hết hạn = trust wedge (đối thủ reset hàng tháng).

## 7. Việc cho BE (chặn số cuối)
1. **Re-quote 5 format** (ugc/demo/review/motion/unboxing) theo recipe 07-07 — hoặc giảm beat để về COGS cũ.
2. Xác nhận **credit budget/gói** = 300/500/1200 (hay khác) → mình mới ghi lên paywall.
3. Xác nhận **flat vs per-format credit** ở quote engine (dry.quote) — phải per-format, KHÔNG flat 20.

---
*Giá model verified fal MCP 2026-07-16. Recipe: format_recipes.v1.json (look_note 07-07). Store-cut: Apple SBP 30% năm 1 / 15% năm 2.*
