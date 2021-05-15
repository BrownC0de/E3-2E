# E3-2E Universal system to control your home. 
[![Donate](https://img.shields.io/badge/donate-Coffee-yellow.svg)](https://www.buymeacoffee.com/BrownCode)
[![Donate](https://img.shields.io/badge/donate-Yandex-red.svg)](https://money.yandex.ru/to/)


Многофункциональный модульный контроллер для домашней автоматизации, на основе ESP32 с Ethernet. 

<img src="/MainBoard/images/case.jpg" width="600">

#### Проект состоит из базовой платы в корпусе 4-DIN, на которой размещен esp32, и включает в себя:

- 8 Портов ввода\вывода, с подключаемой внешней подтяжкой резисторм pulldown на 10к
- 1 Порт ввода\вывода, с внешней подтяжкой pullup или pulldown на 10к
- 2 порта, на которые можно припаять вшнешний резистор (например для подключения светодиодных лент)
- i2c порт (в случае не надобности, превращаеться в 2 порта ввода\вывода)
- Ethernet port для подключение к сети по кабелю
- Для питания платы можно использовыать micro usb/5v/7-20v


То есть по сути базовая плата являеться удобным решением для подключения входов\выходов. 

Магия происходит дальше) 

Вторым уровнем в данный корпус встает модуль расширения (шилд), и он раширяет функционал под кокретную задачу.
На данный момоент спроектированы следующие шилды

### Shield 8R\4+4IO
<img src="/MainBoard/images/Shield_1.png" width="600">
Расширительрный модуль на 16 портов, из которых 

- 8 Реле на 5а
- 4 входа\выхода с возможностью подтяжки pulldown резистором на 10к
- 4 Входа\выхода с возможностью подключения через опторазвязку

### Shield 5M\3R\5IO
<img src="/MainBoard/images/Shield_2.png" width="600">
Расширительный модуль на 8 портов, из которых

- 5 Мосфетов, для подключение светодиодных лент, моторов
- 3 Реле на 5а
- 5 Вводов\выводов с  с возможностью подтяжки pulldown внешним резистором на 10к

#### Важно! При подключении данного модуля, на базовой плате нельзя использовать пины 2, 4, 12, 14, 15

### Shield 16IO (1\2)
<img src="/MainBoard/images/Shield_3.png" width="600">
Модуль на 16 портов, все с возможностью подтяжки pulldown
Из интересного - модуль половинчатый, и таких модулей можно подключить одновременно два. 
Так же можно подключить в дополнение к этому любой модуль формата 1\2. 

### Shield 12+4IO (1\2)
<img src="/MainBoard/images/Shield_4.png" width="600">
Модуль на 16 входов\выходов, похож предидущий, с той лишь разничей что портов с подтяжкой всего 12 + 4 с опторазвязкой. 
Аналогично можно подлючить к нему любой другой модуль в формате 1\2

### Shield 5M (1\2)
Половинчитый модуль с 5 мосфетами, например для светодиодных лент. 
#### Важно! Во первых модуль подключаеться только в дополнение к любому из предидущих формата 1\2, во вторых на базовой плате нельзя использовать пины 2, 4, 12, 14, 15

### Shield 9R/PM
Это модуль под большую нагрузку, состоящий из 9 реле. 1 на 16а, с счетчиком потребления, и 8 на 10а. 
#### Важно! При подключении данного модуля, на базовой плате нельзя использовать пины 2, 4, 12, 14

***

### Лирическое вступление
Проект изначально создавался под собственные потребности как автономномная охранноая система на прошивке EspHome, на датчиках движения\вибрации\герконах.
Но показав отличную стабильность и переспективность - проект вырос в универсальную модульную систему. 
На текущий момоент данный конкроллер, по мимо охранных функций используеться для:
- Управление освещение
- Управление отоплением
- Управление вентиляцией
- Управление инжинерными коммуникациями

Благодаря esp32, в связке с EspHome вся логика крутиться на самом контроллере. То есть при зависании\отключении сервера УД, отопление продолжит работу, охранная система пришлет уведопление, или вклчит серену, а включить свет всегда можно будет обычнм включаетелем. 

### Лирическое отступление

Ну и для тех кто близко не знаком с esp32, чем обсусловлен выбор в пользу именно ее:
- двухъядерный процессор, с частотой 240МГц
- Сопроцессор с низким энергопотреблением
- 520 КБ памяти SRAM
- Wi-Fi: 802.11 b/g/N
- Bluetooth: v4.2 (в том числе BLE)




