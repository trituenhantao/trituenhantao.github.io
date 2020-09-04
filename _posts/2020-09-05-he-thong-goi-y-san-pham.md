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

Ý tưởng của Lọc cộng tác: “người tương tự” có thể thích “sản phẩm tương tự” hoặc ngược lại, từ đó việc của chúng ta cần làm là tìm ra mối tương quan giữa các user và item