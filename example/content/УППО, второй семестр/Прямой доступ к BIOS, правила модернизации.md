﻿/*
Title: 
Sort: 12
*/

Принцип работы

Большинство устройств ПК нуждаются в периодическом обмене данными не только с центральным процессором (ЦП), но и с оперативной памятью. В первых вариантах  персональных компьютеров процесс обмена данными какого-либо устройства с ОЗУ протекал при помощи процессора. Такой метод получил название PIO (Programmable Input-Output, программируемый ввод-вывод). Однако этот метод имел ряд недостатков. Прежде всего, было очевидно, что поскольку процессор загружен множеством задач, то он не всегда может отвлекаться на то, чтобы управлять процессом чтения и записи данных ОЗУ, тем более, что объем этих данных в результате прогресса компьютерной техники все увеличивался и увеличивался.

Так появилась идея технологии DMA (сокращение от Direct Memory Access, т.е. Прямой Доступ к Памяти), состоящая в том, чтобы позволить различным устройствам обращаться к оперативной памяти напрямую, минуя ЦП. Также часто используется русская аббревиатура данной технологии – ПДП.

Первоначально практическая реализация этой технологии (в материнских платах на основе шины ISA) была осуществлена при помощи встроенного в материнскую плату контроллера ПДП, который был призван управлять процессом обмена данными между устройством и ОЗУ. При этом процессор также не был полностью исключен из этого процесса. Прежде всего, механизм ПДП инициализировался самим процессором, однако в ход процесса передачи данных он не вмешивался, занимаясь в это время другими задачами. После того, как обмен информацией между устройством и ОЗУ завершался, то процессор получал соответствующее прерывание, которое отсылал ему контроллера DMA.

В шине ISA также использовались специальные каналы ПДП, которые часто  закреплялись за отдельным устройством:

Обновление DRAM
Аппаратный пользовательский канал, обычно использовался для 8-битных звуковых карт
Контроллер дисковода гибких дисков
Жесткий диск. Канал не использовался для жестких дисков с поддержкой PIO, а затем с UDMA. Также канал использовался для некоторых звуковых карт и параллельного порта
Каскадное прерывание от XT-контроллера ПДП
Пользовательский канал, иногда использовался для жестких дисков или 16-битных звуковых карт
Пользовательский канал
Пользовательский канал
Обычно данные каналы можно было устанавливать программным путем, но на некоторых старых устройствах, например, картах расширения для подключения накопителей CD-ROM, необходимо было вручную устанавливать значения нужных каналов при помощи перемычек.

Современная реализация

Начиная с появления шины ввода-вывода PCI, концепция практической реализации ПДП претерпела изменения. В материнских платах с шиной PCI больше не использовался контроллер DMA, а вместо этого стала применяться технология Bus Mastering. Суть этой технологии заключается в том, что любое устройство может обратиться к шине и полностью использовать ее в своих целях, в том числе, и для доступа к оперативной памяти. Кроме того, в шине PCI отпала необходимость в использовании каналов доступа к памяти. Подобный механизм используется также и в преемниках шины PCI –сверхбыстрых шинах AGP и PCI-Express.

Прямой доступ к памяти могут использовать любые устройства, расположенные в слотах расширения  материнской платы, или подключенные к ней при помощи внутренних шин. Это могут быть, например, жесткие диски, накопители для оптических дисков, видеокарты, звуковые и сетевые карты, и т.д. Кроме того, технология DMA может использоваться как внутри процессоров – для передачи данных между отдельными ядрами, так и внутри самой оперативной памяти – для обмена данными между различными участками памяти.

Современные операционные системы, такие как MS Windows, умеют управлять режимом ПДП для многих устройств. В частности, пользователь имеет возможность включить или выключить режим DMA для жестких дисков.

В жестких дисках с интерфейсом IDE технология ПДП получила свое развитие в виде дополнительных режимов ПДП, получивших название Ultra DMA (UDMA).  Всего стандарт Ultra DMA поддерживает 8 основных режимов передачи данных, обеспечивающих  скорость от 16,7 до 167 МБ/c. Использование режимов Ultra DMA для винчестеров позволило значительно увеличить пропускную способность шины IDE. Включить или изменить режим Ultra DMA для жестких дисков можно при помощи специальной опции BIOS, обычно носящей название DMA (UDMA) Mode.

Заключение

Появление технологии ПДП позволило разгрузить процессор и избавить его от большого объема рутинной работы по пересылке данных между оперативной памятью и устройствами, расположенными на материнской плате или подключенными к ней. Особенно важно использование разновидности технологии ПДП – Ultra DMA в винчестерах на основе интерфейса IDE, что позволяет значительно ускорить обмен данными между накопителем IDE и материнской платой.

