---
layout: default
title: CƠ BẢN VỀ TENSORFLOW
---

Tensorflow (TF) là một thư viện mã nguồn mở phát triển bởi Google hoạt động trên nền tảng nhiều ngôn ngữ lập trình, đặc biệt thích hợp cho Machine Learning (ML) và Deep Learning (DL). Trong các ứng dụng ML/DL chủ yếu sử dụng TF với ngôn ngữ Python. TF cung cấp nhiều lớp, module và hàm ở những mức độ trừu tượng khác nhau hỗ trợ cho ML/DL, do vậy phát triển ML/DL trên TF sẽ rất nhanh chóng.

Trong phần đầu của bài viết này sẽ trình bày một số khái niệm cơ bản của TF ở mức độ trừu tượng thấp (Low level API). Để chạy một chương trình (tính toán) trong TF cần phải xây dựng một tf.Graph (luồng dữ liệu) thực hiện tf.Session (chạy luồng dữ liệu đó). Hai khái niệm này giúp cho TF có thể thực hiện một cách nhanh chóng thông qua tính toán phân tán (thực ra cũng chẳng cần quan tâm làm gì).
## tf.Graph()
 TF định nghĩa một sơ đồ luồng dữ liệu (tf.Graph) là một dãy các toán tử TF (Tensorflow operation) sắp xếp thành một sơ đồ (graph). Mỗi sơ đồ gồm có 2 đối tượng:
- tf.Operation (ops): Thể hiện bằng các node của sơ đồ, Operation thông thường là các phép toán trả về kết quả là tensor
- tf.Tensor: Là các cạnh của sơ đồ, thể hiện giá trị sẽ chạy qua sơ đồ dữ liệu. Tensor dịch ra tiếng Việt là khối dữ liệu (nhiều chiều). Trong TF thì số chiều của tensor gọi là rank
```
3. # a rank 0 tensor; a scalar with shape [],
[1., 2., 3.] # a rank 1 tensor; a vector with shape [3]
[[1., 2., 3.], [4., 5., 6.]] # a rank 2 tensor; a matrix with shape [2, 3]
[[[1., 2., 3.]], [[7., 8., 9.]]] # a rank 3 tensor with shape [2, 1, 3]
**Quy luật:** Đếm dấu ngoặc vuông suy ra rank, ví dụ [[[1., 2., 3.]], [[7., 8., 9.]]] có 3 dấu ngoặc vuông $\rarrow$ rank(3). 

Đếm số phần tử trong từng dấu ngoặc vuông suy ra số phần tử trong chiều (shape). Ví dụ [[[1., 2., 3.]], [[7., 8., 9.]]], dấu ngoặc vuông đầu tiên có 2 phần tử, dấu ngoặc thứ 2 có 1 phần tử, dấu ngoặc thứ 3 có 3 phần tử $rarrow$ shape (2,1,3)
```
Ví dụ: Grap như hình 1 trong TF sẽ thực hiện bằng các câu lệnh sau:
<img src="./images/bai-03/tfgraph.PNG"
align="middle">