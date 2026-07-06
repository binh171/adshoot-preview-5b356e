# AdShort — App UI Preview (CHÍNH THỨC từ 06/07/2026)

**Demo:** https://binh171.github.io/adshoot-preview-5b356e/
**Deck so sánh trước/sau:** https://binh171.github.io/adshoot-preview-5b356e/compare.html
**Roadmap + spec + bẫy kỹ thuật:** [UI_ROADMAP.md](UI_ROADMAP.md)

Redesign theo iOS 26 Liquid Glass + trend app creative 2026 (10 vòng iterate v2→v11).
Thay thế bản cũ `adshoot-preview-f5bbdd` (giữ làm archive đối chiếu).

- Toàn bộ app = 1 file `index.html` (CSS token ở `:root`, dark theme ở `.phone.dark`, các đợt sửa đánh dấu V3→V11).
- Theme mặc định **light**, nút ☾ trên header Store bật dark.
- Push lên `main` → GitHub Actions tự deploy (~1 phút). KHÔNG dùng builder legacy (bị treo với repo này).
- Handoff chi tiết cho dev: `UI_PREVIEW_2026-07-06.md` trong repo `adshoot-engine-handoff`.
