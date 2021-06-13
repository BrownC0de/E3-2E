### Использование контроллера E3-2E с модулем [5M/3R/5IO](/Shield%205M%5C3R%5C5IO) на кухне

*Не обращайте внимание на внешний вид, это подключение временное (которое в принципе имеет все шансы стать постоянным)*

<img src="/cases/images/kitchen_01.jpg" width="800">


В большинстве квартир кухня обычно граничит с сантехническим шкафом, а заодно и с ванной и  туалетом, и разместив контроллер на кухне - можно одной платой 
контролировать довольно большое количество устройств. 
Я использую контроллер с модулем [5M/3R/5IO](/Shield%205M%5C3R%5C5IO), к которому у меня подключено: 
- Управление вытяжкой
- Управление RGBW светодиодной лентой, которая используется для подсветки рабочей поверхности
- Управление одноцветной лентой, для подсветки шкафов
- Адресная светодиодная лента для подсветки в коридоре
- Датчик движения
- Датчик протечки (Кухня-Ванна-Сантехнический шкаф). Можно каждый датчик на отдельный пин. Можно все на один повесить. 
- Управление электро-кранами, для перекрытия воды
- Снятие показание с водяных счетчиков
- Несколько датчиков температуры Dallas. (Температуру на кухне, температура в ванной, температура горячей воды) 

Контроллер питается от БП на 12вольт, от него же питается светодиодная лента. 
Адресная лента ws2812, для которой нужно +5v - подключена в выход на базовой плате. Если использовать ленты длинною до 3х метров - то штатный DC-DC установленный на плату - справляется, и в общем то не сильно греется. 

### Как подключено 
Что куда подключено

**MainBoard**
|PIN|ТИП|УСТРОЙСТВО|
|---|---|---|
|5|IN|Счетчик холодной воды|
|17|IN|Счетчик горячей воды|
|39|IN|Датчик температуры ds18b20|
|0*|OUT|Адресная светодиодная лента WS2812|
|15|MOSFET|RGBW светодиодная лента. Красный цвет|
|4|MOSFET|RGBW светодиодная лента. Зеленый цвет|
|12|MOSFET|RGBW светодиодная лента. Синий цвет|
|14|MOSFET|RGBW светодиодная лента. Белый цвет|
|15|MOSFET|Белая светодиодная лента|

Пин 0 - можно использовать только при подключении к сети по Wifi. При подключении по проводу он занят LAN портом. 

**Shield 5M/3R/5IO**
|PIN|ТИП|УСТРОЙСТВО|
|---|---|---|
|0_4|Relay|Вытяжка|
|0_5|Relay|Открытие кранов|
|0_6|Relay|Закрытие кранов|
|0_0|IN|Датчик движения|
|0_1|IN|Датчик протечки|
|0_2|IN|Датчик протечки|
|0_3|IN|Датчик протечки|


