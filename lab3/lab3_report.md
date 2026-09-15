University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [Введение в веб технологии](https://itmo-ict-faculty.github.io/introduction-in-web-tech/)  
Year: 2026/2027  
Group: U4225  
Author: Davidyan Milana Eduardovnа  
Lab: Lab0  
Date of create: 13.09.2026  
Date of finished: 

# Лабораторная работа №3

## Мониторинг с Prometheus и Grafana

### Ход работы

Для выполнения лабораторной работы была подготовлена локальная система мониторинга на базе Docker, Prometheus, Node Exporter и Grafana.

## Создание конфигурации Prometheus

Была создана папка:

```text
prometheus
```

В ней был создан файл:

```text
prometheus/prometheus.yml
```

Содержимое конфигурации:

```yaml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['prometheus:9090']

  - job_name: 'node-exporter'
    static_configs:
      - targets: ['node-exporter:9100']
```

В конфигурации был установлен интервал сбора метрик `15s`.

Также были добавлены два источника метрик:

- Prometheus;
- Node Exporter.

## Создание Docker-сети

Для взаимодействия контейнеров была создана общая сеть:

```powershell
docker network create monitoring
```

Наличие сети было проверено командой:

```powershell
docker network ls
```

## Запуск Node Exporter

Для сбора системных метрик был запущен контейнер Node Exporter:

```powershell
docker run -d --name node-exporter --network monitoring -p 9100:9100 prom/node-exporter
```

Работа Node Exporter была проверена в браузере по адресу:

```text
http://localhost:9100/metrics
```

На странице отображались системные метрики.

## Запуск Prometheus

Для хранения данных Prometheus был создан Docker volume:

```powershell
docker volume create prometheus-data
```

После этого был запущен контейнер Prometheus:

```powershell
docker run -d --name prometheus --user 0:0 --network monitoring --restart unless-stopped -p 9090:9090 -v prometheus-data:/prometheus -v "C:\Users\user\Desktop\monitoring-lab\prometheus:/etc/prometheus" prom/prometheus --config.file=/etc/prometheus/prometheus.yml --storage.tsdb.path=/prometheus --storage.tsdb.retention.time=200h --web.enable-lifecycle
```

Для обхода проблемы с запуском контейнера был явно указан пользователь:

```text
--user 0:0
```

Работа Prometheus была проверена в браузере по адресу:

```text
http://localhost:9090
```

Интерфейс Prometheus успешно открылся.

## Запуск Grafana

Для хранения данных Grafana был создан volume:

```powershell
docker volume create grafana-data
```

После этого был запущен контейнер Grafana:

```powershell
docker run -d --name grafana --network monitoring --restart unless-stopped -p 3000:3000 -v grafana-data:/var/lib/grafana -e "GF_SECURITY_ADMIN_PASSWORD=admin" grafana/grafana
```

Grafana была открыта в браузере:

```text
http://localhost:3000
```

Для входа использовались данные:

```text
Login: admin
Password: admin
```

## Настройка Grafana

В Grafana был добавлен источник данных Prometheus.

Для подключения использовался адрес:

```text
http://prometheus:9090
```

После сохранения источника данных была проверена успешность подключения.

## Создание дашборда

В Grafana был создан дашборд:

```text
System Monitoring
```

Для визуализации были добавлены три панели.

### CPU

Для отображения данных процессора использовалась метрика:

```promql
node_cpu_seconds_total
```

### Память

Для отображения доступной памяти использовалась метрика:

```promql
node_memory_MemAvailable_bytes
```

### Диск

Для отображения доступного дискового пространства использовалась метрика:

```promql
node_filesystem_avail_bytes
```

На дашборде были успешно построены графики для CPU, памяти и диска.

## Проверка контейнеров

Состояние всех контейнеров было проверено командой:

```powershell
docker ps
```

В результате были запущены три контейнера:

```text
node-exporter
prometheus
grafana
```

Все контейнеры находились в состоянии `Up`.

## Вывод

В ходе лабораторной работы была настроена система мониторинга с использованием Prometheus и Grafana.

Node Exporter использовался для сбора системных метрик, Prometheus — для их хранения и обработки, а Grafana — для визуализации.

Был создан дашборд с графиками для CPU, памяти и дискового пространства.

Также была настроена общая Docker-сеть для взаимодействия контейнеров и выполнена финальная проверка их работы.

<img width="1902" height="745" alt="image" src="https://github.com/user-attachments/assets/36dcc040-85f3-40e8-baa6-06ede6317dde" />
<img width="1897" height="589" alt="image" src="https://github.com/user-attachments/assets/783f8237-3cd5-4f8c-860a-44b484acf226" />
<img width="957" height="191" alt="image" src="https://github.com/user-attachments/assets/d784ecf5-4673-4cd1-834a-06efc616bc7c" />
<img width="779" height="561" alt="image" src="https://github.com/user-attachments/assets/74de9ef9-c264-449c-adc1-3c66bb179585" />
<img width="742" height="608" alt="image" src="https://github.com/user-attachments/assets/8df21099-6064-4ef6-ba21-f122a10faa8e" />
<img width="730" height="231" alt="image" src="https://github.com/user-attachments/assets/60f919ca-695c-45a3-81f1-598de7cb720b" />
<img width="943" height="308" alt="image" src="https://github.com/user-attachments/assets/3b3917c0-ba85-4a21-a6a7-e476799ebffe" />
<img width="1082" height="835" alt="image" src="https://github.com/user-attachments/assets/542aff32-e8a2-4d5a-bbea-9bacf114e70c" />
<img width="1095" height="850" alt="image" src="https://github.com/user-attachments/assets/911bc3f3-7529-4aac-8489-67a71d9c75c8" />
<img width="1101" height="868" alt="image" src="https://github.com/user-attachments/assets/b796c069-c0d2-44c6-944c-8106992eb5ed" />
<img width="1114" height="835" alt="image" src="https://github.com/user-attachments/assets/8e977e51-dd2c-45fc-9a85-c12eabe4150a" />
<img width="1329" height="212" alt="image" src="https://github.com/user-attachments/assets/52f1c8af-b7b0-44ff-ae8f-6c8287a40038" />
