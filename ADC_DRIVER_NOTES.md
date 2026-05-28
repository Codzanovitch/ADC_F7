# Analog to Digital Conversion (ADC) STM32F7

---

## 1. Overview
The STM32F7 ADC input clock is generated from the **PCLK2** clock divided by a prescaler. The maximum frequency must not exceed **14 MHz**.

For a visual representation of the ADC architecture, refer to the [ADC Block Diagram](./docs/images/ADC_BLOCK%20DIAGRAM.vsdm).

## 2. Power Control
The ADC is managed via the **ADON** bit in the `ADC_CR2` register:
- **Power On:** Setting the **ADON** bit for the first time wakes the ADC from Power-down mode.
- **Start Conversion:** Conversion begins when either the **SWSTART** or **JSWSTART** bit is set.
- **Power Down:** Clearing the **ADON** bit stops conversion and puts the ADC into power-down mode. In this state, the ADC consumes minimal power (only a few μA).

## 3. Clock Configuration
The ADC utilizes two distinct clocks:

- **Analog Circuitry Clock (ADCCLK):** Common to all ADCs. This clock is generated from the **APB2** clock divided by a programmable prescaler (`/2`, `/4`, `/6`, or `/8`). Refer to the datasheets for the maximum value of **ADCCLK**.
- **Digital Interface Clock:** Used for register read/write access. This clock is equal to the **APB2** clock. It can be enabled or disabled individually for each ADC through the `RCC_APB2ENR` (RCC APB2 peripheral clock enable register).

---

## References
For more detailed information, refer to the official documentation:
- [RM0385 Reference Manual - STM32F75xxx and STM32F74xxx (Online)](https://www.st.com/resource/en/reference_manual/rm0385-stm32f75xxx-and-stm32f74xxx-advanced-armbased-32bit-mcus-stmicroelectronics.pdf)
- [STM32F722 Datasheet (Online)](https://www.st.com/resource/en/datasheet/stm32f722ze.pdf)
- [Local Documentation Backup](./docs/external/)
