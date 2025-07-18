## Lab 4 - Phân Vùng Ảnh

* Sinh viên thực hiện: Lê Hoài Phương
* MSSV: 207CT10264
* Môn học: Nhập môn Xử lý ảnh số
* Giảng viên: Đỗ Hữu Quân

## Giới thiệu

Bài Lab 4 này tập trung vào việc thực hiện các thao tác xử lý ảnh cơ bản trong lĩnh vực phân đoạn ảnh (Image Segmentation) và biến đổi hình học (Geometric Transformation). Các kỹ thuật này đóng vai trò quan trọng trong việc trích xuất thông tin, nhận dạng đối tượng và chuẩn bị dữ liệu ảnh cho các tác vụ phân tích chuyên sâu.

## Công nghệ sử dụng

* **Python:** Ngôn ngữ lập trình chính.
* **Pillow (PIL):** Để đọc và xử lý ảnh 
* **NumPy:** Xử lý dữ liệu ảnh dưới dạng mảng số hiệu quả.
* **OpenCV:** Thư viện mạnh mẽ cho các phép biến đổi hình học và phân đoạn ảnh (Otsu, Adaptive Thresholding, các hàm liên quan đến xoay, dịch chuyển).
* **Scikit-image :** Cung cấp các thuật toán xử lý ảnh, ví dụ 
* **Scipy :** Hỗ trợ các phép toán hình thái học
* **Matplotlib:** Để hiển thị ảnh trực quan các bước xử lý và kết quả.

## Chi tiết các Bài Tập & Công thức

Các bài tập được thực hiện trên ảnh "Đà Lạt" ('dalat.jpg'), với các vùng ảnh cụ thể được chọn để áp dụng các phép biến đổi.

## Chi tiết các Bài Tập & Công thức

Các bài tập được thực hiện trên ảnh "Đà Lạt" (giả định là `dalat.jpg`), với các vùng ảnh cụ thể được chọn để áp dụng các phép biến đổi.

### Bài 1: Phân vùng LangBiang - Dịch chuyển & Otsu Thresholding
* **Mục đích:** Tìm và tách vùng núi LangBiang trong ảnh.
* **Dịch chuyển vùng chọn:** Di chuyển vùng LangBiang sang phải 100 pixel.
    * **Cách làm:** Cộng thêm 100 vào vị trí ngang của mỗi điểm ảnh.
* **Phân vùng bằng Otsu:** Tự động chia vùng đã dịch chuyển thành hai phần (ví dụ: núi và trời) bằng cách tìm một ngưỡng sáng phù hợp nhất.
    * **Nguyên lý:** Thuật toán tự tìm điểm phân chia tốt nhất dựa trên độ sáng của ảnh.
* **Lưu ảnh:** `lang_biang.jpg`

### Bài 2: Phân vùng Hồ Xuân Hương - Xoay & Adaptive Thresholding
* **Mục đích:** Xoay một phần ảnh và làm rõ chi tiết bằng cách phân chia độ sáng cục bộ.
* **Xoay đối tượng:** Xoay vùng Hồ Xuân Hương một góc 45 độ quanh tâm của nó.
    * **Cách làm:** Dùng các phép tính toán để thay đổi vị trí điểm ảnh theo góc xoay.
* **Adaptive Thresholding:** Chia vùng ảnh đã xoay thành đen trắng, nhưng ngưỡng chia này tự động thay đổi theo từng khu vực nhỏ của ảnh, thay vì dùng một ngưỡng chung.
    * **Nguyên lý:** Mỗi vùng nhỏ trong ảnh sẽ có ngưỡng sáng riêng, giúp xử lý tốt ảnh thiếu sáng hoặc có vùng sáng không đều.
* **Lưu ảnh:** `ho_xuan_huong.jpg`

### Bài 3: Phân vùng Quảng trường Lâm Viên - Coordinate Mapping & Binary Closing
* **Mục đích:** Chọn một vùng cụ thể và làm mịn ranh giới của nó.
* **Coordinate Mapping:** Tạo một "bản đồ" (mask) chỉ ra vị trí chính xác của Quảng trường Lâm Viên trên ảnh. Các điểm thuộc vùng này được đánh dấu, còn lại thì không.
    * **Nguyên lý:** Dùng tọa độ để tạo một vùng trắng trên nền đen.
* **Binary Closing:** Làm đầy các lỗ nhỏ hoặc nối các phần bị đứt của vùng đã chọn.
    * **Nguyên lý:** Là sự kết hợp của giãn nở (làm phình to) và co hẹp (làm thu nhỏ) để đóng các khoảng trống.
* **Lưu ảnh:** `quan_truong_lam_vien.jpg`

### Bài 4: Tạo Menu tương tác
* **Mục đích:** Cho phép người dùng dễ dàng chọn và thử các chức năng xử lý ảnh khác nhau.
* **Menu:** Hiển thị danh sách các phép biến đổi hình học (như dịch chuyển, xoay, co giãn, chọn vùng) và các phép phân đoạn (như Otsu, ngưỡng thích nghi, làm phình, làm co).
* **Lựa chọn:** Người dùng có thể chọn một chức năng riêng lẻ hoặc kết hợp một phép biến đổi hình học với một phép phân đoạn.
* **Hiển thị:** Kết quả của mỗi phép xử lý sẽ được hiển thị trên màn hình.

   ## Hướng dẫn sử dụng

### 1. Cài đặt môi trường
pip install opencv-python

### 2. Chạy Notebook
Mở Jupyter Notebook (hoặc JupyterLab, VSCode với extension Jupyter) từ thư mục chứa file main.ipynb.

Chạy từng cell trong notebook để xem từng bước xử lý và kết quả của các thuật toán.

Đối với Bài 4 (Menu tương tác), bạn sẽ cần chạy cell chứa hàm main() và làm theo hướng dẫn trên cửa sổ console/output của notebook.

### 3. Tùy chỉnh tham số
Bạn có thể thay đổi các giá trị tham số trong các cell tương ứng (ví dụ: góc xoay, hệ số co giãn, số lần lặp cho các phép toán hình thái học, block size và C value cho Adaptive Thresholding) để quan sát tác động khác nhau lên ảnh.
