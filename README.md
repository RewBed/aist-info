# Установка WSL на Windows Server 2019

Это руководство поможет вам установить Windows Subsystem for Linux (WSL) на **Windows Server 2019**, который поддерживает WSL 1, но не имеет доступа к Microsoft Store для загрузки дистрибутивов Linux.

## Шаг 1: Включение WSL через PowerShell

1. **Откройте PowerShell с правами администратора**:
   - Нажмите `Win + X` и выберите **"Windows PowerShell (Admin)"**.

2. **Включите WSL**:
   - Выполните следующую команду для включения WSL:
     ```powershell
     Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
     ```
   - После выполнения команды **перезагрузите сервер**, чтобы изменения вступили в силу.

## Шаг 2: Загрузка дистрибутива Linux

Так как Windows Server 2019 не имеет доступа к Microsoft Store, вам нужно вручную загрузить дистрибутив Linux.

1. **Скачайте дистрибутив Linux**:
   - Перейдите на официальную страницу Microsoft, чтобы найти дистрибутивы для WSL: [WSL Distributions](https://docs.microsoft.com/en-us/windows/wsl/install-manual).
   - Примеры загрузки:
     - [Ubuntu 18.04](https://aka.ms/wsl-ubuntu-1804)
     - [Ubuntu 20.04](https://aka.ms/wsl-ubuntu-2004)

2. **Установите дистрибутив Linux**:
   - После загрузки файла `.appx` (например, `Ubuntu.appx`), откройте PowerShell с правами администратора и перейдите в папку, где находится файл.
   - Выполните следующую команду:
     ```powershell
     Add-AppxPackage .\Ubuntu.appx
     ```
   - Это установит дистрибутив Linux на вашу систему.

3. **Запуск и настройка дистрибутива**:
   - После установки найдите дистрибутив Linux в списке приложений и запустите его. При первом запуске вам потребуется создать учетную запись пользователя и задать пароль.
   - Система выполнит начальные настройки.

## Шаг 3: Обновление и настройка дистрибутива Linux

1. **Обновите пакеты**:
   - Чтобы убедиться, что у вас установлены все последние обновления, выполните команду:
     ```bash
     sudo apt update && sudo apt upgrade
     ```

2. **Установите необходимые инструменты**:
   - Если вы планируете развернуть веб-сервер или другие сервисы, установите дополнительные пакеты, такие как PHP 8.2, Composer, MySQL, Redis и другие необходимые расширения:
     ```bash
     sudo apt install software-properties-common
     sudo add-apt-repository ppa:ondrej/php
     sudo apt update
     sudo apt install php8.2 php8.2-cli php8.2-fpm php8.2-mbstring php8.2-xml php8.2-zip php8.2-curl php8.2-pgsql php8.2-redis php8.2-ctype php8.2-dom php8.2-fileinfo php8.2-filter php8.2-hash php8.2-openssl php8.2-pcre php8.2-session php8.2-tokenizer php8.2-xml composer mysql-server redis-server postgresql postgresql-contrib librdkafka-dev
     ```

   - Убедитесь, что все необходимые библиотеки установлены, такие как `pcntl`, `pdo_pgsql`, `pgsql`, `redis`, `rdkafka`, `zip`, `ctype`, `curl`, `dom`, `fileinfo`, `filter`, `hash`, `mbstring`, `openssl`, `pcre`, `session`, `tokenizer`, `xml`.

## Шаг 4: Работа с WSL

1. **Запуск WSL**:
   - После установки дистрибутива вы можете запустить WSL напрямую из командной строки или PowerShell, выполнив команду:
     ```powershell
     wsl
     ```
   - Либо просто запустите установленный дистрибутив (например, `Ubuntu`).

2. **Доступ к файловой системе Windows**:
   - Внутри WSL вы можете получить доступ к файловой системе Windows через `/mnt/`. Например, диск `C:` доступен по пути `/mnt/c`.

3. **Обновление WSL**:
   - Windows Server 2019 поддерживает только **WSL 1**, и его нельзя обновить до **WSL 2**, так как WSL 2 был представлен в более поздних версиях Windows.

## Ограничения WSL на Windows Server 2019

- **Версия WSL**: Поддерживается только **WSL 1**. Windows Server 2019 не может использовать WSL 2, который был представлен в более поздних версиях.
- **Производительность**: WSL 1 работает напрямую с файловой системой Windows, что может снижать производительность по сравнению с полноценной виртуальной машиной или WSL 2, использующим виртуализированное ядро Linux.
- **Поддержка Docker**: Docker можно установить, но его функциональность будет ограничена из-за использования WSL 1.

## Альтернативы WSL на Windows Server 2019

Если вам нужны более широкие возможности для работы с Linux-приложениями на Windows Server, рассмотрите следующие альтернативы:

1. **Hyper-V**:
   - Используйте **Hyper-V** для запуска полноценной виртуальной машины с Linux. Это даст вам полный контроль над окружением и лучшую производительность.

2. **Полная установка Linux в виртуальной машине**:
   - Используйте VirtualBox или VMware для запуска виртуальной машины с Linux. Это может быть хорошей альтернативой для более сложных задач.

## Резюме

Вы можете развернуть **WSL** на **Windows Server 2019**, что обеспечит вам возможность работы с Linux прямо на сервере. Однако эта версия поддерживает только **WSL 1**, что ограничивает производительность и функциональность по сравнению с **WSL 2**.

Шаги для установки WSL включают:
1. Включение функции WSL через PowerShell.
2. Ручную загрузку и установку дистрибутива Linux.
3. Настройку и обновление установленного дистрибутива.

Для большей производительности и лучшей совместимости рассмотрите возможность обновления до **Windows Server 2022** или использования полноценной **виртуальной машины с Linux**.


Ссылки:  

https://dotnet.microsoft.com/ru-ru/download/dotnet/8.0  
https://disk.yandex.ru/d/RPsxDOfwA_l-mA  
https://dev.mysql.com/downloads  


server {
    listen 80;
    server_name donors;
    root "C:/OpenServer/domains/donors/public";

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        fastcgi_pass   127.0.0.1:9000;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include        fastcgi_params;
    }
}
