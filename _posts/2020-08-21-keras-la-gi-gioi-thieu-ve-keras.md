---
layout:     post
title: Giới thiệu tổng quan về keras
SEOTitle : Keras là gì ? Giới thiệu tổng quan về keras | blog TTNT
description: Keras là gì ? Giới thiệu tổng quan về keras - Trong bài viết này mình sẽ giới thiệu cho các bạn về keras và các cú pháp của keras một các dễ hiểu nhất thông qua ví dụ xây dựng một mô hình đơn giản bằng keras.
keywords: "framework keras, keras là gì, keras la gi, giới thiệu về keras, tổng quan về keras, nhận diện chữ số viết tay sử dụng keras, nhan dien chu so viet tay su dung keras, thư viện keras, classification sử dụng keras"
sub_url: "http://trituenhantao.github.io/keras-la-gi-gioi-thieu-ve-keras" 
#subtitle:   từ lý thuyết đến áp dụng 
date:       2020-08-21
author:     admin
#header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - keras
    - deep learning
    - classification 
---

Keras là một thư viện mạng nơ ron được viết bằng python năm 2015 bởi 1 kỹ sư deep learning của google. Ta có thể kết hợp keras với các thư viện deep learning. (Mình hay kết hợp sử dụng keras và tensorflow).

## I. Giới thiệu tổng quan về keras : 

![Keras là gì ? giới thiệu về keras ](/img/keras-la-gi-gioi-thieu-ve-keras.jpg "Keras là gì ? giới thiệu về keras")

Ưu điểm nổi bật của keras so với các thư viện deep learning khác có lẽ là cú pháp dễ sử dụng và trực quan của nó. Ngoài ra nó còn có thể chạy trên cả CPU và GPU.
### 1. Cài đặt : 

Cài đặt môi trường :

```
pip install keras
```

Kiểm tra đã cài đặt thành công hay chưa :

```
python -c 'import keras; print(keras.__version__)'
```
### 2. xây dựng model trong keras :

Bạn có thể xây dựng model trong keras bằng 2 cách đó là Sequential model và Function API.

## II. Nhận diện chữ số viết tay sử dụng keras :

Để hiểu rõ keras hoạt động như thế nào mình sẽ đi vào thực tế với bài toán nhận diện chữ số viết tay. Cùng với bài toán phân loại chó mèo, thì nhận diện chữ số viết tay cũng có thể được xem là bài hello world cho người học deep learning.

### 1. Bộ dữ liệu : 

Dữ liệu cho bài này mình sẽ sử dụng tập MNIST, đây là tập dữ liệu chứa 70.000 ảnh chữ số viết tay từ 0 - 9 kích thước mỗi hình là 28x28.

![Dự đoán chữ số viết tay sử dụng keras](/img/chu-so-viet-tay-mnist-keras.jpg "Dự đoán chữ số viết tay sử dụng keras")

### 2. Import thư viện :

Đầu tiên chúng ta cần import các thư viện cần thiết cho bài toán, mình sẽ sử dụng keras để xây dựng model nên phải import keras rồi :v

```
import keras

from keras.models import Sequential
from keras.layers import *
from keras.utils import to_categorical
import matplotlib.pyplot as plt
from keras.datasets import mnist

```

### 3. Load và chia dữ liệu :

Sau khi import các thư viện cần thiết chúng ta cần load dữ liệu và kiểm tra dữ liệu.

```
(X_train, y_train), (X_test, y_test) = mnist.load_data()
X_train = X_train / 255
X_test = X_test / 255

y_train = to_categorical(y_train)
y_test = to_categorical(y_test)

```

Để mình giải thích đoạn code trên cho mọi người dễ hiểu
dữ liệu mnist người ta chia sẵn làm 2 phần gồm 60.000 dữ liệu training và 10.000 dữ liệu test
X_train, X_test là các dữ liệu thể hiện các số
y_train, y_test là các nhãn của các số đó
mình chia các số cho 255 để normalize chúng từ 0-255 về 0-1
còn đối với label của các số mình sử dụng hàm to_categorical để one hot encode nó



### 4. Xây dựng model cho bài toán :

mặc dù keras có hỗ trợ sẵn cho chúng ta classification_model() cho các bài toán classification nhưng trong bài này mình sẽ hướng dẫn cho các bạn xây dựng 1 model từ đầu bằng 2 cách là Sequential model và Function API.

