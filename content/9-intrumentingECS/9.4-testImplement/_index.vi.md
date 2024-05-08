---
title : "Testing the implementation"
date :  "`r Sys.Date()`" 
weight : 4
chapter : false
pre : " <b> 9.4 </b> "
---

#### Testing the implementation

1. Quay trở là **productsservice** project. Đóng gói project bằng jar trong Grade

   ![Architect](/images/8/createRepositories/71.png?featherlight=false&width=60pc)

2. Mở DockerFile và tạo image tag là **productsservice:1.3.0**

   ![Architect](/images/8/createRepositories/72.png?featherlight=false&width=60pc)

3. Sau khi hoàn thành buid Docker Image. Push nó lên ECR Repository với Remote Tag là **1.3.0**

   ![Architect](/images/8/createRepositories/73.png?featherlight=false&width=60pc)


4. Trở lại **FCJ2024_CDK** project thay đổi image tag của **fargateTaskDefinition.addContainer** là **1.3.0**

   ![Architect](/images/8/createRepositories/74.png?featherlight=false&width=60pc)

5. Deploy service bằng dòng lệnh

```
cdk deploy --all --require-approval never
```

   ![Architect](/images/8/createRepositories/75.png?featherlight=false&width=60pc)

6. Sau khi hoành thành deploy. Chúng ta truy cập vào giao diện **ECS** chọn **Task**. Sau đó chọn 1 task bất kỳ trong 2 task đang chạy.

   ![Architect](/images/8/createRepositories/76.png?featherlight=false&width=60pc)

7. Trong giao diện **task** vừa được chọn. Ta có thể thấy một container phụ (sidecar) tên **XRayProductsService** đang chạy cùng với **productsService** container

   ![Architect](/images/8/createRepositories/77.png?featherlight=false&width=60pc)

8. Tiếp theo chúng ta sẽ test API trên postman để kiểm tra Đo lường dịch vụ AWS ECS trên AWS X-ray

   ![Architect](/images/8/createRepositories/78.png?featherlight=false&width=60pc)

9. Truy cập vào giao diện **CloudWatch** chọn **Trace Map** để xem được đường đi của request

   ![Architect](/images/8/createRepositories/79.png?featherlight=false&width=60pc)

10. Cuối cùng để xem thông tin do lường của ECS chúng ta chọn biểu tượng ECS trên **trace map**

   ![Architect](/images/8/createRepositories/80.png?featherlight=false&width=60pc)

11. Tượng tự với DynamoDB

   ![Architect](/images/8/createRepositories/81.png?featherlight=false&width=60pc)

