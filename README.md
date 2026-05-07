
## Project Name: [Logistics Operations & Delivery Performance Analytics]

## Tech Stack: Power BI | DAX | Data Modeling | Excel/SQL

## Tóm tắt project 
Dự án phân tích transport & logistics của một doanh nghiệp vận chuyển tại Ấn Độ, từ xử lý làm sạch dữ liệu cho tới làm báo cáo dashboard. Dữ liệu được thu thập từ hơn 2000 phương tiện vận chuyển và hơn 1200 tài xế trong vòng hơn 1 năm (từ tháng 9/2019 đến 11/2020). Các trường dữ liệu phục vụ cho việc phân tích bao gồm: Thời gian, địa điểm của các chuyến vận chuyển; thông tin về phường tiên, tài xế; tọa độ, thời điểm các vị trí mà các chuyến hàng đi qua; bên cạnh đó là các loại hàng hóa và khách hàng. Từ đó đưa ra được insight và các quyết định hỗ trợ doanh nghiệp trong vận tải và vận chuyển. 

## Project Process:
Business Problem Statement -> Data Cleaning & Transformation -> Data Modeling -> DAX Calculation -> Data Visualization

### Business Problem Statement:
<img width="852" height="343" alt="image" src="https://github.com/user-attachments/assets/fc9d599c-f139-4683-850a-844c7bf47ade" />

Factors_affecting_transportation_fishbone_diagram

❓Business Questions: <br>
Theo dõi số lượng đơn hàng? Số lượng xe? Thời gian trễ hàng trung bình? Thời gian, quãng đưỡng trung bình cho đơn hàng? Thời gian dispatch trung bình là bao nhiêu?<br>
Tỉ lệ giao hàng đúng giờ (On-time Performance) hiện tại là bao nhiêu? Xu hướng này tăng hay giảm qua các Quý/Tháng?<br>
Bang nào (State) có sản lượng vận chuyển cao nhất? Bang nào là "điểm đen" về độ trễ cần được can thiệp ngay lập tức?<br>
Những tài xế nào có chỉ số On-time tốt nhất? Ai là những người thường xuyên gây trễ chuyến để có biện pháp xử lý?<br>
Loại phương tiện nào đang có hiệu suất vận hành tốt nhất trên các tuyến đường trọng điểm?<br>
Loại hàng hóa nào đang có thời gian tháo dỡ trung bình lâu nhất? Mối quan hệ giữa các loại hàng và thời gian trễ chuyến.

### Data Cleaning & Transformation: <br>
Xử lý Missing -> Xử lý Duplicate & Data Consistency -> Datetime Standardization -> Tính toán khoảng cách bằng công thức Haversine -> Custom Classification -> Data Quality Check

### Data Modeling
<img width="673" height="620" alt="image" src="https://github.com/user-attachments/assets/f7a7db15-9c7a-4aaa-aeaa-918aa1f9c67c" />
Project sử dụng Star Schema với 4 dim và 1 fact:<br>
Bảng Fact: Fact_Shipments<br>
- Chứa các dữ liệu định lượng (Measures) như: Delay_Minutes, Dispatch_time, Actual_shiptime.<br>
- Lưu trữ các khóa ngoại (Foreign Keys) để liên kết với các bảng chiều.<br>
Các bảng Dimension:<br>
- Dim_Date: Quản lý thời gian, cho phép phân tích theo Năm, Tháng, Ngày, Thứ trong tuần và các ngày lễ/Flashsale.<br>
- Dim_Location: Chứa thông tin địa lý như Thành phố, Bang, Kinh độ/Vĩ độ để trực quan hóa trên Bản đồ.<br>
- Dim_Vehicle_Driver: Quản lý thông tin tài xế, loại phương tiện và mã đăng ký xe.<br>
- Dim_Partners_Materials: Chứa thông tin về khách hàng, nhà cung cấp GPS và các loại hàng hóa vận chuyển.<br>
  
### DAX Calculation <br>
3 nhóm chính để tối ưu hóa khả năng phân tích và trải nghiệm người dùng<br>
<img width="429" height="370" alt="image" src="https://github.com/user-attachments/assets/45868095-657a-4253-b67c-08cf64bd9cea" />

