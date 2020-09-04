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
Ví dụ mình có một bảng dưới đây thể hiện sự rating sao của 10 người dùng cho 8 app trên điện thoại của họ( các ô trống là những ô người dùng không hoặc chưa đánh giá) từ đó chúng ta cần đưa ra dự đoán sự yêu thích của họ với các ô trống chưa được đánh giá để gợi ý cho người dùng.

![Hệ thống gợi ý recommender systems](/img/he-thong-goi-y-recommender-systems-2.jpg "Hệ thống gợi ý recommender systems")
