# Hashcat / John the Ripper

## Описание
Инструменты для взлома хэшей паролей: Hashcat (GPU-ускоренный) и John the Ripper для брутфорса различных типов хэшей.

## Уровень
Средний

## Примеры использования
- Определение типа хэша: `hashcat --example-hashes`
- Взлом SHA-1 хэша: `hashcat -m 100 hash.txt rockyou.txt`
- Взлом passphrase SSH-ключа: `john --wordlist=rockyou.txt id_rsa`

## Ресурсы для изучения
- [Hashcat Documentation](https://hashcat.net/hashcat/)
- [John the Ripper](https://www.openwall.com/john/)
- [Hashcat Mode Reference](https://hashcat.net/wiki/doku.php?id=hashcat)

## Заметки
(Добавляйте свои заметки, примеры кода или ссылки на видео.)

