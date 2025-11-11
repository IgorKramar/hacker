# Hydra

## Описание
Hydra — инструмент для брутфорса паролей различных протоколов и сервисов: SSH, FTP, HTTP, веб-формы авторизации с использованием словарей.

## Уровень
Средний

## Примеры использования
- Брутфорс SSH: `hydra -l user -P passwords.txt ssh://target.com`
- Брутфорс FTP: `hydra -l user -P passwords.txt ftp://target.com`
- Брутфорс веб-форм: `hydra -l admin -P passwords.txt http-get://target.com/login`
- Использование wordlists для подбора паролей.

## Ресурсы для изучения
- [Hydra GitHub](https://github.com/vanhauser-thc/thc-hydra)
- Методики брутфорса паролей
- Wordlists для брутфорса (rockyou.txt)

## Заметки
(Добавляйте свои заметки, примеры кода или ссылки на видео.)

