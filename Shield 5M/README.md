# Модуль 1/2 из 5 мосфетов

<img src="/Shield%205M%5C3R%5C5IO/photo_mosfet.jpg" width="1000">

Данный модуль состоит из 5 полевых транзисторов (мофсетов), в размерности 1/2

Подходит для управления светодиодным освещением. Например к нему можно подключить светодиодную ленты RGBWW, либо 5 отдельных одноцветных лент. 
Так же им отлично управляться моторы на 12вольт, к примеру для вытяжки, и благодаря подключению через мосфет можно регулировать скорость вращения. 


<img src="/MainBoard/images/Shield_2.png" width="600">

#### Особенности:
- 5 Мосфетов, для диммирования светодиодных лент, или регулировки оборотов у моторов
- Для работы использует порт GPIO-Shield c основной платы. 
- Выходы 2,4,12,14,15 с основной платы - используются мосфетами. На них лучше нечего больше не подключать. 
- Устанавливаеться вторым модулем к любому "половинчатому" - [16IO](/Shield%2016IO)/ или [12+4IO](/Shield%2012%2B4IO)


 
<img src="/Shield%205M%5C3R%5C5IO/PCB.png" width="600">


 

Перейдем к сборке.  
### Для заказа печатных плат на производстве

[Скачать GERBER]

В Китае полно сервисов для печати плат, но я предпочитаю пользоваться [jlcpcb.com](https://jlcpcb.com/) поскольку: 
5 плат (это минималка) за 2-4 доллара + доставка, это совсем недорого, за печатные платы заводского исполнения. 
На других сервисах малые партии - дороже, но дешевле большие. 

### Схемотехника
<img src="/Shield/Schematic_E3-2e-5M_3R_5IO.png" width="1000">

***

Размеры и тип компонентов:
- K1, К7, К8 - Реле ALDP105W [Ali](https://aliexpress.ru/item/4001081126200.html),[ChipDip](https://www.chipdip.ru/product1/8003573908)
- U1 - PCF8574T 8 канальные расширители портов [Ali](https://aliexpress.ru/item/32964941533.html),[ChipDip](https://www.chipdip.ru/product/pcf8574t-3)
- D1 - Матрица Дарлингтона из восьми транзисторов [Ali](https://aliexpress.ru/item/32792767122.html),[ChipDip]
- U2 - Двойной клемник 5.0 [Ali],[ChipDip]
- P1, P2 - Тройные клемники 5.0 [Ali](https://aliexpress.ru/item/32861603911.html),[ChipDip]
- P3 - Тройной клемник 2.54 [Ali](https://aliexpress.ru/item/1005001894448937.html),[ChipDip]
- С1, C7, C19, C20 - Двойные клемники 2.54 [Ali](https://aliexpress.ru/item/1005001894448937.html),[ChipDip]
- Q1, Q2, Q3, Q4, Q5 - Мосфеты IRF3205 [Ali](https://aliexpress.ru/item/32511028751.html),[ChipDip]
- I2c-Shield Гребенка на 5 пинов, 2.54 [Ali](https://aliexpress.ru/item/32519474531.html),[ChipDip]
- GPIO-Shield Гребенка на 6 пинов, 2.54 [Ali](https://aliexpress.ru/item/32519474531.html),[ChipDip]
- R1, R2,R3,R5,R10 - Резисторы от 220 до 500 Ом, размером 0805 [Ali](https://aliexpress.ru/item/4000095368506.html),[ChipDip]
- R4, R6, R7, R8, R9, R11, R12 ,R13, R14, R20  - Резисторы 10к, в размере 0805 [Ali](https://aliexpress.ru/item/4000095368506.html),[ChipDip]
- J - Гребенка на 2 пина 2.54 с перемычкой [Ali](https://aliexpress.ru/item/32519474531.html),[ChipDip]
- J - Перемычка [Ali](https://aliexpress.ru/item/4001139171872.html), [ChipDip]

Для заказа компонентов: [Файл BOM](/MainBoard)

### Вариации при сборке:
- Вместо мосфета IRF3205 можно паять IRF520

***

### Прошивка EspHome
Примеры конфигурационных файлов под эту плату ниже: 
- [YAML Универсальный](/Shield/Esphome.yaml)


### Сборка платы

Сначала паять потом резисторы, потом уже все остальное. 

