`Шаги по установке и настройке 3X-UI для сервера X-Ray с поддержкой VLESS и других протоколов:`
<details>
<summary>Подготовка</summary>

`1. Выбор домена для маскировки:`
   - Найдите подходящий иностранный сервер, который не заблокирован Роскомнадзором и поддерживает TLSv1.3 и HTTP/2.
   - Убедитесь, что у сервера есть статическая главная страница без редиректов.

`2. Подготовка сервера:`
   - Установите Docker на ваш VPS, если он ещё не установлен.
   - Убедитесь, что ваш VPS имеет статический публичный IP-адрес.
</details>





<details>
  <summary>Установка панели 3X-UI в Docker</summary>

#### Установка

1 Устанавливаем докер:

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
ИЛИ
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
<summary> Настройка 3X-UI:</summary>
   осталось - настроить ее:

Для 3X-UI идем браузером по адресу http://yourserverip:2053/panel/, где yourserverip - IP-адрес вашего сервера или доменное имя, если оно у вас есть и настроено (обратите внимание, протокол http://, а не https://).

Логинимся под стандартными реквизитами admin/admin и видим панель управления:

![image](https://github.com/sakol86/my_guides/assets/86907205/4b6ce615-f9ad-4eae-ba75-fbbe936597c7)


`4.1 Обязательно Переходим в Настройки панели и там:`

- Изменить порт на котором работает панель со стандартного 2053 на какой-нибудь другой (лучше всего где-нибудь в верхнем конце диапазона, до 65535) ;

Дополнительно Не обязательно:
- Изменить корневой путь URL-адреса панели с / на что-то  /secretpanel/

![image](https://github.com/sakol86/my_guides/assets/86907205/b82201b4-4576-4de3-be89-74a86fb31077)


на вкладке "Настройки безопасности" изменить стандартный админский пароль на свой:

![image](https://github.com/sakol86/my_guides/assets/86907205/b9fb3818-6bbb-4b7d-a680-784c5cc5b2f8)


`5. Настройка маскировки(Vless):`

  [скрин vl4](https://downloader.disk.yandex.ru/preview/c2e40ca6bfd6122a94164f4aa9584999f111b4a2bc2c1c11ba6af8645b281e85/662cf995/HlnUSckG2n_UPColvw_7xyoeQ_yhELpCREq4Nyw4cBUlqgXX41-O8WVMM5j_TBFBh1iMx91DkwNNQ414uxAsGw%3D%3D?uid=0&filename=vl4%20%282%29.png&disposition=inline&hash=&limit=0&content_type=image%2Fpng&owner_uid=0&tknv=v2&size=2048x2048)

 `Примечание` - любое название;
`Протокол` - "vless",
`Listening IP`  - оставляем пустым;
"Порт" -  ставим 443;

`5.1 Добавление Пользователя:`

![image](https://github.com/sakol86/my_guides/assets/86907205/dda5a4e6-16c4-40ac-bcce-71c7d72f6471)
![image](https://github.com/sakol86/my_guides/assets/86907205/217e2e52-3375-43ee-bfbe-905fc2364f43)

`6. Подключение:`

Нажав на значок QR-кода, панель покажет QR-код, который можно отсканировать камерой в мобильных клиентах (v2rayNG или Nekobox на Android, Wings X/FoXray или Shadowrocket на iOS).

![image](https://github.com/sakol86/my_guides/assets/86907205/b7c12b66-4c50-461d-8149-8735db30720c)
</details>



`7. Мониторинг:`

   ![image](https://github.com/sakol86/my_guides/assets/86907205/7ca86bc6-8b39-4555-adf8-978ab3660de3)
