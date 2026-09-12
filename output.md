# Automatic Sensor-Based LED Control System Using STM32

## Aim

To interface a digital sensor with an STM32 microcontroller and automatically control an LED according to the sensor output.

## Apparatus Required

| S. No. | Component | Quantity |
|---:|---|---:|
| 1 | STM32 development board | 1 |
| 2 | Digital sensor or push button | 1 |
| 3 | LED | 1 |
| 4 | 220–330 Ω resistor | 1 |
| 5 | Breadboard | 1 |
| 6 | Jumper wires | As required |
| 7 | USB cable | 1 |

## Algorithm
Step 1: Start the program.

Step 2: Initialize the STM32 GPIO pins.

Step 3: Configure the LDR sensor input pin as an ADC input.

Step 4: Configure the LED pin as a digital output.

Step 5: Start the ADC and read the LDR sensor value.

Step 6: Compare the sensor value with a predefined threshold.

Step 7:

If the ambient light level is low, turn ON the LED.
If the ambient light level is high, turn OFF the LED.

Step 8: Repeat the sensor reading and LED control continuously.

Step 9: Stop.


## Program
    #include "main.h"

    ADC_HandleTypeDef hadc1;

    #define LIGHT_THRESHOLD 2000

    uint32_t ldr_value;

    int main(void)
    {
    HAL_Init();
    SystemClock_Config();

    MX_GPIO_Init();
    MX_ADC1_Init();

    while (1)
    {
        /* Start ADC */
        HAL_ADC_Start(&hadc1);

        /* Wait for ADC conversion */
        HAL_ADC_PollForConversion(&hadc1, HAL_MAX_DELAY);

        /* Read LDR value */
        ldr_value = HAL_ADC_GetValue(&hadc1);

        /* Stop ADC */
        HAL_ADC_Stop(&hadc1);

        /* Automatic LED control */
        if (ldr_value < LIGHT_THRESHOLD)
        {
            HAL_GPIO_WritePin(GPIOA, GPIO_PIN_5, GPIO_PIN_SET);
        }
        else
        {
            HAL_GPIO_WritePin(GPIOA, GPIO_PIN_5, GPIO_PIN_RESET);
        }

        HAL_Delay(100);
    }
    }  



## Result

The digital sensor was successfully interfaced with the STM32 microcontroller. The LED connected to `PA5` turned ON when the sensor input at `PA0` was HIGH and turned OFF when the sensor input was LOW.
