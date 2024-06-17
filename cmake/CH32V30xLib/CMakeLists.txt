cmake_minimum_required(VERSION 3.22)

project(CH32V30xLib)
add_library(${PROJECT_NAME} INTERFACE)
enable_language(C ASM CXX)

target_compile_definitions(${PROJECT_NAME} INTERFACE
        $<$<CONFIG:Debug>:DEBUG>
)

target_include_directories(${PROJECT_NAME} INTERFACE
        ../../Core
        ../../Debug
        ../../Peripheral/inc
        ../../User
)

target_sources(${PROJECT_NAME} INTERFACE
        ../../User/main.cpp
        ../../User/ch32v30x_it.c
        ../../User/system_ch32v30x.c
        ../../Peripheral/src/ch32v30x_adc.c
        ../../Peripheral/src/ch32v30x_bkp.c
        ../../Peripheral/src/ch32v30x_can.c
        ../../Peripheral/src/ch32v30x_crc.c
        ../../Peripheral/src/ch32v30x_dac.c
        ../../Peripheral/src/ch32v30x_dbgmcu.c
        ../../Peripheral/src/ch32v30x_dma.c
        ../../Peripheral/src/ch32v30x_dvp.c
        ../../Peripheral/src/ch32v30x_eth.c
        ../../Peripheral/src/ch32v30x_exti.c
        ../../Peripheral/src/ch32v30x_flash.c
        ../../Peripheral/src/ch32v30x_fsmc.c
        ../../Peripheral/src/ch32v30x_gpio.c
        ../../Peripheral/src/ch32v30x_i2c.c
        ../../Peripheral/src/ch32v30x_iwdg.c
        ../../Peripheral/src/ch32v30x_misc.c
        ../../Peripheral/src/ch32v30x_opa.c
        ../../Peripheral/src/ch32v30x_pwr.c
        ../../Peripheral/src/ch32v30x_rcc.c
        ../../Peripheral/src/ch32v30x_rng.c
        ../../Peripheral/src/ch32v30x_rtc.c
        ../../Peripheral/src/ch32v30x_sdio.c
        ../../Peripheral/src/ch32v30x_spi.c
        ../../Peripheral/src/ch32v30x_tim.c
        ../../Peripheral/src/ch32v30x_usart.c
        ../../Peripheral/src/ch32v30x_wwdg.c
        ../../Debug/debug.c
        ../../Core/core_riscv.c
)

if(USE_CPP)
    message("enable cxx toolchain")
    target_sources(${PROJECT_NAME} INTERFACE ../../Startup/startup_ch32v30x_D8.S)
else()
    target_sources(${PROJECT_NAME} INTERFACE ../../Startup/startup_ch32v30x_D8C.S)
endif()

target_link_directories(${PROJECT_NAME} INTERFACE
)

target_link_libraries(${PROJECT_NAME} INTERFACE
)

# Validate that STM32CubeMX code is compatible with C standard
if(CMAKE_C_STANDARD LESS 11)
    message(ERROR "Generated code requires C11 or higher")
endif()

if(CMAKE_CXX_STANDARD LESS 17 AND USE_APP)
    message(ERROR "Generated code requires C++ 17 or higher")
endif()