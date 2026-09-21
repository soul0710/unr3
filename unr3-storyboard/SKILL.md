---
name: unr3-storyboard
description: Chuyển mỗi shot tổng trong kịch bản thành một ảnh storyboard chứa nhiều shot nhỏ có chú thích và một prompt video điện ảnh 8 giây với camera chậm, êm, phù hợp video relaxing. Tổng thời lượng các shot nhỏ trong mỗi ảnh đúng 8 giây; xuất hai file prompt tiếng Anh, mỗi prompt một dòng.
---

# unr3-storyboard — Kịch bản → Storyboard + video điện ảnh

Đọc kịch bản người dùng đưa, giữ nội dung và thứ tự kể chuyện. Tạo `image_prompts.md` và `video_prompts.md`. Mỗi cặp dòng tạo một ảnh storyboard tham chiếu và một clip Veo 3.1 dài đúng 8 giây, khung hình 16:9. Chỉ viết prompt, không tự gọi công cụ tạo ảnh/video.

## Input và phân cấp shot
- Nhận kịch bản tiếng Việt hoặc ngôn ngữ khác, có hoặc không có STYLE ANCHOR, SHOT hay timestamp. Không bắt người dùng chuyển sang mẫu của unr3-writing.
- Trích bối cảnh, nhân vật, phục trang, đạo cụ, diễn biến và phong cách. Nếu thiếu chỉ dẫn mỹ thuật, đề xuất nhất quán theo nội dung, ghi giả định ngắn ngoài hai file; chỉ hỏi khi thiếu thông tin cốt truyện quan trọng hoặc có mâu thuẫn ảnh hưởng kết quả.
- Phân biệt SHOT TỔNG (shot nguồn trong kịch bản) và SHOT NHỎ (ô hình bên trong ảnh storyboard). Mỗi shot tổng tạo đúng một ảnh storyboard và một clip dài 8 giây. Tuyệt đối không gom nhiều shot tổng thành một ảnh.
- Chia nội dung của từng shot tổng thành 2–3 shot nhỏ mặc định; chỉ dùng 4 khi nội dung thật sự cần và mỗi shot nhỏ vẫn có ít nhất 2 giây. Các shot nhỏ là các góc máy/cỡ cảnh/chi tiết bổ trợ của cùng shot tổng, không phải các shot tổng kế tiếp trong kịch bản. Nếu người dùng yêu cầu hơn 4 panel trong 8 giây, giải thích rằng nhịp cắt sẽ không còn relaxing và hỏi họ chọn giảm panel hay chấp nhận nhịp nhanh hơn.
- Nhận các mục SHOT trong kịch bản là shot tổng. Với văn xuôi chưa chia shot, xác định các đơn vị cảnh/khoảnh khắc làm shot tổng trước, rồi mới chia shot nhỏ trong từng đơn vị; nêu cách chia ngoài hai file. Dùng nhiều cỡ cảnh của cùng khoảnh khắc để có nhiều ô mà không thêm diễn biến mới. Nếu nội dung không đủ để chia hợp lý, hỏi làm rõ thay vì tự gộp shot tổng hoặc xuất storyboard một ô.
- Giữ ánh xạ một-một và thứ tự: SHOT tổng k → ảnh storyboard k → clip k. Không bỏ, lặp, gộp hay tách một shot tổng thành nhiều ảnh. Nếu shot nguồn quá dài/phức tạp để thể hiện trong 8 giây hoặc có thời lượng tường minh mâu thuẫn, hỏi cách rút gọn trước khi tạo prompt.
- Với N shot tổng, xuất N ảnh storyboard và N clip, tổng bộ video là N × 8 giây. Tổng thời lượng các shot nhỏ TRONG TỪNG ẢNH đúng 8 giây; không phải mỗi shot nhỏ 8 giây. Ví dụ 6 shot tổng → 6 dòng ảnh + 6 dòng video → 48 giây, dù mỗi ảnh có 2, 3 hay 4 ô.

