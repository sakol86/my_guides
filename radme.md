`Шаги по установке и настройке 3X-UI для сервера X-Ray с поддержкой VLESS и других протоколов:`

`1. Выбор домена для маскировки:`
   - Найдите подходящий иностранный сервер, который не заблокирован Роскомнадзором и поддерживает TLSv1.3 и HTTP/2.
   - Убедитесь, что у сервера есть статическая главная страница без редиректов.

`2. Подготовка сервера:`
   - Установите Docker на ваш VPS, если он ещё не установлен.
   - Убедитесь, что ваш VPS имеет статический публичный IP-адрес.

`3. Установка 3X-UI:`
## Установка и обновление

```
bash <(curl -Ls https://raw.githubusercontent.com/mhsanaei/3x-ui/master/install.sh)
```
## Установка кастомной версии

установка кастомной версии для примера используем
, ver `v2.3.0`:

```
bash <(curl -Ls https://raw.githubusercontent.com/mhsanaei/3x-ui/master/install.sh) v2.3.0
```
## Установка панели 3X-UI в Docker

<details>
  <summary>Click for Docker details</summary>

#### Usage

1. Устанавливаем Docker:

   ```sh
   bash <(curl -sSL https://get.docker.com)
   ```

2. Клонируем Repository:

   ```sh
   git clone https://github.com/MHSanaei/3x-ui.git
   cd 3x-ui
   ```

3. Запускаем docker-compose

   ```sh
   docker compose up -d
   ```

   Или

   ```sh
   docker run -itd \
      -e XRAY_VMESS_AEAD_FORCED=false \
      -v $PWD/db/:/etc/x-ui/ \
      -v $PWD/cert/:/root/cert/ \
      --network=host \
      --restart=unless-stopped \
      --name 3x-ui \
      ghcr.io/mhsanaei/3x-ui:latest
   ```

Обновление до последней версии

   ```sh
    cd 3x-ui
    docker compose down
    docker compose pull 3x-ui
    docker compose up -d
   ```

Удаление 3x-ui из docker 

   ```sh
    docker stop 3x-ui
    docker rm 3x-ui
    cd --
    rm -r 3x-ui
   ```

</details>

4. Настройка 3X-UI:
   осталось - настроить ее:

Для 3X-UI идем браузером по адресу http://yourserverip:2053/panel/, где yourserverip - IP-адрес вашего сервера или доменное имя, если оно у вас есть и настроено (обратите внимание, протокол http://, а не https://).

Логинимся под стандартными реквизитами admin/admin и видим панель управления:

скрин vl1

4.1 Обязательно Переходим в Настройки панели и там:

- Изменить порт на котором работает панель со стандартного 2053 на какой-нибудь другой (лучше всего где-нибудь в верхнем конце диапазона, до 65535) ;

Дополнительно Не обязательно:
- Изменить корневой путь URL-адреса панели с / на что-то  /secretpanel/

скрин vl2

на вкладке "Настройки безопасности" изменить стандартный админский пароль на свой:
скрин vl3

5. Настройка маскировки(Vless):
  скрин vl4

 `Примечание` - любое название;
`Протокол` - "vless",
`Listening IP`  - оставляем пустым;
"Порт" -  ставим 443;

Добавление Пользователя:
скрин vl5,6
6. Подключение:
Нажав на значок QR-кода, панель покажет QR-код, который можно отсканировать камерой в мобильных клиентах (v2rayNG или Nekobox на Android, Wings X/FoXray или Shadowrocket на iOS).
   vl7


7. Мониторинг:
   скрин vl8