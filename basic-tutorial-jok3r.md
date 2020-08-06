# Hướng dẫn cài đặt và sử dụng cơ bản Jok3r

## Mục lục


1. [Cài đặt](#setup)
1. [Hướng dẫn sử dụng cơ bản](#basic-usage)
   1. [Thử nghiệm kiểm tra bảo mật bằng toolbox](#demo-security-testing)
   1. [Một số lệnh khác](#commands)
      1. [Thao tác quản lý với toolbox](#toolbox-management)
      1. [Thao tác với database](#database-management)


## Cài đặt <a name="setup"></a>

- Clone source code về từ github bằng lệnh:
```
git clone https://github.com/koutto/jok3r.git
```

![image](https://user-images.githubusercontent.com/41882267/89511614-5bcb4500-d7fc-11ea-86fc-5c122dea9d94.png)


- Cài đặt pip3 bằng lệnh:
```
sudo apt install python3-pip
```

![image](https://user-images.githubusercontent.com/41882267/89511713-78677d00-d7fc-11ea-9f38-4fd7c4d1d8e0.png)


- Để cài đặt các module mà toolbox cần, chuyển đến thư mục jok3r và sử dụng lệnh:
```
pip3 install -r requirements.txt
```

![image](https://user-images.githubusercontent.com/41882267/89511908-afd62980-d7fc-11ea-99f2-d13d4860c76d.png)


- Để tiến hành cài đặt, sử dụng lệnh:
```
sudo ./install
```

![image](https://user-images.githubusercontent.com/41882267/89512138-fdeb2d00-d7fc-11ea-9ec8-229abc6b6d05.png)


- *Lưu ý:*

Ở bước cài đặt nếu có lỗi "Please use apt-cdrom to make this CD-ROM recognized by APT. apt-get update cannot be used to add new CD-ROMs" thì có thể sửa bằng cách 
sử dụng lệnh: 
```
sudo nano -c /etc/apt/sources.list
```


Sau đó comment dòng số 5 và lưu lại.

![image](https://user-images.githubusercontent.com/41882267/89512596-a3060580-d7fd-11ea-93ea-be8b25611550.png)


Ở bước cài đặt xuất hiện lỗi NO_PUBKEY. Để sửa lỗi này, sử dụng lệnh:
```
sudo apt-key adv --keyserver hkp://keys.gnupg.net --recv-keys ED444FF07D8D0BF6
```
(Với ED444FF07D8D0BF6 là tên key)

![image](https://user-images.githubusercontent.com/41882267/89512932-1ad43000-d7fe-11ea-80f0-81ce798657c4.png)


Sau khi sửa hết lỗi, tiến hành cài lại bằng cách sử dụng lệnh:
```
sudo ./install
```

![image](https://user-images.githubusercontent.com/41882267/89513418-b9f92780-d7fe-11ea-8a7e-c61cdbc357a8.png)


- Chọn "Yes" trong 2 trường hợp sau:

![image](https://user-images.githubusercontent.com/41882267/89513530-e0b75e00-d7fe-11ea-9280-590fa25f9fef.png)
![image](https://user-images.githubusercontent.com/41882267/89513548-e8770280-d7fe-11ea-9fd4-4b6fde9f4aca.png)


Lần đầu tiên cài có thể sẽ bị lỗi thiếu một số tool.
![image](https://user-images.githubusercontent.com/41882267/89513733-22e09f80-d7ff-11ea-8b04-dac1205c797b.png)

- Thiết lập biến môi trường java, sử dụng lệnh: 
```
sudo nano /etc/environment
```


Và thêm vào đoạn sau:
```
JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64"
```
![image](https://user-images.githubusercontent.com/41882267/89513869-57545b80-d7ff-11ea-9e7e-8dcf1f5976ac.png)


- Để cài từng tool và dò tìm lỗi khi cài đặt,sử dụng lệnh:
```
python3 jok3r.py toolbox --install-all
```
Sau đó sửa theo lỗi mà code trả về. Ví dụ:
![image](https://user-images.githubusercontent.com/41882267/89514070-8ff43500-d7ff-11ea-9739-14559d611b9d.png)


Để sửa lỗi này,ta có thể xóa hết các folder và file trong folder vbscan và tiến hành cài lại.

- Sau khi cài xong, để kiểm tra lại các tool trong toolbox, sử dụng lệnh:
```
python3 jok3r.py toolbox --show-all
```

![image](https://user-images.githubusercontent.com/41882267/89514471-1b6dc600-d800-11ea-8140-2f80292eeb84.png)


## Hướng dẫn sử dụng cơ bản <a name="basic-usage"></a>
 
### Thử nghiệm kiểm tra bảo mật bằng toolbox <a name="demo-security-testing"></a>
Thử nghiệm kiểm tra bảo mật đối với một url cho trước.
- Đầu tiên, vào thư mục jok3r. Để vào database, sử dụng lệnh:
```
python3 jok3r.py db
```

![image](https://user-images.githubusercontent.com/41882267/89515436-473d7b80-d801-11ea-8bd8-a0c529d82082.png)


- *Lưu ý:* 

Nếu bị lỗi AttributeError: do_load thì có thể sửa bằng cách sửa file DbController.py, sử dụng lệnh: 
```
sudo nano -c /home/hungcao/jok3r/lib/controller/DbController.py
```
Sau đó comment dòng 68 và dòng 70
<br/>
dòng 68: del cmd2.Cmd.do_load
<br/>
dòng 70: del cmd2.Cmd.do_pyscript
<br/>
Sau đó lưu lại và thoát ra.


![image](https://user-images.githubusercontent.com/41882267/89515696-adc29980-d801-11ea-8b39-a181dd2b3bfc.png)


Sau khi sửa lỗi, vào lại db bằng lệnh:
```
python3 jok3r.py db
```

![image](https://user-images.githubusercontent.com/41882267/89515878-e6627300-d801-11ea-8088-72a0d6b72da0.png)



Nếu màn hình hiện ra như trên là đã vào db thành công.


- Để tạo mission mới tên "mayhem" trong database, sử dụng lệnh: 
```
mission -a mayhem
```

![image](https://user-images.githubusercontent.com/41882267/89516080-2c1f3b80-d802-11ea-8058-ae3f44aa2181.png)



- Mở một terminal khác. Để tiến hành chạy tất cả các security check đối với một URL trong chế độ tương tác và thêm kết quả vào mission "mayhem" bằng lệnh: 
```
python3 jok3r.py attack -t https://www.example.com/ --add2db mayhem
```

![image](https://user-images.githubusercontent.com/41882267/89516402-9637e080-d802-11ea-9c6f-f1f582ea22a0.png)


- Y/n để đồng ý/từ chối bắt đầu tấn công mục tiêu:

![image](https://user-images.githubusercontent.com/41882267/89516528-bff10780-d802-11ea-81f9-3c79ad1163a8.png)

- Phần mềm sẽ sử dụng các tool được cài sẵn trong quá trình kiểm tra. Mỗi khi sử dụng hệ thống sẽ hỏi người sử dụng.
<br/>
y = Yes
<br/>
n = No
<br/>
f = Switch to fast mode (do not prompt anymore) 
<br/>
q = Quit the program
<br/>
Mặc định Enter là yes
<br/>
![image](https://user-images.githubusercontent.com/41882267/89516745-05add000-d803-11ea-94f9-c332c0765799.png)

- Khi quá trình quét hoàn tất:


![image](https://user-images.githubusercontent.com/41882267/89516887-3130ba80-d803-11ea-95da-049ea898bd3e.png)

- Tạo file HTML report cho mission được chọn bằng lệnh:
```
report
```

![image](https://user-images.githubusercontent.com/41882267/89517066-6937fd80-d803-11ea-9fac-1ec6bbb8ddac.png)


- File results-93.184.216.34-443-http-1.html vừa được tạo có dạng như sau. 
<br/>
Bên trái file là các thẻ Services, Hosts, Web Interface, Specific Options, Products, Credentials, Vulnerabilities

![image](https://user-images.githubusercontent.com/41882267/89517175-8d93da00-d803-11ea-96dd-5fa89482dfdb.png)


- Chọn vào hàng trong bảng để xem chi tiết kết quả quét của các công cụ:
![image](https://user-images.githubusercontent.com/41882267/89517245-a4d2c780-d803-11ea-9ce6-c8f6accd33be.png)



### Một số lệnh khác <a name="commands"></a>


#### Thao tác quản lý với toolbox <a name="toolbox-management"></a>
- Hiển thị tất cả tool trong toolbox bằng: 
```
python3 jok3r.py toolbox --show-all
```


- Tự động cài đặt tất cả tool trong toolbox: 
```
python3 jok3r.py toolbox --install-all --auto
```


- Update tất cả các tool trong toolbox và hỏi khi update từng tool: 
```
python3 jok3r.py toolbox --update-all
```


- Update tự động tất cả các tool trong toolbox mà không hỏi: 
```
python3 jok3r.py toolbox --update-all --auto
```


- Liệt kê các service được hỗ trợ:
```
python3 jok3r.py info --services
```


- Hiển thị kiểm tra bảo mật với một service nhất định:
```
python3 jok3r.py info --checks <service>
```


- Hiển thị hồ sơ tấn công được hỗ trợ cho một service nhất định:
```
python3 jok3r.py info --attack-profiles <service>
```


- Hiển thị các product được hỗ trợ cho tất cả các service:
```
python3 jok3r.py info --products
```


#### Thao tác với database <a name="database-management"></a>
- Vào thư mục jok3r, sử dụng nmap để quét mạng 192.168.182.0/24 và lưu kết quả vào file result1.xml bằng lệnh:
```
sudo nmap 192.168.182.0/24 -oX - result1.xml
```

![image](https://user-images.githubusercontent.com/41882267/89518848-b1f0b600-d805-11ea-9d6a-4d659bb5ddbd.png)


- Nếu bị lỗi Failed to resolve "result1.xml" thì có thể sử dụng lệnh:
```
sudo nmap 192.168.182.0/24 -oX - result1.xml > result1.xml
```

![image](https://user-images.githubusercontent.com/41882267/89519296-53780780-d806-11ea-80fe-a60256170876.png)


- Để import file result1.xml vào database. Chuyển qua terminal đang mở db và sử dụng lệnh:
```
nmap result1.xml
```


![image](https://user-images.githubusercontent.com/41882267/89519467-9cc85700-d806-11ea-9f69-a402c688db3f.png)


- Kiểm tra các host bằng lệnh: 
```
hosts
```
![image](https://user-images.githubusercontent.com/41882267/89519678-f2046880-d806-11ea-812f-618bea9513a0.png)


- Kiểm tra các service bằng lệnh: 
```
services
```
![image](https://user-images.githubusercontent.com/41882267/89519752-0c3e4680-d807-11ea-9b04-6e12c3dad16a.png)


- Kiểm tra các product bằng lệnh: 
```
products
```
![image](https://user-images.githubusercontent.com/41882267/89519897-490a3d80-d807-11ea-9679-a0933f8fe6c7.png)


- Kiểm tra các credential bằng lệnh: 
```
creds
```
![image](https://user-images.githubusercontent.com/41882267/89520048-7f47bd00-d807-11ea-98cd-fdb6be5f056a.png)


- Tìm kiếm bằng chuỗi trong các kết quả kiểm tra ở mission được chọn:
```
results --search '<search_string>'
```
![image](https://user-images.githubusercontent.com/41882267/89530004-f2f1c600-d817-11ea-8a7a-e28474cdff6a.png)


- Kiểm tra các lỗ hổng bằng lệnh: 
```
vulns
```
![image](https://user-images.githubusercontent.com/41882267/89520194-aef6c500-d807-11ea-8d14-a7c9985b016d.png)