Bắt đầu thôi nào !!!

#### 4.1. Xây dựng model keras bằng Sequential model :

```
model = Sequential()
model.add(Flatten(input_shape=[28, 28]))
model.add(Dense(output_dim=256, activation="relu"))
model.add(Dense(output_dim=128, activation="relu"))
model.add(Dense(output_dim=10, activation="softmax"))
model.compile(loss='categorical_crossentropy',
              optimizer='adam',
              metrics=['accuracy'])
model.summary()
````

![Keras là gì ? giới thiệu về keras ](/img/keras-la-gi-gioi-thieu-ve-keras-1.jpg "Keras là gì ? giới thiệu về keras")

Mình sẽ giải thích cho bạn bạn đoạn code này mình viết gì

    + Đầu tiên mình sẽ khởi tạo model Sequential cho bài toán

    + Đầu vào của chúng ta là ma trận có số chiều là 28x28 chúng ta sẽ sử dụng Flatten để duỗi thẳng chúng ta thành một mảng

    + Dense là cách khai báo 1 layer trong Keras, với output_dim là số chiều đầu ra của layer đó, và activation là hàm kích hoạt của 
    layer mọi người nên tìm hiểu về tất cả các hàm kích hoạt để chọn được hàm kích hoạt phù hợp cho mỗi bài toán.
    
    + Đầu ra của bài toán chúng ta sẽ sử dụng hàm activation để tính xác suất của ảnh đó là số gì.

    + Hàm compile là hàm chúng ta cần để xác định các optimizer trong quá trình train.

#### 4.2. Xây dựng model keras bằng Function API :

```
input_ = Input(shape=[28, 28])
flatten = Flatten(input_shape=[28, 28])(input_)
hidden1 = Dense(2**14, activation="relu")(flatten)
hidden2 = Dense(512, activation='relu')(hidden1)
hidden3 = Dense(28*28, activation='relu')(hidden2)
reshap = Reshape((28, 28))(hidden3)
concat_ = Concatenate()([input_, reshap])
flatten2 = Flatten(input_shape=[28, 28])(concat_)
output = Dense(10, activation='softmax')(flatten2)
model = keras.Model(inputs=[input_], outputs=[output] )
model.compile(loss='categorical_crossentropy',
              optimizer='adam',
              metrics=['accuracy'])
model.summary()
```

![Keras là gì ? giới thiệu về keras ](/img/keras-la-gi-gioi-thieu-ve-keras-2.jpg "Keras là gì ? giới thiệu về keras")

Mọi người có thể sử dụng một trong 2 cách trên nhé mình đã trình bày ở trên nhé

### 5. Thực hiện train model :

```
model.fit(X_train, y_train, epochs=10, verbose=2)

```
Hàm fit là hàm dùng để bắt đầu training dữ liệu. Các bạn cần đưa vào hình ảnh các số và label các số đã được xử lý ở trên. Epochs là số lần lặp training. Vì đây là bài đơn giản nên mình không chia dữ liệu validation.
### 6. Đánh giá mô hình :

```
score = model.evaluate(X_test, y_test, verbose=0)
print(score)
```
Để đánh giá mô hình cho bài toán chúng ta có thể hiển thị độ chính xác trên tập test của bài toán.

### 7. Dự đoán :

```
plt.imshow(X_test[1998].reshape(28,28))

y_predict = np.argmax(model.predict(X_test[1998].reshape(1,28,28,1)))
print('Giá trị dự đoán: ', y_predict)
```
![Dự đoán chữ số viết tay sử dụng keras](/img/chu-so-viet-tay-keras.jpg "Dự đoán chữ số viết tay sử dụng keras")

Chúng ta có thể kiểm tra độ chính xác của mô hình này thông qua việc hiển thị một số 1 tập dataset và dự đoán số đó bằng mô hình ta vừa train xong.

Như vậy qua bài này mình đã hướng dẫn các bạn xây dựng 1 mô hình neural network căn bản bằng keras áp dụng thực tế để dự đoán chữ số viết tay. Mọi người có thể tham khảo code tại [đây](https://colab.research.google.com/drive/1S191tvQ-2ChUAXuAJkJWaajHf-l826_w?usp=sharing)