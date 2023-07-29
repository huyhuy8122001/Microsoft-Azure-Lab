# Lab 03 - Khởi tạo virtual network

## Lab scenario
Bài này sẽ tạo ra một virtual network, triển khai hai VMs lên virtual network đó và cấu hình cho phép các VMs ping lẫn nhau bên trong nội bộ virtual network.

## Task 1: Khởi tạo virtual network

1. Đăng nhập vào [Azure portal](https://portal.azure.com).

2. Tại Azure portal, tìm và chọn vào từ khóa **Virtual networks**, sau đó nhấn **+Create**.

3. Ở **Create virtual network** blade, điền vào những thông tin như sau (để defaults những thông tin không được cung cấp):

    | Setting | Value |
    | --- | --- |
    | Subscription | **Chọn vào subscription của bạn** |
    | Resource group | **myRGVNet** (create new) |
    | Virtual network name  | **vnet1** |
    | Location | **(Asia Pacific) Southeast Asia** |
    | Subnet - Name | **default** |
    | Subnet Address range | **10.1.0.0/24** |

    ![image](../media/lab03a.png)

5. Click nút **Review and Create** để bắt đầu quá trình validation.

6. Chọn **Create** để deploy virtual network.


## Task 2: Khởi tạo hai virtual machine
Trong task này, chúng ta sẽ thực hiện khởi tạo hai máy ảo nằm bên trong **vnet1**.

1. Tại Azure portal, tìm và chọn vào từ khóa **Virtual machines**, sau đó nhấn **+Create** > **Azure virtual machine**.

2. Ở tab **Basics**, điền vào những thông tin như sau (để mặc định những trường thông tin khác):

    | Setting | Value |
    | --- | --- |
    | Subscription | **Chọn vào subscription của bạn** |
    | Resource group | **myRGVNet** (create new) |
    | Virtual machine name  | **vm1** |
    | Location | **(Asia Pacific) Southeast Asia** |
    | Image | **Windows Server 2019 Datacenter - x64 Gen2** |
    | Size | **Standard D2s v3** |
    | Administrator account username | **azureuser** |
    | Administrator account password | **VnPro@123456** |
    | Inbound port rules - Allow select ports | **RDP (3389)** |

3. Trong tab **Networking**. Đảm bảo rằng máy ảo được đặt ở vnet1. không thay đổi các giá trị subnet mặc định.

    | Setting | Value |
    | --- | --- |
    | Virtual network | **vnet1** |
    | Public IP | (new) **vm1-ip** |

4. Click **Review + create**. Sau khi quá trình validation đã được pass, click **Create**. Thời gian deploy có thể mất từ 3 - 6 phút.

5. Theo dõi quá trình deploy, đồng thời thực hiện các bước tiếp theo.

6. Khởi tạo máy ảo thứ hai với các bước tương tự như bước **2** đến bước **4**. Chắc chắn rằng bạn sử dụng một cái tên khác cho máy ảo thứ 2, máy ảo này sử dụng cùng virtual network với **vm1** cùng với một địa chỉ IP public mới:

    | Setting | Value |
    | --- | --- |
    | Resource group | **myRGVNet** |
    | Virtual machine name  | **vm2** |
    | Virtual network | **vnet1** |
    | Public IP | (new) **vm2-ip** |

7. Đợi đến khi cả hai máy ảo hoàn thành deploy.


## Task 3: Kiểm tra kết nối giữa 2 VMs
Trong task này, chúng ta sẽ cho phép kết nối ICMP và kiểm tra xem hai máy ảo có thể giao tiếp (ping) với nhau được không.

1. Tại **Azure Portal**, tìm kiếm từ khóa **vm1**, mở **Overview** blade và đảm bảo rằng **Status** của máy ảo là **Running**. Bạn có thể phải cần **Refresh** lại trang.

2. Tại **Overview** blade của virtual machine, nhấn vào biểu tượng **Connect**.

    >**Note**: Hướng dẫn này thực hiện kết nối đến VM từ một máy tính Windows.

3. Ở trang **Connect**, kết nối đến máy ảo bằng địa chỉ IP public và thông qua port 3389 sau đó chọn **Download RDP File**.

4. Mở file RDP mới vừa download và chọn **Connect**.

5. Trong cửa sổ **Windows Security**, chọn **More choices** và sau đó chọn **Use a diffrent account**. Điền username và password đã tạo trước đó. Nhấn **OK** để connect.

6. Bạn có thể sẽ nhận được cảnh báo về certificate trong quá trình sign-in. Chọn **Yes** hoặc tạo security cert và kết nối đếm VM của bạn.

7. Mở PowerShell command prompt trên máy ảo, bằng cách nhân vào nút **Start**, gõ PowerShell, nhấn chuột phải vào biểu tượng **Windows PowerShell**, và chọn **Run as administrator**.

8. Thử ping với **vm2** (chắc chằn rằng vm2 đang running). Bạn sẽ nhận được thông báo lỗi request timed out. `ping` fails, bởi vì `ping` sử dụng **Internet Control Message Protocol (ICMP)**. Mặc định thì Windows firewall sẽ không cho phép ICMP.

    ```powershell
    ping vm2
    ```

    ![image](../media/lab03b.png)

    >**Note**: Bây giờ bạn cần phải mở RDP session đến vm2 và cho phép kết nối incoming ICMP

9. Làm theo bước **2 đến 6** để kết nối tới **vm2** bằng RDP.

10. Tại vm2, mở **PowerShell** và cho phép ICMP. Câu lệnh sau cho phép ICMP inboud connection thông qua Windows firewall.

    ```powershell
    New-NetFirewallRule -DisplayName "Allow ICMPv4-In" -Protocol ICMPv4
    ```

    ![image](../media/lab03c.png)

    >**Note**: Chuyển sáng RDP sesstion của vm1 và thử ping lại lần nữa

11. Quay lại RDP sesstion của vm1 và thử ping lại lần nữa. Bây giờ bạn sẽ thấy `ping` thành công.

   ```powershell
   ping vm2
   ```

   ![image](../media/lab03d.png)

Chúc mừng bạn! Vậy là qua bài lab này, bạn đã cấu hình và deploy hai VMs nằm trong cùng một virtual network. Bạn cũng đã cấu hình Windows firewall để 2 máy ảo có thể ping được tới nhau.

>**Note**: Để tránh lãng phí tài nguyên, bạn có thể xóa resource group sau khi hoàn thành bài lab, nhấn vào resource group, và sau đó chọn **Delete resourse group**. Nhập lại tên của resource group đó rồi nhấn **Delete**. Quan sát **Notification** để chắc chắn rằng bạn đã xóa thành công.


