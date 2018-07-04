## Các lưu ý khi làm việc với package (module) trong python

### Pip
Pip là công cụ quản lý các package của python

### Virtualenv
- Virtualenv dùng để thiết lập môi trường ảo, cho phép chúng ta tạo ra các môi trường độc lập với global để tùy ý sử dụng các package khác nhau mà không ảnh hưởng đến toàn hệ thống.

- Anaconda cũng có thể sử dụng thay cho Virtualenv.


### Sử dụng pip để cài đặt package

- Cài đặt trực tiếp 
```
$ pip install something 
```

- Cài đặt package từ public github repository
```
$ pip install git+git://github.com/something/somewhat.git
```

- Cài đặt package từ private github repository
```
$ pip install git+ssh://git@github.com/echweb/echweb-utils.git
```

- Cài đặt tất cả package được khai báo trong requirements.txt
```
$ pip install -r requirements.txt
```

### Khai báo package trong requirements.txt

```
underthesea==1.1.8
flask==1.0.2
html2text==2018.1.9
requests==2.19.1
-e git://github.com/TinTran710/textrank-1#egg=textrank
```
