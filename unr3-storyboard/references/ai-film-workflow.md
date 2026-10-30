# Quy trình ảnh → video từ hướng dẫn “7 trạm”

Đọc §1–2 trước khi lập prompt, §3 cho scene hoặc §4 cho storyboard, §5–7 khi kiểm và bàn giao.
Đây là bổ sung cho quy tắc đầu ra của skill, không thay đổi chúng hay cho phép tự tạo media.

## Nguồn và phạm vi

Chắt lọc từ video người dùng cung cấp “Phim AI đẹp không nhờ prompt thần chú — 7 trạm của creator
Trung Quốc”, dài 4:47.85, nhận ngày 30/10/2026. Đối chiếu chữ và phụ đề tại các khung hình đã xem;
không phải bản chép toàn bộ âm thanh. Mốc thời gian gần đúng. **[Video]** là điều quan sát được;
**[UNR3]** là cách áp dụng vào bộ skill. Ví dụ bên dưới được viết lại cho nhịp relaxing.
Các trích dẫn “hướng dẫn chính hãng” trong video chưa được kiểm chứng độc lập ở đây.
Đối chiếu bổ sung: file `*_2-transcription-report.txt` chỉ liệt kê 82 mục bị đánh dấu trong 95 dòng
phụ đề, không phải toàn bộ transcript. Dùng phần chữ đọc được để bổ sung khung cuối, cảnh ngắn và
cú pháp theo model; không xem timestamp là chính xác tuyệt đối hay tự khôi phục các dòng bị thiếu.
Chuẩn hóa lỗi nhận dạng rõ như Kling/Seedance, “trạm”, “giây”. Phần kiểm nguồn hãng giới hạn ở §5
được ghi riêng; không có nghĩa mọi lời trong video đã được hãng xác nhận.

| Trạm | Đoạn gần đúng | Áp dụng |
|---|---|---|
| Một câu: ai, muốn gì, vướng gì | 0:20–0:42 | Sợi dây câu chuyện trong bước writing |
| Viết bằng hình | 0:42–1:08 | Hành động/chi tiết quan sát được, không chỉ nhãn cảm xúc |
| Storyboard trước khi tạo | 1:08–1:40 | Kế hoạch từng SHOT, không tạo clip đẹp rời rạc |
| Chốt nhân vật | 1:40–2:25 | Nhận diện cố định và bộ ảnh tham chiếu |
| Image trước, video sau | 2:25–2:52 | Chốt khung đầu rồi mới diễn hoạt |
| Công thức prompt | 2:52–3:32 | Chủ thể, động tác, bối cảnh; bổ sung máy/ánh sáng/phong cách |
| Một chuyển động máy | 3:32–4:08 | Một cú máy cho scene, một cú cho mỗi shot nhỏ storyboard |
| Thử, sửa, dựng | 4:08–hết | Đổi một yếu tố mỗi lần, giữ bản đạt, âm nhạc ở hậu kỳ |

## 1. Câu chuyện và cảm xúc nhìn thấy được

**[Video]** Ý tưởng cần nhân vật, mong muốn, trở ngại; cảm xúc phải chuyển thành biểu hiện cơ thể
hoặc môi trường. **[UNR3]** Không ép trở ngại kịch tính vào chuyến dạo phố: một ý định nhỏ, một điểm
dừng hoặc sự thay đổi ánh sáng đủ tạo tiến trình. Không nhân vật thì dùng hành trình khám phá/motif.
Nguồn đã duyệt quyết định nội dung; bước prompt không được sáng tác thêm sự kiện để đủ công thức.

| Còn mơ hồ | Cụ thể hơn, nếu nguồn cho phép |
|---|---|
| Cô gái rất hoài niệm. | Cô ngồi nhìn chiếc ghế trống bên kia bàn, hai tay yên quanh cốc. |
| Phố đẹp, cinematic, masterpiece. | Nắng xiên qua mái hiên lên nền đá ẩm, một chiếc lá nằm cạnh bậc cửa. |
| Cô thư giãn rồi đứng lên đi dạo và quay về. | Một SHOT chỉ giữ khoảnh khắc cô ngồi bên cửa sổ, đầu xoay nhẹ ra phố. |

Chọn một biểu hiện đủ đọc, không gom nhiều động tác. Cảm xúc có thể còn là nhãn trong `Cảm xúc`,
nhưng prompt phải có vật, tư thế, ánh nhìn hoặc ánh sáng thể hiện nó. Không tự thêm buồn bã, phép thuật
hay hi sinh từ ví dụ robot trong video vào phim relax.

