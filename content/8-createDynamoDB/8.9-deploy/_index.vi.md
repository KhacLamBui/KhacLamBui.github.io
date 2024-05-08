---
title : " Thực hiện deploy để kiểm thử"
date :  "`r Sys.Date()`" 
weight : 9
chapter : false
pre : " <b> 8.9 </b> "
---

#### Thực hiện deploy để kiểm thử"

1. Trong **productsservice** project chúng ta chọn biểu tượng **Grade** và chọn **jar** để đóng gói project

   ![Architect](/images/8/createRepositories/21.png?featherlight=false&width=60pc)

2. Tiếp theo chúng ta cần tạo một image mới. Mở **DockerFile** chọn **Edit dockerfile**

   ![Architect](/images/8/createRepositories/22.png?featherlight=false&width=60pc)

3. Trong giao diện **Edit Dockerfile**. Thay đổi image tag là 1.1.0 để tạo một Docker image mới sau chọn chọn **Run**

   ![Architect](/images/8/createRepositories/23.png?featherlight=false&width=60pc)

4. Push image vừa tạo lên ECR Repository bằng cách mở **AWS Toolkit** chọn **ERC** và sau đó chọn **productsservice**. Cuối cùng click phải chọn **Push to Repository**

   ![Architect](/images/8/createRepositories/24.png?featherlight=false&width=60pc)

5. Trong popup **Push to ECR** chọn Local image là **productsservice:1.0.0** và **Remote Tag** là **1.1.0** và chọn **Push**

   ![Architect](/images/8/createRepositories/25.png?featherlight=false&width=60pc)

6. Kiểm tra image vừa push trên giao điện **ECR**

   ![Architect](/images/8/createRepositories/26.png?featherlight=false&width=60pc)

7. Mở **FCJ2024_CDK** project. Sau đó mở file **ProductsServiceStack** và thay đổi tag trong phần **fargateTaskDefinition.addContainer** là **```1.1.0```**

   ![Architect](/images/8/createRepositories/27.png?featherlight=false&width=60pc)

8. Tiếp theo, sử dụng **```cdk deploy --all --require-approval never```**

   ![Architect](/images/8/createRepositories/28.png?featherlight=false&width=60pc)

9. Tiếp theo ta cần kiểm tra xem task definition mới của chúng ta có chạy hay không bằng cách mở giao điện **ECS** chọn **CLuster** sau đó chọn **ECommerce** và cuối cùng là chọn **task**

   ![Architect](/images/8/createRepositories/29.png?featherlight=false&width=60pc)

10. Truy cập giao điện DymanoBD để kiểm tra product table đã được tạo hạy chưa

   ![Architect](/images/8/createRepositories/30.png?featherlight=false&width=60pc)

11. Truy cập giao diện API Gateway để xác minh các phương thức đã tạo.

   ![Architect](/images/8/createRepositories/31.png?featherlight=false&width=60pc)

12. Trong giao diện **API Gateway**, hãy điều hướng đến **Giai đoạn** và sao chép **Gọi URL** để kiểm tra API trong Postman.

   ![Architect](/images/8/createRepositories/32.png?featherlight=false&width=60pc)

13. Để thêm sản phẩm bằng phương thức POST, hãy mở Postman và tạo yêu cầu POST với điểm cuối **`Gọi URL/sản phẩm`**.

   ![Architect](/images/8/createRepositories/33.png?featherlight=false&width=60pc)

14. Tiếp theo, truyền tham số bằng cách chọn **Body** và chọn **raw**. Sau đó nhập dữ liệu theo mẫu sau:

    ```json
    {
        "name": "Product1",
        "code": "COD1",
        "model": "Model1",
        "price": 10.50
    }
    ```

    Press **Send** to submit the request. Similarly, you can add more product data.



   ![Architect](/images/8/createRepositories/34.png?featherlight=false&width=60pc)


15.  Tiếp theo chúng ta sẽ lấy tất cả product đã tạo bằng phương thức GET với đường dẫn là  **```Invoke URL/product```**

   ![Architect](/images/8/createRepositories/35.png?featherlight=false&width=60pc)

16. Làm tương tự với các phương thức còn lại.

