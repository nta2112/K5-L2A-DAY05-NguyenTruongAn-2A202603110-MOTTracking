# Báo cáo cá nhân — Nguyễn Trường An (2A202603110)

Đoạn video: MOT17-09, 150 frame (frame 1–150), nguồn MOTChallenge, giấy phép CC BY-NC-SA 3.0.

## 0. Thông tin học viên

- Họ tên: Nguyễn Trường An
- MSSV: 2A202603110
- Mã đề (A/B/C): A
- Email: 26ai.annt5@vinuni.edu.vn
- Link repository: https://github.com/nta2112/K5-L2A-DAY05-NguyenTruongAn-2A202603110-MOTTracking
- Giờ bắt đầu: 16:15pm
- Giờ kết thúc: 19:00pm

## 1. Xem trước đoạn video (CP0)

Ghi **trước khi vẽ**, mỗi người một dòng.

| Mã | Frame xuất hiện | Frame cuối thấy được | Rẽ / dừng / đổi tốc độ ở frame | Bị che ở frame | Ghi chú |
|---|---|---|---|---|---|
| P1 |frame 1 | frame 149| frame 58| frame 39 | Người đàn ông áo đen trong cửa hàng|
| P2 | frame 61| frame 149|frame 97 |từ frame đầu đến frame 59 |Người phụ nữ áo trắng trong cửa hàng |
| P3 |frame 1 | frame 149|tốc độ đều, gần như ko đổi hay dừng lại ở mọi frame| frame đầu tiên|Người phụ nữ trung niên áo xanh lá cây bên ngoài |
| P4 | frame 1| frame 149|tốc độ đều, gần như ko đổi hay dừng lại ở mọi frame| ko bị che|Người đàn ông trung niên áo xanh dương bên ngoài |
| P5 | frame 21| frame 145| frame 143|frame 109 |Đứa trẻ bên cạnh mẹ |

## 2. Keyframe và thời gian (CP1, CP4)

Số keyframe lấy từ kết quả `src/check_submission.py`.


| Mã | Số keyframe | Keyframe ở frame | Số frame có mặt | Keyframe / 100 frame | Thời gian (phút) | Chỗ khó |
|---|---|---|---|---|---|---|
| P1 | 16 | `[0, 10, 20, 30, 40, 50, 60, 70, 80, 90, 100, 110, 120, 130, 140, 149]` | 150 | 10.7 | 20 | không |
| P2 | 6 | `[0, 10, 20, 30, 40, 140]` | 116 | 5.2 |20 | ko|
| P3 | 14 | `[0, 10, 20, 30, 50, 60, 70, 80, 90, 100, 110, 130, 140, 149]` | 140 | 10.0 | 30| không|
| P4 | 14 | `[20, 30, 40, 50, 60, 70, 80, 90, 100, 110, 120, 130, 140, 149]` | 130 | 10.8 | 15| đoạn đầu bị khuất chỉ còn phân nửa người, ko biết có nên gán ko|
| P5 | 9 | `[60, 70, 80, 90, 100, 110, 130, 140, 149]` | 90 | 10.0 | 15| không|
| **Tổng** | **59** | — | **626** | **9.4** |100 | |
Keyframe / 100 frame của cả bài = 59 ÷ 626 × 100 = 9.4.

Đặt keyframe nhiều nhất ở person 3 ( phụ nữ trung niên áo xanh) vì người này di chuyển liên tục.

## 3. Đoạn bị che (CP2)

Người bị che: `P2`

| Mốc | Frame |
|---|---:|
| Bắt đầu bị che một phần (bật `occluded`) |frame 27 |
| Mất hẳn (bật `outside`) |frame 38 |
| Hiện lại (tắt `outside`) |frame 52 |
| Thấy rõ trở lại (tắt `occluded`) | frame 54 |

- Thời gian khuất hẳn:  38-52frame = 0.47 giây.
- Quyết định: giữ cùng ID.
- Lý do (trả lời 3 câu: khuất bao lâu so với 60 frame, ngoại hình có khớp, chỗ hiện lại có đúng hướng và tốc độ): Đối tượng chỉ khuất hẳn trong 14 frame (từ frame 38 đến 52), ngắn hơn rất nhiều so với ngưỡng 60 frame, do đó không bị tính là ra khỏi khung hình hoàn toàn hay đối tượng mới. Khi xuất hiện trở lại ở frame 52–54, trang phục, tỷ lệ cơ thể và đặc điểm ngoại hình hoàn toàn khớp với đối tượng P2 trước khi bị che khuất. Vị trí xuất hiện lại tuân theo đúng quán tính di chuyển, hướng đi và vận tốc của P2 từ đoạn trước lúc bị che, không có sự xuất hiện bất thường ở vị trí khác.