## 2. Khóa nhận diện và phân vai ảnh tham chiếu

**[Video]** Hồ sơ nhân vật nhiều góc giúp người làm giữ nhận diện; mô tả cố định được lặp qua cảnh.
**[UNR3]** Trích một cụm nhận diện từ nguồn: tên nếu có, tuổi/ngoại hình được xác lập, tóc, phục trang,
màu/chất liệu và điểm phân biệt. Dùng cùng cụm trong các dòng nhân vật xuất hiện; tên không thay thế
mô tả. Giữ cả bản dịch tiếng Anh ổn định. Không bắt cảnh cận tay phải nhìn thấy toàn thân hay mặt.

Phân biệt phần cố định với tư thế, biểu cảm, vị trí, độ ướt và đạo cụ đang cầm. Những phần sau thay đổi
theo câu chuyện và phải nối đúng; không sao chép trạng thái đầu mãi qua các cảnh. Thay trang phục theo
nguồn là một biến thể có chủ đích, không cớ tự thay khuôn mặt.

Nếu thiếu ảnh, vẫn xuất được prompt; trong lời bàn giao nêu ảnh cận mặt và ảnh toàn thân cần chuẩn bị
cho nhân vật lặp lại. Chỉ bổ sung góc nghiêng/sau khi cần. Không tự gọi tạo ảnh, không ghi “đã có ảnh”,
không bịa đường dẫn hoặc ID. Khi có ảnh thật, kiểm cùng mặt/tóc/tỷ lệ/trang phục trước khi dùng.

**Ngoại lệ có trong video khoảng 2:00–2:12:** riêng **Seedance 2.0**, video cảnh báo ảnh ghép nhiều
góc có thể bị hiểu thành nhiều người và đề xuất cận mặt + toàn thân. Phân biệt tấm thiết kế để người
xem với asset đưa vào model. Đây là lời khuyên theo phiên bản trong video, không phải lệnh cấm chung
cho character sheet, storyboard, Veo, Kling hoặc Vidu. Không áp giới hạn số ảnh của công cụ này sang
công cụ khác. Khi thực thi công cụ khác, kiểm tài liệu hiện hành; mặc định Veo 3.1 của skill vẫn giữ.

Với nhiều ảnh thực tế, nói rõ ảnh nào là nhân vật, bối cảnh, khung đầu hoặc storyboard. Ví dụ minh họa
`@Image1 = character`, `@Image2 = location` chỉ là sơ đồ vai trò; chỉ xuất token đúng khi công cụ
đích hỗ trợ và ảnh đã được gắn thật. Một dòng chỉ “same woman” hoặc ID nội bộ không tự đứng độc lập.

## 3. Scene: ảnh đầu là trạng thái trước hành động

**[Video]** Ảnh đã có bối cảnh thì video tập trung vào chuyển động. **[UNR3]** Đối chiếu trước khi viết:
`trạng thái đầu có thể vẽ → một cử chỉ nhỏ → trạng thái cuối nối sang SHOT sau`.

- Ảnh chốt chủ thể/tư thế tĩnh, vật trong tay/trên bàn, bố cục, ống kính, nguồn sáng, màu và chất phim.
- Video diễn hoạt đúng ảnh đó. Nhắc lại nhận diện, bối cảnh và STYLE ANCHOR đủ để dòng tự đứng độc lập,
  không thiết kế lại cảnh. Không nhồi lại mọi chi tiết nền nếu không phục vụ nhận diện hoặc chuyển động.
- Nếu ảnh đã cho tay cầm cốc thì video không yêu cầu với lấy cốc từ bàn nữa. Nếu cần đổi trạng thái đầu,
  sửa ảnh trước; không trông chờ video âm thầm sửa lỗi.
- Chốt ảnh bằng kiểm tra thực tế trước khi chạy I2V: đúng người, tay/đạo cụ, ánh sáng, khoảng trống máy.
  Chỉ có prompt thì đây là bước người dùng cần thực hiện, không tuyên bố ảnh đã được duyệt.

Ví dụ ảnh đầu, một dòng tiếng Anh (giả sử nguồn đã xác lập các chi tiết):

`Mai, a 25-year-old woman with short black hair wearing a blue cotton jacket, seated at a wooden table in a quiet Hanoi old-quarter cafe on an autumn morning, her right hand resting beside a white cup on the table, gaze toward the window, medium shot, 35mm lens, soft window light from the left, amber-brown palette, fine 35mm film grain, calm nostalgia, 16:9`

