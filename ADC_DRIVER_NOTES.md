# Analog to Digital Conversion (ADC) STM32F7

---

## 1. Overview
The STM32F7 ADC input clock is generated from the **PCLK2** clock divided by a prescaler. The maximum frequency must not exceed **14 MHz**.

### ADC Block Diagram
![ADC Block Diagram](./docs/images/Blank%20board.png)
*Visual representation of the ADC architecture. See also the [original VSDM diagram](./docs/images/ADC_BLOCK%20DIAGRAM.vsdm).*

---

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

## 4. Configuration Requirements
For our driver implementation, we will use the following settings:
1. **12-bit Resolution**
2. **Single Mode**

---

## 5. Channel Selection
There are **16 multiplexed channels**. Conversions can be organized into two groups:
- **Regular Group:** Up to 16 conversions. The sequence and order are defined in the `ADC_SQRx` registers. The total number of conversions must be specified in the **L[3:0]** bits of `ADC_SQR1`.
- **Injected Group:** Used for higher-priority conversions.

A sequence can include any channel in any order (e.g., `ADC_IN3`, `ADC_IN8`, `ADC_IN2`, `ADC_IN2`, `ADC_IN0`).

---

## 6. Single Conversion Mode
In **Single Conversion Mode**, the ADC performs one conversion and then stops. This mode is active when the **CONT** bit is set to `0`.

### Execution
It can be triggered by:
- Setting the **SWSTART** bit in the `ADC_CR2` register (Regular channels).
- Setting the **JSWSTART** bit (Injected channels).
- External triggers.

### Completion
Once the conversion is finished:
- **Regular Channels:**
  - Data is stored in the 16-bit `ADC_DR` register.
  - The **EOC** (End of Conversion) flag is set.
  - An interrupt is generated if **EOCIE** is enabled.
- **Injected Channels:**
  - Data is stored in the 16-bit `ADC_JDR1` register.
  - The **JEOC** (End of Conversion Injected) flag is set.
  - An interrupt is generated if **JEOCIE** is enabled.

---

## References
For more detailed information, refer to the official documentation:
- [RM0385 Reference Manual - STM32F75xxx and STM32F74xxx (Online)](https://www.st.com/resource/en/reference_manual/rm0385-stm32f75xxx-and-stm32f74xxx-advanced-armbased-32bit-mcus-stmicroelectronics.pdf)
- [STM32F722 Datasheet (Online)](https://www.st.com/resource/en/datasheet/stm32f722ze.pdf)
- [Local Documentation Backup](./docs/external/)
