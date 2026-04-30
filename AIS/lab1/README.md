**Лабораторная работа № 1**  
**по дисциплине “Администрирование информационных систем”**

Факультет: ПМИ  
Группа: ПМИ-23  
Студент: Болотин Д.В.  
Бригада: 13  
Преподаватели: Аврунев Олег Евгеньевич 


# Цели

- Развернуть виртуальный сервер в облачной платформе cloud.nstu.ru;
- Установить следующее компоненты информационной системы:
  - СУБД Postgres Pro Standard;
  - Web-сервер Nginx;
  - Web-приложение администрирования СУБД pgAdmin 4;
- Развернуть тестовую базу данных.

# Ход работы

## 1.Создание и настройка виртуальной машины

1.1 Авторизировались на сайте <https://cloud.nstu.ru/ui> и зашли на вкладку "Серверы".

1.2 Создали виртуальный сервер 
![](./pic/server_create.png)
![](./pic/server_prepare.png)
![](./pic/server_started.png)

1.3 Запустили виртуальный сервер и получили IP Адрес
![](./pic/server_ip.png)

1.4 Публикация сервера
![](./pic/server_publish.png)
![](./pic/server_ssh_info.png)

1.5 Вход на сервер, создание пользователя dba и выдача прав администратора
![](./pic/server_last.png)


## 2.Установка Postgres 18

2.1 Установка RPM репозитория
![](./pic/repo_install.png)

2.2 Установка PostgreSQL
![](./pic/psql_server_install.png)

2.3 Инициализация базы данных и добавление в автозапуск
![](./pic/db_init.png)
![](./pic/sysctl_postgre.png)
![](./pic/servise_status.png)

2.4 Проверка расположения файлов

2.4.1 Исполняемые файлы и кластера баз данных
![](./pic/location_bin&dbcluster.png)

2.4.2 Список баз данных
![](./pic/list_of_db.png)

2.4.3 Расположение файла параметров  
![](./pic/config_file.png)

2.4.4 Расположение файла параметров  
![](./pic/filepath_datadir.png)

2.4.5 Расположение файла журнала
![](./pic/logdir_path.png)

2.4.6 Данные о пользователях хранятся в системном каталоге pg_authid. Содержимое файла паролей:
![](./pic/pwd_data.png)

2.5 Создание пользователя СУБД dba с правами администратора.
![](./pic/posgres_usercreation.png)

## 3.Установка Nginx

3.1 Установка пакет nginx.
![](./pic/nsinx_install.png)
![](./pic/nginx_status&startup.png)

3.2 Доступ в локальном файерволе
![](./pic/firewall-cmd.png)

3.3 Публикация порта 80 как приложения TCP
![](./pic/server_publishing_2.png)
![](./pic/publishing_result.png)

3.4 Проверка доступности nginx  
![](./pic/curl_local.png)
![](./pic/httpserver.png)

## 4.Установка pgAdmin

4.1 Проверка наличие python3  
![](./pic/python3.png)

4.2 Установка pgAdmin4-web
![](./pic/pgAdmin4-web_1.png)
![](./pic/pgAdmin4-web_2.png)
![](./pic/pgAdmin4-web_3.png)
![](./pic/pgAdmin4-web_4_1.png)
![](./pic/pgAdmin4-web_4_2.png)

4.3 Создание необходимых каталогов  
![](./pic/6_3_1.png)
![](./pic/6_3_2.png)

4.4 Создание файла конфигурации  
![](./pic/6_4_1.png)

4.5 Создание файла службы pgadmin.service  
![](./pic/6_5_1.png)

4.6 Включение автозапуска и проверка состояния
![](./pic/6_7_1.png)

## 5.Проксирование pgAdmin через Nginx

5.1 Установка разрешения взаимодействия веб-сервера с сетью (проксирование).  
![](./pic/7_1_1.png)

5.2 Создание конфигурационного файла  
![](./pic/7_2_1.png)

5.3 Перезапуск nginx  
![](./pic/7_3_1.png)

5.4 Вход из браузера на url бригадной машины в pgAdmin и создание сервера, для адреса 127.0.0.1 и пользователя dba.  
![](./pic/7_4_1.png)
![](./pic/7_4_2.png)
![](./pic/7_4_3.png)
![](./pic/7_4_4.png)

## 6.Установка тестовой базы данных