Video tương ứng, cùng trạng thái và một cử chỉ:

`Animate the supplied first frame: Mai, a 25-year-old woman with short black hair wearing a blue cotton jacket, seated beside the white cup at the wooden table in the quiet Hanoi old-quarter cafe on an autumn morning, her right hand remaining beside the cup as she turns her head slightly toward the window; one very slow constant-speed push-in with a 35mm lens, faint steam rising from the cup, steady soft window light from the left, amber-brown palette and fine 35mm film grain maintained, one continuous shot, constant camera speed from first to last frame, no easing, no acceleration or deceleration, minimal ambient sound, no music or voiceover, calm pacing, 8s, 16:9`

Prompt dở: “Beautiful cinematic woman, walk in, sit, pick up coffee, orbit and zoom.” Nó thiếu nhận diện,
gộp nhiều hành động và nhiều đường máy. Sửa bằng một khoảnh khắc đã có trong nguồn, không thêm động tác.

### Khung cuối tùy chọn: tương thích và có thể đi tới được

**[Video, mục 58–59 của report]** Video nhắc `Add End Frame` của Kling và cảnh báo khung đầu/cuối
khác quá dễ gây nhảy cảnh. Tên/vị trí nút là thông tin video kể, không bảo đảm giao diện hiện tại.
**[UNR3]** Chỉ dùng khung cuối khi người dùng cung cấp/yêu cầu và chế độ đích thực sự hỗ trợ. Không tự
tạo thêm file thứ ba, không coi ô cuối storyboard là asset end-frame đã được gắn vào công cụ.

- So cả hai ảnh về mặt/tóc/trang phục, địa điểm/hình học, giờ/thời tiết/nguồn sáng, vật trong tay,
  hướng nhìn, cỡ cảnh và đường camera. Trạng thái cuối phải đạt được từ đầu bằng hành động đã định
  trong thời gian clip. “Giống nhau” là cùng cảnh/nhận diện, không phải bắt hai ảnh giống từng pixel.
- Ví dụ hợp lý: cùng Mai áo xanh trong quán sáng ban ngày, đầu nhìn cốc → cuối nhìn cửa sổ, camera
  chỉ dịch một quãng nhỏ. Ví dụ xung đột: cuối là người khác, áo khác, quán ban đêm; không ép model
  biến hình để đạt ảnh cuối. Nêu điểm xung đột và cần sửa asset nào hoặc làm rõ chuyển cảnh có chủ đích.
- Dòng video nêu trạng thái đầu → một động tác → đích cuối, giữ đúng một lựa chọn máy. Clip relax
  không tự thêm cut hoặc đổi thời gian/địa điểm để dung hòa hai ảnh. Chuyển cảnh thật cần được xử lý
  ở kế hoạch shot; bước prompt không tự đổi sự kiện, số SHOT hoặc cổng duyệt nguồn.
- Không có ảnh cuối thì chỉ mô tả đích hành động; không bịa đường dẫn/ID hay khẳng định đã attach.
  Nếu sửa ảnh đầu/cuối, rà lại prompt video cùng dòng và đầu clip kế tiếp. Với clip loop do người
  dùng yêu cầu, đích trở lại trạng thái đầu là chủ đích riêng, không mặc định mọi clip phải loop.

## 4. Storyboard: tách kế hoạch thành các khung đầu, không tách câu chuyện

Lập kế hoạch mỗi SHOT tổng trước khi viết hai dòng prompt. Dùng nội bộ bảng ngắn nếu cần:
`SHOT tổng | panel/thời gian | trạng thái đầu → cuối | cỡ cảnh/ống kính | máy | sáng/màu | âm thanh | cầu nối`.
Không bắt tạo file thứ ba hoặc đưa bảng này vào hai file prompt. Số ô không làm tăng thời lượng clip.

- Một ảnh nhiều ô cho đúng một SHOT tổng; 2–3 shot nhỏ mặc định, tổng đúng 8 giây. Không gom nhiều SHOT
  tổng vào một tấm để “tiết kiệm”. Mỗi ô là khung đầu của đoạn video tương ứng, không phải kết quả cuối.
- Ví dụ kế hoạch 4+4 giây: ô 1 trung cảnh cô ngồi cạnh cốc, hơi nước nhẹ; ô 2 cận tay vẫn nằm cạnh cốc,
  cùng tay áo, mặt bàn và nguồn sáng. Không để cô nhấc cốc ở ô 1 rồi cốc lại nằm trên bàn ở ô 2.
