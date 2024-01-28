# Дополнительные материалы ***

В данном файле вы найдёте всё, на что я ссылался видео.  
Также тут будут некоторые команды которые пригодятся для установки приложений в Docker.

## Варианты мини пк

[Orange Pi PC+](http://www.orangepi.org/html/hardWare/computerAndMicrocontrollers/details/Orange-Pi-PC-Plus.html) - мой мини пк. С 2020 года работает 24/7. Никаких проблем замечено не было, работает стабильно.  
[Orange Pi 3 LTS](http://www.orangepi.org/html/hardWare/computerAndMicrocontrollers/details/orange-pi-3-LTS.html) - тот мини пк, что я бы покупал сейчас.  
Вариант на процессоре N100 - мини пк для тех кому нужно много мощности.  
Таблица сравнения процессоров [Orange Pi](https://www.cpubenchmark.net/compare/4197vs4128vs5273vs4906/ARM-Cortex-A7-4-Core-1200-MHz-vs-ARM-Cortex-A53-4-Core-1800-MHz-vs-Rockchip-RK3399-Board-(Android)-vs-Rockchip-RK3588) и [Raspberry Pi с N100](https://www.cpubenchmark.net/compare/4143vs4078vs5743vs5157/ARM-Cortex-A53-4-Core-1400-MHz-vs-ARM-Cortex-A72-4-Core-1800-MHz-vs-ARM-Cortex-A76-4-Core-2400-MHz-vs-Intel-N100)  
Ссылки на Aliexpress: [Orange Pi PC+](https://fas.st/z_2-k) | [Orange Pi 3 LTS](https://fas.st/aZPTx) | [N100](https://fas.st/DOr-H)

## Zigbee адаптер

[SONOFF ZBDongle-P](https://fas.st/bS0gQg) - у меня такой.  
[Список](https://www.zigbee2mqtt.io/guide/adapters/) рекомендованных адаптеров для Zigbee2MQTT.

## Выбираем Linux

Подходящие [дистрибутивы linux](http://www.orangepi.org/html/hardWare/computerAndMicrocontrollers/service-and-support/Orange-pi-3-LTS.html) для Orange Pi 3 LTS.  
[Armbian](https://www.armbian.com/orangepi3-lts/) для Orange Pi 3 LTS.  
[Armbian](https://www.armbian.com/orange-pi-pc-plus/) для Orange Pi PC plus.

## Установка Linux:

Записать образ на карту памяти можно через [balenaEtcher](https://etcher.balena.io/).  
Подключаться по SSH можно через [putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).  
[Официальная инструкция](https://docs.armbian.com/User-Guide_Getting-Started/) по установке Armbian.  
[Инструкция](https://jumptuck.com/blog/2023-02-13-install-linux-orange-pi-3-lts-emmc/) как установить Linux на Orange Pi 3 LTS и потом перенести его во встроенную память.  
[Ещё одна инструкция](https://wiki.kobol.io/helios64/install/transfer/) о том как перенести Armbian во встроенную память (в видео я показывал скриншоты из этой инструкции).

## Docker:

Установить Docker можно при помощи команды: **apt-get install docker.io**, если не получилось, то:

 - [Инструкция](https://docs.armbian.com/User-Guide_Advanced-Features/#how-to-run-docker) из документации Armbian о том как установить Docker.
 - [Скрипт](https://github.com/docker/docker-install) который должен установить Docker куда угодно.
 - [Официальная инструкция](https://docs.docker.com/engine/install/) по установке Docker. 
 - [Ссылка](https://www.google.com/search?q=%D0%BA%D0%B0%D0%BA%20%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C%20docker) которая точно поможет установить Docker.

## Portainer:

Установить Portainer можно при помощи двух команд.  
Нужно создать volume:

    docker volume create portainer_data

И выполнить основную команду установки контейнера

    docker run -d \
      -p 8000:8000 \
      -p 9443:9443 \
      --name portainer \
      --restart=always \
      -v /var/run/docker.sock:/var/run/docker.sock \
      -v portainer_data:/data \
      portainer/portainer-ce:latest

Если не получилось, то:

 - [Официальная инструкция](https://docs.portainer.io/start/install-ce/server/docker/linux) по установке.
 - [Ссылка](https://www.google.com/search?q=%D0%BA%D0%B0%D0%BA%20%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C%20Portainer) которая точно поможет установить Portainer.

## Node-RED

Установить Docker можно при помощи команды (поменяйте временную зону если это необходимо):

    docker run -it \
      -p 1880:1880 \
      -v node_red_data:/data \
      --name mynodered \
      -e TZ=Europe/Moscow \
      --restart unless-stopped \
      nodered/node-red

Если не получилось, то:

 - [Официальная инструкция](https://nodered.org/docs/getting-started/docker) по установке.
 - [Ссылка](https://www.google.com/search?q=%D0%BA%D0%B0%D0%BA%20%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C%20node-red%20%D0%B2%20docker) которая точно поможет установить Node-RED.

А также:

 - Как [поменять время](https://wiki.alpinelinux.org/wiki/Setting_the_timezone) в контейнере Node-RED.
 - [Список](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) временны зон.

## Mosquitto

Чтобы установить Mosquitto нужно создать два файла и папку вот этой командой (при этом нужно находится в домашней директории):

    mkdir mosquitto && \
    touch mosquitto/mosquitto.conf mosquitto/mosquitto_password_file && \
    echo -e "listener 1883\nallow_anonymous false\npassword_file /mosquitto/config/mosquitto_password_file" > mosquitto/mosquitto.conf

Потом выполняем команду установки контейнера с Mosquitto:

    docker run -it \
      -p 1883:1883 \
      -p 9001:9001 \
      -v `pwd`/mosquitto:/mosquitto/config \
      --name mosquitto \
      --restart unless-stopped \
      eclipse-mosquitto

И в конце нужно задать пароль для пользователя от имени которого будет подключаться Zigbee2MQTT и другие устройства (если они у вас будут):

    docker exec -it mosquitto mosquitto_passwd -c /mosquitto/config/mosquitto_password_file iot_user

Если не получилось, то:

 - [Официальная инструкция](https://hub.docker.com/_/eclipse-mosquitto) по установке в Docker.
 - [Ссылка](https://www.google.com/search?q=%D0%BA%D0%B0%D0%BA%20%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C%20Mosquitto%20%D0%B2%20docker) которая точно поможет установить Mosquitto.

## Zigbee2MQTT

В начале нужно скачать файл где мы укажем адрес MQTT брокера:

    wget https://raw.githubusercontent.com/Koenkk/zigbee2mqtt/master/data/configuration.yaml -P data

В скаченном файле указываем ip адрес, а также логин:пароль MQTT брокера.  
Далее выполняем команду которая покажет id zigbee адаптера вставленного в мини пк.

    ls /dev/serial/by-id

Теперь меняем в этой команде id адаптера на тот, что только что узнали и устанавливаем Zigbee2MQTT:

```
docker run \
  --name zigbee2mqtt \
  --restart=unless-stopped \
  --device=/dev/serial/by-id/usb-Texas_Instruments_TI_CC2531_USB_CDC___0XDF-if00:/dev/ttyACM0 \
  -p 8080:8080 \
  -v $(pwd)/data:/app/data \
  -v /run/udev:/run/udev:ro \
  -e TZ=Europe/Amsterdam \
  koenkk/zigbee2mqtt
```
Если не получилось, то:

 - [Официальная инструкция](https://www.zigbee2mqtt.io/guide/installation/02_docker.html) по установке в Docker.
 - [Ссылка](https://www.google.com/search?q=%D0%BA%D0%B0%D0%BA%20%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C%20Zigbee2MQTT%20%D0%B2%20docker) которая точно поможет установить Zigbee2MQTT.

## Разное

Ссылки на статьи про сбои: [1](https://nsn.fm/society/yandeks-vosstanovil-rabotu-gadzhetov-umnogo-doma-posle-sboya), [2](https://3dnews.ru/1097364/uyandeksa-proizoshyolmasshtabniy-sboy-v-prilogeniiumniy-dom-ne-rabotayut-kolonki-salisoy-i-drugie-gadgeti), [3](https://ria.ru/20230904/sboy-1894192706.html)  
Тут можно бесплатно [скачать VirtualBox](https://www.virtualbox.org/wiki/Downloads), а тут можно [скачать Ubuntu](https://ubuntu.com/download/server).
