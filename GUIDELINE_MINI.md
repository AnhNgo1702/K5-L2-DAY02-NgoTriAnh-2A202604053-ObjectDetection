# Mini guideline — bài làm cá nhân

> Điền nội dung này trước khi bắt đầu gán nhãn. Giữ lại các quyết định sau khi self-QC.

## Định nghĩa lớp

| Lớp | Định nghĩa của bạn | Ví dụ/điểm phân biệt |
| --- | --- | --- |
| `car` |Xe con, sedan, SUV, taxi, xe bán tải (pickup) |Ví dụ: Toyota Vios, Hyundai Tucson, Ford Ranger, Toyota Fortuner. Phân biệt: Xe bán tải dù có thùng phía sau vẫn xếp vào car, không xếp vào truck. |
| `truck` |Xe tải chở hàng, xe đầu kéo |Ví dụ: Xe tải thùng chở hàng có cabin và thùng tách biệt rõ ràng, xe tải ben. Phân biệt: Thân hình lớn, chuyên chở hàng hóa cồng kềnh, không phải xe bán tải gia đình. |
| `bus` |Xe buýt, minibus chở khách |Ví dụ: Xe buýt đô thị lớn, xe khách 16 - 29 chỗ (Ford Transit, Hyundai Solati). Phân biệt: Chuyên dùng chở khách theo tuyến/hợp đồng, kích thước dài/lớn hơn xe van gia đình. |
| `van` |Xe van, minivan (chở hàng hoặc chở người) |Ví dụ: Xe van chở hàng nội đô, xe minivan gia đình cửa lùa. Phân biệt: Khác với xe buýt (bus) ở chỗ không chạy khách tuyến cố định/không phải xe khách lớn; khác với xe con (car) ở thiết kế thân xe dạng hình hộp (box-like). |

## Quy tắc chung

- Box bám sát vật thể nghĩa là: Khung bounding box phải ôm trọn các cạnh ngoài cùng của vật thể xe (bao gồm cả gương chiếu hậu nếu nằm trong phạm vi thân xe), không để khoảng trống thừa quá lớn và không được cắt vào các bộ phận chính của thân xe.
- Vật thể bị che khuất: Vẫn phải vẽ bounding box nếu phần thân xe còn lại đủ lớn để nhận diện rõ ràng loại phương tiện đó thuộc lớp nào dựa trên hình dáng cấu trúc.
- Vật thể bị cắt bởi rìa ảnh: Nếu xe bị cắt bởi biên của khung hình nhưng phần nhìn thấy vẫn đủ cấu trúc đặc trưng để phân loại, vẽ box bám theo phần hiển thị và mở rộng biên box chạm đúng viền cạnh ảnh.
- Vật thể rất nhỏ/mơ hồ: Nếu xe ở quá xa, mờ, vỡ hạt hoặc bị che khuất quá nặng dẫn đến việc không thể xác định chính xác thuộc lớp nào, hãy bỏ qua để tránh làm nhiễu nhãn huấn luyện của mô hình.

## Ghi lại quyết định cho ít nhất ba ca mơ hồ

| Ảnh | Tình huống | Quyết định cuối | Lý do theo schema |
| --- | --- | --- | --- |
| `drive_0012.jpg` |Xe bán tải (Pickup) có phần thùng chở hàng phía sau khá dài, thoạt nhìn dễ nhầm với xe tải nhẹ. |Gán lớp car (ID 0) |Theo schema bắt buộc của dự án, các dòng xe bán tải (pickup) dù chuyên chở hàng hóa nhẹ phía sau vẫn được quy định nằm trong nhóm car. |
| `drive_0025.jpg` |Xe minibus 16 chỗ đang đỗ sát lề đường, có kích thước lớn hơn xe con nhưng nhỏ hơn xe buýt đô thị. |Gán lớp bus (ID 2) |Thuộc nhóm minibus chuyên chở khách theo định nghĩa của lớp bus, không phải xe van chở hàng hóa hay xe con gia đình. |
| `drive_0041.jpg` |Xe van chở hàng cỡ nhỏ (như dạng van thùng kín đô thị) bị che khuất phần đầu xe, chỉ lộ phần thân và đuôi hộp. |Gán lớp van (ID 3) |Cấu trúc thân xe hình hộp (box-like) đặc trưng của dòng van chở hàng, phần nhìn thấy đủ để xác định không phải xe con sedan hay xe tải lớn (truck). |