## Khớp theo dòng và format file
- Dòng k của `image_prompts.md` ⇄ dòng k của `video_prompts.md` ⇄ SHOT tổng k. Cả hai file có đúng N dòng bằng số shot tổng, không bằng số shot nhỏ.
- Mỗi prompt tiếng Anh là một dòng vật lý hoàn chỉnh, tự đứng độc lập. Không tiêu đề, bullet, số thứ tự đầu dòng, code fence hoặc dòng trống. Nhãn `Panel 1`, `Subshot 1` và timestamp bên trong prompt được phép và cần thiết.
- Ghi UTF-8 và kết thúc file bằng newline. Mọi giải thích, bảng đối chiếu hoặc lưu ý nằm ngoài hai file. Không ghi đè file có sẵn của lượt khác; dùng thư mục đầu ra riêng khi cần.

## Prompt ảnh storyboard
- Mô tả một tấm storyboard điện ảnh có BỐ CỤC RÕ: ví dụ hai ô ngang hoặc lưới 2 × 2; xác định thứ tự đọc từ trái sang phải, trên xuống dưới. Mỗi ô là khung hình 16:9 riêng; cho phép tổng tấm ảnh dùng tỷ lệ phù hợp lưới và dải chú thích, không ép toàn tấm 16:9 khiến ô bị méo.
- Mỗi ô mô tả khung hình tĩnh của một shot nhỏ thuộc cùng shot tổng: chủ thể, trạng thái, địa điểm, cỡ cảnh, bố cục, tiêu cự, ánh sáng, màu và chiều sâu. Mọi chủ thể/đạo cụ video cần đều hiện diện ở ô tương ứng.
- Yêu cầu chú thích tiếng Anh ngắn, dễ đọc ở dải riêng dưới từng ô, ngoài khung hình: nhãn `Subshot 1` và nội dung/cỡ cảnh/chuyển động dự kiến. Chú thích không thay thế mô tả đầy đủ trong prompt. Không có ô rỗng hoặc ô phụ.
- Lặp nhận diện nhân vật, phục trang, motif, bảng màu và chất phim trong từng dòng. Giữ nhất quán giữa các ô. Ảnh dạng khung phim photorealistic trừ khi kịch bản yêu cầu phong cách khác; không mặc định bản phác thảo chỉ vì gọi là storyboard.

## Prompt video theo các ô
- Nói rõ dùng ảnh storyboard làm tham chiếu cho chuỗi shot toàn màn hình, không quay toàn tấm storyboard, không split-screen và không tạo chuyển động bay trên các ô.
- Mỗi ô có đúng một đoạn timeline tương ứng theo thứ tự đọc, ví dụ `Subshot 1 / Panel 1 [0.00–3.00s]: ...; Subshot 2 / Panel 2 [3.00–8.00s]: ...`. Timeline đặt lại từ 0 ở mỗi dòng.
- Mỗi đoạn nêu lại chủ thể, bối cảnh, cỡ cảnh/ống kính khớp ô ảnh, đúng một chuyển động máy quay chậm có chủ đích và chuyển động chủ thể/môi trường vừa đủ. Không chỉ viết “animate panel 1”.
- Các khoảng thời gian phải liên tiếp, không chồng lấn, không có khoảng trống, bắt đầu 0.00s và kết thúc 8.00s; tổng đúng 8 giây. Chia không đều theo cảm xúc khi có lợi, ví dụ hai shot 3+5 giây hoặc ba shot 3+2+3 giây.
- Cắt giữa các shot đúng tại mốc đã chỉ định, tại điểm chuyển động đã giảm tốc hoặc tạm nghỉ. Dùng clean cut/match cut nhẹ có động cơ; không whip transition, không morph giữa các ô, không thêm transition chiếm thời gian ngoài timeline. Không thêm cảnh hay nhân vật không có trong storyboard.
- Yêu cầu full-frame 16:9, `8s total`, `minimal ambient sound`, `no music or voiceover`, `no visible captions, panel labels, borders or storyboard grid`. Chú thích của ảnh không xuất hiện trong video.

