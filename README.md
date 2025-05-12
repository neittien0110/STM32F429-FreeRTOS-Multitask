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
3. Mở file __.ioc__ và thiết lập xung nhịp đồng hồ CPU clock rate ở 90 MHz với 2 bước cấu hình như trong ảnh.
   - Kích hoạt __RCC__.\
    ![RCC Enable](./assets/RCCEnable.png)
   - Thiết lập __CPU Clock = 180MHz__.\
    ![Thiết lập CPU Clock](./assets/ClockConfigration_90MHz.png)
4. Vẫn ở file __.ioc__, câu hình __USART1__ ở chế độ __Asynchronous__, tốc độ __baudrate = 115200 bps__.
    ![cấu hình UART kiểu polling](./assets/UART_Enable_NoInterrupt.png)
5. Vẫn ở file __.ioc__, câu hình timer 6__TIM6__ qua 3 bước như sau:
   - Activate TIM6
     ![TIM6 Enable](./assets/TIM_Enable.png)
   - __Prescaler = 89__, __Counter Period = 99__ để có tần số 10kHz. _Xem ảnh trên_.
     ![Prescaler và Counter](./assets/TIM_Prescaler_Counter_10k.png)
6. Ở file __.ioc__,cấu hình __FreeRTOS__ để có thêm __Task__ mới, bênh cạnh __Task__ mặc định của hệ điều hành.
   - Trong __Categories__, chọn __Middleware and Software Packs__, chọn __FREERTOS__. Trong cửa số bên phải __FREERTOS Mode and Configuration__ / phần __Mode__, hãy gán dropdownboax __Interface__ bằng __CMSIS_V2__.
   ![Kích hoạt và Thêm Task mới](./assets/FreeRTOS_RegisterNewTask.png)
   - Ở phần __Configuration__ bên dưới, chọn tab __Tasks and Queues__, bấm __Add__ và khai báo thêm một __Task__ mới như trong ảnh trên.
      - Tên task: myTask
      - Độ ưu tiên: osPriorityNormal
      - Tên hàm handler: StartMyTask

## Kết quả
