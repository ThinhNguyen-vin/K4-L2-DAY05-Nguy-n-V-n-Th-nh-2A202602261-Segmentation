# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên VLearn. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202602261 - Nguyễn Văn Thịnh
- Ngày / CVAT local: 17/09/2026 / CVAT local
- Công cụ đã dùng: Brush / Polygon / SAM2

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh VLearn đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | `easy_semantic.zip` | 3 / 3 | 20 |
| medium_instance | `medium_instance.zip` | 3 / 3 | 32 |
| hard_panoptic | `hard_panoptic.zip` | 2 / 2 | 30 |
| cp1_holes |  `cp1_holes.zip` | 1 / 1 | 3 |
| cp2_slice | `cp2_slice.zip` | 1 / 1 | 3 |
| cp5_occlusion | `cp5_occlusion.zip` | 1 / 1 | 3 |
| cp3_thin | `cp3_thin.zip` | 1 / 1 | 3 |
| cp4_curb | `cp4_curb.zip` | 1 / 1 | 3 |
| cp6_coverage | `cp6_coverage.zip` | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: ảnh 000000181542.jpg, chiếc ô tô màu trắng nằm ở nửa phải ảnh, phía sau một xe máy và gần mép đường.
- Class và quy tắc tôi dùng để chọn biên: class car; tôi bám theo phần thân xe thực sự nhìn thấy, gồm mui xe, kính, thân xe và phần bánh xe còn lộ ra. Tôi dừng mask tại mép tiếp xúc giữa xe với mặt đường, xe máy phía trước và các vật che khuất; không đoán thêm phần thân xe bị che và không lấy bóng đổ dưới xe vào mask.
- Nếu dùng gợi ý sau đó: tôi dùng SAM 2.1 Tiny để tạo gợi ý cho các object còn lại. Với các xe nằm gần nhau, gợi ý đôi lúc bị dính sang xe kế bên hoặc lấy thêm một phần mặt đường. Tôi giữ các vùng bám đúng biên thân xe, xóa phần tràn sang nền và tách riêng từng xe thành từng instance trước khi Save.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: task `medium_instance`, ảnh `000000181542.jpg`, vùng có các xe máy đứng sát nhau ở nửa phải ảnh.

- Lỗi thuộc loại: **biên / phủ vùng**.

- Bằng chứng tôi nhìn thấy: mask của một xe máy bị tràn ra ngoài đường bao của xe, lấy thêm một phần mặt đường và một vùng nhỏ thuộc xe nằm sát bên cạnh. Khi bật mask lên có thể thấy phần annotation không dừng ở mép bánh xe/thân xe mà tiếp tục phủ sang các pixel nền.

- Quy tắc và hành động sửa: mỗi vật phải là một instance riêng và mask chỉ bao phủ phần pixel thực sự thuộc object nhìn thấy. Tôi dùng công cụ chỉnh mask để xóa phần bị tràn xuống mặt đường và phần dính sang xe bên cạnh, sau đó kiểm tra lại biên quanh thân và bánh xe để đảm bảo hai xe không bị gộp chung.

- Sau sửa đã Save và export lại chưa? **Đã Save annotation sau khi sửa và export lại bản annotation cuối để dùng làm submission.**


Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): … / chưa có điểm. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1. `000000181542.jpg`, cụm xe máy ở nửa phải ảnh | Một xe máy bị che một phần có thể vẽ theo toàn bộ hình dạng ước đoán, hoặc chỉ vẽ phần đang nhìn thấy | Guideline yêu cầu mask theo phần object thực sự nhìn thấy, không suy đoán phần bị che khuất | Tôi chọn chỉ vẽ phần xe máy nhìn thấy và dừng mask tại mép vật đang che phía trước |
| 2. `000000181542.jpg`, khu vực gần giữa ảnh có người đứng sát xe máy | Có thể coi phần người và xe máy đang chạm nhau là một vùng liên tục, hoặc tách thành hai instance riêng | person và motorcycle là hai class khác nhau; ngay cả các object cùng class cũng phải tách instance nếu là các vật độc lập | Tôi tách người và xe máy thành hai instance riêng, chỉnh biên để mask của người không ăn sang xe |
| 3.`000000181542.jpg`, phần bánh xe sát mặt đường | Có thể lấy cả vùng tối/bóng ngay dưới bánh vào mask vì màu gần giống object, hoặc dừng mask ở mép bánh xe | Bóng đổ thuộc nền chứ không phải cấu trúc của object; biên mask cần bám theo pixel thực sự của vật thể | Tôi không lấy phần bóng đổ và vùng mặt đường vào mask; chỉ giữ phần bánh/thân xe mà tôi xác định thuộc object |
