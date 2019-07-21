---
layout: default
title: CƠ BẢN VỀ TENSORFLOW
---

Tensorflow (TF) là một thư viện mã nguồn mở phát triển bởi Google hoạt động trên nền tảng nhiều ngôn ngữ lập trình, đặc biệt thích hợp cho Machine Learning (ML) và Deep Learning (DL). Trong các ứng dụng ML/DL chủ yếu sử dụng TF với ngôn ngữ Python. TF cung cấp nhiều lớp, module và hàm ở những mức độ trừu tượng khác nhau hỗ trợ cho ML/DL, do vậy phát triển ML/DL trên TF sẽ rất nhanh chóng.

Trong phần đầu của bài viết này sẽ trình bày một số khái niệm cơ bản của TF ở mức độ trừu tượng thấp (Low level API). Để chạy một chương trình (tính toán) trong TF cần phải xây dựng một tf.Graph (luồng dữ liệu) thực hiện tf.Session (chạy luồng dữ liệu đó). Hai khái niệm này giúp cho TF có thể thực hiện một cách nhanh chóng thông qua tính toán phân tán (thực ra cũng chẳng cần quan tâm làm gì).
## tf.Graph()
TF định nghĩa một sơ đồ luồng dữ liệu (tf.Graph) là một dãy các toán tử TF (Tensorflow operation) sắp xếp thành một sơ đồ (graph). Mỗi sơ đồ gồm có 2 đối tượng:
- tf.Operation (ops): Thể hiện bằng các node của sơ đồ, Operation thông thường là các phép toán trả về kết quả là tensor.
- tf.Tensor: Là các cạnh (edge) của sơ đồ, thể hiện giá trị sẽ chạy qua sơ đồ dữ liệu. Tensor dịch ra tiếng Việt là khối dữ liệu (nhiều chiều). Trong TF thì số chiều của tensor gọi là rank.
```
    3 --> a rank 0 tensor; a scalar with shape [],
    [1., 2., 3.] --> a rank 1 tensor; a vector with shape [3]
    [[1., 2., 3.], [4., 5., 6.]] --> a rank 2 tensor; a matrix with shape [2, 3]
```
    **Quy luật:** Đếm dấu ngoặc vuông suy ra rank, ví dụ [[[1., 2., 3.]], [[7., 8., 9.]]] có 3 dấu ngoặc vuông $\Rightarrow$ rank(3). 

    Đếm số phần tử trong từng dấu ngoặc vuông suy ra số phần tử trong chiều (shape). Ví dụ [[[1., 2., 3.]], [[7., 8., 9.]]], dấu ngoặc vuông đầu tiên có 2 phần tử, dấu ngoặc thứ 2 có 1 phần tử, dấu ngoặc thứ 3 có 3 phần tử $\Rightarrow$ shape (2,1,3)

**Ví dụ:** Graph như hình 1 trong TF sẽ thực hiện bằng các câu lệnh sau:

```python
a = tf.constant(2, name='a') # Kiểu dữ liệu tự động suy ra từ giá trị constant
b = tf.constant(3, name = 'b')
c = tf.constant(4, name ='c')
x = tf.add(a, b)
y = tf.multiply(x,c)
print(a)
print(x)
print(y)
```

<div class="imgcap">
 <img src ="/images/bai-03/tfgraph.PNG" align = "center">
 <div class = "thecap">Hình 1. tf.grahp()</div>
</div>

Trên graph ở Hình 1 thì các node là Operation (x: Add, y: Multiply, cả a, b,c: Constant nữa), còn cạnh là tensor (nhìn kỹ có chữ scalar). Khi chạy chương trình trên chỉ in ra tên, số chiều (shape) và loại (dtype) dữ liệu của các tensor mà chưa cho ra giá trị của phép tính.
```python
Tensor("a_7:0", shape=(), dtype=int32)
Tensor("Add_7:0", shape=(), dtype=int32)
Tensor("Mul_7:0", shape=(), dtype=int32)
```
 Muốn thực thi chương trình trên thì cần phải tạo một runtime cho nó
## tf.Session()
Có hai cách tạo Session (chọn 1 trong 2 cách). Có thể hiểu ```tf.Gphaph()``` giống như là tạo ra một file mã nguồn (```.py```) và ```tf.Session()``` là chạy mã nguồn đó.

```python
sess = tf.Session()
print(sess.run(a))
print(sess.run(x))
print(sess.run(y))
sess.close()

'''Cách này tự động close session'''
with tf.Session() as sess:
    print(sess.run(a))
    print(sess.run(x))
    print(sess.run(y))
```

Sẽ cho ra kết quả:

