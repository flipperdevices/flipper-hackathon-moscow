# Удаленный сервер с Флиппером и ST-Link

<img src=https://cdn.flipperzero.one/flipper_hackaton_vm_photo.jpg>

Удаленный сервер с Флиппером и отладчиком для участников хакатона. На нем можно запустить свою прошивку на реальном устройстве.  
К удаленному серверу подключен Флиппер по USB и ST-Link V3 по USB. 

## Подключиться к серверу

Подключиться к серверу так: `ssh -p 228 furippa@flipper-hackaton-vm.flipp.dev` 

* **Адрес сервера:** `flipper-hackaton-vm.flipp.dev`
* **Имя пользователя:** `furippa`  
* **Порт SSH:** `228`
* **Ключ SSH:** ⚠️Запросите добавление вашего SSH ключа в телеграм-чате [@FlipperHackathon2021](https://t.me/FlipperHackathon2021). Чтобы ваш ключ добавили на сервер, он должен быть добавлен в Github-аккаунте.

## Порты устройств

* **Флиппер подключенный по USB:** `/dev/flipper_vcp`
* **Консоль 1 ST-Link.** Подключено к USART порту флиппера. В этот порт выводится лог с флиппера `/dev/stlink_debug_usart`  
* **Консоль 2 ST-Link.** Подключен к LP UART флиппера. Никак не задействован.



## Сборка и установка прошивки

```
cd ~/flipperzero-firmware
make clean
make flash
```

## Установка своей прошивки 

Загрузите на сервер файл собранной прошивки и выполните:  

```
st-flash write flipper-z-f7-full-local.bin  0x8000000
st-flash reset
````

## Стриминг экрана, утилита screech

Утилита screech вывод изображение с экрана флиппера прямо в ASCII консоль. Можно эмулировать ввод с джойстика клавишами курсора, enter, esc.  
⚠️⚠️⚠️ ВАЖНО ⚠️⚠️⚠️
В утилите есть баг: скрин-стриминг может не работать, если запустить его ПОСЛЕ подключения к консоле флиппера через minicom. Это связано с конфирурирование tty порта. Если после запуска screech вы видите черный экран, убейте все процессы go, перезапустите флиппер и подключитесь заново.

Запуск:
```
~/screech
./run.sh
```

<img width=700 src="https://cdn.flipperzero.one/screech-screen-stream.jpg" />

## Подключение к CLI флиппера 

`minicom -D /dev/flipper_vcp -b 115200`

<img width=700 src="https://cdn.flipperzero.one/flipper_cli_screenshot.png" />

## Подключение к debug логу

`minicom -D /dev/stlink_debug_usart -b 230400`

<img width=700 src="https://cdn.flipperzero.one/flipper_debug_console_exampe_screenshot.png" />