6.1 Скачивание тестовой базы данных и распаковка  
![](./pic/8_1_1.png)
![](./pic/8_1_2.png)

6.2 Запуск psql с аргументом в виде извлеченного файла  
![](./pic/8_2.png)

6.2 Проверка налиция базы данных demo  
![](./pic/8_3.png)

# Таблицы с информацией о компонентах информационной системы
- Таблица 1  

<table><thead>
  <tr>
    <th>№</th>
    <th>Расположение исполняемых файлов, файлов данных</th>
    <th>Конфигурационные файлы</th>
    <th>Расположение журналов</th>
    <th>Как выполняется запуск</th>
  </tr></thead>
<tbody>
  <tr>
    <td>1</td>
    <td>/usr/bin</td>
    <td>/etc</td>
    <td>/var/log</td>
    <td>Подключение по ssh</td>
  </tr>
  <tr>
    <td>2</td>
    <td>/usr/pgsql-18/bin</td>
    <td>/var/lib/pgsql/18/data/postgresql.conf</td>
    <td>/var/lib/pgsql/18/data/log</td>
    <td>Служба systemd</td>
  </tr>
  <tr>
    <td>3</td>
    <td>/usr/pgadmin4/venv/bin</td>
    <td>/user/pgadmin4/web/config_local.py</td>
    <td>/home/dba/.pgadmin/pgadmin4.log</td>
    <td>Служба systemd с доступом к веб-приложению через прокси-соединение</td>
  </tr>
  <tr>
    <td>4</td>
    <td>/usr/sbin/nginx</td>
    <td>/etc/nginx</td>
    <td>/var/log/nginx/</td>
    <td>Служба systemd</td>
  </tr>
</tbody>
</table>

- Таблица 2  

<table><thead>
  <tr>
    <th>№</th>
    <th>Назначение, условное обозначение</th>
    <th>Наименование, версия, лицензия</th>
    <th>Метод доступа, url </th>
    <th>Учетные записи</th>
  </tr></thead>
<tbody>
  <tr>
    <td>1</td>
    <td>Операционная система</td>
    <td>AlmaLinux 9.4 (Seafoam Ocelot)</td>
    <td>ssh, ssh.cloud.nstu.ru:5980</td>
    <td>root, dba</td>
  </tr>
  <tr>
    <td>2</td>
    <td>СУБД</td>
    <td>PostgreSQL 18.3 <br> PostgreSQL License (free and open-source, permissive) </td>
    <td>Интерактивный терминальный интерфейс (CLI) psql</td>
    <td>postgres, dba</td>
  </tr>
  <tr>
    <td>3</td>
    <td>Пользовательский интерфейс</td>
    <td>pgadmin4-web <br>pgAdmin 4 is released under the PostgreSQL licence </td>
    <td>http://217.71.129.139:4775/browser/</td>
    <td>postgres, dba</td>
  </tr>
  <tr>
    <td>4</td>
    <td>Web-сервер</td>
    <td>nginx/1.20.1 <br>Nginx: BSD-2-Clause License</td>
    <td>http://217.71.129.139:4775/browser/</td>
    <td>nginx, dba</td>
  </tr>
</tbody>
</table>

**Последние записи журнала логов каждой компоненты:**
- OS  
![](./pic/OS_log.png)
- СУБД  
![](./pic/DB_log.png)
- PgAdmin4  
![](./pic/pgadmin_log.png)
- Nginx  
![](./pic/nginx_log.png)

**Диаграмма взаимодействия компонентов информационной системы**

```mermaid
graph TB
    Client["Web Browser<br/>http://localhost:8000"]
    
    subgraph VM["ВМ на облачной платформе cloud.nstu.ru"]
        subgraph Compose[" docker-compose"]
            Backend[" Backend приложение<br/>(Python FastAPI / Node.js Express)"]
            Postgres[" PostgreSQL 18<br/>port 5432"]
        end
    end
    
    Client -->|HTTP запросы<br/>GET/POST/PUT/DELETE| Backend
    Backend -->|SQL запросы| Postgres
    Postgres -->|результаты| Backend
    Backend -->|JSON ответы| Client
    
    style Client fill:#e1f5ff
    style Backend fill:#fff3e0
    style Postgres fill:#f3e5f5
    style Compose fill:#f0f0f0,stroke:#999,stroke-width:2px
```



# Вывод

Все поставленные цели были выполнены