### Data Visualization
<img width="1411" height="788" alt="image" src="https://github.com/user-attachments/assets/52d1e420-f57f-4b3f-ab42-44d1e71043e7" />
- Các chỉ số KPI<br>
Với 1,685 bookings và 2,019 phương tiện, hệ thống đang vận hành ở quy mô khá lớn.<br>
Chỉ số Ontime Ratio chỉ đạt 30.4% cho thấy hơn 2/3 đơn hàng đang bị trễ. Đây là copn số đáng báo động ❗<br>
Thời gian giao hàng trung bình là 183 giờ (~7.6 ngày) và thời gian điều phối tại kho là 18 giờ. Đây là chỉ số cần được đào sâu hơn để hiểu xem nó tốt hay xấu.<br>
- Các biểu đồ đường <br>
Shipment Analysis với sản lượng có xu hướng tăng trưởng mạnh vào Q3 (vọt lên 1,309 đơn). Điều này có thể do tính thời vụ (mùa lễ hội hoặc mua sắm tại Ấn Độ).<br>
Tháng 6 có tỉ lệ đúng giờ thấp kỷ lục, trong khi tháng 8 đang có dấu hiệu cải thiện rõ rệt<br>
Dispatch Time Trend: Biểu đồ cho thấy sự biến động mạnh theo ngày nhưng nhìn chung đang ở mức "Stable" (ổn định). Tuy nhiên, có một vài ngày đỉnh điểm vọt lên mức 40, chỉ số này cần điều tra xem có sự cố gì vào những ngày đó không.<br>
- Map<br>
Tamil Nadu là "ngôi sao" của dự án với 510 đơn hàng (chiếm gần 1/3 tổng sản lượng). Ngược lại, Telangana chỉ có 2 đơn.<br>
💭 **Đề xuất:** Doanh nghiệp nên tập trung tối ưu quy trình tại Tamil Nadu trước để có tác động lớn nhất đến kết quả kinh doanh.<br>
- Các biểu đồ cột và tròn:<br>
Phương tiện Heavy Commercial (HCV) đang chiếm nhiều nhất.<br>
Shipment Type: Gần như 100% là đơn hàng Regular.<br>

<img width="1410" height="789" alt="image" src="https://github.com/user-attachments/assets/679d97b4-c994-4247-a820-42e5e409a63a" />
- Card Chart:<br>
Số lượng nhân sự: Hệ thống ghi nhận 1,231 tài xế phục vụ cho 1,685 chuyến hàng. Có nghĩa còn khoảng 900 phương tiện chưa được sử dụng. <br>
💭 **Đề xuất:** Tuyển và đào tạo thêm tài xế để tăng cường sử dụng hết các phương tiện đang có và mở rộng mạng lưới vận tải.<br>
Phân hóa hiệu suất: Biểu đồ Bar Chart cho thấy tài xế MURUGAN đang dẫn đầu với 20 chuyến hàng thành công. Việc sử dụng màu xanh lá (Green) cho những người đứng đầu giúp nhà quản lý nhận diện nhanh nhóm "Star Drivers".<br>
- Biểu đồ cột kết hợp đường (Performance by Provider): <br>
Nhà cung cấp Consent có sản lượng vận chuyển cao nhất vượt trội -> Là đối tác tin cậy.<br>
💭 **Đề xuất:** Ưu tiên hơn với những đối tác lớn như Comstar, Ashok Leyland về thủ tục, phương tiện, thời gian.
- Tree map chart:<br>
Sự chậm trễ đang ảnh hưởng trực tiếp đến các "ông lớn" trong ngành công nghiệp ô tô. Nếu không cải thiện tỉ lệ Ontime 30.4% (từ trang 1), doanh nghiệp có rủi ro cao bị mất các hợp đồng chiến lược này.<br>
💭 **Đề xuất:**  Có thể ưu tiên những đơn vận chuyển đối với các khách hàng lớn này, bằng cách ưu tiên những xe có tải trọng và hiệu suất tốt, tập trung nhiều nhân lực cho các đơn hàng này, giảm trừ các thủ tục quy trình nếu có thể nhằm giảm thời gian vận chuyển và lưu kho.<br>
- Decomposition tree:<br>
Biểu đồ tree cho thấy Đa số doanh nghiệp phục vụ chính cho chuỗi cung ứng linh kiện ô tô (một ngành yêu cầu tính thời điểm cực cao),<br>
💭**Đề xuất:** có thể xây dựng tự động hóa các thủ tục ưu tiên xuất kho và vận chuyển cho những mặt hàng này.<br>
Bên cạnh đó, ta thấy được 1 Insight khác: Trung tâm Ấn Độ (như Telangana, Madhya Pradesh) thường là các vùng nội địa, xa các cảng biển và cụm công nghiệp nặng, cùng với địa hình đồi núi gồ ghề không có nhiều đơn hàng thậm chí có những nơi không có đơn hàng nào. Trong khi đó Tamil Nadu lại là 1 bang có thế mạnh bậc nhất về sản xuất ô tô và cơ khí tại Ấn Độ, vì vậy cũng giải thích được vì sao nhiều đơn hàng lại xuất hiện tại bang này và ít xuất hiện tại Telengana.<br>
Linh kiện Ô tô (Auto Parts) đang chiếm nhiều trong chuỗi cung ứng của doanh nghiệp như biểu đồ Sankey cho thấy, thì dữ liệu này xác nhận rằng mạng lưới của doanh nghiệp đang tập trung ở các Hub sản xuất ven biển chứ không phải mạng lưới phân phối tiêu dùng toàn quốc. <br>
Mặt khác, một vùng đồi núi khác là Ultar predesh lại có nhiều đơn hàng và hiệu suất giao hàng cũng rất tốt, vì đây là bang lớn nhất Ấn Độ, đông dân cư và có cơ sở giao thông hạ tầng tốt nhất.<br>
💭 **Đề xuất:**: Có thể giảm tải 1 số địa điểm phân phối và trung chuyển tại khu vực nội địa và thuê Outsourcing cho 1 số điuạ điểm này. (Có thể sẽ tiết kiệm được chi phí, dữ liệu cần thu thập thêm thông tin về chi phí vận hành, hàng hóa,... để đưa ra quyết định tối ưu), tuy nhiên trong tương lai nếu giao thông phát triển, có thể cân nhắc đưa các tuyến đường về khu vực này để rút ngắn quãng đường).<br>


