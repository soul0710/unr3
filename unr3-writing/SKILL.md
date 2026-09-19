---
name: unr3-writing
description: Dùng khi người dùng đưa một ý tưởng và muốn tạo KỊCH BẢN video kể chuyện dạng chill/relax để phủ nhạc piano (dạo phố, phong cảnh, hoài niệm). Là bước 1 của quy trình, tạo trước khi sinh prompt ảnh/video bằng unr3-scene hoặc unr3-storyboard.
---

# unr3-writing — Ý tưởng → Kịch bản

## Overview
Biến một ý tưởng thành kịch bản video dạng câu chuyện, tông chill/relax để phủ nhạc
piano. Mục tiêu: khán giả hứng thú và cảm động, KHÔNG giật gân. Output là 1 file
`kich_ban.md` tiếng Việt, chia thành các SHOT không ghi mốc thời gian, có khối STYLE ANCHOR ở đầu — đúng
chuẩn để `unr3-scene` hoặc `unr3-storyboard` đọc và sinh prompt ảnh/video.

## Khi nào dùng
- Người dùng đưa ý tưởng (bối cảnh, mood) và muốn kịch bản video relax.
- Bước 1 của quy trình 2 skill: unr3-writing (kịch bản) → unr3-scene (prompt ảnh + video).
- KHÔNG dùng để sinh prompt ảnh/video — đó là việc của unr3-scene.

## Input
1. Ý tưởng: bối cảnh, mùa, thời điểm, cảm xúc mong muốn.
2. Số shot `N` nếu người dùng chỉ định; phải là số nguyên dương. Nếu chỉ có thời lượng, hỏi chọn đầu ra một ảnh/clip (`unr3-scene`) hay storyboard nhiều shot/clip (`unr3-storyboard`) khi chưa rõ; không tự lấy thời lượng chia 8 để suy ra số shot cho storyboard.
   - Nếu thiếu cả số shot lẫn thời lượng: hỏi một lần về độ dài mong muốn rồi chờ câu trả lời, không tự bịa độ dài.
   - Thời lượng chỉ dùng để lên quy mô câu chuyện; không ghi timestamp, khoảng thời gian hoặc thời lượng từng shot trong `kich_ban.md`.

## Bố cục file kịch bản (BẮT BUỘC đúng format này)
File `kich_ban.md`:

    # [Tên video]

    ## STYLE ANCHOR
    - Mùa / thời điểm: [vd: thu, hoàng hôn]
    - Bảng màu: [vd: ấm, cam-nâu, nắng nghiêng]
    - Chất phim: [vd: 35mm, grain nhẹ, điện ảnh]
    - Ống kính / mood: [vd: 35–50mm, hoài niệm, chill]
    - Nhân vật / motif cố định: [vd: cô gái áo len be — hoặc "không có nhân vật"]

    ## SHOT 01
    - Cảnh: [mô tả hình ảnh cụ thể]
    - Cảm xúc: [mood của cảnh]
    - Máy quay: [gợi ý MỘT chuyển động cam chậm]
    - Nhạc: [nhịp piano / cường độ lúc này]

    ## SHOT 02
    ...

Quy tắc:
- STYLE ANCHOR viết MỘT lần, áp cho cả video → giữ mọi cảnh cùng một "bộ phim".
- Đánh số SHOT liên tục, không ghi mốc thời gian hay gắn thời lượng cố định cho từng shot. Bước tạo prompt video sẽ phân bổ thời gian.
- Mỗi shot = MỘT khoảnh khắc, một chuyển động máy quay chậm và chuyển động môi trường nhẹ. Không nhồi nhiều hành động; không cắt cảnh trong một shot.
- Thiết kế khung hình 16:9. Ghi chuyển động môi trường nhẹ trong trường Cảnh.
- Trường Nhạc chỉ là hướng dẫn phủ piano hậu kỳ, không yêu cầu mô hình video tạo nhạc.

## Mạch cảm xúc (chill, chạm, không giật gân)
Phân bổ đúng N shot theo 4 đoạn dưới đây; tỷ lệ là định hướng, không cộng các phần đã làm tròn độc lập. Với N < 4, gộp các nhịp cảm xúc trong mạch kể, vẫn giữ mỗi shot một khoảnh khắc:
1. Mở đầu gợi mở — thiết lập không gian, mời gọi (~10–15%).
2. Dạo bước — chuỗi cảnh quan sát, chi tiết đời thường đẹp (~55–65%).
3. Lắng đọng — những khoảnh khắc chậm lại, chạm cảm xúc (~15–20%).
4. Kết ấm — đóng lại nhẹ nhàng, để dư vị (~10%).

## Nguyên tắc "chill"
- Cảnh tĩnh hoặc chuyển động chậm; không rượt đuổi, không cao trào kịch tính.
- Ưu tiên chi tiết gợi cảm giác: ánh sáng, lá rơi, hơi nước cà phê, bước chân.
- Ngôn từ kịch bản gợi hình, gọn, dễ hình dung để bước sau chuyển thành prompt.

## Output
- Ghi ra `kich_ban.md` và present cho người dùng.
- Nhắc: "Xem lại, sửa STYLE ANCHOR / thêm bớt shot tuỳ ý; xong đưa file này cho unr3-scene (một ảnh/clip) hoặc unr3-storyboard (nhiều ô shot/clip)."

## Tự kiểm trước khi giao
- [ ] Có STYLE ANCHOR đủ 5 dòng.
- [ ] Đúng số shot đã thống nhất, không có mốc thời gian hoặc thời lượng từng shot.
- [ ] Mỗi shot chỉ một nhịp/một cú máy.
- [ ] Có mạch mở/dạo/lắng/kết phù hợp số shot, có kết ấm.
- [ ] Không có yếu tố giật gân.
