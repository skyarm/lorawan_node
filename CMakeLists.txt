# SPDX-License-Identifier: Apache-2.0

# lorawan_node.c depends on the include directories exposed by the loramac-node
# library. Hence, if it exists then the source files are added to that otherwise
# a library with same name is created.

zephyr_library()

zephyr_compile_definitions_ifdef(CONFIG_LORAWAN_NODE_REGION_AS923 REGION_AS923)
zephyr_compile_definitions_ifdef(CONFIG_LORAWAN_NODE_REGION_AU915 REGION_AU915)
zephyr_compile_definitions_ifdef(CONFIG_LORAWAN_NODE_REGION_CN470 REGION_CN470)
zephyr_compile_definitions_ifdef(CONFIG_LORAWAN_NODE_REGION_CN779 REGION_CN779)
zephyr_compile_definitions_ifdef(CONFIG_LORAWAN_NODE_REGION_EU433 REGION_EU433)
zephyr_compile_definitions_ifdef(CONFIG_LORAWAN_NODE_REGION_EU868 REGION_EU868)
zephyr_compile_definitions_ifdef(CONFIG_LORAWAN_NODE_REGION_KR920 REGION_KR920)
zephyr_compile_definitions_ifdef(CONFIG_LORAWAN_NODE_REGION_IN865 REGION_IN865)
zephyr_compile_definitions_ifdef(CONFIG_LORAWAN_NODE_REGION_US915 REGION_US915)
zephyr_compile_definitions_ifdef(CONFIG_LORAWAN_NODE_REGION_RU864 REGION_RU864)
zephyr_compile_definitions_ifdef(CONFIG_LORAWAN_NODE_CLASSB LORAMAC_CLASSB_ENABLED)

zephyr_include_directories(crypto)
zephyr_library_sources(
  crypto/lorawan_aes.c
  crypto/cmac.c
  crypto/soft-se.c
)

zephyr_include_directories(mac)
zephyr_include_directories(mac/Region)
zephyr_library_sources(
  mac/LoRaMac.c
  mac/LoRaMacAdr.c
  mac/LoRaMacClassB.c
  mac/LoRaMacCommands.c
  mac/LoRaMacConfirmQueue.c
  mac/LoRaMacCrypto.c
  mac/LoRaMacParser.c
  mac/LoRaMacSerializer.c
)

zephyr_library_sources(
  mac/Region/Region.c
  mac/Region/RegionCommon.c
)
zephyr_library_sources_ifdef(CONFIG_LORAWAN_NODE_REGION_EU868
  mac/region/RegionEU868.c
)
zephyr_library_sources_ifdef(CONFIG_LORAWAN_NODE_REGION_US915
  mac/Region/RegionBaseUS.c
  mac/Region/RegionUS915.c
)
zephyr_library_sources_ifdef(CONFIG_LORAWAN_NODE_REGION_CN779
  mac/Region/RegionCN779.c
)
zephyr_library_sources_ifdef(CONFIG_LORAWAN_NODE_REGION_EU433
  mac/Region/RegionEU433.c
)
zephyr_library_sources_ifdef(CONFIG_LORAMAC_REGION_AU915
  mac/Region/RegionBaseUS.c
  mac/Region/RegionAU915.c
)
zephyr_library_sources_ifdef(CONFIG_LORAWAN_NODE_REGION_AS923
  mac/Region/RegionAS923.c
)
zephyr_library_sources_ifdef(CONFIG_LORAWAN_NODE_REGION_CN470
  mac/Region/RegionBaseUS.c
  mac/Region/RegionCN470.c
  mac/Region/RegionCN470A20.c
  mac/Region/RegionCN470A26.c
  mac/Region/RegionCN470B20.c
  mac/Region/RegionCN470B26.c
)
zephyr_library_sources_ifdef(CONFIG_LORAWAN_NODE_REGION_KR920
  mac/Region/RegionKR920.c
)
zephyr_library_sources_ifdef(CONFIG_LORAWAN_NODE_REGION_IN865
  mac/Region/RegionIN865.c
)
zephyr_library_sources_ifdef(CONFIG_LORAWAN_NODE_REGION_RU864
  mac/Region/RegionRU864.c
)

zephyr_include_directories(radio)
zephyr_include_directories(radio/stm32_radio_driver)
zephyr_library_sources(
  radio/stm32_radio_driver/radio_driver.c
  radio/stm32_radio_driver/radio.c
  radio/stm32_radio_driver/radio_fw.c
  radio/stm32_radio_driver/lr_fhss_mac.c
  radio/stm32_radio_driver/wl_lr_fhss.c
)

zephyr_include_directories(config)

zephyr_include_directories(sysdep)
zephyr_library_sources(
  sysdep/systime.c
  sysdep/timer.c
  sysdep/rtctime.c
  sysdep/utilities.c
  sysdep/subghz.c
)

zephyr_include_directories(lorawan)
zephyr_library_sources(lorawan/lorawan_node.c)
