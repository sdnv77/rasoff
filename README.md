# rasoff

**1C RAS Offensive Security Tool**

Автоматизированный инструмент поиска 1С серверов в инфраструктуре и выгрузка данных из Консоли Администрирования Кластера 1С в `.csv` файл.

## Установка
`git clone https://github.com/sdnv0x4d/rasoff.git`

Установка зависимостей:
```bash
apt install nmap
pip3 install -r req.txt
```

Запуск скрипта с указанием пути до утилиты `rac`: 
```bash
python3 main.py -u admin -p "p@$$w0rD" -b /opt/1cv8/x86_64/8.3.18.1741/rac -r 10.0.0.0/24 -n "--max-rate 10"
```

## Использование

| Аргумент                                     | Пример                                 | Пояснение
| :---------------------------------------------- | :-------------------------------------- | :----
| Помощь | `./main.py --help` |
| Утилита rac | `./main.py -b, --bin /opt/1cv8/x86_64/8.3.*.*/rac` | Утилита взаимодействия с Консолью администрирования кластеров 1С, поставляемая вместе с Технологической платформой/Сервером 1С.
| Диапазоны/хосты IP   | `./main.py -r, --range "10.0.0.3 10.0.0.4"`, `--range 10.0.0.0/24` | Диапазоны сетей/адреса хостов для сканирования через пробел.
| Имя Пользователя | `./main.py -u, --username "admin"` | Имя Пользователя консоли администрирования 1С.
| Пароль Пользователя | `./main.py -p, --password "p@$$w0rD"` | Пароль Пользователя консоли администрирования 1С.
| NMAP  | `./main.py -n, --nmap "--max-rate 10 -T4"` | Дополнительные аргументы для nmap-сканнера

### Работа приложения

**Преимущество данного инструмента в том, что можно использовать одну клиентскую версию вне зависимости от версии сервера.**

- Сканирование и поиск хостов с открытым 1545 портом
- Сбор информации по кластерам через `rac` подключение к найденным 1С серверам
- Получение списка информационных баз через `rac` подключение к 1С
- Получение информации по сессиям через `rac` подключение к 1С
- Создание отдельных `.csv` файлов с именами 1С серверов с информацией по сессиям 1С

> Где получить rac утилиту?
> 
> Согласно лицензионному соглашению, распространение серверных утилит 1С запрещено.
> 
> Официальный ресурс с диструбутивами [releases.1c.ru](https://releases.1c.ru/project/Platform83)

### Данные
Данные, которые получаем на выходе:
- Имя информационной базы
- Имя пользователя 1С
- Имя хоста, с которого осуществляется подключение к серверу
- Тип приложения
- Начало подключения
- Последняя активность
- IP-адрес клиента

## Лицензия

Licensed under the [GNU General Public License v3.0](https://www.gnu.org/licenses/gpl-3.0.html) License.