<h3>Правильная модернизация BIOS, и как это делается с помощью AMIFlash</h3>

Рано или поздно большинство пользователей ПК сталкиваются с проблемами, решить которые может только модернизация системной BIOS. Кроме этого, многие подготовленные пользователи обновляют BIOS своей материнской платы каждый раз после выхода новой версии, предупреждая саму возможность возникновения таких проблем. Мы подробно рассмотрим универсальный и удобный инструмент — утилиту AMIFlash, пригодную для обновления BIOS всех производителей и обладающую богатыми возможностями тонкой настройки.

Альтернативы нет

Существует достаточное количество программ, предназначенных для модернизации BIOS. Среди них есть универсальные (как, например, AwardFlash, UniFlash, ECSFlash, AMIFlash) и специальные — к примеру PhoenixPhlash, которая может использоваться только совместно с конфигурационным файлом для определенных материнских плат. Однако именно AMIFlash от American Megatrends является лучшим универсальным инструментом модернизации большинства системных BIOS. Утилита обладает несколькими неоспоримыми достоинствами, выгодно отличающими ее от других аналогичных программ и делающими ее в своем роде уникальным продуктом.

Итак, чем же она хороша?

Во-первых, эта утилита написана с использованием технологии DOS/4G от Tenberry Software, которая позволяет снять многие ограничения, накладываемые на программы в среде операционной системы DOS, а именно:

преодолеть лимит 640 KB основной памяти и обеспечить доступ практически ко всей памяти, используя защищенный режим работы центрального процессора;
минимизировать использование тех самых 640 KB — программа занимает от 5 до 20 KB основной памяти;
получить полный и прямой доступ к любому аппаратному устройству, например PCI-to-ISA Bridge или Firmware HUB.
Последний момент особенно важен. Технология DOS/4G открывает 32-битовый доступ к памяти и пространству I/O-портов, что позволяет производить прямую адресацию всех регистров чипсета. Управление этими регистрами, в свою очередь, позволяет осуществлять операции в адресном пространстве микросхемы Flash. На практике это означает, что становится возможным прочитать из FlashROM код производителя и тип микросхемы, чтобы выбрать правильный алгоритм для записи/чтения данных.

Отметим, что такое, казалось бы, простое решение, как применение DOS/4G, не используется другими производителями утилит для обновления BIOS, например Award Software. В недавнем прошлом попытка всеми силами уменьшить размер flash-утилиты, пусть даже в ущерб качеству и возможностям, выглядела логичной. Ведь размер файла ограничен объемом накопителя FDD, в "былые времена" составлявшим 360 KB. Однако сейчас, когда привычной уже давно является емкость FDD 1,44 MB, подобный "традиционный" подход выглядит несколько странным.

Во-вторых, AMIFlash можно использовать для модернизации не только AMI BIOS, но и любого другого производителя (хотя такая возможность, конечно же, нигде не заявлена). Это достигается благодаря наличию модулей поддержки соответствующих чипсетов и микросхем FlashROM. По всей видимости, American Megatrends основной упор делает на распространение этой утилиты среди своих партнеров, которые доставляют программный продукт до конечных пользователей. Подтверждением этому служит тот факт, что сама утилита появилась на сайте AMI совсем недавно, а ее описание там вообще отсутствует (есть только небольшой readme-файл, идущий в комплекте с самой программой). Кроме того, на Web-сайте производителя утилиты далеко не всегда доступна последняя версия, поэтому найти ее можно по адресу http://ic.doma.kiev.ua/inside/ami/flash.htm. Отметим, что, несмотря на общую универсальность, в настоящее время AMIFlash не поддерживает обновление Award BIOS на материнских платах, оснащенных чипсетами Intel i810 и i815.

И наконец, в-третьих, программа обладает модульной структурой, позволяющей оперативно и безболезненно добавлять поддержку новых типов микросхем и чипсетов. Ценность такого подхода становится все более очевидной при стремительном увеличении количества видов используемых в материнских платах Flash-микросхем. Так, последняя версия утилиты включает в себя 92 модуля поддержки чипсетов, в том числе и такие экзотичные, как SMSC VictoryBX-66 и Transmeta TM3200/TM5400, и 59 модулей поддержки микросхем FlashROM.

Ключи к успеху

Теперь рассмотрим правила использования этого могучего инструмента модернизации BIOS. Как известно, прежде чем приступать к обновлению BIOS, необходимо произвести ряд несложных манипуляций, являющихся залогом успешного обновления. Поэтому опишем вкратце порядок действий, предшествующих запуску самой утилиты. При этом предполагается, что у нас уже есть необходимый файл обновления BIOS и сама утилита.

