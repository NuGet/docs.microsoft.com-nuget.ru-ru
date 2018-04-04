#### <a name="windows"></a>Windows
1. Посетите [nuget.org/downloads](https://nuget.org/downloads) и выберите NuGet 3.3 или более поздней версии (2.8.6 не совместим с моно). Рекомендуется всегда использовать последнюю версию, и 4.1.0+ требуется для публикации пакеты в nuget.org.
2. Каждый загрузки `nuget.exe` непосредственно. Настроить браузер, чтобы сохранить файл в папку по своему усмотрению. Файл *не* в установщик; ничего не отображается, если запустить его непосредственно из браузера.
3. Добавить папку, в котором размещена `nuget.exe` в переменную среды PATH использовать средство CLI из любого места.

#### <a name="macoslinux"></a>macOS/Linux
Поведение может несколько отличаться по распределению ОС.

1. Установка [моно 4.4.2 или более поздней версии](http://www.mono-project.com/docs/getting-started/install/).
2. Выполните следующие команды в командную строку:
    
    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    # Give the file permissions to execute
    sudo chmod 755 /usr/local/bin/nuget.exe
    ```
3. Создать псевдоним, добавив следующий скрипт к соответствующему файлу для вашей операционной системы (обычно `~/.bash_aliases` или `~/.bash_profile`):
    
    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```
4. Перезагрузите оболочки.  Проверьте установку, введя `nuget` без параметров. Отображать справку NuGet CLI.