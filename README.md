
<a href="https://postimg.cc/rKXQqz5n" target="_blank"><img src="https://i.postimg.cc/rKXQqz5n/Clock-configuration.png" alt="
The timer clock was configured with the High speed internal RC oscillator (HSI) The 64Mhz clock was pre-scaled down to 8Mhz

![GPIO config]("C:\Users\kashish\OneDrive\Desktop\Screenshot 2025-01-29 020502.png"?raw=true "GPIO config")

![GPIO config]("C:\Users\kashish\OneDrive\Desktop\Timer config.png"?raw=true "GPIO config")

Configured P in 13 port C with external switch  configured with external interrupt triggered by falling edge , the switch is internally pulled down implying that it’s value will be 0 at reset
Pin 6 port A was configured with alternate function of Timer 3 channel 1 to generate a PWM wave with varying frequency , Timer details
Pre-scaler = 8000-1      frequency =8Mhz/7999= 1 khz
Counter period = 0

Now , for a frequency of say 1Khz , we can change the counter period to 1000-1 , by directly addressing the Time register TIM3->ARR=1000-1 , Counter period value can be changed depending on the frequency required
The interrupt was then enabled in NVIC settings.
Implemented power optimization by calling the Enter_LowPowerMode() function that calls the GPIO_deinit function , this turns off all the oscillators and timers. When the LED is turned off.