## Chất điện ảnh
- Thiết kế diễn tiến cỡ cảnh có mục đích: establishing → medium → detail/reaction khi phù hợp câu chuyện, không áp mọi loại cảnh vào mọi clip.
- Dùng ánh sáng có nguồn hợp lý, tương phản có kiểm soát, chiều sâu tiền/trung/hậu cảnh, màu nhất quán và chuyển động có trọng lượng. Thể hiện bằng mô tả cụ thể thay vì chỉ thêm “cinematic, 8K, masterpiece”.
- Có thể đổi tiêu cự giữa các shot để kể chuyện, nhưng từng cặp ô ảnh/shot video phải cùng tiêu cự và phối cảnh. Giữ trục 180 độ, hướng nhìn/hướng chuyển động, vị trí đạo cụ và tính liên tục của hành động giữa các cú cắt.
- Giữ tông cảm xúc của kịch bản; với nội dung piano relax, dùng nhịp thong thả và chuyển động nhẹ, không thêm kịch tính hay cắt quá nhanh để cố làm điện ảnh.

## Ví dụ một cặp dòng
Một SHOT tổng nguồn: cô gái ngồi bên tách cà phê ở quán phố cổ Hà Nội. Một ảnh chia hai shot nhỏ: trung cảnh cô gái và cận cảnh tay cạnh tách. Video tương ứng dài 3 + 5 = 8 giây. Đây không phải ghép hai shot tổng.

Ảnh (một dòng, chỉ nội dung dòng được ghi vào file):

Create a photorealistic cinematic storyboard with two panels arranged left to right, each panel a 16:9 film frame with an opaque white caption strip beneath it, large bold black sans-serif text, generous padding, crisp readable lettering, exact captions, no tiny or overlapping text, a quiet Hanoi old-quarter cafe on an autumn morning, a young woman in a beige knit sweater, warm amber-brown grading, soft side window light, restrained contrast and fine 35mm film grain throughout; Panel 1: medium shot, 35mm lens, the woman seated at a wooden table with a steaming white coffee cup in front of her, window on her left and old street softly visible outside, caption below: "Subshot 1 - Quiet coffee moment"; Panel 2: close-up, 85mm lens, her right hand resting beside the same white coffee cup on the same table, beige sweater cuff visible, steam suspended in the side light, caption below: "Subshot 2 - Hand beside cup"; exactly two panels, no extra frames.

Video (một dòng, chỉ nội dung dòng được ghi vào file):

Use the supplied two-panel storyboard as visual reference for sequential full-screen cinematic shots in reading order, a quiet Hanoi old-quarter cafe on an autumn morning, the same woman in a beige knit sweater and the same white coffee cup, warm amber-brown grading, soft window light from the left, restrained contrast and fine 35mm film grain throughout; Subshot 1 / Panel 1 [0.00–3.00s]: medium shot with a 35mm lens, very slow push-in toward the woman seated at the wooden table with the steaming cup in front of her, subtle breathing and drifting steam, old street softly visible through the window, camera gently easing to a near stop before the cut; soft match cut at 3.00s, preserving screen direction and visual rhythm; Subshot 2 / Panel 2 [3.00–8.00s]: close-up with an 85mm lens, very slow lateral slide in the same screen direction past her right hand resting beside the same cup, beige cuff visible and steam curling through the same side light, camera easing out at the end to hand off calmly to the next parent shot; nostalgic quiet pacing, full-frame 16:9, 8s total, minimal ambient sound, no music or voiceover, no visible captions, panel labels, borders or storyboard grid, no morphing, whip pan, fast zoom, handheld shake or extra shots.

