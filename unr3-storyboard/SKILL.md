---
name: unr3-storyboard
description: Chuyển kịch bản thành hai file prompt tiếng Anh, một prompt ảnh storyboard có chú thích từng ô shot và một prompt video điện ảnh nhiều shot có timeline tổng đúng 8 giây. Dùng khi muốn diễn hoạt nhiều ô storyboard trong một clip; mỗi prompt nằm trên một dòng.
---

# unr3-storyboard — Kịch bản → Storyboard + video điện ảnh

Đọc kịch bản người dùng đưa, giữ nội dung và thứ tự kể chuyện. Tạo `image_prompts.md` và `video_prompts.md`. Mỗi cặp dòng tạo một ảnh storyboard tham chiếu và một clip Veo 3.1 dài đúng 8 giây, khung hình 16:9. Chỉ viết prompt, không tự gọi công cụ tạo ảnh/video.

## Input và chia storyboard
- Nhận kịch bản tiếng Việt hoặc ngôn ngữ khác, có hoặc không có STYLE ANCHOR, SHOT hay timestamp. Không bắt người dùng chuyển sang mẫu của unr3-writing.
- Trích bối cảnh, nhân vật, phục trang, đạo cụ, diễn biến và phong cách. Nếu thiếu chỉ dẫn mỹ thuật, đề xuất nhất quán theo nội dung, ghi giả định ngắn ngoài hai file; chỉ hỏi khi thiếu thông tin cốt truyện quan trọng hoặc có mâu thuẫn ảnh hưởng kết quả.
- Ưu tiên cách chia storyboard và số ô người dùng đã chỉ định. Mặc định nhóm 2–4 shot liên tiếp có liên hệ thành một storyboard, chọn ít ô để đủ thời gian cảm nhận chuyển động. Không mặc định mỗi shot dài 8 giây.
- Với kịch bản văn xuôi, chia thành các khoảnh khắc nhìn thấy được. Có thể dùng nhiều cỡ cảnh cho một khoảnh khắc nhưng không thêm diễn biến mới. Nếu chỉ có một shot không thể chia hợp lý, dùng một ô 0.00–8.00s; không bịa shot để đủ lưới.
- Giữ mỗi shot nguồn trong một nhóm, đủ nội dung và đúng thứ tự; không bỏ hoặc lặp shot tại ranh giới các nhóm. Nhóm cuối có thể ít ô hơn. Nếu người dùng yêu cầu toàn bộ video chỉ 8 giây nhưng nội dung quá nhiều, hỏi ưu tiên nội dung trước khi rút gọn.
- Mỗi storyboard = một clip 8 giây; với B storyboard, tổng bộ video là B × 8 giây. Nêu B và tổng thời lượng ngoài các file. Không nhầm tổng thời lượng cả bộ với thời lượng mỗi dòng.

## Khớp theo dòng và format file
- Dòng k của `image_prompts.md` tương ứng duy nhất với dòng k của `video_prompts.md` và storyboard k; cả hai file có đúng B dòng.
- Mỗi prompt tiếng Anh là một dòng vật lý hoàn chỉnh, tự đứng độc lập. Không tiêu đề, bullet, số thứ tự đầu dòng, code fence hoặc dòng trống. Nhãn `Panel 1`, `Shot 1` và timestamp bên trong prompt được phép và cần thiết.
- Ghi UTF-8 và kết thúc file bằng newline. Mọi giải thích, bảng đối chiếu hoặc lưu ý nằm ngoài hai file. Không ghi đè file có sẵn của lượt khác; dùng thư mục đầu ra riêng khi cần.

## Prompt ảnh storyboard
- Mô tả một tấm storyboard điện ảnh có BỐ CỤC RÕ: ví dụ hai ô ngang hoặc lưới 2 × 2; xác định thứ tự đọc từ trái sang phải, trên xuống dưới. Mỗi ô là khung hình 16:9 riêng; cho phép tổng tấm ảnh dùng tỷ lệ phù hợp lưới và dải chú thích, không ép toàn tấm 16:9 khiến ô bị méo.
- Mỗi ô mô tả khung hình tĩnh của shot: chủ thể, trạng thái, địa điểm, cỡ cảnh, bố cục, tiêu cự, ánh sáng, màu và chiều sâu. Mọi chủ thể/đạo cụ video cần đều hiện diện ở ô tương ứng.
- Yêu cầu chú thích tiếng Anh ngắn, dễ đọc ở dải riêng dưới từng ô, ngoài khung hình: nhãn `Shot 1` và nội dung/cỡ cảnh/chuyển động dự kiến. Chú thích không thay thế mô tả đầy đủ trong prompt. Không có ô rỗng hoặc ô phụ.
- Lặp nhận diện nhân vật, phục trang, motif, bảng màu và chất phim trong từng dòng. Giữ nhất quán giữa các ô. Ảnh dạng khung phim photorealistic trừ khi kịch bản yêu cầu phong cách khác; không mặc định bản phác thảo chỉ vì gọi là storyboard.

