---
layout:     post
title: Hệ thống gợi ý sản phẩm
SEOTitle : Triển khai hệ thống gợi ý sản phẩm đơn giản cho website
description: Gợi ý sản phẩm ( Recommender systems) là hệ thống giúp các website cá nhân hóa được sản phẩm đến từng người dùng, từ đó giúp người dùng đưa ra các quyết định mua hàng một cách nhanh chóng.
keywords: "hệ thống gợi ý sản phẩm, triển khai hệ thống gợi ý sản phẩm, hệ thống gợi ý session-based, hệ thống gợi ý content-based, hệ thống gợi ý user-based, hệ thống gợi ý content-based, các hệ thống gợi ý sản phẩm"
sub_url: "http://trituenhantao.github.io/he-thong-goi-y-san-pham" 
#subtitle:   từ lý thuyết đến áp dụng 
date:       2020-09-05
author:     admin
#header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - machine learning
    - scikit learn
    - Recommender systems
---

Ngày nay với sự phát triển của các website thương mại điện tử, việc chú trọng đến trải nghiệm người dùng cũng như tiếp cận những sản phẩm đến tay người dùng vô cùng quan trọng. Hệ thống gợi ý sản phẩm ra đời để giúp người dùng có thể tìm thấy các sản phẩm mà họ mong đợi.

## I. Hệ thống Recommender systems là gì ?

Nói một cách đơn giản recommender systems là hệ thống dựa vào "sở thích" của người dùng trong quá khứ, để dự đoán "sở thích" người dùng trong tương lai và thực hiện gợi ý cho người dùng. Để một hệ thống recommender systems hoạt động tốt điều tiên quyết là phụ thuộc vào sự phản hồi của người dùng. Các phản hồi này có thể là đánh giá sao, bình luận, số lần click chuột vào sản phẩm, thời gian quan sát sản phẩm,...
Về cơ bản recommender systems được chia làm 3 công nghệ chính : 
+ Collaborative filtering ( Lọc cộng tác )

+ Content-based filtering (Lọc theo nội dung)

+ Hybrid filtering ( Lọc hỗn hợp )

![Hệ thống gợi ý recommender systems](/img/he-thong-goi-y-recommender-systems.jpg "Hệ thống gợi ý recommender systems")

Trong khuôn khổ bài viết này mình sẽ hướng dẫn cho các bản triển khai 4 hệ thống gợi ý bao gồm : user-based, item-based, content-based và session-based.
## II. Lọc công tác (Collaborative filtering) :
Ý tưởng của Lọc cộng tác: “người tương tự” có thể thích “sản phẩm tương tự” hoặc ngược lại, từ đó việc của chúng ta cần làm là tìm ra mối tương quan giữa các user và item để gợi ý các sản phẩm cho người dùng.
### 1. User-based :
User-base là một dạng recommender systems dựa vào độ tương quan giữa các user để gợi ý sản phẩm cho các user.

Đến đây các bạn sẽ có một câu hỏi : làm sao để tính độ tương quan của người dùng ?

Chúng ta sẽ tính độ tương quan của các user dựa vào khoảng cách giữa các user trong ma trận biểu diễn user - item. Nếu khoảng cách giữa 2 user càng nhỏ tức 2 user có độ tương tự như nhau và ngược lại.

Vậy chúng ta tính khoảng cách bằng gì? Tất nhiên là không phải bằng thước rồi :v. Chúng ta sẽ tính khoảng cách bằng các công thức Ơ-clit, Minkowski, Cosin,.. Trong bài này mình sẽ sử dụng công thức tính khoảng cách cosin.

Tuy không phải là người Hải Phòng nhưng mình cũng không thích lòng vòng. Mình triển khai ngay một hệ thống gợi ý sử dụng user-based để mọi người cùng hiểu nhé.

Ví dụ mình có một bảng dưới đây thể hiện sự rating sao của 10 người dùng cho 8 app trên điện thoại của họ( các ô trống là những ô người dùng không hoặc chưa đánh giá) từ đó chúng ta cần đưa ra dự đoán sự yêu thích của họ với các ô trống chưa được đánh giá để gợi ý cho người dùng. mọi người có thể tải data mẫu tại [đây](https://github.com/trituenhantao/data-web/blob/master/data_collaborative.csv)

![Hệ thống gợi ý recommender systems](/img/he-thong-goi-y-recommender-systems-1.jpg "Hệ thống gợi ý recommender systems")

Mình sẽ sử dụng công thức cosin để tính độ tương quan của user :

![Hệ thống gợi ý recommender systems](/img/he-thong-goi-y-recommender-systems-4.jpg "Hệ thống gợi ý recommender systems")

Đầu tiền mình sẽ import một số thư viện cần thiết cho bài toán :

```
import numpy as np
from sklearn.metrics.pairwise import cosine_similarity
import pandas as pd
```

Load dữ liệu và visualization dữ liệu bằng dataframe :

```
data = pd.read_csv('./data_collaborative.csv', sep=';')
print(data)
```

sử dụng hàm ```cosine_similarity``` trong thư viện sklearn để tính khoảng cách giữa các user

```
Sim = cosine_similarity(data_matrix,data_matrix)
Sim = np.round(Sim, decimals = 2)
Sim
```
Sau khi tính xong ta sẽ được ma trận khoảng cách giữa các user như hình:

![Hệ thống gợi ý recommender systems](/img/he-thong-goi-y-recommender-systems-2.jpg "Hệ thống gợi ý recommender systems")

Tiếp tục chúng ta sẽ dựa vào độ tương quan của các user để dự đoán các đánh giá các item mà user trước đó chưa đánh giá, mình sẽ áp dụng công thức dự đoán tại từng điểm dữ liệu :

![Hệ thống gợi ý recommender systems](/img/he-thong-goi-y-recommender-systems-5.jpg "Hệ thống gợi ý recommender systems")

```
def predict(A, u,i, k=2):
    user_rated_i = np.where(A[:,i] !=0)[0]
    sim = Sim[u, user_rated_i]
    a = (np.argsort(sim))[-k:]
    nearest_s =sim[a] 
    rating = A[user_rated_i[a],i]
    r_bar = (rating*nearest_s).sum()/(np.abs(nearest_s).sum())
    return np.round(r_bar)

predict_matrix = data_matrix.copy()
for u in range(0, predict_matrix.shape[0]):
  for i in range(0, predict_matrix.shape[1]):
    if data_matrix[u,i] ==0:
      id = i
      predict_matrix[u,i] = predict(data_matrix,u,id)

```
Kết quả chúng ta sẽ thu được ma trận dự đoán như sau :

![Hệ thống gợi ý recommender systems](/img/he-thong-goi-y-recommender-systems-3.jpg "Hệ thống gợi ý recommender systems")

Từ ma trận dự đoán này bạn có thể gợi ý cho người dùng các app mặc dù họ chưa dùng nhưng bạn nghĩ họ sẽ thích nó dựa vào các điểm dự đoán. Bạn có thể tham khảo code đầy đủ tại [đây](https://colab.research.google.com/drive/1Vj9rS2laS39z0IrMHn3Kkq8BvENo8gkv?usp=sharing)

### 2. Item - based:

Đây là một bài toán tương tự hoàn toàn user -based chỉ khác ở chỗ các bạn sẽ dựa vào độ tương tự giữa các item thay vì độ tương tự giữa các user, nên mình sẽ không thực hiện lại. Mọi người có thể tự kiểm tra và so sánh kết quả với user - based.

### 3. Content - based :