<img width="1405" height="784" alt="image" src="https://github.com/user-attachments/assets/71e92fe8-e20e-45ed-8ac6-46ffec138240" />

Sản lượng trung bình hàng ngày cao nhất rơi vào giai đoạn After Flash Sale, tuy nhiên thì không có sự chênh lệch quá nhiều, vì vậy tác động của flash sale là không đáng kể.<br>
Số lượng đơn hàng trung bình các ngày trong tuần cao hơn cuối tuần.<br>
Biểu đồ phân tán cho thấy một xu hướng chung: khi quãng đường tăng lên, số phút trễ cũng có xu hướng tăng theo.<br>
Các bang như Haryana và Assam đang được đánh dấu xanh lá cây đậm, cho thấy đây là những khu vực có hiệu suất điều phối hoặc vận chuyển đang ổn định hơn so với nhóm còn lại. Tuy nhiên để đưa ra quyết định nên đầu tư mạnh vào những nơi có hiệu suất tốt sẵn hay tập trung cải thiện những khu vực có hiệu suất kém thì cần dựa vào thêm 1 số thông tin về chi phí vận hành và lợi nhuận trên mỗi đơn hàng.<br>

### Compilation of proposals <br>
- Doanh nghiệp nên tập trung tối ưu quy trình tại Tamil Nadu trước để có tác động lớn nhất đến kết quả kinh doanh. <br>
- Tuyển và đào tạo thêm tài xế để tăng cường sử dụng hết các phương tiện đang có và mở rộng mạng lưới vận tải <br>
- Có thể ưu tiên những đơn vận chuyển đối với các khách hàng lớn này, bằng cách ưu tiên những xe có tải trọng và hiệu suất tốt, tập trung nhiều nhân lực cho các đơn hàng này, giảm trừ các thủ tục quy trình nếu có thể nhằm giảm thời gian vận chuyển và lưu kho<br>
- Có thể xây dựng tự động hóa hoặc ưu tiên xuất kho và vận chuyển cho những mặt hàng linh kiện ô tô<br>
- Ưu tiên hơn với những đối tác lớn như Comstar, Ashok Leyland.
- Có thể giảm tải 1 số địa điểm phân phối và trung chuyển tại khu vực nội địa và thuê Outsourcing cho 1 số điuạ điểm này. (Có thể sẽ tiết kiệm được chi phí, dữ liệu cần thu thập thêm thông tin về chi phí vận hành, hàng hóa,... để đưa ra quyết định tối ưu), tuy nhiên trong tương lai nếu giao thông phát triển, có thể cân nhắc đưa các tuyến đường về khu vực này để rút ngắn quãng đường)<br>




