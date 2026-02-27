markdown

# Xray Configuration

Настройка Xray (VLESS + Reality) для базовой версии проекта.

**Основной конфиг:**

```bash
/usr/local/etc/xray/config.json

Пример с комментариями: ../config/example.config.json
Server Configuration
Минимальные параметры inbound
Field	Description
port	Порт входящего подключения (обычно 443)
protocol	vless
id	UUID пользователя
email	Идентификатор пользователя (для логов)
flow	Для Reality: xtls-rprx-vision
Пример секции clients
json

"clients": [
  {
    "id": "uuid-пользователя",
    "flow": "xtls-rprx-vision",
    "email": "username@server.com"
  }
]

Adding a New User
1. Сгенерировать UUID
bash

xray uuid
# или
uuidgen  # если установлен

2. Добавить в секцию clients

Открой конфиг:
bash

nano /usr/local/etc/xray/config.json

Найди секцию clients и добавь нового пользователя:
json

"clients": [
  {
    "id": "старый-uuid",
    "flow": "xtls-rprx-vision",
    "email": "old@server.com"
  },
  {
    "id": "новый-uuid",      # сгенерированный UUID
    "flow": "xtls-rprx-vision",
    "email": "new@server.com"
  }
]

3. Проверить конфиг
bash

xray run -test -config /usr/local/etc/xray/config.json

4. Перезапустить Xray
bash

systemctl restart xray

Reality Keys
Генерация ключей
bash

xray x25519

# Пример вывода:
# Private key: 6PojkKen7NLwOCgOzXK12R-pi0knJx7Qq-Gxxxxxxxx
# Public key: 6PojkKen7NLwOCgOzXK12R-pi0knJx7Qq-Gyyyyyyyyyy

# ShortID (8 символов)
openssl rand -hex 8
# Пример: 3a8f5c1e9d2b7a4c

Где использовать
Key	Где разместить
privateKey	В realitySettings сервера (конфиг Xray)
publicKey	В клиентском конфиге (для подключения)
shortId	В обоих конфигах (сервер и клиент)
Пример в конфиге
json

"realitySettings": {
  "show": false,
  "target": "www.microsoft.com:443",
  "xver": 0,
  "serverNames": [
    "www.microsoft.com"
  ],
  "privateKey": "6PojkKen7NLwOCgOzXK12R-pi0knJx7Qq-Gxxxxxxxx",
  "publicKey": "6PojkKen7NLwOCgOzXK12R-pi0knJx7Qq-Gyyyyyyyyyy",
  "shortIds": [
    "3a8f5c1e9d2b7a4c"
  ]
}

Validate Configuration

Перед перезапуском всегда проверяй конфиг:
bash

xray run -test -config /usr/local/etc/xray/config.json

Если ошибок нет — можно перезапускать:
bash

systemctl restart xray
systemctl status xray

Logs

Логи подключений пишутся в:
bash

/var/log/xray/access.log

Просмотр в реальном времени:
bash

tail -f /var/log/xray/access.log

Пример записи в логе:
text

192.168.1.100:54321 accepted tcp: www.google.com:443 [user@server.com]

Quick Troubleshooting
Проверить статус сервиса
bash

systemctl status xray

Проверить логи systemd
bash

journalctl -u xray -f

Проверить access.log
bash

tail -f /var/log/xray/access.log

Проверить, слушает ли порт
bash

ss -tulpn | grep 443
# или
netstat -tulpn | grep 443

Основные ошибки
Ошибка	Решение
permission denied	Проверь права на /var/log/xray
address already in use	Порт 443 занят другим сервисом (nginx?)
invalid private key	Неправильный формат ключа
failed to start	Ошибка в конфиге — проверь -test
Recommended Workflow

    Сгенерировать ключи (xray x25519 + openssl rand -hex 8)

    Сгенерировать UUID для пользователя

    Добавить пользователя в config.json

    Проверить конфиг (-test)

    Перезапустить Xray

    Проверить логи (journalctl -u xray -f)

    Проверить подключение с клиента

📚 Дополнительно

    Официальная документация Xray   - https://xtls.github.io/

    Генератор конфигов - https://raw.githubusercontent.com/chise0713/warp-reg.sh/master/warp-reg.sh
