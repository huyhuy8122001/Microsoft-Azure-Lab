# Lab 02 - Triển khai Azure Container Instances

## Lab scenario
Trong bài lab này, chúng ta sẽ thực hiện khởi tạo, cấu hình và triển khai Docker container bằng Azure Container Instances (ACI) trên Azure Portal. Container là một ứng dụng web được hiển thị dưới dạng một trang web HTML.

## Task 1: Khởi tạo container instance

Trong task này, chúng ta sẽ tạo ra một container instance chạy ứng dụng web

1. Đăng nhập vào [Azure portal](https://portal.azure.com).

2. Tại Azure portal, tìm và chọn vào từ khóa **Container Instances**, sau đó nhấn **+Create**.

3. Ở tab **Basics**, điền vào những thông tin như sau (để defaults những thông tin không được cung cấp):

    | Setting | Value |
    | --- | --- |
    | Subscription | **Chọn vào subscription của bạn** |
    | Resource group | **myRGContainer** (create new) |
    | Container name  | **mycontainer** |
    | Location | **(Asia Pacific) Southeast Asia** |
    | Image source | **Other registry** |
    | Image type | **Public** |
    | Image | **mcr.microsoft.com/azuredocs/aci-helloworld** |
    | OS type | **Linux** |
    | Size | **Để mặc định** |

4. Cấu hình **Networking** tab (thay thế **xxx** bằng tên mà bạn mong muốn, lưu ý tên này phải là unique). Các giá trị còn lại để mặc định.

    | Setting | Value |
    | --- | --- |
    | DNS name label | **mycontainerdns-xxx** |

    >**Note**: Container của bạn sẽ được truy cập công khai tại địa chỉ url mycontainerdns-xxx.xxxx.region.azurecontainer.io. Nếu bạn nhận được một thông báo lỗi sau **DNS name label not available** trong quá trình triển khai container, thay đổi DNS name label khác và re-deploy. 

    ![image](../media/lab02a.png)

5. Click **Review and Create** để bắt đầu quá trình validation.

6. Chọn **Create** để khởi tạo container instance.

7. Quan sát trang deployment và chuông **Notification**.


## Task 2: Kiểm tra quá trình triển khai của container instance
Task này thực hiện rà soát container instance đang chạy và kiểm tra truy cập trang web.

1. Sau khi hoàn thành quá trình deployment, chọn **Go to resource** link ở trang deployment hoặc trên **Notification** area.

2. Tại **Overview** blade của **mycontainer**, đảm bảo rằng container **Status** là **Running**.

3. Xác định Fully Qualified Domain Name (FQDN).

    ![image](../media/lab02b.png)

4. Copy FQDN của container bỏ vào thanh URL trên web brower và nhấn **Enter**. Welcome page sẽ được hiển thị.

    >**Note**: Bạn cũng có thể dùng địa chỉ IP của container để truy cập brower.

Chúc mừng! Bạn đã sử dụng Azure Portal để triển khai thành công Azure Container Instance.

>**Note**: Để tiết kiệm chi phí, bạn có thể xóa resource group sau khi hoàn thành bài lab, nhấn vào resource group, và sau đó chọn **Delete resourse group**. Nhập lại tên của resource group đó rồi nhấn **Delete**. Quan sát **Notification** để chắc chắn rằng bạn đã xóa thành công.
