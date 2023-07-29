# Lab 04 - Khởi tạo blob storage

## Lab scenario
Bài lab này thực hiện tạo ra một SQL database trên Azure và sau đó truy vấn đến dữ liệu bên trong database đó.

## Task 1: Khởi tạo virtual network

1. Đăng nhập vào [Azure portal](https://portal.azure.com).

2. Tại Azure portal, tìm và chọn vào từ khóa **SQL databases**, sau đó nhấn **+ Create**.

3. Trong phần **Basics** tab, điền vào các thông tin sau.

    | Setting | Value |
    | --- | --- |
    | Subscription | **Chọn vào subscription của bạn** |
    | Resource group | **myRGdb** (create new) |
    | Database name  | **db1** |

4. tại dòng **Server** sẽ có một dropdown list, chọn **Create new** và nhập thông tin như sau (thay thế **xxx** bằng tên bạn mong muốn). Click **OK** sau khi hoàn thành.

    | Setting | Value |
    | --- | --- |
    | Server | **sqlserverxxxx**  (must be unique) |
    | Location | **(Asia Pacific) Southeast Asia** |
    | Authentication method | **Use SQL authentication** |
    | Server admin login | **sqluser** |
    | Password | **VnPro@123456** |

    ![image](../media/lab05a.png)

    ![image](../media/lab05b.png)

5. Chuyển sang tab **Networking**, cấu hình như sau
    
    | Setting | Value |
    | --- | --- |
    | Connectivity method | **Public endpoint** |
    | Allow Azure services and resources to access this server | **No** |
    | Add current client IP address | **No** |

    ![image](../media/lab05d.png)

6. Chuyển sang tab **Additional setting**, chúng ta sẽ sử dụng AdvantureWorksLT sample database. 

    | Setting | Value |
    | --- | --- |
    | Use existing data | **Sample** |

7. Click **Review + create** và rồi click **Create** để deploy resource group, server, và database. Quá trình deploy có thể mất 2-5 phút.

8. Theo dõi quá trình deploy.


## Task 2: Test Database
Task này sẽ cấu hình SQL server và khởi chạy truy vấn SQL.

1. Tại Azure portal, tìm và chọn vào **db1** là SQL database mà bạn vừa tạo

2. Sau đó chọn vào **Query editor (preview)** ở thanh menu trái.

3. Đăng nhập dưới tên username **sqluser** và mật khẩu là **VnPro@123456**.

4. Bạn sẽ không thể login vào được. Đọc kỹ vào phần error và bạn cần chú ý vào địa chỉ IP address mà chúng ta sẽ sử dụng để cho phép thông qua firewall.

    ![image](../media/lab05e.png)

5. Sau đó quay lại **db1** blade, ở phần **Overview**, chọn **Set server firewall**

    ![image](../media/lab05f.png)

6. Ở mục **Public access**, kéo xuống phần **Firewall rules** sau đó nhập vào địa chỉ ip chúng ta thấy ở bước trước

    ![image](../media/lab05g.png)

7. Quay trở lại SQL database của bạn vào phần login của **Query editor (preview)**. Thử đăng nhập lại với username và password. Lần này bạn sẽ đăng nhập thành công.

8. Sau khi đăng nhập thành công, mục truy vấn sql sẽ xuất hiện. Nhập câu truy vấn sau vào editor:

   ```sql
    SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
    FROM SalesLT.ProductCategory pc
    JOIN SalesLT.Product p
    ON pc.productcategoryid = p.productcategoryid;
   ```

    ![image](../media/lab05i.png)

9. Chọn **Run**, và sau đó review lại kết quả truy vấn trong phần **Results**.

    ![image](../media/lab05h.png)

Bạn đã hoàn thành lab 05, tạo thành công SQL database trên Azure và truy vấn đến dữ liệu bên trong database đó.

>**Note**: Để tiết kiệm chi phí, bạn có thể xóa resource group sau khi hoàn thành bài lab, nhấn vào resource group, và sau đó chọn **Delete resourse group**. Nhập lại tên của resource group đó rồi nhấn **Delete**. Quan sát **Notification** để chắc chắn rằng bạn đã xóa thành công.