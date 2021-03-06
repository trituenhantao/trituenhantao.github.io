---
layout:     post
title: Hồi quy tuyến tính
SEOTitle : Hồi quy tuyến tính trong machine learning | blog TTNT
description: Hồi quy tuyến tính trong machine learning từ lý thuyết đến thực tế sử dụng python, giúp mọi người tiếp cận một các dễ dàng
keywords: "hồi quy tuyến tính, Hồi quy tuyến tính trong machine learning, linear regression, hồi quy tuyến tính scikit learn, thuật toán hồi quy tuyến tính, áp dụng hồi quy tuyến tính, hoi quy tuyen tinh, thuat toan hoi quy tuyen tinh, Multiple Linear Regression, Simple Linear Regression"
sub_url: "http://trituenhantao.github.io/hoi-quy-tuyen-tinh-trong-machine-learning" 
#subtitle:   từ lý thuyết đến áp dụng 
date:       2020-08-20
author:     admin
#header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - machine learning
    - scikit learn
    - Supervised learning
---
Hồi quy tuyến tính ( Linear Regression ) là bài toán cơ bản và đơn giản nhất của Machine Learning. Hồi quy tuyến tính thuộc nhóm Học có giám sát ( Supervised Learning ). Trong bài này mình sẽ hướng dẫn cho các bạn triển khai một Simple Linear Regression và Multiple Linear Regression trong môi trường thực tế sử dụng thư viện scikit learn.

## I. Simple Linear Regression
Simple Linear Regression (Hồi quy tuyến tính đơn giản ) là là một phương pháp thống kê để hồi quy dữ liệu với biến phụ thuộc có giá trị liên tục trong khi các biến độc lập có thể có một trong hai giá trị liên tục hoặc là giá trị phân loại.
### 1. Bộ dữ liệu
Trường học A đã khảo sát số giờ học ở nhà trong tuần sinh viên giành môn học Giải tích 1 và kết quả đạt được sau khi kết thúc môn học, thống kê được như sau :

| Hours | Scores |
|-------|--------|
| 2.0   | 4.1    |
| 4.6   | 6.7    |
| 2.5   | 4.7    |
| 8.0   | 8.2    |
| 3.0   | 5.0    |
| ...   | ...    |


(Các bạn có thể tải file đầy đủ tại [đây](https://raw.githubusercontent.com/trituenhantao/data-web/master/giai-tich1.csv){:target="_blank"} ) 

### 2. Import thư viện:

Đầu tiên chúng ta cần phải import các thư viện cần thiết cho bài bài toán hồi quy tuyến tính

```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression 
```
_để import được các thư viện trước tiên bạn phải đảm bảo đã cài đặt thư viện này tại môi trường python đang làm việc._
### 3. Đọc dữ liệu từ file csv :

Sau khi đã tải file csv về bạn cần đọc các dữ liệu từ file csv đó, chúng ta sử dụng hàm read_csv trong thư viện pandas và hiển thị nó ra màn hình để kiểm tra lại.

```
data = pd.read_csv('giai-tich1.csv')
data.head()
```

_ngoài ra bạn còn có thể sử dụng các hàm describe trong pandas xem tổng quan về dữ liệu của mình_

### 4. Biễu diễn dữ liệu trên biểu đồ :

Bạn có thể sử dụng thư viện matplotlib để biểu diễn dữ liệu của bài toán hồi quy tuyến tính một cách trực quan hơn.

```
data.plot(x='Hours', y='Scores', style='ro')
plt.xlabel('Số giờ học')
plt.ylabel('Số điểm')
plt.show()
```
![Hồi quy tuyến tính Linear Regression](/img/hoi-quy-tuyen-tinh-linear-regression.jpg "Hồi quy tuyến tính Linear Regression")

### 5. Tính hồi quy tuyến tính do dữ liệu :

Để tính hồi quy tuyến tính cho dữ liệu mình sẽ sử dụng hàm LinearRegression của thư viện scikit learn đã import ở trên

```
X_train = data.iloc[:, :-1].values
y_train = data.iloc[:, 1].values
regression = LinearRegression()
regression.fit(X_train, y_train)
```

### 6. Dự đoán đối với dữ liệu mới :

Để dự đoán kết quả tổng kết môn giải tích 1 với một sinh viên mới học ta chỉ cần sử dụng lại kết quả của hồi quy tuyến tính trên như sau :
ví dụ số giờ về nhà sinh viên mới giành cho môn giải tích 1 là 5.3 giờ/tuần.

```
print('Điểm thi của người đó là: ',regression.predict(np.array([[5.3]]))[0])
```

Ngoài ra bạn còn có thể chia tập dữ liệu thành 80% để tính, và 20% để kiểm tra. Sau đó dùng các hàm tính độ chính xác để tính độ chính xác của hồi quy tuyến tính trên tập kiểm tra.

Bạn có thể chạy và tham khảo code [tạiđây](https://colab.research.google.com/drive/1w-e15IPjao1zbQiOdYTQ5UMBIvjubrFK?authuser=2#scrollTo=DstS-E7MlGCx){:target="_blank"}

## II. Multiple Linear Regression :

Multiple Linear Regression (Hồi quy tuyến tính đa biến ) là là một phương pháp thống kê để hồi quy dữ liệu có nhiều biến độc lập.

Tương tự Simple Linear Regression, Bạn có thể sử dụng thư viện scikit learn để khảo sát bài toán này.