Итак, для начала необходимо подготовить компьютер к процессу модернизации. Для этого нужно сделать следующее.

1. Обязательно перевести систему в штатный режим, если она разогнана.

2. Отключить в BIOS Setup все функции, предназначенные для защиты BIOS от перепрограммирования. Как правило, такая возможность предусмотрена, чтобы предотвратить несанкционированную запись в BIOS FlashROM, и используется для защиты от вирусов типа CIH.

3. Установить перемычку управления записью BIOS, если таковая имеется на материнской плате, в разрешающее положение.

Естественно, после успешной модернизации BIOS все измененные таким образом установки необходимо вернуть в исходное состояние.

Далее можно непосредственно приступать к обновлению BIOS. Для этого нужно загрузиться с системной дискеты, на которой, помимо системных файлов, должны присутствовать сама утилита (amiflash.exe) и файл с обновлением BIOS (newbios.bin). Здесь следует сделать важное замечание: если планируется использовать AMIFlash для модернизации BIOS 4 Mb (524288 байт), то сохранение предыдущей версии BIOS на дискете объемом 1,44 MB будет невозможно, так как сама программа занимает немногим более 500 KB, и свободного места на загрузочной дискете не останется.


Рис. 1. Основной экран диалогового режима AMIFlash
Утилита AMIFlash может работать как в диалоговом режиме, так и в режиме командной строки. В отличие от AwardFlash, диалоговый режим предоставляет такие же широкие возможности конфигурирования, как и командная строка, поэтому далее будут параллельно рассмотрены оба режима запуска программы (на примере версии 8.26.14).

Основной экран программы состоит из четырех частей (рис. 1).

Main Menu — доступные пункты меню.
Go ahead — опции, доступные для текущего пункта меню.
Information — сведения о важных для модернизации BIOS компонентах системы (чипсет, тип и размер FlashROM). Если в этом окне в любом из пунктов появилась надпись Unknown, то выполнять программирование не следует, это может привести к разрушению микропрограммы BIOS. Обычно такая ситуация возникает, если данная версия AMIFlash не содержит необходимых компонентов чипсета или FlashROM, установленных на системной плате, или же не выполнены подготовительные пункты, описанные выше. Кроме того, не стоит забывать, что плата или FlashROM может быть просто неисправна.
Help/Message — небольшая подсказка по текущему пункту меню.
Поскольку практически вся информация, вводимая в диалоговом режиме, может быть также передана с помощью параметров запуска, мы сразу же опишем синтаксис командной строки утилиты и в дальнейшем наряду с диалоговыми возможностями будем приводить описания соответствующих ключей.
Итак, AMIFlash из командной строки запускается следующим образом:

AMIFLASH.EXE [имя_файла_для_программирования] 
[/ключ [/ключ...]]
Большинство опций может быть как включено, так и деактивировано, для чего непосредственно перед ключом (т. е. сразу после косой черты) ставится знак "-" (минус, без кавычек). Такая возможность необходима, так как программа может запоминать текущее состояние каждого ключа и записывать во внутренний файл конфигурации. Соответственно если опция по умолчанию включена, ее всегда можно отключить из командной строки. Справку по всем доступным ключам можно получить традиционным способом, запустив утилиту с параметром /? или /H.

Теперь вкратце остановимся на каждом из пунктов меню программы и соответствующих им ключах.

Go ahead — запуск процедуры обновления BIOS. Однако прежде необходимо указать имя файла для модернизации и в случае необходимости — имя файла для сохранения текущей версии BIOS. Для этих целей служит следующий пункт меню.

File — задание имен файлов с новой BIOS и для сохранения старой версии. Отметим, что нажатие Enter в этом экране запускает обновление BIOS. Поэтому если есть необходимость предварительно установить некоторые параметры модернизации, нужно просто ввести в соответствующие поля имена файлов и нажать клавишу Escape. С помощью командной строки можно указать лишь имя для нового файла BIOS. Для этого необходимо запустить AMIFlash следующим образом: amiflash.exe newbios.bin. Передача в программу имени файла для сохранения не поддерживается, однако можно сохранить текущую BIOS в файле с помощью ключа /S: amiflash.exe /Soldbios.bin. При использовании этого ключа диалоговый режим не активируется, т. е. сразу после сохранения файла происходит выход из программы и возврат в командную строку.


Рис. 2. При обновлении BIOS в AMIFlash доступен большой выбор параметров
Switch — применяется для установки параметров обновления BIOS (рис. 2). Каждому параметру соответствует ключ командной строки (более подробно см. вставку).

