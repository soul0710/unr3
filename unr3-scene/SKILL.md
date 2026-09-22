---
name: unr3-scene
description: Dùng khi người dùng đưa một KỊCH BẢN dạng SHOT có STYLE ANCHOR (thường từ unr3-writing) và muốn sinh PROMPT tạo ảnh và PROMPT tạo video. Dùng cho một ảnh tĩnh thành một clip 8 giây với camera rất chậm ở tốc độ cố định, không ease-in/ease-out; dùng unr3-storyboard khi cần nhiều ô shot và cắt cảnh trong một clip. Không dùng để viết kịch bản.
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
`[một chuyển động cam rất chậm ở tốc độ cố định: very slow constant-speed push-in / constant-speed gentle pan / constant-speed subtle parallax], [chủ thể chuyển động nhẹ], [chuyển động nền: lá rơi, hơi nước, người xa xa], [ánh sáng giữ nguyên mood], constant camera speed from first to last frame, no easing, no acceleration or deceleration, minimal ambient sound, slow calm pacing, 8s, 16:9`

Ví dụ (1 dòng):
`Very slow constant-speed push-in, 35mm lens, on a young woman in a beige knit sweater holding a coffee cup at a quiet old-town street corner with wet cobblestone, her head turning slightly as autumn leaves drift and steam rises from the cup, soft morning light from the left holding steady, amber-brown palette with gentle 35mm film grain, nostalgic and calm, one continuous shot, camera speed remains unchanged from first to last frame, no easing, no acceleration or deceleration, minimal ambient sound, no music or voiceover, slow calm pacing, 8s, 16:9`

## Kỷ luật "frame → animate"
- Video prompt phải mô tả CÙNG khung ảnh, chỉ thêm chuyển động. CẤM mô tả cảnh mới,
  cắt cảnh, hay nhân vật mới trong 8s.
- Một cú cam rất chậm ở một tốc độ cố định từ đầu đến cuối + world motion nhẹ. Cấm `ease-in/ease-out`, acceleration/deceleration, speed ramp, whip pan, crash zoom, snap zoom, fast orbit, handheld shake và đổi hướng camera trong clip. Không nhồi nhiều hành động.
- Âm thanh: để `minimal ambient sound` bắt buộc vì người dùng phủ nhạc piano lên.
  Không thêm nhạc/giọng đọc trong prompt.

## Giữ nhất quán
- Giữ nhân vật/trang phục/motif nhất quán theo kịch bản. Địa điểm có thể đổi giữa các SHOT nếu kịch bản yêu cầu; trong từng cặp ảnh/video phải trùng khớp. Không tự thêm đạo cụ hay nhân vật vào video nếu ảnh không có. Kịch bản đã sửa là nguồn chính thức; không dùng lại chi tiết của bản cũ.
- Cùng ống kính/bảng màu/chất phim ở mọi dòng.

## Output
- Ghi `image_prompts.md` và `video_prompts.md` dạng UTF-8, mỗi prompt đúng một dòng vật lý; không tiêu đề, code fence, bullet hay dòng trống. Kết thúc file bằng một ký tự xuống dòng để công cụ đếm dòng chính xác.
- Present cả hai file; giải thích hoặc ghi chú chỉ viết ngoài file. Chỉ tạo prompt, không tự gọi công cụ tạo ảnh/video.

## Mạch truyện và liên kết giữa các shot
- Toàn bộ kịch bản phải kể một câu chuyện có mở đầu, diễn tiến và kết thúc hợp lý. Mỗi shot đóng góp vào cùng hành trình/chủ đề cụ thể; cùng màu sắc hoặc cùng mood chưa đủ để tạo liên kết.
- Mỗi cặp shot tổng liền kề phải có cầu nối nhìn thấy được: hành động tiếp diễn, nguyên nhân–kết quả, ánh nhìn–đối tượng, di chuyển theo tuyến đường, hoặc một chi tiết dẫn sang diễn biến tiếp theo. Không chèn cảnh đẹp rời rạc chỉ để đủ số shot.
- Theo dõi trạng thái qua từng shot: vị trí, thời điểm, nhân vật, phục trang, đạo cụ đang ở đâu/trong tay ai, hướng nhìn, hướng di chuyển và cảm xúc. Đầu shot sau phải tương thích với cuối shot trước; thay đổi địa điểm/thời gian phải có dấu hiệu chuyển tiếp rõ.
- Với câu chuyện không có nhân vật, dùng tuyến khám phá không gian, biến chuyển ánh sáng/thời tiết hoặc motif có diễn tiến làm sợi dây dẫn chuyện; không chỉ ghép phong cảnh ngẫu nhiên.
- Đọc toàn bộ kịch bản trước khi sinh từng dòng. Giữ các cầu nối và trạng thái của kịch bản trong cả prompt ảnh lẫn prompt video; mô tả cụ thể trạng thái đầu/cuối có liên quan, không chỉ viết “same as previous shot”. Mỗi dòng vẫn tự đứng độc lập.
- Giữa clip k và k+1, giữ một camera handoff cụ thể: cùng hướng pan/slide, cùng điểm nhìn, cùng motif hoặc trạng thái tĩnh tương ứng. Camera của clip k giữ nguyên tốc độ chậm đến khung cuối; camera của clip k+1 bắt đầu ngay ở tốc độ chậm cố định. Dùng clean cut/match cut tại một điểm nối rõ, không giảm tốc, dừng, tăng tốc hoặc dùng `ease-in/ease-out` để tạo chuyển cảnh.
- Nếu kịch bản nguồn bị đứt mạch, nêu đúng cặp shot và hỏi phần nối cần thiết trước khi xuất; không tự thêm sự kiện, đổi thứ tự hoặc bỏ shot để che lỗi. Có thể bổ sung chi tiết dàn cảnh không đổi nội dung để làm rõ liên kết có sẵn.
- Tự kiểm từng cặp dòng k/k+1: cuối clip k nối hợp lý với ảnh đầu clip k+1 về hành động, không gian, đạo cụ và cảm xúc. Giữ mỗi clip một cú máy 8 giây và khớp ảnh/video theo dòng.

