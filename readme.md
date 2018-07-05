## Các lưu ý khi làm việc với package (module) trong python

### Pip
Pip là công cụ quản lý các package của python

### Virtualenv
- Virtualenv dùng để thiết lập môi trường ảo, cho phép chúng ta tạo ra các môi trường độc lập với global để tùy ý sử dụng các package khác nhau mà không ảnh hưởng đến toàn hệ thống.

- Anaconda cũng có thể sử dụng thay cho Virtualenv.


### Sử dụng pip để cài đặt package

- Cài đặt trực tiếp:
```
$ pip install something 
```

- Cài đặt package từ public github repository:
```
$ pip install git+git://github.com/something/somewhat.git
```

- Cài đặt tất cả package được khai báo trong requirements.txt:
```
$ pip install -r requirements.txt
```

### Sử dụng pip để cài đặt package từ các private repository

**Cài đặt package từ private github repository:**
```
$ pip install git+ssh://git@github.com/echweb/echweb-utils.git
```
- Cách này yêu cầu chúng ta set username cho git.
- Lưu ý: Thay dấu `:` thành dấu `/` trong kết quả từ việc chạy câu lệnh `git remote -v` trước khi sử dụng địa chỉ đó vào trong câu lệnh `pip`: 

```
$ git remote -v
origin  git@github.com:echweb/echweb-utils.git (fetch)
                      ^ thay bằng dấu '/' character
```

**Cài đặt package trực tiếp từ HTTPS URL private github repository:**
```
$ pip install git+https://github.com/username/repo.git
```
- Lưu ý: Với private repo, ta sẽ cần nhập username/password

**Cài đặt package từ repository đã được clone về local:**
```
$ pip install git+file://c:/repo/directory
```

Với những local repo mà đã trải qua những sửa đổi, để cài đặt bằng pip mà không cần phải commit những thay đổi cho repo đó, ta dùng câu lệnh:
```
$ pip install -e C:\repo\directory
```

**Cài đặt package trực tiếp từ Bitbucket:**
```
$ pip install git+ssh://git@bitbucket.org/username/projectname.git
```

Trường hợp này pip cũng sẽ sử dụng SSH key

**Cài đặt package từ private GitLab repository:**
Cách này sử dụng GitLab Deploy keys và SSH config file để ta có thể deploy sử dụng key khác với SSH key cá nhân.

- Khởi tạo SSH Key mới
```
ssh-keygen -t rsa -C "GitLab_Robot_Deploy_Key"
```
Các key sẽ xuất hiện tại `~/.ssh/GitLab_Robot_Deploy_Key and ~/.ssh/GitLab_Robot_Deploy_Key.pub`

Copy và paste nội dung của file tại `~/.ssh/GitLab_Robot_Deploy_Key.pub` vào mục GitLab "Deploy Keys".

- Kiểm tra Deploy Key mới

Câu lệnh sau sẽ báo SSH sử dụng deploy key mới để thiết lập kết nối. Nếu thành công, bạn sẽ nhận được thông báo: "Welcome to GitLab, UserName!"

```
ssh -T -i ~/.ssh/GitLab_Robot_Deploy_Key git@gitlab.mycorp.com
```
- Tạo SSH Config File
Sử dụng trình soạn thảo để tạo file `~/.ssh/config`. Thêm nội dung sau vào. Giá trị cho 'Host' có thể là bất kỳ (nhưng hãy nhớ rằng giá trị này bạn sẽ sử dụng sau này). "HostName" là URL tới GitLab instance. "IdentifyFile" là đường dẫn tới file SSH key mà bạn tạo ra ở bước trên.

```
Host GitLab
  HostName gitlab.mycorp.com
  IdentityFile ~/.ssh/GitLab_Robot_Deploy_Key
```

- Trỏ SSH tới file Config
```
$ pip install git+ssh://git@gitlab.mycorp.com/my_name/my_repo.git
```
Ta chỉ cần sửa đổi một chút để SSH sử dụng Deploy Key mới. Ta thực hiện điều này bằng cách trỏ SSH tới Host entry (vị trí/giá trị Host). Replace 'gitlab.mycorp.com' trong câu lệnh bằng giá trị của "Host" ta sử dụng trong file SSH config:

```
$ pip install git+ssh://git@GitLab/my_name/my_repo.git
```

Đến lúc này package sẽ được tải về mà ta không cần nhập password


### Ví dụ về khai báo package trong requirements.txt

```
underthesea==1.1.8
flask==1.0.2
html2text==2018.1.9
requests==2.19.1
-e git://github.com/TinTran710/textrank-1#egg=textrank
```