- Mỗi shot nhỏ có một lựa chọn máy riêng. Đổi góc bằng cut đúng mốc; không yêu cầu cả clip là một cú máy.
  Camera rất chậm, tốc độ cố định trong từng đoạn; không easing để che điểm cắt.
- Storyboard là tham chiếu chuỗi góc quay, không phải toàn tấm cần quay/zoom. Video là từng cảnh toàn
  màn hình; không đưa lưới, viền, nhãn hoặc chú thích của storyboard vào video.
- Kiểm ánh sáng theo tọa độ không gian, không mặc định “trái màn hình” khi máy đã đổi góc. Giữ trạng thái
  đạo cụ, trục nhìn và màu nhận diện. Chú thích ảnh vẫn phải có, dễ đọc, đặt ngoài khung phim.

**[Video → UNR3]** Cột ánh sáng theo cảm xúc, âm thanh và trạng thái giúp theo dõi sản xuất. Nếu người
dùng cần theo dõi thật, báo trạng thái từng ảnh/clip trong trao đổi hoặc bảng họ đã dùng: planned,
generated, reviewed, accepted; không ghi accepted khi chỉ mới viết prompt. Khung 16:9 đã được quy định;
fps chỉ chốt ở công cụ xuất khi biết yêu cầu, không giả vờ rằng chữ “30fps/8K” điều khiển được render.

### Cảnh ngắn: không nhầm khuyến nghị với giới hạn model

**[Video, mục 34–35 của report]** Một hướng dẫn được video dẫn lại khuyên cảnh không quá 8 giây vì
nửa sau cảnh dài thường kém đi, mỗi cảnh một động tác chính. Đây là lời khuyên về khả năng kiểm soát,
không phải chứng minh mọi model chỉ tạo được 8 giây hoặc cảnh dài luôn hỏng.
**[UNR3]** 8 giây hiện là hợp đồng đầu ra của bộ skill; storyboard chia thời gian bên trong 8 giây,
không phải 8 giây cho mỗi ô. Nếu yêu cầu 16 giây liên tục, nêu mâu thuẫn để chọn giữ liên tục bằng
workflow hỗ trợ thời lượng đó hay chấp nhận hai clip 8 giây có cầu nối; không âm thầm chia/gom hoặc
rút ngắn. Nếu nguồn đã có hai SHOT tổng 8 giây thì giữ hai cặp dòng, tổng 16 giây. Thay thời lượng
đã thống nhất phải cập nhật kế hoạch, timeline, ảnh/video khớp dòng và kiểm lại nguồn; không thay
giới hạn kỹ thuật của model bằng con số rút ra từ video.

## 5. Công thức là lớp thông tin, không phải thần chú hoặc cú pháp chung

**[Video]** Kling được minh họa bằng chủ thể + chuyển động + bối cảnh, thêm máy quay; Seedance thêm
ánh sáng/phong cách/chất lượng; Hailuo có ví dụ lệnh máy trong ngoặc vuông.
**[UNR3]** Dùng các lớp để kiểm thông tin có thiếu không; ưu tiên điều nhìn thấy được hơn nhãn “epic,
masterpiece, 8K”. Không bê `[Push in]` của ví dụ Hailuo hoặc placeholder `@Image` sang Veo một cách máy móc.
Không thêm yếu tố đã trái STYLE ANCHOR để điền đủ công thức. “Chất lượng” nên được cụ thể hóa bằng bố cục,
độ rõ chi tiết cần thấy, ánh sáng và màu nhất quán; tên model không bảo đảm đầu ra đạt.

### Tách timeline dựng khỏi cú pháp gửi model

**[Video, mục 83–85 của report]** Seedance 2.0 được mô tả theo “cảnh 1, cảnh 2…” thay vì ép số giây;
Kling 4.0 theo mốc giây. Ghi đây là lời hướng dẫn video kể, không tự biến thành lệnh cấm timestamp
cho Seedance hay bảo đảm Kling hiểu mọi format. Giữ một kế hoạch nhịp/tổng thời lượng; diễn đạt theo
model/mode thực tế là lớp khác. Chữ trong prompt không thay thế thông số duration của công cụ.