### Прошивка. Конфигурация EspHome
```yaml
substitutions:
  board: ESP32
  board_name: e3-2e_04 #Указываем свое название платы
  comment: e3-2e 5m\3r\5io

  
esphome:
  name: $board_name
  platform: ESP32
  board: esp-wrover-kit
  comment: $comment


wifi:
  ssid: 'Ваша wifi сеть'
  password: 'Ваш пароль'

  # Enable fallback hotspot (captive portal) in case wifi connection fails
  ap:
    ssid: "${board_name} Fallback Hotspot"
    password: "45678900"

captive_portal:

####Расскоментировать для подключения к сети по LAN кабелю.######
####И не забыть убрать кусок конфига Wifi и captive_portal#######
#ethernet:
#  type: LAN8720
#  mdc_pin: GPIO23
#  mdio_pin: GPIO18
#  clk_mode: GPIO0_IN
#  phy_addr: 1
#  power_pin: GPIO16
#  use_address: 192.168.20.128
#################################################################

# Enable logging
logger:
  level: DEBUG

# Enable Home Assistant API
api:
  reboot_timeout: 0s
ota:

web_server:
  port: 80

switch:
  - platform: restart
    name: "${board_name}_restart"
#########################Shield 3 Relay####################    
  - platform: gpio
    name: "${board_name}_relay_0_5"
    pin:
      pcf8574: pcf8574_3r_5io
      number: 5
      # One of INPUT or OUTPUT
      mode: OUTPUT
      inverted: False   
  - platform: gpio
    name: "${board_name}_relay_0_6"
    pin:
      pcf8574: pcf8574_3r_5io
      number: 6
      # One of INPUT or OUTPUT
      mode: OUTPUT
      inverted: False
  - platform: gpio
    name: "${board_name}_Kitchen airvent"
    pin:
      pcf8574: pcf8574_3r_5io
      number: 4
      # One of INPUT or OUTPUT
      mode: OUTPUT
      inverted: False
            
binary_sensor:
  - platform: status
    name: "${board_name}_status"
  - platform: gpio
    pin: 39
    name: "${board_name}_pin_39"
    device_class: sound     
  - platform: gpio
    pin: 36
    name: "${board_name}_pin_36"
    device_class: vibration     
  - platform: gpio
    pin: 35
    name: "${board_name}_pin_35"
    device_class: motion
  - platform: gpio
    pin: 5
    name: "${board_name} Cold Water"
    filters:
      - delayed_on: 50ms    
  - platform: gpio
    pin: 17
    name: "${board_name} Hot Water"
    filters:
      - delayed_on: 50ms    
#########################Shield 5 IO####################
  - platform: gpio
    name: "${board_name}_pin_0_7"
    pin:
      pcf8574: pcf8574_3r_5io
      number: 7
      # One of INPUT or OUTPUT
      mode: input
      inverted: true
  - platform: gpio
    name: "${board_name}_pin_0_3"
    pin:
      pcf8574: pcf8574_3r_5io
      number: 3
      # One of INPUT or OUTPUT
      mode: input
      inverted: true
  - platform: gpio
    pin: 
      pcf8574: pcf8574_3r_5io
      number: 0
      # One of INPUT or OUTPUT
      mode: input
      inverted: false   
    name: "${board_name}_Kitchen motion"
    device_class: motion
############## Этот кусок кода - включение подсветки по датчику движения###############
#    on_press:
#    - if:
#        condition:
#          lambda: 'return id(some_sensor).state < 30;'
#        then:
#          - logger.log: "The sensor value is below 30!"
#          - light.turn_on: my_light
#          - delay: 5s    
#        then:
#          - light.turn_on:
#              id: led_top_illumination
#              transition_length: 5s
#              brightness: 50%
#    on_release:
#      then:            
#        - light.turn_off: 
#            id: led_top_illumination
#            transition_length: 10s
#######################################################################################
  - platform: gpio
    name: "${board_name}_pin_0_1"
    pin:
      pcf8574: pcf8574_3r_5io
      number: 1
      # One of INPUT or OUTPUT
      mode: input
      inverted: false
  - platform: gpio
    name: "${board_name}_pin_0_2"
    pin:
      pcf8574: pcf8574_3r_5io
      number: 2
      # One of INPUT or OUTPUT
      mode: input
      inverted: true

i2c:
  sda: 33
  scl: 32
  scan: True
  id: i2c_bus    
    
pcf8574:
  - id: 'pcf8574_3r_5io'
    address: 0x20
    pcf8575: False      
    
text_sensor:
  - platform: version
    name: "${board_name}_firmware"
  - platform: template
    name: "${board_name}_uptime_min"
    lambda: |-
      uint32_t uptime = (id(id_uptime).state);
      int minutes = (uptime % 3600) / 60;
      int hours = (uptime % 86400) / 3600;
      int days = uptime / 86400;
      if (days > 0) {
        return { (String(days) + " д." + String(hours) + " ч." + String(minutes) + " мин.").c_str() };
      }
      if (hours > 0) {
        return { (String(hours) + " ч. " + String(minutes) + " мин.").c_str() };
      } else {
        return { (String(minutes) + " мин.").c_str() };
      }
    update_interval: 60s
    icon: mdi:clock-start     
    
sensor: 
  - platform: uptime
    id: id_uptime
    internal: true
    name: "${board_name}_uptime"        
     
output:
#####RGBW STRIP#####
  - platform: ledc
    pin: 15
    id: out_red
  - platform: ledc
    pin: 4
    id: out_green 
  - platform: ledc
    pin: 12
    id: out_blue
  - platform: ledc
    pin: 14
    id: out_white 
#####White strip######
  - platform: ledc
    pin: 2
    id: out_white2  
    
light:
######RGBW STRIP###### 
  - platform: rgbw
    name: "${board_name}_working_area"
    red: out_red
    green: out_green
    blue: out_blue
    white: out_white
    effects:
      - strobe:
          name: Strobe Effect
          colors:
            - state: true
              brightness: 100%
              duration: 600ms
            - state: true
              duration: 600ms
              brightness: 0%
      - flicker:
          name: Flicker Effect With Custom Values
          alpha: 95%
          intensity: 1.5%
      - strobe:
          name: Strobe Effect With Custom Values
          colors:
            - state: True
              brightness: 100%
              red: 100%
              green: 90%
              blue: 0%
              duration: 500ms
            - state: False
              duration: 250ms
            - state: True
              brightness: 100%
              red: 0%
              green: 100%
              blue: 0%
              duration: 500ms    
####### White Strip#######
  - platform: monochromatic
    id: led_top_illumination
    output: out_white2
    name: ${board_name}_top_illumination
    default_transition_length: 1s
###### Adressable Led Strip#####
  - platform: fastled_clockless
    id: ws_led
    chipset: WS2812B
    pin: 0
    num_leds: 240
    rgb_order: BRG
    internal: false
    name: "${board_name}_WS2812_Light"
    effects:
      - addressable_rainbow:
      - addressable_rainbow:
          name: Rainbow Effect With Custom Values
          speed: 10
          width: 50
      - addressable_color_wipe:
      - addressable_color_wipe:
          name: Color Wipe Effect With Custom Values
          colors:
            - red: 100%
              green: 100%
              blue: 100%
              num_leds: 1
            - red: 0%
              green: 0%
              blue: 0%
              num_leds: 1
          add_led_interval: 100ms
          reverse: False
      - addressable_scan:
      - addressable_scan:
          name: Scan Effect With Custom Values
          move_interval: 100ms
          scan_width: 1
      - addressable_twinkle:
      - addressable_twinkle:
          name: Twinkle Effect With Custom Values
          twinkle_probability: 5%
          progress_interval: 4ms
      - addressable_random_twinkle:
      - addressable_random_twinkle:
          name: Random Twinkle Effect With Custom Values
          twinkle_probability: 5%
          progress_interval: 32ms
      - addressable_fireworks:
      - addressable_fireworks:
          name: Fireworks Effect With Custom Values
          update_interval: 32ms
          spark_probability: 10%
          use_random_color: false
          fade_out_rate: 120
      - addressable_flicker:
      - addressable_flicker:
          name: Flicker Effect With Custom Values
          update_interval: 16ms
          intensity: 5%          
      - addressable_lambda:
          name: "Expo Light"
          update_interval: 16ms
          lambda: |-
            static int x = -400;
            float y = 0.35+0.65*exp(-pow(x, 2)/49000);
            int8_t r = ceil(current_color.r * y);
            int8_t g = ceil(current_color.g * y);
            int8_t b = ceil(current_color.b * y);
            it.all() = ESPColor(r,g,b);
            x += 1;
            if (x == 400)
              x = -400;          


          
  - platform: partition
    name: "${board_name}_WS2812_Partition Light 1"
    segments:
      # Use first 10 LEDs from the light with ID light1
      - id: ws_led
        from: 0
        to: 50
  - platform: partition
    name: "${board_name}_WS2812_Partition Light 2"
    segments:
      # Use first 10 LEDs from the light with ID light1
      - id: ws_led
        from: 60
        to: 120
    

```

### Конфигурация для Home-Assistant
**Счетчик воды**
```yaml
В процессе
```
**Автоматическое включение света на кухне**
```yaml
В процессе
```
**Перекрытие кранов с случае протечки**
```yaml
В процессе
```
**Освежитель воздуха**
```yaml
В процессе
```

### Передача показаний воды на портал mos.ru

Позже

### В планах
По сколько контроллер стоит в месте где его не видно, а именно сверху на кухонном шкафу, то корпус я использовать особо не планирую. А раз нет ограничения по высоте, 
то на модуль 5M/3R/5IO сверху установлю еще 12+4io.
Выглядеть это будет следующим образом:

<img src="/cases/images/kitchen_02.jpg" width="1000">

И тем самым получу еще 16 бинарных входов\выходов, 4 из которых с опторазвязкой.

И собственно какой функционал добавиться: 
- 3 Геркона, на двери (ванна\туалет\кухня)
- Датчик движения в Ванну
- Датчик движения туалет
- Автоматизация освежителя AirWick
- Счетчик на фильтр для воды


