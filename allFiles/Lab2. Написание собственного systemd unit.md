#linux 
Цель: научиться писать systemd unit, изучить секции **Unit**, **Service**, **Install**, разобрать концепцию **security hardening**

Архитектура модуля systemd:
[Unit]
Description=Heartbeat Tracker
After=network.target

[Service]
Type=exec
User=svc-heartbeat
Group=svc-heartbeat
WorkingDirectory=/opt/heartbeat

##security hardening
NoNewPrivileges=true
ProtectSystem=strict
ReadWritePaths=/var/lib/heartbeat
ProtectHome=true
RestrictAddressFamilies=AF_UNIX

ExecStart=/bin/bash /opt/heartbeat/heart.sh
Restart=always

[Install]
WantedBy=multi-user.target

**Bash скрипт**
`#!/bin/bash
while true; do
	echo "$(date) $ $  I am alive > /var/lib/heartbeat/heartbeat.log"
	sleep 60
done`

**Краткое описание**

Каждые systemd от имени системного пользователя svc-heartbeat выполняет скрипт heart.sh в директории /opt/heartbeat `(Права на директорию:
`drwx-r-x--- root:svc-heartbeat; Права на heart.sh:
`-rw-r-x--- root:svc-heartbeat)` 
который логирует строку "I am alive" каждые 60 секунд в /var/lib/heartbeat/heartbeat.log
(Права на директорию: drwx-r-x--- root:svc-heartbeat;
Права на файл: -rw-------- svc-heartbeat:svc-heartbeat)

**Результаты проверок**
работа модуля логируется в journald, скрипт отрабатывает, процесс работает от svc-heartbeat, а не от root, перезапускается при любом падении, автоматически запускается после перезагрузки машины


**Что нового понял**
1. Улучшил понимание настройки прав на файлы и директории
2. Узнал о секциях unit, service, install. разобрался с их параметрами
3. Узнал о systemd security hardening
4. Написал собственный systemd unit и простейший bash-script
5. Разобрался с типами запуска simple, exec, forking, oneshot
6. Разобрался с Exec* и Restart* операциями
7. узнал о *.target режимах запуска в секции install
8. Понял разницу между правами файловой системы и ограничениями, накладываемыми systemd.
9. Разобрался с принципом минимальных привилегий (Principle of Least Privilege).
10. Научился диагностировать проблемы сервиса через `journalctl`, `systemctl status` и перезапуск конфигурации.


---
Раздел [[Linux]]