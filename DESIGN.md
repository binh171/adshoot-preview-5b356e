# AdShort — Design System (DESIGN.md)

> Single source of truth. **Kiến trúc 2 tầng**: Story (cinematic) + Work (pro sạch).
> Locked: 2026-07-14 sau nhiều vòng iterate. Map token 1:1 vào `index.html` `:root`.
> Nguyên tắc vàng (từ research iOS 26 Liquid Glass): **kính chỉ ở lớp nav/chrome/nút nổi — KHÔNG phủ lên content**.

---

## 0. Two-Tier Architecture (đọc trước tiên)

| Tầng | Màn | Bề mặt | Kính |
|---|---|---|---|
| **STORY** (kể chuyện) | Welcome · Aha · Paywall · Result · Onboarding Q1/Q2 | Ảnh sản phẩm full-bleed + dark/bright scrim | Kính phủ tự do (đây là marketing moment) |
| **WORK** (làm việc) | Store · Product · AdVideo · Editor · Picker | **Surface ĐẶC, sạch, sáng** (Linear/Mercury) | Kính **CHỈ** ở bottom-nav, sticky header, FAB |

**Vì sao:** màn nhiều tool cần rõ ràng + mật độ; kính-phủ-content làm đục. Story cần cảm xúc → kính hợp. Đừng ép 1 skin cho cả 2.

---

## 1. Brand
- **Emerald** `--em:#0E5C43` — brand + action chính.
- **Emerald bright** `--em-l:#2EC494` · **Mint** `--mint:#8FE9C8` — accent/glow trên dark, text "Short".
- **Emerald deep** `--em-d:#0A4632` — hover/pressed.
- **Gold** `--gold:#C9A254` — accent premium HIẾM (Pro badge, số điểm). Không dùng cho action.
- **Fonts**: `Fraunces` (display + wordmark, dùng ít) · `Geist` (UI/body). Sans = Geist. Wordmark "AdShort" **luôn viết liền**.

---

## 2. Color — theo tầng

### STORY (trên ảnh)
- Text: trắng `#FFFFFF` / `rgba(255,255,255,.82)` phụ · accent mint.
- Scrim tối: `linear-gradient(180deg,rgba(6,12,9,.5),rgba(6,10,8,.9))`.
- Grain overlay ~5% (fractalNoise) cho chất.

### WORK (surface đặc)
| Token | Light | Dark |
|---|---|---|
| `--bg` (page) | `#F4F6F5` | `#0C0E0D` |
| `--surface-1` (card) | `#FFFFFF` | `#141917` |
| `--surface-2` (raised) | `#F0F3F1` | `#1B211E` |
| `--ink` | `#0D1A16` | `#F2F5F3` |
| `--ink-2` | `#41504B` | `#B9C6C0` |
| `--muted` | `#7C8A85` | `#8A968F` |
| `--line` | `#E2E7E4` | `#242A27` |
| `--em-soft` | `#E4EEE9` | `rgba(46,196,148,.14)` |

> Fix cũ: `--muted #8E8E93` fail AA ở light → dùng `#7C8A85`.

---

## 3. Typography (scale 7 bậc)
| Token | Size / LH | Font · Weight | Tracking | Dùng |
|---|---|---|---|---|
| `display` | 44 / .96 | Fraunces 500 | -1px | hero story ("One photo in.") |
| `h1` | 30 / 1.05 | Geist 700 | -.6px | tiêu đề màn work |
| `h2` | 22 / 1.1 | Geist 700 / Fraunces 500 | -.3px | section / story sub |
| `h3` | 17 / 1.2 | Geist 600 | -.2px | card title |
| `body` | 15 / 1.5 | Geist 500 | 0 | mặc định |
| `small` | 13 / 1.45 | Geist 500 | 0 | meta |
| `caption` | 10.5 / 1.3 | Geist 700 | +.18em UPPER | eyebrow/label |
- Fraunces: CHỈ wordmark + 1 display/màn. Không italic < 16px.

---

## 4. Spacing · Radius · Elevation
- **Spacing (4pt):** 4 · 8 · 12 · 16 · 20 · 24 · 32 · 40. Gutter màn = 20–22.
- **Radius:** `--r-sm 12` · `--r-md 16` · `--r-lg 20` · `--r-pill 999`. Phone 40.
- **Elevation (work):** `--e1 0 1px 2px rgba(0,0,0,.06)` · `--e2 0 8px 24px rgba(0,0,0,.10)` · `--e3 0 14px 32px rgba(0,0,0,.16)`.

