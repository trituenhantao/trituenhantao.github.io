---
layout:     post
title: Tạo botchat đơn giản với Wit
SEOTitle : Tạo một botchat facebook đơn giản với Wit.ai | blog TTNT
description: Trong bài viết hôm nay mình sẽ giúp các bạn tạo một botchat đơn giản với wit.ai sử dụng ngôn ngữ python. Bạn có thể làm con botchat cho các mục đích riêng của bạn.
keywords: "tạo botchat facebook, botchat facebook, tạo botchat bằng wit, tạo botchat bằng python, tạo botchat tiếng việt, botchat fanpage, botchat messenger, xây dựng botchat, tạo botchat python, botchat tiếng viêt, build botchat bằng python, tạo botchat fanpage facebook, chatbot facebook, tạo chat bot facebook b"
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

+ Nếu bạn muốn xây dựng một chatbot bằng tiếng việt thì chuyển ngôn ngữ thành tiếng Việt nhé 

## 2. Tìm hiểu về giao diện wit.ai :

Mình sẽ nói qua về giao diện trang chủ wit.ai

![Tạo chatbot với wit.ai bằng python](/img/tao-chat-bot-facebook-voi-wit-ai-python.jpg "Tạo chatbot với wit.ai bằng python")

Utterance : đây là phần câu thoại mà con bot của bạn sẽ nhận được để phân tích

Intents : Ý định của câu thoại đó

Traits : Đặc điểm của câu thoại

## 3. Cách phân tích câu thoại :

Mình sẽ phân tích mẫu 1 câu thoại và training câu thoại đó để mọi người có thể dễ dàng làm sau này

ví dụ fanpage mình là fanpage bán giày và mình nhận được câu hỏi là : " Bạn có bán giày Nike SB size UK 10 không vậy ? " mình sẽ hướng dẫn các bạn phân tích câu thoại này. 

ở đây các bạn thấy cụm từ "giày Nike SB" là sản phẩm của mình bán, cụm từ "size UK 10" là size của giày khách cần mua, còn lại 2 cụm từ "bạn có bán " và " không vậy ?" là 2 cụm từ thể hiện hành động cần mua của người mua. 

Sau khi phân tích được các từ trong câu ta cần cho bot học để hiểu, khi bot gặp những trường hợp này bot sẽ biết đây là người hỏi mua giày Nike SB size UK 10, từ đó sẽ đưa ra được câu trả lời phù hợp. Mình bắt đầu dạy bot nhé :v

![Tạo chatbot với wit.ai bằng python](/img/tao-chat-bot-facebook-voi-wit-ai-python-1.jpg "Tạo chatbot với wit.ai bằng python")


Học càng nhiều dữ liệu thì bot của ta sẽ càng thông minh.

## 4. Thêm tính năng developer cho fanpage :

Sau khi đã hoàn thiện 1 con bot vừa ý bây giờ là lúc bạn cần kết nối con bot với fanpage bán hàng của mình.