```python
2
5
20
```
## Placeholder và Variable
Khi muốn thay đổi các giá trị truyền vào graph, thay vì cứ sủ dụng một giá trị không đổi (constant) như ở trên thì sử dụng ```tf.placehoder```; khi truyền giá trị vào placeholder thì dùng phương thức ```feed_dict```. Placeholder thường dùng để chứa train/validation/test data. Ví dụ:

```python
x = tf.placeholder(tf.float32) # Có thể khởi tạo name, dtype
y = tf.placeholder(tf.float32)
z = x + y
with tf.Session() as sess:
    print(sess.run(z, feed_dict={x: 3, y: 4.5}))
    print(sess.run(z, feed_dict={x: [1, 3], y: [2, 4]}))
```

Khi muốn lưu trữ một biến (một giá trị tạm thời) mà giá trị của nó có thể thay đổi khi chạy chương trình thì sử dụng ```tf.Variable``` (class có nhiều operation hơn function) hoặc ```tf.get_variable``` (function). Variable thường dùng để chứa Weights cho model. Ví dụ:
```python
#tf.Variable is a class with many operations
sca = tf.Variable(2.0, name="scalar") # gia tri khoi tao 2, ten 'scalar', shape, type tu dong sinh ra tu ininitial value
m=tf.Variable([[1,2],[3,4]], name='matrix')
print(sca)
print(m)
#tf.get_variable is a function
sca1 = tf.get_variable("scalar1",initializer = 3.)
m1 = tf.get_variable("matrix1", initializer=tf.constant([[0, 1], [2, 3]]))
print(sca1)
print(m1)
```

Kết quả:

```python
<tf.Variable 'scalar:0' shape=() dtype=float32_ref>
<tf.Variable 'matrix:0' shape=(2, 2) dtype=int32_ref>
<tf.Variable 'scalar1:0' shape=() dtype=float32_ref>
<tf.Variable 'matrix1:0' shape=(2, 2) dtype=int32_ref>
```

Để sử dụng Varible phải khởi tạo cho nó. Ví dụ:

```python
m= 2*m
m1 = 2+m1
init = tf.global_variables_initializer()
with tf.Session() as sess:
    sess.run(init)
#   sess.run(tf.global_variables_initializer()) #bat buoc phai co cau lenh khoi tao nay
    print("Mỗi lần chạy là giá trị của m được nhân 2:",sess.run(m))
    print("Mỗi lần chạy là giá trị của m1 được cộng 2:", sess.run(m1))
```

Kết quả:

```python
Mỗi lần chạy là giá trị của m được nhân 2: [[ 64 128], [192 256]]
Mỗi lần chạy là giá trị của m1 được cộng 2: [[10 11], [12 13]]
```

Đây là những khái niệm cơ bản nhất của TF, ngoài ra TF còn hỗ trợ nhiều lớp, đối tượng, hàm,...ở mức trừu tượng cao hơn. Trong hướng dẫn sử dụng của TF khuyên nên sử dụng high level API mỗi khi có thể, chỉ sử dụng low level API khi high level API không thể giải quyết được. Bây giờ vận dụng TF để thử một 
ví dụ cơ bản: Linear Regression.
## Linear Regression với Tensorflow
Giới thiệu sơ lược về **Machine Learning**, trong nhiều giáo trình hoặc trên mạng Internet có thể dễ dàng tìm được định nghĩa ML là gì. Ở đây chấp nhận một định nghĩa của Wikipedia như sau *"Machine learning is the subfield of computer science that gives computers the ability to learn without being explicitly programmed"*. Dịch ra thành "ML là một ngành hẹp của khoa học máy tính cho phép máy tính có thể học (từ dữ liệu) mà không cần được lập trình cụ thể". Người ta có nhiều cách phân loại, cách phân loại rộng nhất là chia thành Supervised learning, unsupervised learning và reinforcement learning, Deep learning là một lĩnh vực hẹp của ML sử dụng kiến trúc mạng neuron nhiều lớp. Để làm rõ định nghĩa ở trên xét ví dụ sau:

**Ví dụ:** Cho bảng số liệu chiều cao (x) và cân nặng (y):

```
x = [147, 150, 153, 158, 163, 165, 168, 170, 173, 175, 178, 180, 183]
y = [49, 50, 51,  54, 58, 59, 60, 62, 63, 64, 66, 67, 68]
```

Đồ thị của nó như hình 2

<div class="imgcap">
 <img src ="/images/bai-03/linreg.PNG" align = "center">
 <div class = "thecap">Hình 2. Đồ thị liên hệ x và y</div>
</div>

