# Lab 04 - Khởi tạo blob storage

## Lab scenario
Lab này sẽ hướng dẫn chúng ta cách khởi tạo một storage account, và cách làm việc với blob storage files.

## Task 1: Khởi tạo virtual network

1. Đăng nhập vào [Azure portal](https://portal.azure.com).

2. Tại Azure portal, tìm và chọn vào từ khóa **Storage accounts**, sau đó nhấn **+Create**.

3. Trong phần **Basics** tab của **Create storage account** blade, điền vào những thông tin như sau(Thay đổi *xxx* trong phần tên storage account bằng tên bạn mong muốn) .Để mặc định những thông tin không được cung cấp:

    | Setting | Value |
    | --- | --- |
    | Subscription | **Chọn vào subscription của bạn** |
    | Resource group | **myRGStorage** (create new) |
    | Storage account name  | **storageaccountxxx** |
    | Location | **(Asia Pacific) Southeast Asia** |
    | Performance | **Standard** |
    | Redundancy | **Locally redundant storage (LRS)** |

4. Chuyển sang tab **Advanced**

    | Setting | Value |
    | --- | --- |
    | Blob storage | **Hot** |

5. Click **Review** để review lại các thiết lập storage account và cho phép Azure validate cấu hình của chúng ta.

6. sau khi đã validate xong, click **Create**. Đợi đến lúc account được tạo thành công.

7. Từ **Home page**, tìm kiếm và chọn storage account bạn mới vửa tạo.


## Task 2: Làm việc với blob storage
Trong task này, chúng ta thực hiện tạo ra một Blob container và upload một blob file.

1. Click nào tên của storage account vừa mới tạo, kéo xuống mục **Data storage**, và click vào **Containers**. 

2. Chọn **+ Container** và điền thông tin. Sau khi hoàn thành click **OK**.

    | Setting | Value |
    | --- | --- |
    | Name | **container1** |
    | Public access level | **private (no anonymous access)** |

    ![image](../media/lab04a.png)

3. Chọn vào **container1**, rồi click **Upload**.

4. Chọn một file trên máy tính local của bạn.

    >**Note**: Bạn có thể tạo ta một file `.txt` rỗng hoặc sử dụng một file có sẵn. Cân nhắc sử dụng file có size nhỏ để giảm thời gian upload.

5. Chọn vào thanh Advanced, review lại các trường thông tin và click **Upload**. 

    >**Note**: Bạn có thể nhiều blobs khác nhau theo cách này.

6. Sau khi upload xong, chuột phải vòa file và chú ý các option như View/edit, Download, Properties, and Delete.


## Task 3: Giám sát storage account

1. Trở lại **Storage account** blade và chọn **Diagnose and solve problems**.

2. Khám phá một số vấn đề storage phổ biến. Lưu ý rằng ở đây có nhiều trình khắc phục sự cố.

3. Tại **Storage account** blade, kéo xuống phần **Monitoring** và chọn **Insights**. Ở đây có các trường thông tin giúp chúng ta giám sát storage như Failures, Performance, Availability, và Capacity.

    ![image](../media/lab04b.png)

Chúc mừng! Bạn đã hoàn thành tạo ra một storage account, sau đó làm việc với blobs storage.

>**Note**: Để tiết kiệm chi phí, bạn có thể xóa resource group sau khi hoàn thành bài lab, nhấn vào resource group, và sau đó chọn **Delete resourse group**. Nhập lại tên của resource group đó rồi nhấn **Delete**. Quan sát **Notification** để chắc chắn rằng bạn đã xóa thành công.



