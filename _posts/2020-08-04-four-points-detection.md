---
layout: post
title: Bài toán xác định 4 góc áp dụng trong nhận dạng CMND, biển số xe 
subtitle: Four points detection
tags: [keypoints detection]
commmens: true 
---

***Tổng quan:***
Nhận dạng CMND, biển số xe là những bài toán khá phổ biến. Đầu vào là 1 ảnh chứa CMND hoặc biển số xe, đầu ra là thông tin trích xuất được từ ảnh đó. Chúng ta có rất nhiều cách để giải quyết bài toán này như áp dụng Opencv thuần hay là Deep learning. 
Nhìn chung, hầu hết các phương pháp đều trải qua các bước sau:
- Bước 1: Từ ảnh đầu vào, xác định vùng đối tượng (CMND, biển số xe), crop và xoay đối tượng thẳng nhất có thể. 
- Bước 2: Phát hiện các vùng text trong ảnh đã crop 
- Bước 3: Nhận dạng các text từ các vùng text ở bước 2 

Mỗi bước đều có các kỹ thuật, phương pháp xử lý riêng. Chất lượng của bước trước ảnh hưởng khá nhiều đến bước sau. Bài viết này sẽ tập trung vào bước 1.
Tại bước này, kỹ thuật mình sử dụng là xác định 4 góc của đối tượng và crop đối tượng từ 4 góc này. Chúng ta có thể sử dụng các model object detection để phát hiện các góc này (như Yolo, CenterNet, ...) cho kết quả khá tốt. Tuy nhiên, hạn chế của phương pháp này là góc trả về chưa được tốt nhất có thể. Để tăng độ chính xác hơn, mình đã áp dụng 
một phương pháp lấy ý tưởng từ Centernet : Objects as keypoints. Chúng ta sẽ coi các góc như các điểm và sẽ huấn luyện một model để phát hiện các điểm này thay vì một vùng chứa góc. 