Đầu tiên bạn vào trang web dành cho developers tại [https://developers.facebook.com](https://developers.facebook.com){:target="_blank"} và đăng ký cho mình 1 app bằng facebook (phần này cũng tương tự như wit)

Sao khi hoàn thành đăng ký tại giao diện developer ở phần *Access tokens* bạn chọn *Add or remove pages* và thêm fanpage của mình cần kết nối chat bot vào. vậy là hoàn thành !

![Tạo chatbot với wit.ai bằng python](/img/tao-chat-bot-facebook-voi-wit-ai-python-2.jpg "Tạo chatbot với wit.ai bằng python")


## 5. Kết nối wit với fanpage bằng python :

Mình sẽ hướng dẫn các bạn sử dụng ngôn ngữ python để kết nối wit với fanpage.

Đầu tiên bạn cần cài đặt 2 thư viện wit và flask về máy của mình bằng các mở terminal và gõ :

```
pip install wit flask
```
Lưu ý bản phải đảm bảo máy của bạn đã cài đặt python nhé ( nếu chưa bạn có thể search google mình không muốn đi quá kỹ những cái google đã có )

Sau khi cài đặt thành công bạn tạo 1 file main.py và coppy đoạn code này vào :

```
from flask import Flask, request, Response
from pymessenger.bot import Bot
from wit import Wit
import requests

app = Flask(__name__)

ACCESS_TOKEN = 'ACCESS_TOKEN'
VERIFY_TOKEN = 'VERIFY_TOKEN'
WIT_TOKEN    = 'ACCESS_TOKEN'
bot = Bot(ACCESS_TOKEN)
client = Wit(access_token=WIT_TOKEN)

#We will receive messages that Facebook sends our bot at this endpoint 
@app.route("/webhook", methods=['GET', 'POST'])
def receive_message():
    if request.method == 'GET':
        """Before allowing people to message your bot, Facebook has implemented a verify token
        that confirms all requests that your bot receives came from Facebook.""" 
        token_sent = request.args.get("hub.verify_token")
        return verify_fb_token(token_sent)
    #if the request was not get, it must be POST and we can just proceed with sending a message back to user
    else:
        """
        Handler for webhook (currently for postback and messages)
        """
        data = request.json
        if data['object'] == 'page':
            for entry in data['entry']:
                # get all the messages
                messages = entry['messaging']
                if messages[0]:
                    # Get the first message
                    message = messages[0]
                    # Yay! We got a new message!
                    # We retrieve the Facebook user ID of the sender
            
                    fb_id = message['sender']['id']
                    print('fb_id :', fb_id)
                    # We retrieve the message content
                    text = message['message']['text']
                    print('text:', text)
                    # Let's forward the message to Wit /message
                    # and customize our response to the message in handle_message
                    response = client.message(text)
                    handle_message(response=response, fb_id=fb_id)
        else:

            return 'Received Different Event'
    return 'Message Processed!!!'


def verify_fb_token(token_sent):
    #take token sent by facebook and verify it matches the verify token you sent
    #if they match, allow the request, else return an error 
    if token_sent == VERIFY_TOKEN:
        return request.args.get("hub.challenge")
    return 'Invalid verification token'

def fb_message(sender_id, text):
    """
    Function for returning response to messenger
    """
    data = {
        'recipient': {'id': sender_id},
        'message': {'text': text}
    }
    # Setup the query string with your PAGE TOKEN
    qs = 'access_token=' + ACCESS_TOKEN
    # Send POST request to messenger
    resp = requests.post('https://graph.facebook.com/me/messages?' + qs,
                         json=data)
    return resp.content

def first_trait_value(traits, trait):
    """
    Returns first trait value
    """
    if trait not in traits:
        return None
    val = traits[trait][0]['value']
    if not val:
        return None
    return val


def handle_message(response, fb_id):
    """
    Customizes our response to the message and sends it
    """
    greetings = first_trait_value(response['traits'], 'wit$greetings')
    if greetings:
        text = "hello!"
    else:
        text = "We've received your message: " + response['text']
    # send message
    fb_message(fb_id, text)

```
Lưu ý : Bạn chỉ thay đổi 3 giá trị ACCESS_TOKEN, VERIFY_TOKEN, WIT_TOKEN. 

ACCESS_TOKEN chính là token bạn lấy trong [https://developers.facebook.com](https://developers.facebook.com){:target="_blank"} tại mục *Generate Token*

VERIFY_TOKEN là mã bí mật bạn tự tạo để kết nối đến fanpage của bạn

WIT_TOKEN là token bạn lấy trong [https://wit.ai](https://wit.ai){:target="_blank"} tại mục *Server Access Token* ở phần *setting*

## 6. Deploy file lên heroku:

Sau khi đã kết nối thành công các bạn cần deploy file đó lên server để có thể hoạt động được. mình chọn heroku vì nó dễ deploy và đặc biệt là nó free :v

1. Đầu tiên các bạn vào trang web [https://www.heroku.com/](https://www.heroku.com/){:target="_blank"} để đăng ký cho mình 1 tài khoản.

2. Sau khi đăng ký tài khoản xong các bạn vào folder bạn đã lưu file app.py tiếp tục tạo 1 file mới có tên là wsgi.py và sao chép đoạn code sau đây vào.

```
from main import app 
  
if __name__ == "__main__": 
        app.run() 
```

3. tiếp tục tại folder hiện tại bạn mở terminal và gõ các lệnh sau :

```
pip install gunicorn 
pip freeze > requirements.txt
touch Procfile
touch runtime.txt
```
Sau khi hoàn thành bạn sẽ thấy trong folder xuất hiện thêm 3 file, file requirements là file chứa các thư viện cần thiết để bạn thiết lập trên server, file runtime là file chứa môi trường python hiện tại của bạn, còn file cuối cùng là file Procfile bạn chỉ cần dán đoạn mã sau đây là là xong nhé ```web: gunicorn app:wsgi```

Như vậy là hoàn thành việc setup các file để deploy lên heroku. Chúng ta bắt đầu deploy thôi nào :v

Tại folder chứa các file bạn tiếp tục mở terminal và bấm các lệnh sau : 

```
git init
git add .
git commit -m "Initial Commit"
heroku login
```
Đến đây sẽ có 1 cửa sổ đăng nhập keroku xuất hiện bạn chỉ cần click login là thành công, chúng ta tiếp tục quay lại cửa sổ terminal và bấm các lệnh :

```
heroku create namechatbot-app
git push heroku master
```
Đợi tầm 3-5ph để code của bạn được deploy lên server.

## 7. Callback URL chatbot với fanpage :

Sau khi deploy thành công bạn vào lại trang [https://developers.facebook.com](https://developers.facebook.com){:target="_blank"} tại phần messenger bạn chọn setting và dán đường dẫn bạn vừa deploy được vào ô Callback URL , và Verify Token là token bạn đã tạo trong code ở file main.py.

Vậy là xong, vậy là bạn đã tạo được 1 con chatbot cho fanpage của riêng mình. Để con chatbot thông minh thì bạn phải cho nó học thật nhiều nhé. Đây là thành quả của mình. Chúc các bạn thành công.

