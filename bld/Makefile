EXEC = blinker

OBJECTS = \
	main.o \

DEPS += \
	libchain \
	libmsp \
	libio \

CONFIG_EDB ?= 0

export MAIN_CLOCK_FREQ = 8000000

export CLOCK_FREQ_ACLK = 32768
export CLOCK_FREQ_SMCLK = $(MAIN_CLOCK_FREQ)
export CLOCK_FREQ_MCLK = $(MAIN_CLOCK_FREQ)

export LIBMSP_CLOCK_SOURCE = DCO
export LIBMSP_DCO_FREQ = $(MAIN_CLOCK_FREQ)

export LIBMSP_SLEEP_TIMER = B.0.0
export LIBMSP_SLEEP_TIMER_CLK = ACLK
export LIBMSP_SLEEP_TIMER_DIV = 8*1

# To use add: libmspsoftuart to DEPS
#export LIBIO_BACKEND = swuart
#ifeq ($(BOARD_MAJOR),1)
#export LIBMSPSOFTUART_PIN_TX = 3.6
#else ifeq ($(BOARD_MAJOR),2)
#export LIBMSPSOFTUART_PIN_TX = 3.5
#endif # BOARD_MAJOR
#export LIBMSPSOFTUART_BAUDRATE = 9600
#export LIBMSPSOFTUART_CLOCK_FREQ = $(MAIN_CLOCK_FREQ)
#export LIBMSPSOFTUART_TIMER = B.0.5

export LIBIO_BACKEND = hwuart
export LIBMSP_UART_IDX = 0
export LIBMSP_UART_PIN_TX = 2.0
export LIBMSP_UART_BAUDRATE = 115200
export LIBMSP_UART_CLOCK = SMCLK