Trước khi nói tới việc máy học thì người học ra sao? Dừng lại một chút, nếu bạn nhìn vào bảng số và đồ thị trên bạn sẽ "học" được điều gì? Đối với một người học hết cấp 2, trí tuệ bình thường, dễ thấy đó là mối quan hệ tuyến tính giữa cân nặng và chiều cao $y=ax+b$. Chỉ cần biết $a, b$ thì sẽ suy ra quy luật này, và bây giờ nếu có một giá trị chiều cao $x$ mới sẽ suy ra được cân nặng $y$ tương ứng. Tương tự như vậy, nếu đưa cho máy tính bảng số liệu trên rồi bằng cách nào đó máy tính cho ta biết dược giá trị của $a, b$ thì đó chính là học máy. Nếu so sánh với phương pháp không phải là ML thì chúng ta phải lập trình cụ thể, đó là con người tìm ra các con số $a, b$ trước, sau đó lập trình hàm số $y=ax+b$, dựa vào đây máy cho đầu ra $y$ tương ứng với $x$. Đây là một ví dụ đơn giản, gọi là hồi quy tuyến tính (Linear regression), có thể coi bài toán Hello World của ML. Thực tế ML phức tạp hơn nhiều, ví dụ đầu vào máy là bức ảnh, đầu ra máy phải cho biết trong bức ảnh đó con mèo hay không? đầu ra trong bức ảnh đó có mấy cái oto, nằm ở vị trí nào? đầu ra là một đoạn text mô tả nội dung bức ảnh đó.... Bất cứ từ dữ liệu (con số, hình ảnh, tiếng nói, video,...) mà con người nhìn vào đó có thể rút ra được thông tin gì mà máy cũng làm được điều tương tự thì đó có thể coi là ML. Làm thế nào máy có thể làm được điều kì diệu đó? Nó phải học. Vậy con người học như thế nào? Đó là phải được dạy lý thuyết, được thực hành qua các ví dụ, được kiểm tra, đánh giá (học chưa được thì phải học lại). Như ví dụ trên chẳng hạn, đầu tiên phải chỉ ra được đây là quy luật tuyến tính (lý thuyết), đưa các dữ liệu $x, y$ vào để tìm $a, b$ (thực hành) và phải có một tiêu chuẩn nào đó để kiểm tra xem $a, b$ tìm được đã tốt chưa? Máy học (ML) cũng như vậy.

Quay trở lại ví dụ Linear Regression ở trên. Theo ngôn ngữ của ML thì hàm số tuyến tính bậc nhất $y=ax+b$ là mô hình (model), $a, b$ là các tham số của mô hình (parametes hoặc weights). Mô hình làm nhiệm vụ dự đoán (predict), đầu ra của nó thường được gọi là $y_{hat}$. Tiêu chuẩn đánh giá (trong ví dụ này) $y_{hat}$ có đúng với giá trị thực (giá trị đúng) hay không gọi là hàm mất mát (loss/cost function). Mục tiêu là phải làm cho sự sai lệch này càng nhỏ càng tốt (optimization).

Thường khi giải bài toán ML/DL cơ bản thực hiện các bước sau:
- Chuẩn bị dữ liệu
- Xây dựng mô hình
- Xác định hàm mất mát và phương pháp tối ưu hóa
- Training/Fitting mô hình với dữ liệu
- Đánh giá mô hình
- Ứng dụng

Ví dụ Linear Regression như trên thực hiện trong TF như sau:
```jupyter
x_data = np.array([[147, 150, 153, 158, 163, 165, 168, 170, 173, 175, 178, 180, 183]], dtype=float)
y_data = np.array([[49, 50, 51,  54, 58, 59, 60, 62, 63, 64, 66, 67, 68]],dtype = float)
x_data = x_data.T/100
y_data = y_data.T/100
def init_weight(shape):
    return tf.Variable(tf.random.normal(shape,stddev = 0.1))
def model(_input,w1,b1):
    return tf.add(tf.matmul(_input,w1), b1)
iteration = 1000
learning_rate = 0.01

x = tf.placeholder(tf.float32, shape=(None,1))
y = tf.placeholder(tf.float32, shape = (None,1))

_input = x
w1 = init_weight([1,1])
b1 = tf.Variable([0.])
y_pred = model(_input,w1,b1)
loss_op = tf.reduce_mean(tf.square(y - y_pred))
optimizer = tf.train.GradientDescentOptimizer(learning_rate)
train_op = optimizer.minimize(loss_op)

with tf.Session() as sess:
    sess.run(tf.global_variables_initializer())    
    for epoch in range (iteration):
        sess.run(train_op,feed_dict = {x:x_data,y:y_data})
        if (epoch+1) % 100 == 0:
            print('Epoch = ',epoch+1,'Training loss = ', sess.run(loss_op,feed_dict={x:x_data,y:y_data}))
    print('training done!')
    print('w=',sess.run(w1),'b=',sess.run(b1))
```