Следующие два пункта меню — Part List и Chipset List — позволяют вручную задать типы компонентов системы, необходимых для корректной модернизации BIOS: микросхему FlashROM и чипсет, на основе которого сделана материнская плата. Практическая необходимость в использовании этих двух пунктов меню может возникнуть лишь в том случае, если данные компоненты не определились автоматически или же определились неправильно. Излишне говорить, что устанавливать тип микросхем вручную стоит, только будучи абсолютно уверенным в правильности производимых действий. Для повторной инициации автоматического определения микросхемы FlashROM и чипсета служит отдельный пункт Auto Detect.

Module — как уже было сказано, программа имеет модульную структуру. Каждый поддерживаемый чипсет (ID = 0) или микросхема FlashROM (ID = 1) представлен отдельным модулем, с которым можно провести ряд операций: удалить, сохранить в отдельный файл или добавить новый модуль из внешнего файла. Последнюю операцию можно также осуществить с помощью ключа командной строки/U[file], где file — имя файла, содержащего добавляемый модуль. К сожалению, описание формата модулей является закрытой информацией, поэтому добавление новых модулей пользователем не представляется возможным.

Дополнительные возможности

Помимо перечисленных выше, AMIFlash обладает также рядом возможностей, которые доступны только при использовании командной строки.

Ключ /A[+] инициирует обновление BIOS в автоматическом режиме без какого-либо вмешательства пользователя. Чипсет и установленная микросхема FlashROM определяются автоматически. Использование постфикса "+" разрешает оконный интерфейс, в противном случае обновление происходит в режиме командной строки. Применение данного ключа подразумевает обязательное указание имени файла обновления BIOS в командной строке. Все настройки в этом случае следует проводить только с помощью параметров командной строки, так как диалоговый режим становится недоступным.

Ключ /T[n] может быть использован только в сочетании с ключом /A и задает количество попыток перепрограммирования BIOS в случае, если первая попытка не привела к желаемому результату. Значение параметра n изменяется в пределах 0—65535.

Ключ /Q отключает вывод каких-либо сообщений во время обновления BIOS.

Ключ /X задает режим, при котором запрещается используемое по умолчанию автоматическое определение типа FlashROM и набора системной логики.


Рис. 3. Ключ /P открывает "скрытый" пункт меню Security
Ключ /P открывает "секретный" пункт меню Security (рис. 3), позволяющий:

установить пароль на вход в этот пункт меню при следующих запусках программы;
удалить этот пароль, если он был ранее установлен;
указать, какие пункты меню будут доступны при следующих запусках программы;
изменить сообщение, которое отображается в нижней части экрана (по умолчанию там выводится "For PCI system board only").
Очевидно, что максимальную пользу из этой функции могут извлечь производители материнских плат, распространяющие AMIFlash вместе со своей продукцией.

Практические рекомендации

После подробного описания возможностей AMIFlash мы приведем оптимальную конфигурацию утилиты для модернизации BIOS — в основном для тех читателей, которые не вполне уверенно чувствуют себя среди многочисленных ключей, опций и параметров.

Итак, для обновления системной BIOS следует выполнить описанные ранее подготовительные шаги 1—3 и создать .bat-файл (например, ami.bat) следующего содержания:

@echo off
if exist oldbios.bin goto program
amiflash.exe /Soldbios.bin
:program
amiflash.exe newbios.bin /A+ /-B /-C /-D /E /-G /I /L /N /R /V
При первом запуске этого bat-файла текущая BIOS будет сохранена в файл oldbios.bin, а файл newbios.bin будет записан в микросхему FlashROM без какого-либо участия со стороны пользователя. При последующих запусках сохранение текущей BIOS происходить не будет, чтобы не затереть файл с исходной версией BIOS, которая может пригодиться в случае неудачной модернизации.

Если же более предпочтительным кажется диалоговый режим, следует просто запустить AMIFlash с такими параметрами:

amiflash.exe /-B /-C /-D /E /-G /I /L /N /R /V
Действие параметров в обоих случаях прозрачно: Boot Block перепрограммироваться не будет, установленные пароли останутся активными, перед программированием будет произведена проверка целостности самого файла с новой BIOS и его соответствия данной материнской плате, а после перепрошивки BIOS установки CMOS Setup примут значения по умолчанию и выполнится автоматическая перезагрузка системы. Остается надеяться, что при соблюдении приведенных выше рекомендаций этот последний пункт выполнится успешно, уже с новой версией BIOS. Удачной модернизации!..