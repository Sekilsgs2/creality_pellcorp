Для установки последнего Klipper с поддержкой тензо датчиков требуется:


1. Провести аппартную модификацию по инструкции (до программной части) - 
	https://github.com/cryoz/K1_tenso_manual/tree/main

2. Обязателен root (раздел Enable Root Access) - 
	https://guilouz.github.io/Creality-Helper-Script-Wiki/firmwares/install-and-update-rooted-firmware-k1/ 

3. Подключившись к принтеру по SSH сделать сброс до заводских настроек выполнив по очереди следующие команды :

	wget --no-check-certificate  https://raw.githubusercontent.com/pellcorp/creality/main/k1/services/S58factoryreset
	chmod +x S58factoryreset
	./S58factoryreset reset 

   После запуска требуется подождать пока принтер сам перезагрузится и переподключиться к нему по SSH

4. Далее можно запускать автоматизированную установку выполнив команды - 

	git config --global http.sslVerify false

	git clone https://github.com/Sekilsgs2/creality_pellcorp.git /usr/data/pellcorp

	sync

	/usr/data/pellcorp/k1/installer.sh --install loadcell

 
   Скрипт выполнит автоматизированную установку klipper и всех нужных модулей - после установки требуется перезапустить 
   и если принтер не выдаст никаких ошибок можно будет запускать калибровку тензо датчиков по инструкции (раздел 4.4 Калибровка ) -
 
	https://github.com/cryoz/K1_tenso_manual/tree/main

   ВНИМАНИЕ!!! В файле loadcell.cfg в строках -
   dout_pin: leveling_mcu:PA0
   sclk_pin: leveling_mcu:PA2
   Если вы припаяли провода к датчику другому у котрого другие пины - нужно их поменять на те что у вас иначе голова принтера может впилится в стол!
   

   После калибровки можно пробовать делать HOME и пробовать печатать, возможно потребуется поправить Z Offset
   Тут есть баг видимо в самом коде load cell - через веб интерфейс z offset не сохранить - ругается на отрицательные значения - но можно получившийся оффсет потом руками внести в 
   файле loadcell.cfg - у меня получился -0.1
   
   Внимание - испольузется мой скрипт очистки сопла - его требуется поправить  - внести изменения в положение головы (X, Y, Z) при чистке. Все настройки находятся в файле NOZZLE_CLEAR.cfg

   Если какие то будут вопросы и пожелания - писать в ТГ - @estenkin


This repo also hosts the wiki:
Go to https://github.com/pellcorp/creality/wiki
