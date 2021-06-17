

<img align="left" width="120" height="120" src="/MainBoard/images/bc-logo.png" alt="icon">

# E3-2E DIY Universal system to control your home ✨
Многофункциональный модульный контроллер для домашней автоматизации, на основе ESP32 с Ethernet. 

<img src="/MainBoard/images/main_photo.png" width="1200">


Проект  состоит из базовой платы, и дополнительных модулей, которые спроектированы, что бы закрыть большинство потребностей для автоматизации "умных" домов. Все это дело упаковано в аккуратный корпус размером 4DIN на рейку. 


📬 [Группа поддержки в Telegram](https://t.me/BrownC0DE) 

### 💡 Примеры использования
[![Donate](https://img.shields.io/badge/donate-YooMoney-8C3FFD.svg)](https://yoomoney.ru/to/410014221244621) 

На текущий момент данный проект успешно используется как:
- [Контроллер для кухни и ванной](/cases/kitchen.md)
- [Контроллер для бани и сауны](/cases/sauna.md)
- [Охранной системы (В процессе)](/cases/Security.md)
- [Управление светом(В процессе)](/cases/Lighting.md)
- [Управление отоплением(В процессе)](/cases/Heating.md)
- [Управление вентиляционной установкой(В процессе)](/cases/Airvent.md)
- [Управление инжинерными коммуникациями(В процессе)](/cases/Communication.md)
- Управления шторами и рольставнями (в перспективе)

Проект подразумевает самостоятельную сборку. Все необходимые файлы в описании к каждой плате. 

### 🧩 [E3-2E Board](/MainBoard)
<img src="/MainBoard/photo_mainboard.jpg" width="1000">
Базовая плата на которой размещен esp32, и включает в себя:

- 8 Портов ввода\вывода, с подключаемой внешней подтяжкой резистором pulldown на 10к
- 1 Порт ввода\вывода, с внешней подтяжкой pullup или pulldown на 10к
- 2 порта*, с площадками на которые можно припаять внешний резистор (например для подключения адресных светодиодных лент)
- i2c порт (в случае не надобности, превращается в 2 порта ввода\вывода)
- Ethernet port для подключение к сети по кабелю
- Для питания платы можно использовать micro usb/5v/7-20v
 

То есть по сути базовая плата является удобным решением для подключения входов\выходов. 

Магия происходит дальше) 

Вторым уровнем в данный корпус встает модуль расширения (шилд), и он расширяет функционал под конкретную задачу.
На данный момент спроектированы следующие шилды

### 🧩 [Shield 8R\4+4IO](/Shield%208R%5C4%2B4IO)
<img src="/Shield%208R%5C4%2B4IO/photo_8r.jpg" width="1000">
Расширительрный модуль на 16 портов, из которых 

- 8 Реле на 5а
- 4 входа\выхода с возможностью подтяжки pulldown резистором на 10к
- 4 Входа\выхода с возможностью подключения через опторазвязку

### 🧩 [Shield 5M\3R\5IO](/Shield%205M%5C3R%5C5IO)
<img src="/Shield%205M%5C3R%5C5IO/photo_mosfet.jpg" width="1000">

Расширительный модуль на 8 портов, из которых

- 5 Мосфетов, для подключение светодиодных лент, моторов
- 3 Реле на 5а
- 5 Вводов\выводов с  с возможностью подтяжки pulldown внешним резистором на 10к

#### Важно! При подключении данного модуля, на базовой плате нельзя использовать пины 2, 4, 12, 14, 15

### 🧩 [Shield 16IO (1\2)](/Shield%2016IO) [Тестирование]
<img src="/MainBoard/images/Shield_3.png" width="600">
Модуль на 16 портов. Все порты на вход\выход с возможностью подтяжки pulldown
Из интересного: модуль половинчатый, и таких модулей можно подключить два одновременно. 
Так же можно подключить в дополнение к этому любой модуль формата 1\2. 

### 🧩 [Shield 12+4IO (1\2)](/Shield%2012%2B4IO). [Тестирование]
<img src="/MainBoard/images/Shield_4.png" width="600">
Модуль на 16 входов\выходов, похож предыдущий, с той лишь разницей что портов с подтяжкой всего 12 + 4 с опторазвязкой. 
Аналогично можно подлючить к нему любой другой модуль в формате 1\2

### 🧩 Shield 5M (1\2) [В разработке]
Половинчатый модуль с 5 мосфетами, например для светодиодных лент. 
#### Важно! Во первых модуль подключается только в дополнение к любому из предыдущих формата 1\2, во вторых на базовой плате нельзя использовать пины 2, 4, 12, 14, 15

### 🧩 Shield 9R/PM [В разработке]
Это модуль под большую нагрузку, состоящий из 9 реле. 1 на 16а, с счетчиком потребления, и 8 на 10а. 
#### Важно! При подключении данного модуля, на базовой плате нельзя использовать пины 2, 4, 12, 14

***

### 💰 О стоимости. 

В зависимости от модуля, себестоимость сборки получается 1800-3000 рублей. Что в сравнении с коммерческими решениями подобного плана в разы дешевле. Но. Некоторые компоненты, заказывая в Китае на широко известных площадках практически не возможно купить в единичном экземпляре, потому что продают их по 5-10 шт., что несколько увеличивает стоимость сборки. 

### 🎼 Лирическое отступление
Данный контроллер полностью отображает мое видение системы автоматизации, и наигравшись в квартире с беспроводными технологиями в виде zigbee, BT, BLE и в какой-то мере wifi (Хотя к нему у меня меньше всего претензий), для загородного дома я пришел к следующему, тезисно это звучит так: 
- Если что-то можно подключить по проводу, то нужно это подключить по проводу.
- Если сенсоры и исполнительные устройства можно объединить в одно - то лучше это сделать. 
- Централизованное управаление, схемой звезда. Каким образом объединять, по помещениям, или по типу - не столь важно. 
- Автономность. Вся логика в критичных узлах должна крутиться внутри контроллера. Серер УД - только получает состояние с датчиков, и передает команды, какой нужен результат, как его достигнуть - должен думать контроллер.
- Энергонезависимость. Ее достигнуть можно разными вариантами, но поставить ИБП в щиток на несколько контроллеров, значительно проще. 
- Масштабируемость. То что не нужно сейчас, не факт что не понадобиться завтра. 
- Взаимозаменяемость, или ремонтопригодность. Как бы я не старался сделать устройства максимально отказоустойчивым, это все таки бытовая электроника. И всегда есть ситуации которые либо не возможно предусмотреть, либо вероятность их настолько мала, что на нее закрываешь глаза. И тут всегда нужно иметь возможность восстановить работоспособность в минимальны срок и минимальным трудозатратами.


Мне нравиться esp32, у нее есть все нужные сетевые протоколы, у нее большой запас по ресурсам, что бы не просто выступать в роли контроллера который будет передавать и принимать, но и для того что бы развернуть на нем всю логику взаимодействия между сенсорами и исполнительными устройствами, и тем самым получить автономное устройство. Которое в случае выхода из строя сервера "умного" дома, продолжит работу. Отопление продолжит поддерживать установленную температуру, причем не просто - а по нужному мне, и дешевому ночному тарифу, охранная система в случае срабатывания пришлет уведомление, или включит сирену, а домашние не заметят проблем с сервером, и включить свет всегда можно будет обычным включателем. 

***


### Почему контроллер получился таким

Проект изначально создавался под собственные потребности как автономная охранная система, на прошивке EspHome. С возможностью более глубокой настройки логики срабатывания, и использования более дешевых датчиков движения\вибрации\открытия, чем предлагают готовые решения.
Но показав отличную стабильность и перспективность - проект вырос в универсальную модульную систему. Особая благодарность Владимиру Ивахову, за помощь в разработке. 


### О лицензировании

Проект некоммерческий, для личных целей можно использовать практически без каких-либо ограничений. А вот право производить для коммерческих целей, в том числе для продажи - я оставляю только за собой.