## Prompt video theo các ô
- Nói rõ dùng ảnh storyboard làm tham chiếu cho chuỗi shot toàn màn hình, không quay toàn tấm storyboard, không split-screen và không tạo chuyển động bay trên các ô.
- Mỗi ô có đúng một đoạn timeline tương ứng theo thứ tự đọc, ví dụ `Shot 1 / Panel 1 [0.00–3.00s]: ...; Shot 2 / Panel 2 [3.00–8.00s]: ...`. Timeline đặt lại từ 0 ở mỗi dòng.
- Mỗi đoạn nêu lại chủ thể, bối cảnh, cỡ cảnh/ống kính khớp ô ảnh, một chuyển động máy quay có chủ đích và chuyển động chủ thể/môi trường vừa đủ. Không chỉ viết “animate panel 1”.
- Các khoảng thời gian phải liên tiếp, không chồng lấn, không có khoảng trống, bắt đầu 0.00s và kết thúc 8.00s; tổng đúng 8 giây. Chia không đều theo cảm xúc khi có lợi, ví dụ hai shot 3+5 giây hoặc ba shot 3+2+3 giây.
- Cho phép cắt giữa các shot đúng tại mốc đã chỉ định. Mặc định dùng clean cut hoặc match cut có động cơ; không morph giữa các ô, không thêm transition chiếm thời gian ngoài timeline. Không thêm cảnh hay nhân vật không có trong storyboard.
- Yêu cầu full-frame 16:9, `8s total`, `minimal ambient sound`, `no music or voiceover`, `no visible captions, panel labels, borders or storyboard grid`. Chú thích của ảnh không xuất hiện trong video.

## Chất điện ảnh
- Thiết kế diễn tiến cỡ cảnh có mục đích: establishing → medium → detail/reaction khi phù hợp câu chuyện, không áp mọi loại cảnh vào mọi clip.
- Dùng ánh sáng có nguồn hợp lý, tương phản có kiểm soát, chiều sâu tiền/trung/hậu cảnh, màu nhất quán và chuyển động có trọng lượng. Thể hiện bằng mô tả cụ thể thay vì chỉ thêm “cinematic, 8K, masterpiece”.
- Có thể đổi tiêu cự giữa các shot để kể chuyện, nhưng từng cặp ô ảnh/shot video phải cùng tiêu cự và phối cảnh. Giữ trục 180 độ, hướng nhìn/hướng chuyển động, vị trí đạo cụ và tính liên tục của hành động giữa các cú cắt.
- Giữ tông cảm xúc của kịch bản; với nội dung piano relax, dùng nhịp thong thả và chuyển động nhẹ, không thêm kịch tính hay cắt quá nhanh để cố làm điện ảnh.

## Ví dụ một cặp dòng
Ảnh (một dòng, chỉ nội dung dòng được ghi vào file):

Create a photorealistic cinematic storyboard with two panels arranged left to right, each panel a 16:9 film frame with a separate readable caption strip beneath it, a quiet Hanoi old-quarter cafe on an autumn morning, a young woman in a beige knit sweater, warm amber-brown grading, soft side window light, restrained contrast and fine 35mm film grain throughout; Panel 1: medium shot, 35mm lens, the woman seated at a wooden table with a steaming white coffee cup in front of her, window on her left and old street softly visible outside, caption below: "Shot 1 - Quiet arrival - Slow push-in"; Panel 2: close-up, 85mm lens, her right hand resting beside the same white coffee cup on the same table, beige sweater cuff visible, steam suspended in the side light, caption below: "Shot 2 - Warmth in small things - Gentle lateral slide"; exactly two panels, no extra frames.

Video (một dòng, chỉ nội dung dòng được ghi vào file):

Use the supplied two-panel storyboard as visual reference for sequential full-screen cinematic shots in reading order, a quiet Hanoi old-quarter cafe on an autumn morning, the same woman in a beige knit sweater and the same white coffee cup, warm amber-brown grading, soft window light from the left, restrained contrast and fine 35mm film grain throughout; Shot 1 / Panel 1 [0.00–3.00s]: medium shot with a 35mm lens, slow push-in toward the woman seated at the wooden table with the steaming cup in front of her, subtle breathing and drifting steam, old street softly visible through the window; clean cut at 3.00s, preserving screen direction; Shot 2 / Panel 2 [3.00–8.00s]: close-up with an 85mm lens, gentle lateral slide past her right hand resting beside the same cup, beige cuff visible and steam curling through the same side light; nostalgic quiet pacing, full-frame 16:9, 8s total, minimal ambient sound, no music or voiceover, no visible captions, panel labels, borders or storyboard grid, no morphing or extra shots.

## Tự kiểm trước khi giao
- Đếm số dòng thực tế: hai file bằng nhau, đúng B, không dòng trống hoặc prompt bị ngắt dòng.
- Với từng cặp dòng, số ô bằng số đoạn timeline; nhãn, thứ tự, chủ thể, đạo cụ, bố cục và tiêu cự tương ứng khớp nhau. Đối chiếu toàn bộ kịch bản nguồn, kể cả shot người dùng đã sửa.
- Tính các khoảng thời gian: độ dài dương, điểm cuối đoạn trước bằng điểm đầu đoạn sau, tổng 8 giây và đoạn cuối kết thúc 8.00s ở mọi dòng.
- Mọi ô có chú thích trong ảnh; video loại bỏ chú thích/lưới, có 16:9, 8s total và minimal ambient sound. Chuyển shot có chủ đích, giữ tính liên tục và cảm xúc.
- Giao hai file và báo số storyboard/clip, tổng thời lượng. Đây là prompt mô tả ý đồ; không tuyên bố đã tạo hoặc kiểm chứng chất lượng video khi chưa chạy mô hình.
