# Lab 01 - Tạo máy ảo trên Azure Portal

## Lab scenario
Trong bài lab này, chúng ta sẽ thực hiện khởi tạo một con máy ảo trên Azure portal, sau đó kết nối đến máy ảo đó, cài đặt web server lên máy ảo.

## Task 1: Khởi tạo virtual machine
Trong task này, chúng ta sẽ tạo ra một máy ảo chảy Windows Server 2019 Datacenter.

1. Đăng nhập vào [Azure portal](https://portal.azure.com).

1. Tại Azure portal, tìm và chọn vào từ khóa **Virtual machines**, sau đó nhấn **+Create** > **Azure virtual machine**.

1. Ở tab **Basics**, điền vào những thông tin như sau (để mặc định những trường thông tin không được cung cấp):

    | Setting | Value |
    | --- | --- |
    | Subscription | **Chọn vào subscription của bạn** |
    | Resource group | **myRGVM** (create new) |
    | Virtual machine name  | **myVM** |
    | Location | **(Asia Pacific) Southeast Asia** |
    | Image | **Windows Server 2019 Datacenter - x64 Gen2** |
    | Size | **Standard D2s v3** |
    | Administrator account username | **azureuser** |
    | Administrator account password | **VnPro@123456** |
    | Inbound port rules - Allow select ports | **RDP (3389)** and **HTTP (80)** |

1. Chuyển sang tab **Monitoring**, chọn theo setting sau:
    | Setting | Value |
    | --- | --- |
    | Boot diagnostics | **Disable** |

1. Để mặc định các tab còn lại và sau đó nhấn **Review + create** ở dưới cùng

1. Sau khi hệ thống báo **Validation passed** thì nhấn chọn **Create**. Sẽ mất tầm 5p để Azure deploy VM này cho chúng ta.

1. Bạn sẽ nhận được thông báo thông qua **Notification** area (biểu tượng cái chuông trên cùng của thanh menu)


## Task 2: Kết nối đến virtual machine
Trong task này, chúng ta sẽ thực hiện kết nối tới máy ảo Windows vừa tạo với giao thức RDP

1. Tìm kiếm **myVM** và chọn vào máy ảo của bạn

>**Note**: Bạn cũng có thể sử dụng **Go to resource** link ở trang deployment hoặc trên **Notification** area

2. Tại **Overview** blade của virtual machine, nhấn vào biểu tượng **Connect**.

    ![image](../media/lab01.png)

>**Note**: Hướng dẫn này thực hiện kết nối đến VM từ một máy tính Windows. Trên MacOS, bạn cần một RDP client được cài đặt trên Mac App Store hoặc nếu trên một máy Linux thì bạn có thể sử dụng open source RDP client

3. Ở trang **Connect**, giữ các giá trị mặc định để kết nối đến máy ảo bằng địa chỉ IP public và thông qua port 3389 sau đó chọn **Download RDP File**.

4. Mở file RDP mới vừa download và chọn **Connect**.

    ![image](../media/lab01a.png)

5. Trong cửa sổ **Windows Security**, chọn **More choices** và sau đó chọn **Use a diffrent account**. Điền username và password đã tạo trước đó. Nhấn **OK** để connect.

    ![image](../media/lab01b.png)

6. Bạn có thể sẽ nhận được cảnh báo về certificate trong quá trình sign-in. Chọn **Yes** hoặc tạo security cert và kết nối đếm VM của bạn

    ![image](../media/lab01c.png)

Vậy là bạn đã deploy và kết nối đến máy ảo Windows Server trên Azure thành công!


## Task 3: Cài đặt Web Server role và kiểm tra truy cập đến Web server
Trong task số 3, chúng ta sẽ cài đặt Web Server role lên server này và đảm bảo rằng server có thể hiển thị được trang IIS Welcome mặc định.

1. Mở PowerShell lên bằng cách chọn nút **Start**, gõ **PowerShell**, nhấn chuột phải vào biểu tượng **Windows PowerShell**, và chọn **Run as administrator**

    ![image](../media/lab01d.png)

2. Cài đặt tính năng **Web-Server** trên máy ảo bằng cách chạy lệnh sau trong PowerShell command prompt.

   ```powershell
   Install-WindowsFeature -name Web-Server -IncludeManagementTools
   ```

3. Sau khi hoàn thành cài đặt, thanh **Success** sẽ có giá trị là **True**. Bạn không cần phải khởi động lại máy ảo.

4. Đóng kết nối RDP tới máy ảo và trở lại trang portal, tại phần **Overview** blade, copy địa chỉ IP public của **myVM**, mở thêm một tab brower, dán địa chỉ ip public vào url và nhấn enter để truy cập đến trang web.

    ![image](../media/lab01e.png)

5. Trang welcome IIS Web Server sẻ xuất hiện

    ![image](../media/lab01f.png)

Chúc mừng! bạn đã tạo thành công một web server được truy cập thông qua địa chỉ IP public. Nếu bạn có một ứng dụng web cần được host, bạn hoàn toàn có thể deploy file của ứng dụng và host chúng để mọi người có thể truy cập được.

>**Note**: Để tránh lãng phí tài nguyên, bạn có thể xóa resource group sau khi hoàn thành bài lab, nhấn vào resource group, và sau đó chọn **Delete resourse group**. Nhập lại tên của resource group đó rồi nhấn **Delete**. Quan sát **Notification** để chắc chắn rằng bạn đã xóa thành công.