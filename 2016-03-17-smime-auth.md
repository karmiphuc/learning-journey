---
layout: post
summary: "Password-less auth with S/MIME"
tags: programming design security
---
Hôm qua mình có sử dụng một trang khá thú vị.

Nó sử dụng S/MIME để auth người dùng. Một dạng password-less auth mà người ta đang hướng đến cho optimal UX.

Flow là:

- Người dùng tải CSR/PrivKey của họ lên cho trang nó sign. Xong rồi import cái cert trả về vô browser.
- Từ đó về sau coi như không cần phải đăng nhập lại trên trình duyệt đó nữa.
- Pretty cool and intuitive to me as a power user (but not friendly for normal users).

https://startssl.com/Account

[![https://startssl.com/Account](https://i.imgur.com/S8QFwMQ.jpg)](https://startssl.com/Account)