Ảnh chụp màn hình:

![Trước khi che](report/individual/images/che_1_truoc.png)
![Giữa đoạn che, thấy cờ trên panel object](report/individual/images/che_2_giua.png)
![Sau khi hiện lại, cùng ID](report/individual/images/che_3_sau.png)

## 4. Tự review ID (CP3)

Lượt 1 theo người (đi ngược từ frame 149 về 0 trên CVAT), lượt 2 theo cảnh (nhảy 10 frame). Ít nhất 3 dòng; không có lỗi thì ghi một dòng "đã kiểm hai lượt, không lỗi".

Loại lỗi dùng đúng một trong 7 mã: `id_switch`, `fragmentation`, `lost`, `merge`, `false_track`, `drift`, `flag`.

| Frame | Mã người | Loại lỗi | Mô tả một câu | Phát hiện ở lượt | Đã sửa? |
|---:|---|---|---|---|---|
|mọi frame |1 |ko lỗi |Không phát sinh lỗi trong quá trình kiểm tra. |Cả 2 lượt | không|
|mọi frame | 2| ko lỗi|Không phát sinh lỗi trong quá trình kiểm tra. |Cả 2 lượt | không|
|mọi frame| 3|ko lỗi|Không phát sinh lỗi trong quá trình kiểm tra. |Cả 2 lượt | không|

Tổng hợp số lỗi theo loại:

| `id_switch` | `fragmentation` | `lost` | `merge` | `false_track` | `drift` | `flag` |
|---:|---:|---:|---:|---:|---:|---:|
|0 |0 |0 |0 | 0| 0| 0|

Đã kiểm hai lượt, không lỗi. Tuy nhiên giả sử có lỗi thì id_switch (hoặc merge / false_track) thường là dạng lỗi dễ chỉ nhìn thấy rõ hơn ở lượt 2  mà lượt 1 có thể bỏ sót. Ở lượt 1, ta theo dõi từng cá nhân xuyên suốt từ frame cuối về đầu, tập trung vào sự liên tục của một ID cụ thể nên dễ bị cuốn theo quỹ đạo của một đối tượng mà quên mất bối cảnh toàn cục xung quanh. Ở lượt 2, việc nhìn toàn bộ khung hình theo từng mốc thời gian giúp ta có cái nhìn tổng quan về không gian. Khi các đối tượng di chuyển gần nhau, giao cắt hoặc đổi chỗ cho nhau, góc nhìn toàn cảnh theo cảnh sẽ phơi bày rõ nhất các trường hợp bị nhầm ID.

## 5. File xuất và kết quả tự kiểm (CP4)

| Kiểm tra | Kết quả |
|---|---|
| Tên file MOT 1.1 | `NguyenTruongAn_mot.zip` |
| Tên file CVAT for video 1.1 | `NguyenTruongAn_cvat_video.zip` |
| Số track ID khác nhau trong `gt/gt.txt` (phải là 5) | 5 (Đạt) |
| Frame `outside` không có dòng trong `gt.txt` (đúng / sai) | đúng |
| Job đã completed trên CVAT máy cá nhân | Hoàn thành |

Dán phần tóm tắt in ra từ `src/check_submission.py`:

```
=== File MOT 1.1: NguyenTruongAn_mot.zip ===
  Số track ID: 5   |   Tổng số box: 626
  [OK]        Đúng 5 track ID.

  Track | Frame có mặt | Số frame | Đoạn vắng (outside)
      1 |   0–149      |      150 | -
      2 |   0–145      |      116 | 110–139
      3 |   0–149      |      140 | 40–49
      4 |  20–149      |      130 | -
      5 |  60–149      |       90 | -


=== File CVAT for video 1.1: NguyenTruongAn_cvat_video.zip ===

  Track | Nhãn   | Frame thấy | Keyframe | KF/100 frame | Frame occluded | Lần bật outside
      0 | person |        150 |       16 |         10.7 |              0 |               0
              Track 0: keyframe ở frame [0, 10, 20, 30, 40, 50, 60, 70, 80, 90, 100, 110, 120
      1 | person |        116 |        6 |          5.2 |              0 |               2
              Track 1: keyframe ở frame [0, 10, 20, 30, 40, 140]
      2 | person |        140 |       14 |         10.0 |              0 |               1
              Track 2: keyframe ở frame [0, 10, 20, 30, 50, 60, 70, 80, 90, 100, 110, 130, 140, 149]
      3 | person |        130 |       14 |         10.8 |              0 |               0
              Track 3: keyframe ở frame [20, 30, 40, 50, 60, 70, 80, 90, 100, 110, 120, 130, 140, 149]
      4 | person |         90 |        9 |         10.0 |              0 |               0
              Track 4: keyframe ở frame [60, 70, 80, 90, 100, 110, 130, 140, 149]

  Tổng: 59 keyframe / 626 frame có mặt = 9.4 keyframe / 100 frame
  [OK]        Đọc được 5 track từ annotations.xml.

=== Tóm tắt ===
  Lỗi: 0   |   Cảnh báo: 0
  Đạt. Dán phần tóm tắt này vào báo cáo mục 5.
```

