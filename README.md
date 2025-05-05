# FreeRTOS và Multitask

Xử lý đa nhiệm với hệ điều hành thời gian thực RTOS
\
> Nội dung trong học phần Hệ nhúng, phần __FreeRTOS và TouchGFXFreeRTOS và TouchGFX__

## Hoạt động

2 đèn led có sẵn trên board sẽ nháy sáng với chu kì và hiệu ứng khác nhau.

## Kết nối STM32F429 với ngoại vi

Sử dụng led sẵn có. Không thêm module phụ trợ.

|Dev Kit STM32F429zIT6-DISC1|
|:--|
|LD3 xanh / PG13 |
|LD4 đỏ / PG14 |

## Các bước lập trình

1. Tạo dự án mới.
2. Mở file __.ioc__, cấu hinh các chân __PG13, PG14__ (tương ứng với đèn led LD3, LD4) ở mode __GPIO Output__.\
   ![alt text](./assets/LD3_LD4_Out.png)
   > Ở dòng cuối hình minh họa, đặt tên nhãn gợi nhớ __User Label = LD3__ để khi lập trình sẽ sử dụng define __LD3_Pin__ dễ hiểu hơn. Tương tự với __LD4__.

## Kết quả
