---
name: unr3-scene
description: Dùng khi người dùng đưa một KỊCH BẢN dạng SHOT có STYLE ANCHOR (thường từ unr3-writing) và muốn sinh PROMPT tạo ảnh và PROMPT tạo video. Dùng cho một ảnh tĩnh thành một clip 8 giây; dùng unr3-storyboard khi cần nhiều ô shot và cắt cảnh trong một clip. Không dùng để viết kịch bản.
---

# unr3-scene — Kịch bản → Prompt ảnh + Prompt video

## Overview
Đọc kịch bản đã duyệt và sinh 2 file prompt tiếng Anh: `image_prompts.md` (khung hình
tĩnh) và `video_prompts.md` (animate đúng khung đó 8 giây bằng Veo 3.1). Người dùng tạo
ảnh trước rồi dùng ảnh làm frame cho video, nên ảnh và video PHẢI khớp theo thứ tự.

## Khi nào dùng
- Có sẵn kịch bản dạng SHOT + STYLE ANCHOR (thường do unr3-writing tạo).
- Bước 2 của quy trình 2 skill.
- KHÔNG dùng để viết kịch bản — đó là unr3-writing.

## Input
- File kịch bản (hoặc dán nội dung). Nếu thiếu STYLE ANCHOR hoặc không tách được SHOT:
  báo và hỏi phần thiếu, chờ trả lời; KHÔNG tự bịa. Kiểm tra STYLE ANCHOR đủ 5 trường, số shot liên tục. Chấp nhận kịch bản không có mốc thời gian; khi xuất video, mỗi SHOT trở thành một clip 8 giây. Nếu kịch bản có thời lượng tường minh khác 8 giây, hỏi cách xử lý thay vì âm thầm đổi. Nếu có lỗi hoặc yêu cầu mâu thuẫn, nêu rõ để người dùng sửa trước khi xuất prompt.

## Cách đọc kịch bản
1. Trích STYLE ANCHOR (mùa, màu, chất phim, ống kính, nhân vật/motif).
2. Đếm số SHOT = N.
3. Sinh đúng N dòng ở MỖI file. **Số dòng 2 file BẰNG NHAU tuyệt đối.**

## Khớp theo dòng (BẤT BIẾN)
Dòng k của `image_prompts.md` ⇄ dòng k của `video_prompts.md` ⇄ SHOT k.
- KHÔNG đánh số, KHÔNG bullet, KHÔNG dòng trống xen giữa.
- Mỗi dòng là MỘT prompt hoàn chỉnh, tự đứng độc lập (copy nguyên dòng là chạy được).

## Prompt ẢNH — công thức (mỗi shot = 1 dòng, tiếng Anh)
Mô tả một KHUNG HÌNH TĨNH. Nhét sẵn STYLE ANCHOR vào từng dòng:
`[subject & trạng thái tĩnh], [bối cảnh cụ thể], [bố cục & ống kính vd 35mm], [ánh sáng & thời điểm], [bảng màu & chất phim/grain], [mood], cinematic, 16:9`

Ví dụ (1 dòng):
`A young woman in a beige knit sweater standing at a quiet old-town street corner, holding a steaming coffee cup, autumn leaves on wet cobblestone, medium shot 35mm, soft morning light from the left, amber-brown palette with gentle 35mm film grain, nostalgic and calm, cinematic, 16:9`

## Prompt VIDEO — công thức (mỗi shot = 1 dòng, Veo 3.1, tiếng Anh)
Chỉ ANIMATE đúng khung ảnh đó trong 8 giây. KHÔNG đổi sang cảnh khác. Mỗi dòng phải nhắc lại chủ thể, bối cảnh và các thuộc tính STYLE ANCHOR áp dụng (mùa/thời điểm, màu, chất phim, ống kính, motif), để tự đứng độc lập. Giữ tông chill/relax, không giật gân.
`[một chuyển động cam chậm: slow push-in / gentle pan / subtle parallax], [chủ thể chuyển động nhẹ], [chuyển động nền: lá rơi, hơi nước, người xa xa], [ánh sáng giữ nguyên mood], minimal ambient sound, slow calm pacing, 8s, 16:9`

Ví dụ (1 dòng):
`Slow push-in, 35mm lens, on a young woman in a beige knit sweater holding a coffee cup at a quiet old-town street corner with wet cobblestone, her head turning slightly as autumn leaves drift and steam rises from the cup, soft morning light from the left holding steady, amber-brown palette with gentle 35mm film grain, nostalgic and calm, one continuous shot, minimal ambient sound, no music or voiceover, slow calm pacing, 8s, 16:9`

## Kỷ luật "frame → animate"
- Video prompt phải mô tả CÙNG khung ảnh, chỉ thêm chuyển động. CẤM mô tả cảnh mới,
  cắt cảnh, hay nhân vật mới trong 8s.
- Một cú cam + world motion nhẹ. Không nhồi nhiều hành động.
- Âm thanh: để `minimal ambient sound` bắt buộc vì người dùng phủ nhạc piano lên.
  Không thêm nhạc/giọng đọc trong prompt.

## Giữ nhất quán
- Giữ nhân vật/trang phục/motif nhất quán theo kịch bản. Địa điểm có thể đổi giữa các SHOT nếu kịch bản yêu cầu; trong từng cặp ảnh/video phải trùng khớp. Không tự thêm đạo cụ hay nhân vật vào video nếu ảnh không có. Kịch bản đã sửa là nguồn chính thức; không dùng lại chi tiết của bản cũ.
- Cùng ống kính/bảng màu/chất phim ở mọi dòng.

## Output
- Ghi `image_prompts.md` và `video_prompts.md` dạng UTF-8, mỗi prompt đúng một dòng vật lý; không tiêu đề, code fence, bullet hay dòng trống. Kết thúc file bằng một ký tự xuống dòng để công cụ đếm dòng chính xác.
- Present cả hai file; giải thích hoặc ghi chú chỉ viết ngoài file. Chỉ tạo prompt, không tự gọi công cụ tạo ảnh/video.

## Tự kiểm trước khi giao
- [ ] Số dòng 2 file bằng nhau và bằng N shot.
- [ ] Không đánh số, không dòng trống, mỗi dòng tự đứng độc lập.
- [ ] Mỗi dòng có `16:9`; video có `8s` + `minimal ambient sound` + nhịp chậm.
- [ ] Video animate đúng khung ảnh cùng dòng, không đổi cảnh.
- [ ] STYLE ANCHOR (màu/ống kính/chất phim) xuất hiện nhất quán ở mọi dòng.
