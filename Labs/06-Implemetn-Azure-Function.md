# Lab 06 - Triển khai Azure Function

## Lab scenario
Bài lab này chúng ta sẽ thực hiện tạo ra một Function App để hiển thị một đoạn Hello message khi có http request gửi đến.

## Task 1: Khởi tạo Function app

1. Đăng nhập vào [Azure portal](https://portal.azure.com).

2. Tại Azure portal, tìm và chọn vào từ khóa **Function App**, sau đó nhấn **+ Create**.

3. Ở tab **Basics**, điền vào những thông tin như sau (thay thế **xxx** bằng tên mà bạn mong muốn, lưu ý tên này phải là unique):

    | Setting | Value |
    | --- | --- |
    | Subscription | **Chọn vào subscription của bạn** |
    | Resource group | **myRGFunction** (create new) |
    | Function App name  | **function-xxxx** |
    | Do you want to deploy code or container image? | **Code** |
    | Runtime stack | **.NET** |
    | Version | **6 (LTS)** |
    | Regions | **Southeast Asia** |

4. Click **Review + Create**, sau khi hệ thống validate thành công, click **Create**

5. Đợi đến khi thông báo resource đã được tạo thành công.

6. Di chuyển sang **Function App** blade, click **Refresh** để thấy được Function app mới vừa tạo, đảm bảo rằng **Status** đang là **Running**

    ![image](../media/lab06a.png)


## Task 2: Tạo ra một HTTP triggered function và kiểm tra
Trong task này, chúng ta sử dụng Webhook + API function để hiển thị một tin nhắn khi có HTTP request gửi tới.

1. Tại **Function App** blade, chọn function app chúng ta mới tạo.

2. Trong phần **Function**, click **Function** sau đó chọn **+ Add.**. Trong tab **Templates** của function, chọn HTTP trigger.

    ![image](../media/lab06b.png)

3. Kéo xuống phần **Template details**, để nguyên các giá trị mặc định và click **Create**

    ![image](../media/lab06c.png)

4. Tại **HttpTrigger1** blade, trong phần **Developer**, Chọn **Code + Test**.

5. Tại **HttpTrigger1 | Code + Test**, review lại đoạn code được tự động generate và chú ý rằng đoạn code này được design để chạy một HTTP request và thông tin log.

    ![image](../media/lab06d.png)

6. Click **Get function URL** trên cùng của function editor.

    ![image](../media/lab06e.png)

7. Mở tab trình duyệt ra và dán function url vào thanh địa chỉ. Trang web sẽ trả lại một message yêu cầu name trong request body.

    ![image](../media/lab06f.png)

8. Chèn `&name=yourname` vào cuổi URL.

    >**Note**: Thay thế **yourname** bằng tên của bạn
    
    ```
    https://function-vnpro.azurewebsites.net/api/HttpTrigger1?code=_JdCFAugGYNrFYQNMXSDJpfvaivvRvFG5tuWzuo3uCF2AzFuWuVnPQ==&name=vnpro
    ```

    ![image](../media/lab06g.png)

9. Để quan sát các gói khi function của bạn run, quay lại **HttpTrigger1 | Code + Test** và click **Monitor**

    ![image](../media/lab06h.png)

Chúc mừng! Bạn đã hoàn thành tạo ra một Function App để hiển thị Hello message khi có request được gửi đến.

>**Note**: Để tránh lãng phí tài nguyên, bạn có thể xóa resource group sau khi hoàn thành bài lab, nhấn vào resource group, và sau đó chọn **Delete resourse group**. Nhập lại tên của resource group đó rồi nhấn **Delete**. Quan sát **Notification** để chắc chắn rằng bạn đã xóa thành công.