## 6. Ba câu kết

1. Nếu được gán lại, bạn sẽ đặt keyframe khác ở đâu? Vì sao?

   Nếu được gán lại, tôi sẽ bổ sung thêm các keyframe dày hơn ở các đoạn đối tượng di chuyển nhanh, đổi hướng đột ngột. Việc tăng mật độ keyframe ở các đoạn chuyển động phức tạp sẽ giúp thuật toán nội suy (interpolation) bám sát đường đi của đối tượng hơn.

2. Có chỗ nào bạn không chắc "cùng ID hay ID mới"? Bạn đã quyết định và ghi chú thế nào?

   Có khoảng thời gian đối tượng P2 bị khuất ngắn. Lúc đó đã có phân vân nhỏ về việc liệu đây có phải người cũ hay một người mới xuất hiện từ góc khuất. Dựa trên việc thời gian khuất ngắn, vị trí xuất hiện trùng khớp với quán tính di chuyển và trang phục hoàn toàn tương đồng, tôi quyết định giữ cùng ID (P2) và đánh dấu thuộc tính outside trong khoảng thời gian bị khuất, không tạo track ID mới để đảm bảo tính liên tục.

3. Một lỗi ID trong job của bạn (nếu không còn sót, chọn lỗi đã sửa) có thể làm xe tự lái dự đoán sai chuyển động của người đó như thế nào? Lỗi đó ảnh hưởng MOTA hay IDF1 nhiều hơn?
   Ảnh hưởng đến xe tự lái: Nếu xảy ra lỗi nhầm ID (id_switch) hoặc đứt gãy track, hệ thống nhận diện trên xe tự lái sẽ xem như người đi bộ cũ biến mất và xuất hiện một người đi bộ hoàn toàn mới ở vị trí khác. Dẫn đến việc bộ lọc dự đoán hướng đi tính toán sai hướng di chuyển hoặc vận tốc tương đối, gây nguy cơ phanh gấp hoặc xử lý tình huống kém chính xác. Lỗi này ảnh hưởng nghiêm trọng đến IDF1 hơn so với MOTA. MOTA chủ yếu đo lường tổng thể sai số đếm box và lỗi đơn lẻ (false positive, false negative, id switch), trong khi IDF1 là chỉ số cốt lõi đánh giá độ nhất quán và duy trì ID dài hạn của đối tượng; bất kỳ lỗi nhầm ID nào cũng sẽ kéo sụt mạnh điểm IDF1.

   

## Bonus (nếu làm)

### B1 — Hai người đi sát

Hai người p3 và p4 đi sát nhau. Trường hợp này nên thêm keyframe dày hơn: Đặt keyframe ngay trước, trong và ngay sau khoảnh khắc hai người đi ngang qua hoặc tiếp xúc gần nhau để cố định chính xác biên dạng bounding box của từng người, không để khung bao bị lan sang người bên cạnh.

### B2 — So cách đặt keyframe

| Cách đặt | Số keyframe | Frame trôi nhất | Ghi chú |
|---|---:|---:|---|
| Đều mỗi 30 frame |5 | Frame 35–45, 95–105|Bỏ lỡ các chuyển động bất ngờ, box dễ bị trượt (drift) lệch khỏi đối tượng khi người có thay đổi nhỏ về dáng đi. |
| Theo chỗ đổi hướng |14 |Ít bị trôi |Bám sát được các bước ngoặt chuyển động, thuật toán nội suy chính xác hơn, giữ được tỷ lệ bounding box tốt nhất. |

### B3 — So với tracker có sẵn

| Frame | Mã người | Tracker làm gì | Nhãn của bạn | Giải thích (đoán rồi sửa / ghép IoU / box score thấp / ngoại hình) |
|---:|---|---|---|---|
| | | | | |
| | | | | |

## 7. Tài liệu tham khảo và công cụ AI đã dùng
Cvat, codex, slide