## Nhịp camera relaxing giữa các shot
- Trong mỗi shot nhỏ, dùng đúng một chuyển động rất chậm và ổn định: locked-off với drift nhẹ, very slow push-in/pull-out, gentle pan/tilt, slow lateral slide hoặc subtle parallax. Chuyển động có ease-in/ease-out, không đổi tốc độ đột ngột.
- Giữa hai shot nhỏ liền kề, shot trước giảm tốc hoặc gần dừng trước điểm cắt; shot sau bắt đầu êm và ưu tiên tiếp tục cùng hướng chuyển động màn hình. Nếu đổi hướng hoặc đổi tiêu cự, dùng ánh nhìn, đạo cụ, hình khối hoặc chuyển động môi trường làm match point để cú cắt không gây giật.
- Giữa hai shot tổng liền kề, shot nhỏ cuối của clip k phải để lại một “camera handoff” cụ thể cho shot nhỏ đầu của clip k+1: cùng hướng pan/slide, cùng điểm nhìn, cùng motif, hoặc trạng thái tĩnh tương ứng. Prompt của cả hai dòng phải mô tả handoff này bằng chi tiết cụ thể, không chỉ ghi “smooth transition”.
- Giữ trục 180 độ, hướng nhìn, hướng di chuyển và vị trí đạo cụ qua mọi cú cắt. Không nhảy từ toàn cảnh sang cực cận, đổi bên trục hoặc đổi hướng máy đột ngột nếu không có shot trung gian/match point hợp lý.
- Cấm whip pan, crash zoom, snap zoom, fast orbit, handheld shake, dutch-angle swing, speed ramp, camera roll và chuyển động bay nhanh. Không dùng nhiều chuyển động máy trong cùng một shot nhỏ.
- Với video relaxing, ưu tiên 2–3 shot nhỏ trong 8 giây; mỗi shot đủ lâu để cảm nhận chuyển động và không cắt dồn. Camera phục vụ cảm xúc yên tĩnh, không phô diễn kỹ thuật.

## Mạch truyện và liên kết giữa các shot
- Toàn bộ kịch bản phải kể một câu chuyện có mở đầu, diễn tiến và kết thúc hợp lý. Mỗi shot đóng góp vào cùng hành trình/chủ đề cụ thể; cùng màu sắc hoặc cùng mood chưa đủ để tạo liên kết.
- Mỗi cặp shot tổng liền kề phải có cầu nối nhìn thấy được: hành động tiếp diễn, nguyên nhân–kết quả, ánh nhìn–đối tượng, di chuyển theo tuyến đường, hoặc một chi tiết dẫn sang diễn biến tiếp theo. Không chèn cảnh đẹp rời rạc chỉ để đủ số shot.
- Theo dõi trạng thái qua từng shot: vị trí, thời điểm, nhân vật, phục trang, đạo cụ đang ở đâu/trong tay ai, hướng nhìn, hướng di chuyển và cảm xúc. Đầu shot sau phải tương thích với cuối shot trước; thay đổi địa điểm/thời gian phải có dấu hiệu chuyển tiếp rõ.
- Với câu chuyện không có nhân vật, dùng tuyến khám phá không gian, biến chuyển ánh sáng/thời tiết hoặc motif có diễn tiến làm sợi dây dẫn chuyện; không chỉ ghép phong cảnh ngẫu nhiên.
- Áp dụng liên kết ở CẢ HAI CẤP: giữa shot tổng k và k+1, và giữa mọi shot nhỏ liền kề trong cùng ảnh. Shot nhỏ phải phát triển cùng khoảnh khắc/hành động của shot tổng, không phải tập hợp góc máy không liên quan.
- Shot nhỏ đầu thiết lập trạng thái được kế thừa từ clip trước; các shot nhỏ giữa phát triển hành động/chi tiết; shot nhỏ cuối để lại trạng thái nối được sang shot tổng kế tiếp. Với clip đầu/cuối, lần lượt thiết lập/khép lại câu chuyện.
- Lặp thông tin trạng thái cần thiết trong mỗi dòng prompt để nó tự đứng độc lập. Giữ hướng nhìn, trục máy, vị trí tay/đạo cụ và tiến trình hành động khi đổi cỡ cảnh; không để nhân vật hoặc đồ vật tự đổi trạng thái qua cú cắt.
- Nếu kịch bản nguồn thiếu cầu nối quan trọng, hỏi đúng phần thiếu trước khi xuất; không tự thêm diễn biến, gộp hoặc sắp lại shot tổng. Kiểm tra cả ranh giới giữa các ảnh và từng cặp ô trong ảnh, giữ tổng timeline của mỗi ảnh đúng 8 giây.

