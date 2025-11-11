# OpenSSH / ssh

## Описание
OpenSSH клиент для безопасного подключения к удаленным серверам через SSH протокол, использование ключей для аутентификации.

## Уровень
Основы

## Примеры использования
- Подключение с паролем: `ssh user@target.com`
- Подключение с ключом: `ssh -i id_rsa user@target.com`
- Проброс портов: `ssh -L 8080:localhost:80 user@target.com`
- Указание порта: `ssh -p 2222 user@target.com`
- Выполнение команды на удаленном сервере: `ssh user@target.com "ls -la"`

## Решение проблем

### Ошибка "Error connecting to agent: No such file or directory"

Эта ошибка возникает когда SSH агент не запущен. Решения:

#### Windows (PowerShell)
1. **Использовать ключ напрямую** (без агента):
   ```powershell
   ssh -i C:\Users\username\.ssh\id_rsa user@target.com
   ```

2. **Установить и запустить службу ssh-agent** (требует админ-прав):
   ```powershell
   # Установка службы (один раз, от администратора)
   Set-Service -Name ssh-agent -StartupType Automatic
   Start-Service ssh-agent
   
   # Добавление ключа
   ssh-add C:\Users\username\.ssh\id_rsa
   ```

3. **Использовать Git Bash** (встроенная поддержка ssh-agent):
   ```bash
   eval $(ssh-agent -s)
   ssh-add ~/.ssh/id_rsa
   ```

#### Linux/macOS
```bash
# Запуск агента
eval $(ssh-agent -s)

# Добавление ключа
ssh-add ~/.ssh/id_rsa

# Проверка добавленных ключей
ssh-add -l
```

### Проверка подключения
```bash
# Тест подключения с отладкой
ssh -v user@target.com

# Проверка доступности порта
nc -zv target.com 22
```

## Ресурсы для изучения
- [OpenSSH Documentation](https://www.openssh.com/manual.html)
- SSH ключи и безопасность

## Заметки
(Добавляйте свои заметки, примеры кода или ссылки на видео.)

