properties ([[$class: 'ParametersDefinitionProperty', parameterDefinitions: [
  [$class: 'StringParameterDefinition', name: 'mbed_os_revision', defaultValue: '', description: 'Revision of mbed-os to build. Use format "pull/PR-NUMBER/head" to access mbed-os PR']
  ]]])

if (params.mbed_os_revision == '') {
  echo 'Use mbed OS revision from mbed-os.lib'
} else {
  echo "Use mbed OS revisiong ${params.mbed_os_revision}"
  if (params.mbed_os_revision.matches('pull/\\d+/head')) {
    echo "Revision is a Pull Request"
  }
}

// List of targets with supported RF shields to compile
def targets = [
  "UBLOX_EVK_ODIN_W2",
  "K64F",
  "NUCLEO_F429ZI"
  ]

// Map toolchains to compilers
def toolchains = [
  ARM: "armcc",
  GCC_ARM: "arm-none-eabi-gcc",
  IAR: "IAR-linux"
  ]

def stepsForParallel = [:]

// Jenkins pipeline does not support map.each, we need to use oldschool for loop
for (int i = 0; i < targets.size(); i++) {
    for(int j = 0; j < toolchains.size(); j++) {
          def target = targets.get(i)
          def toolchain = toolchains.keySet().asList().get(j)
          def compilerLabel = toolchains.get(toolchain)

          def stepName = "${target} ${toolchain}"
          stepsForParallel[stepName] = buildStep(target, compilerLabel, toolchain)
    }
}

timestamps {
  parallel stepsForParallel
}

def buildStep(target, compilerLabel, toolchain) {
  return {
    stage ("${target}_${compilerLabel}") {
      node ("${compilerLabel}") {
        deleteDir()
        dir("mbed-os-example-socket") {
          checkout scm

          // Set mbed-os to revision received as parameter
          execute ("mbed deploy --protocol ssh")
          if (params.mbed_os_revision != '') {
            dir ("mbed-os") {
              if (params.mbed_os_revision.matches('pull/\\d+/head')) {
                execute("git fetch origin ${params.mbed_os_revision}:PR")
                execute("git checkout PR")
              } else {
                execute ("git checkout ${params.mbed_os_revision}")
              }
            }
          }
          execute("mbed new .")
          execute ("mbed compile --build out/${target}_${toolchain}/ -m ${target} -t ${toolchain}")
        }
        stash name: "${target}_${toolchain}", includes: '**/mbed-os-example-socket.bin'
        archive '**/mbed-os-example-socket.bin'
        step([$class: 'WsCleanup'])
      }
    }
  }
}

def IOTC_TLS_LIB_MBEDTLS
def MBEDTLS_PLATFORM_MEMORY
def IOTC_DEBUG_OUTPUT=1
def IOTC_DEBUG_ASSERT=1
def IOTC_DEBUG_EXTRA_INFO=1
def IOTC_FS_MEMORY
def IOTC_PLATFORM_BASE_POSIX
def IOTC_PLATFORM_IS_MBED
def IOTC_MULTI_LEVEL_DIRECTORY_STRUCTURE
def IOTC_LIBCRYPTO_AVAILABLE
def MBEDTLS_PLATFORM_TIME_TYPE_MACRO=long\ long
def IOTC_MULTI_LEVEL_DIRECTORY_STRUCTURE

// translated from Google Make system
def __ASSERT_MSG -std=gnu99 
def TARGET_PSA 
def COMPONENT_SD=1 
def DEVICE_EMAC=1 
def __MBED__=1 
def DEVICE_I2CSLAVE=1 
def __FPU_PRESENT=1 
def TARGET_Freescale 
def DEVICE_PORTINOUT=1 
def TARGET_RTOS_M4_M7 
def COMPONENT_FLASHIAP=1 
def DEVICE_RTC=1 
def COMPONENT_PSA_SRV_EMUL=1 
def DEVICE_SERIAL_ASYNCH=1 
def __CMSIS_RTOS 
def MBED_BUILD_TIMESTAMP=1548998225.02 
def TOOLCHAIN_ARMC6 
def FSL_RTOS_MBED 
def TARGET_KPSDK_MCUS 
def DEVICE_USTICKER=1 
def DEVICE_CRC=1 
def TARGET_CORTEX_M 
def TARGET_KSDK2_MCUS 
def TARGET_LIKE_CORTEX_M4 
def DEVICE_ANALOGOUT=1 
def TARGET_M4 
def TARGET_K64F 
def COMPONENT_PSA_SRV_IMPL=1 
def DEVICE_STORAGE=1 
def DEVICE_LPTICKER=1 
def DEVICE_PWMOUT=1 
def DEVICE_SPI_ASYNCH=1 
def DEVICE_INTERRUPTIN=1 
def TARGET_Freescale_EMAC 
def TARGET_CORTEX 
def DEVICE_I2C=1 
def DEVICE_PORTOUT=1 
def __CORTEX_M4 
def DEVICE_STDIO_MESSAGES=1 
def CPU_MK64FN1M0VMD12 
def TARGET_LIKE_MBED 
def TARGET_FF_ARDUINO 
def TARGET_KPSDK_CODE 
def TARGET_RELEASE 
def COMPONENT_NSPE=1 
def DEVICE_SERIAL_FC=1 
def FEATURE_STORAGE=1 
def MBEDTLS_PSA_CRYPTO_C 
def DEVICE_TRNG=1 
def __MBED_CMSIS_RTOS_CM 
def DEVICE_SLEEP=1 
def TARGET_FRDM 
def TARGET_MCUXpresso_MCUS 
def DEVICE_SPI=1 
def TOOLCHAIN_ARM_STD 
def DEVICE_SPISLAVE=1 
def DEVICE_ANALOGIN=1 
def DEVICE_SERIAL=1 
def DEVICE_FLASH=1 
def DEVICE_PORTIN=1 
def TOOLCHAIN_ARM 
def TARGET_MCU_K64F 
def ARM_MATH_CM4 -nostdinc  -c --target=arm-arm-none-eabi -mthumb -g -O1   
def MULADDC_CANNOT_USE_R7 -fdata-sections -fno-exceptions  
def _LIBCPP_EXTERN_TEMPLATE(...)= -fshort-enums -fshort-wchar -mcpu=cortex-m4 -mfpu=fpv4-sp
def 16 -mfloat-abi=hard 
def __ASSERT_MSG -std=gnu99 
def MBED_ROM_START=0x0 
def MBED_ROM_SIZE=0x100000 
def MBED_RAM_START=0x20000000 
def MBED_RAM_SIZE=0x30000 
def MBED_RAM1_START=0x1fff0000 
def MBED_RAM1_SIZE=0x10000