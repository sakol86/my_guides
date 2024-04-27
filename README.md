
`Краткий гайд по установке и настройке "VPN" VLESS с XTLS-Reality с использованием панели 3X-UI:`

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
  <summary>Полная установка в Docker</summary>

`1. Устанавливаем Docker:`

   ```sh
   bash <(curl -sSL https://get.docker.com)
   ```

`2. Клонируем Repository:`

   ```sh
   git clone https://github.com/MHSanaei/3x-ui.git
   cd 3x-ui
   ```

`3. Запускаем docker-compose`

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
<details>
<summary>4. Настройка 3X-UI</summary>
   осталось - настроить ее:

Для 3X-UI идем браузером по адресу http://yourserverip:2053/panel/, где yourserverip - IP-адрес вашего сервера или доменное имя, если оно у вас есть и настроено (обратите внимание, протокол http://, а не https://).

Логинимся под стандартными реквизитами admin/admin и видим панель управления:

![image](https://s79klg.storage.yandex.net/rdisk/0c8f798c27547b7fa32ac3eaa084b9e5a64262937c82895c1daaa7c89e6c4259/662d0ba1/GVkrPdnEhCiKAChhJEdOdlGYuxg4ITr2RYPsQ7G1DT6XxVSmRh4ieqMeOrCBcO9414z73PQMev8tRk9dJqKXrw==?uid=0&filename=vl1.png&disposition=inline&hash=&limit=0&content_type=image%2Fpng&owner_uid=0&fsize=64646&hid=97dbfce215a22abaa33e029e89d4957e&media_type=image&tknv=v2&etag=95a0357acce7feac1f599c8bc3d9f076&ts=61714d6b16a40&s=63279f9415e16dee14f9ac6b29df73c1468d0e56b6ad86fe73c962309219013f&pb=U2FsdGVkX1-_lGYvcthB7LazejLN_mY7-X54fKvufo3oywMLO1uLPVo0R75q_2o84Wev_K5RKdThZSV-ScI2Ll5DknrFVVlPhCyPkfNJEX4)

`4.1 Обязательно Переходим в Настройки панели и там:`

- Изменить порт на котором работает панель со стандартного 2053 на какой-нибудь другой (лучше всего где-нибудь в верхнем конце диапазона, до 65535) ;

`Дополнительно Не обязательно:`
- Изменить корневой путь URL-адреса панели с / на что-то  /secretpanel/

![image](https://s584vla.storage.yandex.net/rdisk/8612da373081f61d9d8e8484e6fd375eae9ddcd7e01ad598915dfd3f943d71e0/662d0afc/GVkrPdnEhCiKAChhJEdOdtgoI8k7kIDBSwMw81gReCyw7y_xps6W6wcRjcUy4NPKE2DB0eqngkUyn6yod2Jc8Q==?uid=0&filename=vl2.png&disposition=inline&hash=&limit=0&content_type=image%2Fpng&owner_uid=0&fsize=52624&hid=2ac854353aa79edf352dedc17b29e060&media_type=image&tknv=v2&etag=fee7ce417878aaefb770b3b2a25420cd&ts=61714ccdbb700&s=c685332ab867b510aa66ec605e56dbb151e2e674a4d683f1970477cd60982685&pb=U2FsdGVkX1_LAxt06u9-2M_J2G3Bu3Q9UisBfsxpE0bBkwRJSxIfhUiDh2KBaqf06RsNST7J5JFHwwm1Hq4j-o2tVj23lS1-kymyGxOayvc)

на вкладке "Настройки безопасности" изменить стандартный админский пароль на свой:
![image](https://s639sas.storage.yandex.net/rdisk/7b9a06bb9d17b61c715eddd19a4e0d1559572af210bd247c49ced84d72ce081d/662d0ad0/GVkrPdnEhCiKAChhJEdOdjnqkCcG7domqygAmTM5vl3eKKbN2BInQa2UBRXGys9JVzkKl4Pe5zu-p0IwXl3Emg==?uid=0&filename=vl3.png&disposition=inline&hash=&limit=0&content_type=image%2Fpng&owner_uid=0&fsize=38114&hid=de3137cb6450f9e9f90a9f72fef80d3e&media_type=image&tknv=v2&etag=0ba71e8157490c06b265e5f601b69a78&ts=61714ca3c5400&s=894545516a688de63c96b579f79727671055fe88fd2e7d70482ab0deb7581587&pb=U2FsdGVkX18QuM3APIBUZRZz3tWfV0oWjjdTZ1svye8JM1ILOVy7ZN1VF2lhL-HpcpQc930XQ1iaeNFFOkGQQfV1oIIIlk-_F7DuxhKA2os)

`5. Настройка маскировки(Vless):`
  ![image](https://s93klg.storage.yandex.net/rdisk/ae8ad2cf8cb2e98f9f2c223feed7466a2cfb0c1ce1b5695485ed965df456efbd/662d0a9b/GVkrPdnEhCiKAChhJEdOdrmGiHGBD8IruLhSRHGqmTgxheTIxrvGwc68UzPUV7ycayrXVjpfMYQ5v07ihxTnLg==?uid=0&filename=vl4%20%282%29.png&disposition=inline&hash=&limit=0&content_type=image%2Fpng&owner_uid=0&fsize=89166&hid=e537e6d44ca985b570fbe843043930c9&media_type=image&tknv=v2&etag=fd85e3ca87ef311a73cd898d6dc3a6d3&ts=61714c7139cc0&s=a7af59e1472ed9d54c5015147cb6fa9a3028fa5ddd44c2d885a9d3616160c676&pb=U2FsdGVkX1-9n6gLQ2XAC7IqiqE4TGEZcD9Xg24QauMroNI_Po7sQBnvvEm1q3ggocbL35Q_y_NQc4XDgkzf8v7TUeEUtwDJm7KEGKQ-P48)

 `Примечание` - любое название;
`Протокол` - "vless",
`Listening IP`  - оставляем пустым;
"Порт" -  ставим 443;

Добавление Пользователя:
![image](https://s113klg.storage.yandex.net/rdisk/1809ee80fcac56795f038d2972ddb01b3d68354706e013fa5d084eae981e8191/662d0a51/GVkrPdnEhCiKAChhJEdOdhRxTL8yKBy3baAXH3E1S9Bm0BGbXPjGN0IE9LhqYCG1EVuUhWbkj62JXEgcUpbxGQ==?uid=0&filename=vl5.png&disposition=inline&hash=&limit=0&content_type=image%2Fpng&owner_uid=0&fsize=248545&hid=95e83c7fcd2057259b08a00909d4a644&media_type=image&tknv=v2&etag=3b7c712644fb71b4eaceed65125bea6d&ts=61714c2aa7640&s=48fe8232e6d4e626daa266416ee730be4d720f5ee9bf38b8fdc059a834ce53e6&pb=U2FsdGVkX1-GVh5Ll8_Gbt_y7y8oV7xwgxfUM19VSu_6w3OAeKpym6ETwaA9AL-2dfYQBwGAzz9-R7uI0Lw5tqhrbOZfPcCdngje5-fjVik)
![image](https://s113klg.storage.yandex.net/rdisk/1809ee80fcac56795f038d2972ddb01b3d68354706e013fa5d084eae981e8191/662d0a51/GVkrPdnEhCiKAChhJEdOdhRxTL8yKBy3baAXH3E1S9Bm0BGbXPjGN0IE9LhqYCG1EVuUhWbkj62JXEgcUpbxGQ==?uid=0&filename=vl5.png&disposition=inline&hash=&limit=0&content_type=image%2Fpng&owner_uid=0&fsize=248545&hid=95e83c7fcd2057259b08a00909d4a644&media_type=image&tknv=v2&etag=3b7c712644fb71b4eaceed65125bea6d&ts=61714c2aa7640&s=48fe8232e6d4e626daa266416ee730be4d720f5ee9bf38b8fdc059a834ce53e6&pb=U2FsdGVkX1-GVh5Ll8_Gbt_y7y8oV7xwgxfUM19VSu_6w3OAeKpym6ETwaA9AL-2dfYQBwGAzz9-R7uI0Lw5tqhrbOZfPcCdngje5-fjVik)

`6. Подключение:`

Нажав на значок QR-кода, панель покажет QR-код, который можно отсканировать камерой в мобильных клиентах (v2rayNG или Nekobox на Android, Wings X/FoXray или Shadowrocket на iOS).
   ![image](https://s1027sas.storage.yandex.net/rdisk/61709901cc022546024d05d834153f03b79dcdaf86c7f5cced60e6a071339716/662d0d8a/GVkrPdnEhCiKAChhJEdOdkXPUNw7EbJ6SHOcAtHQ7SCmXyjlzp4nkwDYMw4t1LjzUPYI33uh3DwLxqxX_TN1XQ==?uid=0&filename=vl7.png&disposition=inline&hash=&limit=0&content_type=image%2Fpng&owner_uid=0&fsize=76884&hid=6d1e5583ff9799bd8b0b119675b0b127&media_type=image&tknv=v2&etag=17fa42b6a00651a03c3f225f3406a92f&ts=61714f3d6f680&s=1ab503ba73843ef8342cff9cb9fe6ea36169c3bc5573048e97f3dca5cfc29f3e&pb=U2FsdGVkX19D7O-fqpFU7GEMaqNzbExvp8YhPPKQo1b40Bi6qhBDffVjz9Ie5J7vy6KIseCNFF1o5j1b5g_vVKq1ab06_grQ2Yz_VnrLcHE)


`7. Мониторинг:`

   ![image](https://s96vla.storage.yandex.net/rdisk/e9e47e9e912908803da8b0bb10d789dd5cd370a8c3479591335f5ba7f45e9d29/662d09f5/GVkrPdnEhCiKAChhJEdOdlD9mlPDiNndmyPCbITeyjXbF7GXspKXyADEYPIwzkNDksOV3Rek_lUSHKEBdfTHZg==?uid=0&filename=vl8.png&disposition=inline&hash=&limit=0&content_type=image%2Fpng&owner_uid=0&fsize=59061&hid=79430a6623eec164a0635753095128be&media_type=image&tknv=v2&etag=a9e1557cbaeaa73ca3cbe8415879f2b9&ts=61714bd2ea740&s=cba236efda84016d59a3f2b60137aa928bc5c223407e31089834a3b7c75fb804&pb=U2FsdGVkX19NGZZb3xsF7LhCZQkrraReh-HHenng4cuIQLz8XfhH45uT-Hd1_wA7hG9Px0ZuzNRO_-SuY-vJMgMHpZnF7OK5qp4jvaUrm7c)
</details>
