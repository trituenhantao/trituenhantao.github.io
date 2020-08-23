---
layout:     post
title: Tạo botchat đơn giản với Wit
SEOTitle : Tạo một botchat facebook đơn giản với Wit.ai | blog TTNT
description: Trong bài viết hôm nay mình sẽ giúp các bạn tạo một botchat đơn giản với wit.ai sử dụng ngôn ngữ python. Bạn có thể làm con botchat cho các mục đích riêng của bạn.
keywords: "tạo botchat facebook, botchat facebook, tạo botchat bằng wit, tạo botchat bằng python, tạo botchat tiếng việt, botchat fanpage, botchat messenger, xây dựng botchat"
sub_url: "http://trituenhantao.github.io/tao-bot-chat-don-gian-bang-wit-ai" 
#subtitle:   từ lý thuyết đến áp dụng 
date:       2020-08-22
author:     admin
#header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - botchat
    - wit
    - nlp
---
Trong bài viết này mình sẽ hướng dẫn các bạn chi tiết tạo 1 botchat đơn giản trên facebook sử dụng wit.ai, ngôn ngữ mình sử dụng là python và mình dùng heroku để làm server. Mình sẽ đi một cách chi tiết nhất có thể để những bạn không biết gì về python vẫn có thể có được sản phẩm của riêng các bạn.

## 1. Tạo app trên wit.ai :

+ Các bạn truy cập vào trang chủ wit.ai chọn đăng nhập bằng facebook hoặc github

+ Bạn tiếp tục chọn new app -> nhập tên app, trong mục Visibility nhớ để chế độ Open -> Create

+ Nếu bạn muốn xây dựng một chatbot bằng tiếng việt thì chọn mục setting và chuyển ngôn ngữ thành tiếng Việt

## 2. Tìm hiểu về giao diện wit.ai :

Mình sẽ nói sơ qua về giao diện trang chủ wit.ai

(ẢNH)

Utterance : đây là phần câu thoại mà con bot của bạn sẽ nhận được để phân tích
Intents : Ý định của câu thoại đó
Traits : Đặc điểm của câu thoại

## 3. Cách phân tích câu thoại :

Mình sẽ phân tích mẫu 1 câu thoại và training câu thoại đó để mọi người có thể dễ dàng làm sau này

ví dụ fanpage mình là fanpage bán giày và mình nhận được câu hỏi là : " Bạn có bán giày Nike SB size UK 10 không vậy ? " mình sẽ hướng dẫn các bạn phân tích câu thoại này. 

ở đây các bạn thấy cụm từ "giày Nike SB" là sản phẩm của mình bán, cụm từ "size UK 10" là size của giày khách cần mua, còn lại 2 cụm từ "bạn có bán " và " không vậy ?" là 2 cụm từ thể hiện hành động cần mua của người mua. 
Sau khi phân tích được các từ trong câu ta cần cho bot học để hiểu, khi bot gặp những trường hợp này bot sẽ biết đây là người hỏi mua giày Nike SB size UK 10, từ đó sẽ đưa ra được câu trả lời phù hợp. Mình bắt đầu dạy bot nhé :v

... 
..

Học càng nhiều dữ liệu thì bot của ta sẽ càng thông minh.

## 4. Thêm tính năng developer cho fanpage :

Sau khi đã hoàn thiện 1 con bot vừa ý bây giờ là lúc bạn cần kết nối con bot với fanpage bán hàng của mình.
Đầu tiên bạn vào trang web dành cho developers tại https://developers.facebook.com và đăng ký cho mình 1 app bằng facebook (phần này cũng tương tự như wit)
Sao khi hoàn thành đăng ký tại giao diện developer ở phần *Access tokens* bạn chọn *Add or remove pages* và thêm fanpage của mình cần kết nối chat bot vào. vậy là hoàn thành !

## 5. Kết nối wit với fanpage bằng python :

Mình sẽ hướng dẫn các bạn sử dụng ngôn ngữ python để kết nối wit với fanpage, 
