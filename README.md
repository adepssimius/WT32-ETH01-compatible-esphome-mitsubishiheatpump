# Functional Config Example

```yaml
esphome:
  name: "mini-split-office"
  friendly_name: "Office Mini Split"

esp32:
  board: wt32-eth01
  framework:
    type: arduino

logger:

# Enable Home Assistant API
api:
  encryption:
    key: ...

ota:

uart:
  - id: uart_1
    baud_rate: 4800
    rx_pin: GPIO14
    tx_pin: GPIO15
  - id: uart_2 # I'm unsure if the extra params are necessary for the parity and rx_buffer_size
    rx_pin: GPIO05
    tx_pin: GPIO17
    parity: EVEN
    baud_rate: 2400 # CHECK YOUR BAUD RATE. Mine was 2400, but the default for this library is 4800 and some also use 9600
    rx_buffer_size: 512

external_components:
  - source: github://adepssimius/WT32-ETH01-compatible-esphome-mitsubishiheatpump

climate:
  - platform: mitsubishi_heatpump
    name: "Office"
    update_interval: 500ms
    hardware_uart: UART2
    baud_rate: 2400 # check your baud rate. See notes above.
    visual:
      temperature_step: 1.0

ethernet:
  type: LAN8720
  mdc_pin: GPIO23
  mdio_pin: GPIO18
  clk_mode: GPIO0_IN
  phy_addr: 1
  power_pin: GPIO16
```