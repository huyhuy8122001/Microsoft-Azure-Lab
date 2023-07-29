# Lab 06 - Khởi tạo một Virtual Machine bằng PowerShell

## Lab scenario
Trong bài hướng dẫn này, chúng ta sẽ sử dụng Azure Powershell module để tạo ra một resource group và virtual machine

## Task 1: Khởi tạo Function app

1. Đăng nhập vào [Azure portal](https://portal.azure.com).

2. Tại Azure portal, mở **Azure Cloud Shell** bằng cách nhấn vào biểu tượng trên cùng bên phải của Azure Portal.

    ![image](../media/lab07a.png)

3. Nếu bạn chưa từng sử dụng Cloud Shell trước đó, chọn **Create storage** và đợi Azure Cloud Shell khởi tạo cho chúng ta.

## Task 2: Khởi tạo resource group và virtual machine

1. Bạn hãy chọn vào **PowerShell** ở góc trái của trình Cloud Shell.

2. Trong PowerShell session, tạo ra một resource group mới.

   ```powershell
   New-AzResourceGroup -Name myRGPS -Location SouthEastAsia
   ```

3. Xác nhận lại resource group của bạn.

   ```powershell
   Get-AzResourceGroup | Format-Table
   ```

4. Tạo ra một virtual machine. Trình Cloud Shell sẽ yêu cầu bạn cung cấp username(**azureuser**) và password(**VnPro@123456**) của máy ảo.

   ```powershell
    New-AzVm `
    -ResourceGroupName 'myRGPS' `
    -Name 'myVMPS' `
    -Location 'South East Asia' `
    -VirtualNetworkName 'myVnetPS' `
    -SubnetName 'mySubnetPS' `
    -SecurityGroupName 'myNetworkSecurityGroup' `
    -PublicIpAddressName 'myPublicIpAddressPS' `
    -OpenPorts 80,3389
   ```
5. Tắt Powershell session, chuyển sang **Virtual Machine** và thấy rằng **myVMPS** đã **running**. Có thể mất vài phút để thấy được máy ảo.

6. Truy cập máy ảo và review lại các thông tin đã được cấu hình đúng hay chưa.

## Task 3: Thực thi lệnh bên trong Cloud Shell
Task này sẽ thực hành thực thi các dòng lệnh bên trong Cloud Shell.

1. Tại Azure portal, mở **Azure Cloud Shell** bằng cách nhấn vào biểu tượng trên cùng bên phải của Azure Portal.

2. Chọn vào **PowerShell** ở góc trái của trình Cloud Shell.

3. Lấy thông tin về virtual machine bao gồm name, resource group, location, and status.

   ```powershell
   Get-AzVM -name myVMPS -status | Format-Table -autosize
   ```

4. Stop virtual machine. xác nhận (Yes) để thực hiện hành động.

   ```powershell
   Stop-AzVM -ResourceGroupName myRGPS -name myVMPS
   ```

5. Xác nhận tình trạng máy ảo của bạn. Bây giờ tình trạng sẽ là **deallocated**

   ```powershell
   Get-AzVM -name myVMPS -status | Format-Table -autosize
   ```

Chúc mừng! Bạn đã hoàn thành tạo ra VM và Resource group bằng cách sử dụng PowerShell.

>**Note**: Để tránh lãng phí tài nguyên, bạn có thể xóa resource group sau khi hoàn thành bài lab, nhấn vào resource group, và sau đó chọn **Delete resourse group**. Nhập lại tên của resource group đó rồi nhấn **Delete**. Quan sát **Notification** để chắc chắn rằng bạn đã xóa thành công.