## Chữ và nhãn storyboard dễ nhận diện
- Mỗi prompt ảnh phải yêu cầu chữ in rõ, lớn, đậm, font sans-serif đơn giản; nhãn `Subshot 1`, `Subshot 2` nổi bật, thống nhất cách đặt ở mọi ô và mọi ảnh. Không dùng chữ viết tay, font trang trí, chữ mờ hoặc chữ quá nhỏ.
- Dùng dải chú thích nền trắng đục riêng dưới từng ô, chữ đen tương phản cao, chừa lề và khoảng cách đủ rộng. Không đè chữ lên cảnh, không cắt mất chữ; tăng diện tích dải chú thích thay vì thu nhỏ font.
- Ghi chính xác chuỗi chữ cần hiển thị trong dấu ngoặc kép. Mỗi ô chỉ dùng nhãn và 2–5 từ tiếng Anh mô tả hành động/chi tiết; mô tả máy quay dài để trong prompt, không nhồi lên ảnh.
- Ví dụ chỉ dẫn phải có trong dòng ảnh: `large bold black sans-serif text on opaque white caption strips, generous padding, crisp readable lettering, exact captions, no tiny or overlapping text`.
- Tự kiểm prompt có đủ chỉ dẫn đọc chữ và chú thích ngắn cho mọi ô. Nếu người dùng đưa ảnh storyboard đã tạo để kiểm tra, đọc thực tế từng nhãn/chú thích; chữ sai hoặc khó đọc cần sửa/rerender hoặc chèn chữ bằng công cụ dàn trang khi được yêu cầu. Không tuyên bố chữ đã đọc rõ chỉ dựa trên prompt. Video vẫn không hiển thị chữ, nhãn hoặc lưới storyboard.

## Tự kiểm trước khi giao
- Đếm số dòng thực tế: hai file bằng nhau, đúng N shot tổng, không dòng trống hoặc prompt bị ngắt dòng.
- Kiểm tra mỗi dòng chỉ triển khai một shot tổng nguồn, không gom các shot tổng. Với từng cặp dòng, số ô shot nhỏ bằng số đoạn timeline; nhãn, thứ tự, chủ thể, đạo cụ, bố cục và tiêu cự tương ứng khớp nhau. Đối chiếu toàn bộ kịch bản nguồn, kể cả shot người dùng đã sửa.
- Tính các khoảng thời gian: độ dài dương, điểm cuối đoạn trước bằng điểm đầu đoạn sau, tổng 8 giây và đoạn cuối kết thúc 8.00s ở mọi dòng.
- Kiểm tra camera từng shot nhỏ chỉ có một chuyển động chậm, có ease-in/ease-out; mọi ranh giới shot nhỏ và shot tổng đều có camera handoff cụ thể, không đổi hướng/cỡ cảnh gây giật và không có chuyển động bị cấm.
- Mọi ô có chú thích trong ảnh; video loại bỏ chú thích/lưới, có 16:9, 8s total và minimal ambient sound. Chuyển shot có chủ đích, giữ tính liên tục và cảm xúc.
- Giao hai file và báo số storyboard/clip, tổng thời lượng. Đây là prompt mô tả ý đồ; không tuyên bố đã tạo hoặc kiểm chứng chất lượng video khi chưa chạy mô hình.
