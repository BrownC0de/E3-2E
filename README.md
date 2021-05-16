# E3-2E Universal system to control your home. 
[![Donate](https://img.shields.io/badge/donate-Coffee-yellow.svg)](https://www.buymeacoffee.com/BrownCode)
[![Donate](https://img.shields.io/badge/donate-Yandex-red.svg)](https://money.yandex.ru/to/)


Многофункциональный модульный контроллер для домашней автоматизации, на основе ESP32 с Ethernet. 

<img src="/MainBoard/images/case.jpg" width="600">

Проект состоит из базовой платы, и дополнительных модулей, которое спроектированы, что бы закрыть большинство потребностей для автоматизации "умных" домов.

### [E3-2E Board](/MainBoard)
<img src="/MainBoard/images/Board_1.png" width="600">
Базовая плата на которой размещен esp32, и включает в себя:

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

### [Shield 8R\4+4IO](/Shield%208R%5C4%2B4IO)
<img src="/MainBoard/images/Shield_1.png" width="600">
Расширительрный модуль на 16 портов, из которых 

- 8 Реле на 5а
- 4 входа\выхода с возможностью подтяжки pulldown резистором на 10к
- 4 Входа\выхода с возможностью подключения через опторазвязку

### [Shield 5M\3R\5IO](/Shield%205M%5C3R%5C5IO)
<img src="/MainBoard/images/Shield_2.png" width="600">
Расширительный модуль на 8 портов, из которых

- 5 Мосфетов, для подключение светодиодных лент, моторов
- 3 Реле на 5а
- 5 Вводов\выводов с  с возможностью подтяжки pulldown внешним резистором на 10к

#### Важно! При подключении данного модуля, на базовой плате нельзя использовать пины 2, 4, 12, 14, 15

### [Shield 16IO (1\2)](/Shield%2016IO)
<img src="/MainBoard/images/Shield_3.png" width="600">
Модуль на 16 портов. Все порты на вход\выход с возможностью подтяжки pulldown
Из интересного: модуль половинчатый, и таких модулей можно подключить два одновременно. 
Так же можно подключить в дополнение к этому любой модуль формата 1\2. 

### [Shield 12+4IO (1\2)](/Shield%2012%2B4IO)
<img src="/MainBoard/images/Shield_4.png" width="600">
Модуль на 16 входов\выходов, похож предидущий, с той лишь разничей что портов с подтяжкой всего 12 + 4 с опторазвязкой. 
Аналогично можно подлючить к нему любой другой модуль в формате 1\2

### Shield 5M (1\2) [В процессе]
Половинчитый модуль с 5 мосфетами, например для светодиодных лент. 
#### Важно! Во первых модуль подключаеться только в дополнение к любому из предидущих формата 1\2, во вторых на базовой плате нельзя использовать пины 2, 4, 12, 14, 15

### Shield 9R/PM [В процессе]
Это модуль под большую нагрузку, состоящий из 9 реле. 1 на 16а, с счетчиком потребления, и 8 на 10а. 
#### Важно! При подключении данного модуля, на базовой плате нельзя использовать пины 2, 4, 12, 14

***

### Лирическое вступление
Проект изначально создавался под собственные потребности как автономномная охранная система на прошивке EspHome, на датчиках движения\вибрации\герконах.
Но показав отличную стабильность и переспективность - проект вырос в универсальную модульную систему. Особая благодарность Владимиру Ивахову, за помощь в разработке. 
На текущий момоент данный контроллер, по мимо охранных функций используеться для:
- Управление освещение
- Управление отоплением
- Управление вентиляционной установкой
- Управление инжинерными коммуникациями

### Лирическое отступление


Мне нравиться esp32, у нее есть все нужные сетевые протоколы, у нее большой запас по ресурсам, что бы не просто выступать в роли контроллера который будет передавать и принимать, но и для того что бы развернуть на нем всю логику взаимодействия между сенсорами и исполнительными устройствами, и тем самым получить автономное устройство, которое в случае выхода из строя сервера "умного" дома, продолжит работу. Отопление продолжит поддерживать установленную температуру, охранная система пришлет уведопление, или включит серену, а включить свет всегда можно будет обычнм включаетелем. 

### О лицензировании
Проект не коммерческий, для личных целей можно использовать практически без каких либо ограничений. А вот право производить для коммерческих целей, в том числе для продажи - я оставляю только за собой. 