## Chọn ngôn ngữ điện ảnh
- Trước khi tạo bộ prompt, đọc [tham chiếu điện ảnh relaxing](references/cinematic-relaxing.md): chọn theo sáu nhóm góc máy/chuyển động, ánh sáng, bố cục, ống kính/chất phim, phong cách/màu/cảm xúc, chất liệu/thời tiết/tư thế. Chỉ áp dụng lựa chọn phù hợp kịch bản; không liệt kê toàn bộ từ khóa.
- Trước khi viết, xác định điểm người xem cần chú ý và cảm xúc của shot. Chọn cỡ cảnh, góc nhìn, bố cục và ánh sáng phục vụ điểm đó; không tự thêm sự kiện để minh họa một kỹ thuật.
- Ảnh cần nêu cỡ cảnh + góc máy + bố cục + vùng nét. Video kế thừa đúng các lựa chọn đó, thêm một hành động chính nhỏ và một chuyển động camera rất chậm ở tốc độ cố định. Không đưa lệnh chuyển động camera vào mô tả khung ảnh tĩnh.
- Chọn một nguyên tắc bố cục chính: đường dẫn mắt tới chủ thể, khoảng trống theo hướng nhìn, hoặc khung cửa bao quanh chủ thể. Chỉ thêm lớp tiền cảnh khi không che hành động/đạo cụ quan trọng; giữ bố cục đọc được trong suốt đường đi camera.
- Mô tả nguồn sáng nằm ở đâu, chiếu theo hướng nào và mềm hay gắt. Giữ nguồn sáng, thời tiết, thời điểm và bóng đổ hợp lý; một hiện tượng hiếm như mưa dưới nắng cần có nguồn sáng được giải thích, không coi mọi tổ hợp là bất khả thi.
- Chọn vùng nét theo nội dung: cần thấy tuyến đường/bối cảnh thì giữ đủ chiều sâu nét; cần nhấn chi tiết thì tách nền vừa phải nhưng vẫn rõ đạo cụ nối chuyện. Không ghép shallow depth of field với yêu cầu mọi khoảng cách đều sắc nét; giữ tiêu cự theo STYLE ANCHOR.
- Phân biệt dolly/slide là dịch chuyển vị trí máy, pan/tilt là xoay hướng máy, zoom là đổi tiêu cự. Với quy tắc giữ ống kính hiện tại, ưu tiên dolly/slide/pan/tilt; không ghép zoom và dolly hoặc tự thêm rack focus. Nêu hướng, đối tượng hướng tới và quãng di chuyển nhỏ; không hứa lộ phần không gian chưa được ảnh/kịch bản xác lập.
- Chỉ thêm chi tiết chất liệu nếu giúp đọc cảnh: sợi vải ở tay áo, vân gỗ trên bàn, giọt nước trên kính. Giữ màu, chất liệu và dấu hiệu nhận diện cố định giữa các clip; không đổi phong cách ảnh thật/hoạt hình chỉ vì thêm từ khóa.
- Mỗi lựa chọn kỹ thuật phải có tác dụng nhìn thấy được. Bỏ từ đồng nghĩa lặp, tên thiết bị và nhãn chất lượng chung chung; không giới hạn độ dài bằng cách xóa thông tin nhận diện hoặc cầu nối giữa shot.
- Nếu cần loại trừ lỗi, chọn đúng lỗi liên quan đến cảnh, diễn đạt trong cùng dòng prompt; không tạo file negative prompt thứ ba. Không cấm blur toàn cục khi cảnh cần nền mờ hoặc chuyển động môi trường tự nhiên.

Nguồn tham khảo ý tưởng: [Cinematic Video Prompt Skill của Rylaispirit](https://github.com/Rylaispirit/cinematic-video-prompt-skill). Các hướng dẫn trên được viết cho quy trình UNR3; định dạng hai file, clip 8 giây và camera không easing vẫn là yêu cầu bắt buộc.

## Tự kiểm trước khi giao
- [ ] Chất phim và phong cách nhất quán; màu vật thể không đổi vô cớ; chất liệu/độ ướt/hướng gió hợp lý; tư thế đầu–cuối, tay cầm đạo cụ và ánh nhìn nối đúng giữa các clip.
- [ ] Góc máy/bố cục/vùng nét khớp giữa ảnh và video; ánh sáng có nguồn hợp lý, không có yêu cầu kỹ thuật mâu thuẫn; chỉ một hành động chính nhỏ trong clip.
- [ ] Số dòng 2 file bằng nhau và bằng N shot.
- [ ] Không đánh số, không dòng trống, mỗi dòng tự đứng độc lập.
- [ ] Mỗi dòng có `16:9`; video có `8s` + `minimal ambient sound` + nhịp chậm.
- [ ] Video animate đúng khung ảnh cùng dòng, không đổi cảnh.
- [ ] Camera dùng đúng một chuyển động rất chậm ở tốc độ cố định từ đầu đến cuối; không có `ease-in/ease-out`, tăng tốc hoặc giảm tốc; các clip liền kề có camera handoff cụ thể.
- [ ] STYLE ANCHOR (màu/ống kính/chất phim) xuất hiện nhất quán ở mọi dòng.
