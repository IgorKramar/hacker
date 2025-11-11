# Gobuster / Dirbuster / ffuf

## Описание
Инструменты для разведки веб-серверов: поиск скрытых файлов, директорий и эндпоинтов через словарные атаки.

## Уровень
Средний

## Примеры использования
- Поиск директорий: `gobuster dir -u http://target.com -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt`
- Поиск поддоменов: `gobuster dns -d target.com -w subdomains.txt`
- Фазинг с ffuf: `ffuf -w wordlist.txt -u http://target.com/FUZZ`
- Исключение ответов с определенной длиной: `gobuster dir -u http://target.com -w wordlist.txt --exclude-length 1234`
- Использование Dirbuster (GUI) для визуального анализа.

## Ресурсы для изучения
- [Gobuster GitHub](https://github.com/OJ/gobuster)
- [ffuf GitHub](https://github.com/ffuf/ffuf)
- Wordlists: SecLists, dirbuster wordlists

## Заметки
(Добавляйте свои заметки, примеры кода или ссылки на видео.)

