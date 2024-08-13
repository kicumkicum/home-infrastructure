# Инфраструктура домашней сети

## СПб

- Роутер Mikrotik
  - [ ] VPN клиент
- ТВ
  - [ ] Корректная работа YouTube

## Ульяновск

- Роутер Mikrotik `RB952Ui-5ac2nD r2`
  - [ ] VPN клиент
    - [ ] Настройка Wireguard
      - [x] 1. Обновить роутер до версии 7.1+
      - [x] 2. Импортировать во вкладке Wireguard конфиг [wg.conf](./configs/wg.conf). Это создаст Interface и Peer
      - [x] 3. Создать Firewall-NAT правило. Видимо это нужно для корректной работы поверх PPoE провайдера https://dzen.ru/a/YlSlHeNcqySLSmCL (https://kiberlis.ru/mikrotik-wireguard-client/)
      - [x] 4. Создать IP-Route с `Dst. Address: 0.0.0.0/0` на `Gateway: wg (созданный на шаге 1)`. Включение/выключение управляет направлением трафика (через vpn или нет)
      - [x] 5. Создать IP-Addresses с Adress из диапазона Wireguard Server с Network из ip-адреса внутреннего ip адреса сервера (не endpoint)
      - [ ] 6. Создать разные таблицы маршрутизации - для обычного соединения и VPN. Иначе, при переключении на VPN кешированные запросы ходят по прежнему маршруту - через провайдера напрямую https://dzen.ru/a/YlSlHeNcqySLSmCL (https://kiberlis.ru/mikrotik-wireguard-client/)
      - [ ] Настроить список маршрутов
      - [ ] Настроить маркирование пакетов
      - [x] Задать MTU 1400 для интерфейсе VPN. Субъективно это существенно подняло скорость
      - [ ] 7. Динамическое переключение канала на VPN, если контент заблокирован
        - [ ] Если прописать подсети ресурсов руками, то их нужно поддерживать, потому что ip'ы меняются
        - [ ] Если подключать списки по BGP, то это очень большое количество маршрутов, которое в итоге упрется в производительность роутера, ведь списки постоянно растут
        - [ ] Если определять заблокированный контент по косвенным признакам, то это облегчит работу системы, но потребуется настройка для каждого провайдера
          - [ ] У провайдера Evo такое поведение
            1. Запрос висит
            2. Отвечает таймаутом
            3. Итог
              1. Можно по таймауту запросы отправлять в vpn
              2. Если запрос вернулся удачно, то добавить его в список на 1 час
              3. Шаг 0: Если запрос есть в списке, то сразу отправить его в vpn
              4. Удалять ip из списка через час (не известно, можно ли так делать в Mikrotik)
      - [ ] Особенности и проблемы
        - [x] Distance должен быть одинаковым у PPPoE и Wireguard
        - [ ] tracepath показывает, что одни запросы идут на провайдера, а другие на vpn. например, vk.com идет на vpn, а habr.com идет на провайдера
          - [ ] ...
  - [ ] Обход DPI (каким-либо образом)
  - [ ] Блокировка рекламы
- NAS
  - [ ] Настройка системы
    - [ ] 2 x 14TB HDD в зеркале для данных
    - [ ] 2 x 1TB SSD в зеркале (или не в зеркале с бекапом системы) для системы и кеша
    - [ ] Возможность подключения стороннего диска для прочтения данных, без форматирования
    - [ ] Прогресс
      - [x] Попробовал TOS v5: Мало приложений; Разлогины веб-сессии; Нет возможности ставить linux-приложения из какого-нибудь репозитория с помощью opkg или типа того
      - [x] Попробовал TOS v6: Чуточку лужне центр настроек; Мало приложений; (?) Нет разлогинов веб-сессии; Нет возможности ставить linux-приложения из какого-нибудь репозитория с помощью opkg или типа того; Диски все время шумели, возможно туда писались логи. Возможно можно подключать диски без форматирования, еще не пробовал
      - [ ] Нужно попробовать ХРenology. Ожидается: Пакетный менеджер; Больше приложений.
  - [ ] Данные
  - [ ] Бекапы внутренние
  - [ ] Бекапы внешние
    - [ ] Google photo -> NAS
    - [ ] GitHub -> NAS
    - [ ] NAS -> mail.cloud (webdav)
  - [ ] Синхронизации
    - [ ] Google Photo
  - [ ] Сервисы
    - [ ] Torrent-качалка
    - [ ] PLEX
    - [ ] DLNA
  - [ ] Виртуальные машины
    - [ ] Windows для бухгалтерии
    - [ ] Windows для экспериментов и задач
    - [ ] MacOS
  - [ ] Just for fun
    - [ ] Steam Link для игры в браузере
- ТВ Бокс
  - [ ] Корректная работа YouTube
- Прочие клиенты

## Чудово

- Роутер Mikrotik
  - [ ] VPN клиент
- ПК мамы
  - [ ] Корректная работа YouTube
- Прочие клиенты

## Европа

- VPS
  - [ ] VPN сервер
    - [x] Amnesia (черновой вариант)
    - [x] VPN Wireguard server https://habr.com/ru/articles/738408/
      - [x] Настройка Wireguard сервера https://timeweb.cloud/tutorials/network-security/wireguard-na-svoem-servere
        - [x] Настройка локального клиента перед настройкой роутера, для понимания работы с протоколом
          - Локальный конфиг клиента [wg.conf](./configs/wg.conf). Потребуется для настройки роутера
        - `!` После настройки и перезапуска сервиса приконектиться клиентом не получалось. Помогло перезагрузка сервера
        - Пишут, что Wireguard не помогает обойти DPI. Видимо нужно другое решение, но начну с этого
        - Пишут, что OpenVPN очень ресурсоемкий для Miktorik
        - Есть мнение, что наиболее хорошим решением является поднять дополнительный VPS в России, куда идти легковесным протоколом, а дальше уже идти на заграничный серьезный VPN. Но не понятно, как это должно помочь, если трафик то попадет под эвристику. Возможно, внутри страны не будут за этим следить
  - [ ] Настройка сервера
    - [x] https://xakep.ru/2022/02/08/vps-server-todo/
    - [ ] Документировние для последующего воспроизведения
