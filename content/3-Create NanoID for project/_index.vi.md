---
title : "Tạo NanoID cho dự án"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

Chúng ta cần tạo một id duy nhất (Unique identifier) cho dự án của mình, để không có xung đột nào trong tương lai.

{{% notice tip %}}
Đảm bảo bạn đang ở thư mục gốc của dự án:
{{% /notice %}}

```
mkdir scripts
cd scripts
```
![NanoID](/images/2.Create%20NanoID%20for%20project/NanoID1.png?width=90pc)
![NanoID](/images/2.Create%20NanoID%20for%20project/NanoID2.png?width=90pc)

tạo generate_nanoid.py trong thư mục scripts:
{{% notice info %}}
nhấp chuột phải vào "scripts" -> New file
{{% /notice %}}

hoặc gõ trong console:
````
code generate_nanoid.py
````
![NanoID](/images/2.Create%20NanoID%20for%20project/NanoID3.png?width=90pc)

Viết script tạo nanoid:
````
import nanoid
import nanoid_dictionary as nd

if __name__ == "__main__":
    alphabet = nd.lowercase + nd.numbers
    id = nanoid.generate(alphabet, 10)
    print(id)

````
![NanoID](/images/2.Create%20NanoID%20for%20project/NanoID4.png?width=90pc)


Sau đó chạy:
````
python .\generate_nanoid.py
````
![NanoID](/images/2.Create%20NanoID%20for%20project/NanoID5.png?width=90pc)


{{% notice info %}}
Kết quả: 6aqqepemzy
{{% /notice %}}
````
cd ..
code .env 
````
dán mã nanoid vào file .env:
````
 id=[nanoid của bạn ở đây]
 ````
![NanoID](/images/2.Create%20NanoID%20for%20project/NanoID6.png?width=90pc)

{{% notice tip %}}
Lưu (Ctr + S)
{{% /notice %}}
````
#Kiểm tra id bằng cat:
cat .env
````
![NanoID](/images/2.Create%20NanoID%20for%20project/NanoID7.png?width=90pc)

### Nội dung
<!--
3.1. [Kết nối tới EC2 Public Server](3.1-public-instance/) \
3.2. [Kết nối tới EC2 Private Server](3.2-private-instance/)
-->