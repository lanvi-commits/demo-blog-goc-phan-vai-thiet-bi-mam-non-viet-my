# Demo — Ảnh mẫu bài "30+ mẫu trang trí góc phân vai mầm non"

Bài gốc: https://website-demo-02.thcmedia.vn/blog/trang-tri-goc-phan-vai-mam-non/
Bản demo: https://lanvi-commits.github.io/demo-blog-goc-phan-vai-thiet-bi-mam-non-viet-my/

Trang demo là **HTML thật của bài** (header, mục lục, nội dung chữ, footer, nút liên hệ nổi giữ nguyên).
Chỉ đổi **cách xếp các cụm ảnh mẫu** dưới 6 mục "Ý tưởng trang trí góc …". Ảnh, alt, chú thích, thứ tự ảnh
và toàn bộ chữ giữ nguyên (đã so: 6.249 chữ, 40 ảnh, 40 chú thích khớp 100% với bài gốc).

## Thay đổi

| Khổ màn hình | Bài hiện tại | Bản demo |
|---|---|---|
| Máy tính (≥ 992px) | 1 ảnh/hàng, khổ 800px, hai bên trống | **Lưới 2 cột**, mỗi ảnh ~650px. Cụm có số ảnh lẻ: ảnh đầu giữ khổ 800px, các ảnh sau xếp cặp |
| Điện thoại + tablet (< 992px) | 1 ảnh/hàng, cuộn dọc hết từng ảnh | **Mỗi góc 1 slider**: vuốt ngang xem ảnh, ảnh sau ló ra ở mép phải, hàng nút ‹ › + chấm dưới ảnh. **Không tự chạy** |

Chiều dài trang: máy tính 34.886 → 24.124px (−31%), điện thoại 390px 30.996 → 22.809px (−26%).

Cụm ảnh được gom:

| Mục | Ảnh liền nhau |
|---|---|
| Góc gia đình | 6 |
| Góc bán hàng, siêu thị mini | 4 |
| Góc nấu ăn, nhà hàng | 7 (ảnh đầu khổ lớn + 3 cặp) |
| Góc bác sĩ | 6 |
| Các góc nghề nghiệp | 2 (cặp cuối). 3 ảnh đầu đứng xen giữa đoạn văn, mỗi ảnh minh hoạ đoạn ngay trên → **giữ nguyên chỗ** |
| Góc chợ quê, trò chơi dân gian | 5 (ảnh đầu khổ lớn + 2 cặp) |

## Ghi chú cho DEV

1. **HTML** — bọc mỗi cụm ≥ 2 `<figure class="wp-caption">` liền nhau trong khung Splide (xem `index.html`, tìm `vmx-goc`):

   ```html
   <div class="vmx-goc splide [vmx-goc--le nếu số ảnh lẻ]" role="group" aria-label="<tên H2> – N ảnh">
     <div class="splide__track"><ul class="splide__list">
       <li class="splide__slide"><figure class="wp-caption">…giữ nguyên…</figure></li>
     </ul></div>
     <div class="splide__arrows">
       <button class="splide__arrow splide__arrow--prev" type="button" aria-label="Ảnh trước"><i class="fa-solid fa-chevron-left" aria-hidden="true"></i></button>
       <button class="splide__arrow splide__arrow--next" type="button" aria-label="Ảnh sau"><i class="fa-solid fa-chevron-right" aria-hidden="true"></i></button>
     </div>
   </div>
   ```

   Làm tự động được (filter `the_content`: tìm cụm figure liền nhau trong bài) hoặc block gallery riêng cho biên tập viên.

2. **CSS** — khối `<style id="vmx-change">` trong `index.html` (đặt ngay sau `single-post.css`). Có `!important` ở `figure.wp-caption`
   vì WordPress gắn inline `style="width: 800px; margin: 24px auto"`.

3. **JS** — khối `<script id="vmx-page-js">`. Cách chuyển slider ↔ lưới giống hệt `.single-post-related-splide` đang có trong
   `splide-init.js`: `mediaQuery: 'min'` + `breakpoints: { 992: { destroy: true } }`.
   **Bắt buộc tạo bằng `window.Splide.__thcOriginal`** — `splide-autoplay.js` của theme ép `autoplay: true` cho mọi slider
   > 1 slide (truyền `autoplay: false` cũng không tắt được). Slider ảnh có chú thích không được tự chạy.

4. Giữ `type: 'slide'` (không `loop` → không nhân bản ảnh trong DOM), ảnh để `src` thật (không dùng lazy riêng của Splide)
   để Google Hình ảnh vẫn thấy đủ ảnh.

## Chỉ có trong bản demo (không đưa lên site)

- `<script id="vmx-demo-guard">`: chặn mọi yêu cầu POST (fetch/XHR/beacon) và form CF7 — để bấm gửi "Gửi yêu cầu báo giá" trên
  github.io **không** thành yêu cầu thật về site.
- Đã bỏ script: CF7, kk-star-ratings, thêm vào báo giá/giỏ, xem nhanh, so sánh, review, gắn nofollow, theo dõi nguồn khách.
- CSS + font icon nhúng sẵn trong file; JS theme và ảnh bài vẫn tải từ website-demo-02 (cần mạng).

Dựng bằng `nguyen-lieu/2026-10-27_blog-goc-phan-vai-anh-build/build.py` (máy thiết kế) — đừng sửa tay `index.html`.
