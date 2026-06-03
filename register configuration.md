### This is where all the registers to be configured will be listed.
## Basic microntroller initialization

# Clock
The GPIOA clock enable RCC-> AHB1ENR |=(1<<0);  // GPIOA CLOCK ENABLE
ADC1_CLOCK enable- RCC->APB2ENR |=(1<<8);  // ADC1 enable

# GPIO->ANALOG
GPIOA->MODER|=(0x03<<)|(0x03<<); //Using **ADC1_IN18** to be activated possibly in the ADC registers.

## ADC_Initialization
# ADC_CR1
//Clear bit 24 and bit 25 to get 12bit resolution.
//select scan mode by setting bit 8. Interrupt works only if the   **EOCIE** is selected.
# ADC_CR2
//Bit 11 is cleared for right alignment.

# ADC_SMPR1
//Sampling after 3cycles so we clear the whole register.

# ADC_SMPR2
//Sampling after 3cycles so we clear the whole register.

# ADC_SQR1
//Clear only bits 20-23 so that only one conversion is done on the regular channel conversion sequence.

## ADC_Conversion

# ADC_CR2
// Set ADON and the set SWSTART to turn on ADC and start conversion of regular channels.

# ADC_DR
//Variable= ADC_DR;

# ADC_SR
//Wait for EOC bit1 to be cleared after reading from data register.













