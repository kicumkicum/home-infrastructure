# Инфраструктура домашней сети

## СПб

- Роутер Mikrotik
  - [ ] VPN клиент
- ТВ
  - [ ] Корректная работа YouTube

## Ульяновск

- Роутер Mikrotik
  - [ ] VPN клиент
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
        - [ ] Настройка локального клиента перед настройкой роутера, для понимания работы с протоколом
          - Локальный конфиг клиента [wg.conf](./configs/wg.conf). Потребуется для настройки роутера
        - После настройки и перезапуска сервиса приконектиться клиентом не получалось. Помогло перезагрузка сервера
  - [ ] Настройка сервера
    - [x] https://xakep.ru/2022/02/08/vps-server-todo/
    - [ ] Документировние для последующего воспроизведения