| Đích thật sự được chọn | Cách diễn đạt minh họa, sau khi kiểm hướng dẫn đúng mode |
|---|---|
| Seedance 2.0 theo video | `Scene 1: medium shot, Mai seated beside the cup; Scene 2: closer view of the same pose.` Giữ lịch dựng riêng, đặt thời lượng qua control được hỗ trợ. |
| Kling 4.0 theo video | Mô tả beat bằng mốc/độ dài shot nếu mode hỗ trợ, ví dụ `0–4s` rồi `4–8s`; không giả rằng text tự ép kết quả chính xác. |
| Hailuo theo video | Lệnh máy trong ngoặc vuông chỉ dùng khi tài liệu mode xác nhận; không mang sang Veo. |
| UNR3 hiện tại, Veo 3.1 | Giữ hai file độc lập theo dòng và clip 8 giây; storyboard vẫn cần timeline khớp panel, từ 0 đến 8 giây. Không xóa timestamp chỉ vì lời khuyên cho Seedance. |

**[Đối chiếu hãng giới hạn, 30/10/2026]** Kling mô tả clip dài hơn và nhiều keyframe; Seedance mô tả
đầu ra nhiều shot. Hai trang không xác lập quy tắc cú pháp độc quyền mà video nêu:
[Kling guide](https://kling.ai/blog/kling-4-ai-video-model),
[Seedance launch](https://seed.bytedance.com/en/blog/official-launch-of-seedance-2-0/).
Khi đổi công cụ, kiểm mode/API và workflow đích trước. Không chỉ thay chữ “Veo” thành “Seedance/Kling”
trong prompt rồi gọi là tương thích, không tự bỏ timeline/nhãn/định dạng file của hợp đồng hiện tại.

## 6. Một lựa chọn máy cho từng cú quay liên tục

Scene: một cú cho cả 8 giây. Storyboard: một cú cho **mỗi shot nhỏ**, các cú có thể khác nhau khi nguồn
và cầu nối cho phép. Locked-off là lựa chọn đứng yên hợp lệ theo nhánh cho phép; không mô tả vừa tĩnh
vừa dolly. Với máy chuyển động, nêu hướng/đích và giữ tốc độ rất chậm không đổi. Không ghép pan + orbit
+ zoom hoặc đổi chiều giữa cú. Danh sách move trong video không mở quyền dùng fast orbit/whip/zoom
bị skill relaxing cấm. Các quy tắc camera, timing và handoff của SKILL.md vẫn được ưu tiên.

## 7. Thử và sửa có nguyên nhân, không thử vô hạn

**[Video]** Vài giây phim có thể cần nhiều lần thử; mỗi lượt đổi một yếu tố để biết điều gì hiệu quả,
rồi kết hợp lồng tiếng, hiệu ứng, nhạc và dựng. **[UNR3]** Nếu người dùng đưa kết quả để sửa:

1. Xem ảnh/video thực tế nếu công cụ cho phép; nêu một lỗi cụ thể theo dòng/SHOT/panel, phân biệt điều
   quan sát được với suy đoán. Chỉ có prompt thì chỉ kiểm ý đồ, không chấm chất lượng media.
2. Tìm nguyên nhân: mặt/trang phục/đạo cụ sai → sửa reference hoặc ảnh đầu; chuyển động lỗi dù ảnh đúng
   → giảm một hành động; đường máy lỗi → sửa hướng/quãng; nối sai → kiểm cả hai đầu cú cắt.
3. Giữ bản được chấp nhận, thay một yếu tố có quan hệ với lỗi, không đổi cả ánh sáng/áo/góc/động tác cùng
   lúc và không thêm chuỗi cấm chung để che lỗi dàn cảnh. Đổi chi tiết ảnh thì cập nhật cặp video và
   ranh giới liên quan; storyboard sửa một ô phải kiểm lại các ô kế cận, timeline vẫn đủ 8 giây.
4. Lưu phiên bản ngoài hai file có format cố định khi cần. Báo ngắn: lỗi quan sát → yếu tố đổi → điều
   phải giữ → cách kiểm lượt sau. Không tuyên bố đã rerender nếu chỉ mới sửa prompt.

Không tự sinh ảnh/video từ skill viết prompt; không suy “nhiều lần thử” thành ngân sách vô hạn. Nếu
được yêu cầu thực thi riêng, dùng giới hạn lượt/chi phí đã thống nhất; dừng khi đạt, hết giới hạn hoặc
cần quyết định mới. UNR3 vẫn giữ `minimal ambient sound`, `no music or voiceover`; piano, lời và hiệu
ứng dựng được xử lý hậu kỳ theo yêu cầu, không tự thêm vào âm thanh sinh của video.
