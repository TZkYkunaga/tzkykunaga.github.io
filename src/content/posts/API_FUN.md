---
title: API fundamental
published: 2025-10-15
description: 'Đây là một số kiến thức cơ bản trong API security'
image: 'guide/API_funda.jpg'
tags: [api]
category: 'learning'
draft: false 
lang: 'vi'
---
# Api ảnh hưởng như thế nào ?

83% internet traffic là api traiffic

Trở thành hình thức bị tấn công phổ biến nhất

4% APIs là được bảo vệ

## Normal classic cyber attack


## API attack




APIs considered a poplular target for attackers because They exposed data and logic flaws, and are often have over-permissioned.

**API security testing is critical usually cause by business logic flaws**

# OWASP API sec TOP 10



# API1 :Broken Object level Authorization(BOLA) phá vỡ cấp độ ủy quyền của 1 thực thể

> Liên quan tới sự sai sót trong logic/rule trong việc quản lý truy cập

Là loại lỗ hổng API phổ biến 

Rất khó để detect trong runtime

Nên được chú trọng trong khâu kiểm tra trước khi xuất bản
> 


Tỷ lệ cao mất mát dữ liệu

User A truycap dữ liệu của User B

Các giao dịch lừa đảo

> Thực hiện test gửi các request lỗi khiến cho hệ thống in ra các lỗi api, và vì nó không giúp được nhiều mà còn lộ liễu ra
> 

https://www.coinbase.com/en-gb/blog/retrospective-recent-coinbase-bug-bounty-award

Tại bài báo cáo trên. Root cause chỉ ra rằng có một lỗ hổng trong logic kiểm tra tính xác thực trong 1  Retail Brokerage API endpoint

Ví dụ bạn có 100 đồng shiba và 0 btc bạn thiết lập 1 giao dịch và chuyển 100 đồng shiba đó sang user B nhưng bạn edit tay trên 1 ứng dụng nào đó vd burpsuit từ nguồn shiba thành btc. Tại đây ứng dụng đã xảy ra lỗi khi logic kiểm xác thực chỉ check xem là liệu bạn có đủ số lượng hay không Nhưng đã không check liệu có đúng là loại đồng coin đó chưa .

Như kết quả đã xảy ra sau giao dịch tk A đã biến 100SH thành 100BTC

 As a result, we are paying our largest-ever bug bounty for this finding: $250,000.


# API2: Broken authentication phá vỡ xác thực

## BA là gì

> Là lỗ hỏng bảo mật do yếu hoặc xác thực kém
Thường là kết quả của việc thiếu sự bảo vệ kiểm soát hoặc triển khai kiểm soát kém.
> 


Không có `Oauth`, Không 2FA, không captcha, không có các credential (xác thực)  

---

## Rủi ro có thể xảy ra

- data theft
- Unauthorized transaction
- High volume API Abuse(lạm dụng)
- Ransom PII (Personally Identifiable Information)  harvesting

https://www.cequence.ai/blog/api-security/api-breach-duolingo/

## dữ liệu 2.6m users trên duolingo đã bị lộ vào tháng 1 năm 2023


Như bức ảnh ở trên hacker chỉ cần check một email bất kì nếu nó valid trên duolingo thì toàn bộ thông tin user đã lộ ra.

## Cách phòng chống

> Định nghĩa lại các chính sách xác thực dựa trên business requirements

Nhận thức được sự nhạy cảm của dữ liệu trong các chính sách

Triển khai liên tục các bài thử nghiệm để xác định gaps va các điểm yếu 

Đừng nghỉ rằng API đã được che giấu hoặc không thể được tìm thấy. Hãy nhớ đóng của nhà của mình.
> 


# API3 : Broken Object Property Level authorization(BOPLA)

## What is it

> Khai thác endpoint bằng cách đọc hoặc tùy chỉnh giá trị của object

Có khả năng cập nhật các phần tử của object

Tiết lộ các không tin không cần thiết nhưng lại nhạy cảm
> 


## Rủi ro

> Người dùng có khả năng set “account-type=premium”

API trả về quá nhiều, hoặc những chi tiết không cần thiết

Tiết lộ thông tin nhạy cảm của người dùng

Đánh cắp dữ liệu
> 

## Venmom 1 social platform

https://www.wired.com/story/i-scraped-millions-of-venmo-payments-your-data-is-at-risk/

Venmo biến homepage của họ show ra những live feed của các cuộc giao dịch được tạo bởi người lạ. Và nó có một api cái mà trả về các dữ liệu cho bài feed này.


## Giải pháp

- Đảm bảo rằng người dùng chỉ có thể truy cập những vùng hợp háp và được cho phép
- Chỉ trả lại lượng dữ liệu tối thiểu cần thiết cho từng trường hơp
- Định nghĩa lại các yêu cầu về dữ liệu  trong đặc tả API
- Thử nghiệm để xác thực độ tuân thủ chính sách
- Triển khai thi hành khiểm soát thích hợp để chống việc khai thác lượng lớn dữ liệu
- Thử nghiệm các cuộc kiểm soát để xác định sai sót logic

# API4: Unrestricted Resource consumtion

## What is it?

> Được hiểu như là sự thiếu sót về tài nguyên và kiểm soát giới hạn truy cập

Đây là một sự lạm dụng dựa trên việc bạn yêu cầu một lượng lớn API calls, hay request Lơn,etc khá giống các kiểu tấn công Dos
> 


## Potential risk

> Thiếu hoặc không đủ rate control
Lượng lớn dữ liệu bị thu thập
thời gian chờ Thực thi 
Thời gian chờ thực hiện
Test max memory, số lượng các files, uploadsize
Vượt quá mức triển khai có 1 request
Vượt quá số lượng ghi trong 1 request
Dos
Ảnh hưởng hiệu suất
> 

## Trello

1 Api endpoint của trello đã cho phép người dùng không xác thực bất kì gửi 1 email bất kì liệu có trong đó sẽ gửi về dữ liệu và anh hacker đã lên darkweb và sử dụng  15m email khác nhau và dựa trên một rate nhất định nằm dưới rate limit của firewall hoặc bot detect của trello và liên tục spam

## Giải pháp

- Triển khai traffic control
- Test những controls đó
- Test rate limit không chỉ Volume mà còn Velocity của nó nữa. Mỗi phút hacker nó gửi bao nhiêu gói chẳn hạn.

# API5: Broken function level authorization

## What is it?

> Đây là hình thức tấn công lạm dụng chức năng để chỉnh sửa các object bằng cách không đúng đắn (create,update,delete)

Thường liên quan đến thay đổi  các methods bị động(GET) với các chủ động (put,delete)
> 


## Rủi ro là gì ?

> Sử dụng để leo thang quyền 
Chỉnh sửa các Tham số từ user → admin
Khai thác chỉnh sủa các chi tiết của tài khoản
Xóa bỏ các hóa đơn 
Cho tài khoản thành 99999999$
> 

## Dating site bumble

Bị lỗi đổi người dùng từ quyền free sang phải trả phí

## Giải pháp

- Xác định và uu tiên các chức năng mà có tỉ lệ bị phơi bày những khả năng nhạy cảm
- Phát triển kiểm soát hạn chế truy cập
- Triển khai liên tục các thử nghiệm xuất bản để bảo đảm nó hành động đúng
- Review RBAC permission giữa các loại người dùng và detect drift (phát hiện sự trôi dạt)




> Updating……………
