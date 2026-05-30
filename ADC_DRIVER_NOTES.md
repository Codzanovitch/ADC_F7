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
(RCC_APB2ENR).
## What we will use
1.	12 bit resolution
2.	Single mode

# CHANNEL SELECTION
There are 16 multiplexed channels. It is possible to organize the conversions in two groups: regular and injected. A group consists of a sequence of conversions that can be done on any channel and in any order. For instance, it is possible to implement the conversion sequence in the following order: ADC_IN3, ADC_IN8, ADC_IN2, ADC_IN2, ADC_IN0, ADC_IN2, ADC_IN2, ADC_IN15. • A regular group is composed of up to 16 conversions. The regular channels and their order in the conversion sequence must be selected in the ADC_SQRx registers. The total number of conversions in the regular group must be written in the L[3:0] bits in the ADC_SQR1 register.
Single conversion mode In Single conversion mode the ADC does one conversion. This mode is started with the CONT bit at 0 by either: • setting the SWSTART bit in the ADC_CR2 register (for a regular channel only) • setting the **JSWSTART** bit (for an injected channel) • external trigger (for a regular or injected channel) Once the conversion of the selected channel is complete: • If a regular channel was converted: – The converted data are stored into the 16-bit ADC_DR register – The EOC (end of conversion) flag is set – An interrupt is generated if the EOCIE bit is set • If an injected channel was converted: – The converted data are stored into the 16-bit ADC_JDR1 register – The JEOC (end of conversion injected) flag is set – An interrupt is generated if the JEOCIE bit is set Then the ADC stops.
### INITIALIZATION
## SINGLE MODE
In Single conversion mode the ADC does one conversion. This mode is started with the
CONT bit at 0 by either:
• setting the SWSTART bit in the ADC_CR2 register (for a regular channel only)
Once the conversion of the selected channel is complete:
• If a regular channel was converted:
– The converted data are stored into the 16-bit ADC_DR register
– The EOC (end of conversion) flag is set
– An interrupt is generated if the EOCIE bit is set

## CLOCK 

## DATA ALIGNMENT
•The ALIGN bit in ADC_CR2 determines if the data will be right aligned of left aligned. In this case the data will be right aligned.

## ADC_SAMPLING
The ADC samples for for a selected number of ADCCLK cycles. It can be selected for it to sample after 3 clock cycles or 15 clock cycles etc.
The total conversion time becomes Tconv= sampling time + 12clock cycles so if sampling time is 3clock cycles then conversion time becomes 12+3. 
ADC can be made faster by reducing the resolution. The **RES** bit are used to select the number of bits available in the data register.
12 bit Tconv= sampling time + 15cycles.
10 bit Tconv= sampling time + 13cycles
## 
The temperature sensor, VREFINT and the VBAT channel are available only on the master
ADC1 peripheral.






---

## References
For more detailed information, refer to the official documentation:
- [RM0385 Reference Manual - STM32F75xxx and STM32F74xxx (Online)](https://www.st.com/resource/en/reference_manual/rm0385-stm32f75xxx-and-stm32f74xxx-advanced-armbased-32bit-mcus-stmicroelectronics.pdf)
- [STM32F722 Datasheet (Online)](https://www.st.com/resource/en/datasheet/stm32f722ze.pdf)
- [Local Documentation Backup](./docs/external/)
