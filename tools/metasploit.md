# Metasploit (msfconsole)

## Описание
Metasploit Framework — комплексный инструмент для эксплуатации уязвимостей: настройка reverse shell listeners, брутфорс сервисов, сканирование уязвимостей.

## Уровень
Продвинутый

## Примеры использования
- Запуск msfconsole: `msfconsole` (можно без root прав)
- Настройка listener: `use exploit/multi/handler`
- Поиск эксплойтов: `search <vulnerability>`
- Брутфорс SSH: `use auxiliary/scanner/ssh/ssh_login`
- Сканирование портов: использование модуля Port Scanner
- Настройка параметров эксплойта: установка IP-адреса цели, портов
- Использование эксплойтов: запуск Ruby-скриптов для эксплуатации уязвимостей
- Использование Eternal Blue: `use exploit/windows/smb/ms17_010_eternalblue`
- Настройка опций: установка r-хостов (целевой IP) и хоста для прослушивания
- Получение Meterpreter: запуск эксплойта и получение интерактивного доступа к системе

## Ресурсы для изучения
- [Metasploit Documentation](https://docs.metasploit.com/)
- [Metasploit Unleashed](https://www.offensive-security.com/metasploit-unleashed/)

## Заметки
(Добавляйте свои заметки, примеры кода или ссылки на видео.)

