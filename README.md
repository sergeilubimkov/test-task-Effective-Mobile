# Тестовое задание Effective-Mobile

## Содержание

- [Структура и описание проекта](#project_description)
- [Установка и запуск](#install_start)

## <a name="project_description"></a>Структура и описание проекта
Данный проект представляет выполненное тестовое задание для Effective-Mobile. В рамках тестового задания были реализованы bash-скрипт, а также unit-файл и таймер.

**Описание проекта:**

Скрипт выполняет мониторинг процесса `test` каждую минуту и выполняет следующие действия: 
Проверяет состояние процесса каждую минуту и выполняет следующие действия:

- Если процесс **работает**, отправляет HTTP-запрос на `https://test.com/monitoring/test/api`
- Если процесс **перезапущен**, пишет запись в `/var/log/monitoring.log`
- Если **сервер мониторинга недоступен**, также пишет запись в лог
- Если процесс **не запущен**, ничего не делает

**Структура проекта:**
- ```task``` - Основной bash-скрипт мониторинга
- ```test``` - Тестовый процесс для проверки работы 
- ```task.service``` - Unit-файл для systemd 
- ```task.timer``` - Таймер, запускающий скрипт каждую минуту

## <a name="install_start"></a>Установка и запуск
Копирование файлов
```bash
sudo cp task /usr/local/bin/task
sudo chmod +x /usr/local/bin/task
sudo mkdir -p /etc/systemd/system/
sudo cp task.service /etc/systemd/system/
sudo cp task.timer /etc/systemd/system/
```
Включение сервиса
```bash
sudo systemctl daemon-reload 
sudo systemctl enable --now task.timer
```


