Hàm signal.convolve2d trong thư viện scipy.signal thực hiện phép tích chập hai chiều (2D convolution) giữa một ảnh đầu vào và một kernel (bộ lọc). Đây là kỹ thuật quan trọng trong xử lý ảnh và học sâu, giúp áp dụng các hiệu ứng như làm mờ, làm sắc nét, và phát hiện biên cạnh trên ảnh. Dưới đây là giải thích chi tiết về cách hàm signal.convolve2d hoạt động.

1. Ý tưởng cơ bản của Tích chập (Convolution)
   Tích chập là một phép toán giữa một ma trận ảnh đầu vào (ví dụ, ma trận kích thước
   𝑀
   ×
   𝑁
   M×N) và một ma trận kernel (có kích thước nhỏ hơn, ví dụ,
   𝑚
   ×
   𝑛
   m×n). Kernel có thể coi là một công cụ “quét” qua từng vùng nhỏ của ảnh và áp dụng một phép tính để tạo ra giá trị mới cho các điểm ảnh (pixels) của ảnh kết quả.

2. Cách thức hoạt động của signal.convolve2d
   Hàm signal.convolve2d hoạt động bằng cách dịch chuyển kernel qua toàn bộ ảnh và tính tích chập cho từng vùng của ảnh theo các bước sau:

Chọn một phần vùng của ảnh:

Tại mỗi vị trí của kernel trên ảnh, chọn một vùng con từ ảnh có kích thước giống với kernel.
Tính tích của các phần tử tương ứng và cộng tổng:

Nhân từng phần tử của kernel với từng phần tử tương ứng của vùng con trong ảnh.
Cộng tất cả các giá trị tích để được một giá trị duy nhất (tổng tích).
Lưu giá trị kết quả:

Lưu tổng tích vào vị trí tương ứng trong ảnh đầu ra.
Di chuyển kernel:

Di chuyển kernel đến vị trí kế tiếp trên ảnh và lặp lại các bước trên cho đến khi kernel đã đi hết toàn bộ ảnh. 3. Các Tham Số của signal.convolve2d
Hàm signal.convolve2d có các tham số quan trọng giúp tùy chỉnh quá trình tích chập, như:

python
Sao chép mã
signal.convolve2d(input, kernel, mode='full', boundary='fill', fillvalue=0)
input: Ảnh đầu vào (một ma trận 2D).
kernel: Kernel (hoặc bộ lọc) để áp dụng lên ảnh.
mode: Chế độ ảnh đầu ra, với ba tùy chọn chính:
'full': Trả về ảnh lớn nhất có thể khi tích chập, bao gồm cả các vùng rìa mà kernel không hoàn toàn nằm trong ảnh.
'same': Ảnh đầu ra có cùng kích thước với ảnh đầu vào, lấy trung tâm của kết quả tích chập.
'valid': Trả về các phần mà kernel nằm hoàn toàn trong ảnh, làm giảm kích thước ảnh đầu ra.
boundary: Cách xử lý rìa ngoài của ảnh (padding).
'fill': Điền giá trị fillvalue (thường là 0) ở ngoài ảnh.
'wrap': Quấn ảnh lại, đưa các pixel phía đối diện vào để lấp đầy rìa.
'symm': Dùng các pixel lân cận để điền vào rìa ngoài.
fillvalue: Giá trị điền vào vùng ngoài ảnh (mặc định là 0).
