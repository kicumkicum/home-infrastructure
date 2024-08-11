# Инфраструктура домашней сети

## СПб

- Роутер Mikrotik
  - [ ] VPN клиент
- ТВ
  - [ ] Корректная работа YouTube

## Ульяновск

- Роутер Mikrotik
  - [ ] VPN клиент
    - [ ] Настройка Wireguard
      - [x] 1. Обновить роутер до версии 7.1+
      - [x] 2. Импортировать во вкладке Wireguard конфиг [wg.conf](./configs/wg.conf). Это создаст Interface и Peer
      - [x] 3. Создать NAT правило. Видимо это нужно для корректной работы поверх PPoE провайдера
      - [x] 4. Создать Route с `Dst. Address: 0.0.0.0/0` на `Gateway: wg (созданный на шаге 1)`. Включение/выключение управляет направлением трафика (через vpn или нет)
      - [ ] 5. Создать разные таблицы маршрутизации - для обычного соединения и VPN. Иначе, при переключении на VPN кешированные запросы ходят по прежнему маршруту - через провайдера напрямую
- NAS
  - [ ] Данные
  - [ ] Бекапы
  - [ ] Синхронизации
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
  - [x] VPN сервер
    - [x] Amnesia (черновой вариант)
    - [x] VPN Wireguard server https://habr.com/ru/articles/738408/
      - [x] Настройка Wireguard сервера https://timeweb.cloud/tutorials/network-security/wireguard-na-svoem-servere
        - [x] Настройка локального клиента перед настройкой роутера, для понимания работы с протоколом
          - Локальный конфиг клиента [wg.conf](./configs/wg.conf). Потребуется для настройки роутера
        - `!` После настройки и перезапуска сервиса приконектиться клиентом не получалось. Помогло перезагрузка сервера
  - [ ] Настройка сервера
    - [x] https://xakep.ru/2022/02/08/vps-server-todo/
    - [ ] Документировние для последующего воспроизведения
