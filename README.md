# Taller de Sistemas Embebidos

```console
.
|-- app
|   |-- inc
|   |   |-- app_commented_read.me
|   |   |-- app.h
|   |   |-- board.h
|   |   |-- dwt.h
|   |   |-- logger.h
|   |   |-- systick.h
|   |   |-- task_a.h
|   |   |-- task_b.h
|   |   `-- task_c.h
|   |-- src
|   |   |-- app.c
|   |   |-- app_commented_read.me
|   |   |-- logger.c
|   |   |-- systick.c
|   |   |-- task_a.c
|   |   |-- task_a_commented_read.me
|   |   |-- task_b.c
|   |   |-- task_b_commented_read.me
|   |   `-- task_c.c
|   |-- app.txt
|   |-- readme.txt
|   `-- task_x.txt
|-- Core
|   |-- Inc
|   |   |-- main.h
|   |   |-- stm32f1xx_hal_conf.h
|   |   `-- stm32f1xx_it.h
|   |-- Src
|   |   |-- main.c
|   |   |-- stm32f1xx_hal_msp.c
|   |   |-- stm32f1xx_it.c
|   |   |-- syscalls.c
|   |   |-- sysmem.c
|   |   `-- system_stm32f1xx.c
|   `-- Startup
|       `-- startup_stm32f103rbtx.s
|-- Debug
|   |-- app
|   |   `-- src
|   |-- Core
|   |   |-- Src
|   |   `-- Startup
|   |-- Drivers
|   |   `-- STM32F1xx_HAL_Driver
|   |-- makefile
|   |-- objects.list
|   |-- objects.mk
|   |-- sources.mk
|   |-- tdse-tp0_03-hw_sw_test.elf
|   |-- tdse-tp0_03-hw_sw_test.list
|   `-- tdse-tp0_03-hw_sw_test.map
|-- Drivers
|   |-- CMSIS
|   |   |-- Device
|   |   |-- Include
|   |   `-- LICENSE.txt
|   `-- STM32F1xx_HAL_Driver
|       |-- Inc
|       |-- Src
|       `-- LICENSE.txt
|-- README.md
|-- STM32F103RBTX_FLASH.ld
|-- tdse-tp0_03-hw_sw_test.cfg
|-- tdse-tp0_03-hw_sw_test.ioc
`-- tdse-tp0_03-hw_sw_test.launch

23 directories, 45 files
```

## Archivo `Core/Startup/startup_stm32f103rbtx.s`

Esta escrito en arm assembly y se ejecuta al resetear el microcontrolador, el
propósito es inicializar los registros principales (como el stack pointer o el
program counter) la memoria y periféricos, para finalmente transferir el
control a la aplicación principal, la cual el punto de entrada es la función
`main()`, esto se puede ver en la linea 100 del archivo, en la cual se ejecuta
una instrucción `bl` (branch with link) y luego el símbolo `main`. El único tipo
de dato utilizado es `word` que representa una variable de 4 bytes (o 32 bits).

## Archivo `Core/Src/main.c`

El archivo `main.c` es un archivo escrito en C que contiene el punto de entrada
del programa principal, este punto de entrada es invocado al momento de
inicializar el microcontrolador, como se mencionó previamente. El patrón de
diseño de este archivo es procedural, ya que la ejecución del programa se lleva
a cabo mediante la invocación de diferentes funciones o subrutinas.

Los métodos que se encuentran en este archivo además de la (función principal
`main`) son: `initialise_monitor_handles`, `HAL_Init`, `SystemClock_Config`,
`MX_GPIO_Init`, `MX_USART2_UART_Init`, `app_init`, `app_update`,
`Error_Handler`.

## Archivo `Core/app/app.c`

En este archivo se definen las funciones `app_init`,`app_update` que se invocan
en la función `main`, y el callback `HAL_SYSTICK_Callback`, este ultimo es
llamado automáticamente 