---

## 5. Liquid Glass — LUẬT DÙNG
Chỉ dùng ở: **bottom-nav · sticky header · FAB · story CTA · badge nổi trên media**. KHÔNG dùng cho card/list/content-surface ở Work tier.

**Chuẩn kính (1 mức):** `background:rgba(255,255,255,.10-.14)` (dark) / `rgba(255,255,255,.6)` (light-glass) · `backdrop-filter:blur(24px) saturate(160%)` · `border:1px solid rgba(255,255,255,.3)` · specular `inset 0 1.5px 0 rgba(255,255,255,.6)` · noise 5%. **Trên media phải bright** (brightness 1.1–1.15), không để đục tối.

---

## 6. Buttons

### Story CTA (trên ảnh) — 2 biến thể glass, LOCKED
- **Primary (Begin/Continue/Remove…)** = **Bright liquid glass + tia sáng quét**:
  `background:linear-gradient(180deg,rgba(255,255,255,.68),rgba(255,255,255,.5)); backdrop-filter:blur(26px) saturate(140%) brightness(1.15); border:1px solid rgba(255,255,255,.85); color:#0a3a2c; radius 999; height 60`
  + `::after` sweep 4.2s. Dome gloss ::before nhẹ. **Không mũi tên.**
- **Paywall CTA** = bright liquid glass + **breathing glow** (3s). Cùng chất, khác hiệu ứng.

### Work CTA (surface đặc) — cấp bậc
- **Primary** = solid `--em` (hoặc emerald gradient `#12694e→#0a4230`), chữ trắng, radius pill, `--e2`.
- **Secondary** = outline `--line`, chữ `--ink`, nền trong.
- **Tertiary** = soft `--em-soft` fill, chữ `--em`.
- **Icon btn** = 40px, `--surface-1` + `--line` hoặc glass (nếu trên media). Icon set: **Phosphor/Lucide**, KHÔNG vẽ tay, KHÔNG emoji.
- Mọi nút: 5 state (default/hover/active scale .98/disabled/loading).

---

## 7. Components
- **Bottom nav** — glass pill (cả 2 tầng), active = mint/em + label. Icon Phosphor.
- **Header** — 1 component (back + title + trailing). Work: sticky solid + blur khi scroll. Story: trong suốt trên ảnh.
- **Card (Work)** — `--surface-1`, `--r-md`, `--line`, `--e1`. KHÔNG kính. Ảnh trong card có scrim khi đặt text.
- **Chip/Filter** — Work: `--surface-1`+`--line`, active `--em`. Story: glass. **Bỏ emoji.**
- **Marketplace logo** — dùng logo brand thật (Simple Icons/asset), fallback letter-avatar màu brand.
- **Plan card (paywall)** — glass, selected = mint border + tint. Giữ nội dung gốc.
- **Score/metric** — số Geist/Fraunces + label caption. Mint dot cho "live".
- **Toast** — glass, trên nav, auto-dismiss.

---

## 8. Story tier spec
Nền = ảnh sản phẩm + scrim + grain. Fraunces display trắng + accent mint. Glass badge/CTA. Cinematic, ít chrome. Dùng cho: Welcome, Aha (remove-BG demo), Q1/Q2, Paywall, Result/Export.

## 9. Work tier spec (CẦN thiết kế + duyệt)
Nền `--bg` sạch (light default, dark tuỳ). Content = card/list surface đặc. Kính chỉ ở nav/header/FAB. Mật độ cao, rõ ràng, type scale chặt, nhiều khoảng thở. Dùng cho: **Store (đủ tool), Product, AdVideo, Editor, Picker**. → *Bước tiếp: dựng Store theo tầng này để duyệt.*

---

## 10. Migration → index.html
- Giữ engine/logic/animation. Chỉ thay CSS/markup vỏ.
- `:root` mở rộng theo §2. Dark = `.phone.dark` (giữ). Override cuối stylesheet.
- Story screens: skin cinematic. Work screens: skin surface sạch + nav glass.
- **Do:** kính đúng luật §5 · type theo scale · icon pro · logo brand thật.
- **Don't:** kính phủ content · emoji · Fraunces cho UI nhỏ · nút muddy-glass tối.
