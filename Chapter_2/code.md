Đọc ảnh và chuyển đổi ảnh sang dạng grayscale:

python

im = rgb2gray(imread('../image s/cameraman.jpg')).astype(float)
imread đọc ảnh từ đường dẫn '../image s/cameraman.jpg'.
rgb2gray chuyển đổi ảnh từ dạng màu RGB sang ảnh xám (grayscale) để giảm số kênh từ 3 xuống 1, giúp đơn giản hóa quá trình xử lý.
astype(float) chuyển giá trị của ảnh về dạng số thực để thuận tiện cho các phép toán.
In giá trị tối đa của ảnh và kích thước ảnh:

python
Sao chép mã
print(np.max(im)) # In ra 1.0
print(im.shape) # In ra (225, 225)
np.max(im) cho thấy giá trị lớn nhất trong ảnh là 1.0, nghĩa là ảnh đã được chuẩn hóa với các giá trị từ 0 đến 1.
im.shape cho thấy kích thước của ảnh là (225, 225) (chiều cao và chiều rộng 225 pixels).
Định nghĩa bộ lọc (kernel):

python
Sao chép mã
blur_box_kernel = np.ones((3,3)) / 9
edge_laplace_kernel = np.array([[0,1,0],[1,-4,1],[0,1,0]])
blur_box_kernel: Kernel làm mờ hộp 3x3, chia đều các giá trị trong kernel (mỗi ô có giá trị là
1
9
9
1
​
). Khi áp dụng, kernel này sẽ tính trung bình của các pixel xung quanh để làm mờ ảnh.
edge_laplace_kernel: Kernel Laplace cho phát hiện biên cạnh, với ma trận chứa các giá trị làm nổi bật sự khác biệt giữa một pixel và các pixel xung quanh. Điều này giúp tìm ra các biên cạnh trong ảnh.
Áp dụng phép tích chập (convolution):

python
Sao chép mã
im_blurred = signal.convolve2d(im, blur_box_kernel)
im_edges = np.clip(signal.convolve2d(im, edge_laplace_kernel), 0, 1)
signal.convolve2d(im, blur_box_kernel): Phép tích chập (convolution) được áp dụng với kernel làm mờ. Kết quả im_blurred là phiên bản làm mờ của ảnh ban đầu.
signal.convolve2d(im, edge_laplace_kernel): Tích chập với kernel Laplace để phát hiện biên cạnh. np.clip giới hạn giá trị của các pixel trong khoảng [0, 1] để đảm bảo ảnh sau khi xử lý không vượt ra ngoài dải sáng hợp lệ.
Hiển thị ảnh:

python
Sao chép mã
fig, axes = pylab.subplots(ncols=3, sharex=True, sharey=True, figsize=(18, 6))
pylab.subplots tạo một cửa sổ hiển thị với 3 cột.
sharex=True, sharey=True làm cho các trục x và y của các ảnh chia sẻ cùng tỷ lệ, giúp so sánh các ảnh dễ dàng hơn.
Thiết lập và hiển thị các ảnh trên từng ô:

python
Sao chép mã
axes[0].imshow(im, cmap=pylab.cm.gray)
axes[0].set_title('Original Image', size=20)
axes[1].imshow(im_blurred, cmap=pylab.cm.gray)
axes[1].set_title('Box Blur', size=20)
axes[2].imshow(im_edges, cmap=pylab.cm.gray)
axes[2].set_title('Laplace Edge Detection', size=20)
for ax in axes:
ax.axis('off')
pylab.show()
imshow hiển thị các ảnh với màu xám (cmap=pylab.cm.gray).
set_title đặt tiêu đề cho mỗi ảnh.
axis('off') ẩn trục tọa độ.
pylab.show() hiển thị tất cả các ảnh: ảnh gốc, ảnh làm mờ, và ảnh phát hiện biên cạnh.
Tóm tắt
Đoạn code này giúp minh họa cách áp dụng phép tích chập để xử lý ảnh, với hai phép biến đổi: làm mờ và phát hiện biên cạnh.
