# 🤖 Telegram Autoresponder (Userbot)

Легкий и быстрый автоответчик для вашего личного Telegram-аккаунта (не бота @BotFather), написанный на Python с использованием библиотеки **Pyrogram**.

Бот автоматически отвечает на все новые входящие личные сообщения, когда вы заняты, спите или просто не у телефона.

---

## ✨ Особенности

* 👤 **Userbot:** Работает на вашем личном аккаунте.
* ⏳ **Smart Anti-Spam:** Бот не будет спамить человеку. Задержка между повторными ответами настраивается (по умолчанию 1 час).
* 🛡️ **Игнорирует личные действия:** Не отвечает самому себе и в «Избранное» (Saved Messages).
* 🖼️ **Поддержка стикеров:** Можно отправлять стикер перед текстовым сообщением.
* 💎 **Premium эмодзи:** Поддержка HTML-разметки для анимированных эмодзи.
* ⚙️ **Обход спам-фильтров:** Маскировка сессии под *Desktop Windows 10*.

---

## ⚙️ Подготовка (Получение API ключей)

Чтобы скрипт мог работать с вашим аккаунтом, получите ключи разработчика:

1.  Перейдите на [my.telegram.org](https://my.telegram.org) и авторизуйтесь.
2.  Зайдите в **API development tools**.
3.  Создайте приложение (названия любые, например `MyAutoresponder`).
4.  Сохраните **API_ID** и **API_HASH**.

---

## 📦 Установка и запуск

### Вариант 1: Локально на Windows
1.  Установите **Python 3.8+** (отметьте галочку **Add Python to PATH**).
2.  Откройте файл `.env` в папке проекта:
    ```env
    API_ID=12345678
    API_HASH=ваш_длинный_хэш
    ```
3.  Установите зависимости и запустите:
    ```bash
    pip install -r requirements.txt
    python main.py
    ```
4.  Введите номер телефона и код из Telegram.

---

### Вариант 2: На Linux сервере (VDS/VPS)

Если вы хотите настроить всё сразу на сервере, следуйте этой инструкции:

1.  **Загрузите файлы:** Перенесите на VDS только три файла: `main.py`, `requirements.txt` и `.env`. 
    > **Важно:** Файла `autoresponder_session.session` на сервере быть не должно.
2.  **Подключитесь к VDS:** Используйте SSH (PuTTY на Windows или терминал на macOS/Linux).
3.  **Подготовьте среду:**
    ```bash
    cd /путь/к/папке/со/скриптом
    sudo apt update && sudo apt install python3 python3-pip -y
    pip install -r requirements.txt
    ```
4.  **Запустите процесс входа:**
    ```bash
    python3 main.py
    ```
5.  **Пройдите авторизацию прямо в консоли:**
    * Появится надпись: `Enter phone number or bot token:`. Введите свой номер (например, `+79001234567`) и нажмите **Enter**.
    * Telegram пришлет код в приложение. Консоль попросит: `Enter confirmation code:`. Введите 5 цифр и нажмите **Enter**.
    * Если у вас стоит **Облачный пароль** (2FA), появится запрос: `Enter password:`. 
    * **Внимание:** При вводе пароля символы не отображаются (ввод «вслепую») — это нормально. Введите пароль и нажмите **Enter**.

---

## 🚀 Постоянная работа в фоне (systemd)

Чтобы бот не выключался после закрытия консоли, создайте службу:

1.  Создайте файл: `sudo nano /etc/systemd/system/autotg.service`
2.  Вставьте конфигурацию (замените `/opt/autotg` на ваш путь):
    ```ini
    [Unit]
    Description=Telegram Autoresponder
    After=network.target

    [Service]
    User=root
    WorkingDirectory=/opt/autotg
    ExecStart=/usr/bin/python3 main.py
    Restart=always

    [Install]
    WantedBy=multi-user.target
    ```
3.  Запустите:
    ```bash
    sudo systemctl daemon-reload
    sudo systemctl enable autotg.service
    sudo systemctl start autotg.service
    ```

---

## 🛠️ Настройка (`main.py`)

| Параметр | Описание |
| :--- | :--- |
| `AUTO_REPLY_TEXT` | Текст ответа (поддерживает HTML). |
| `STICKER_ID` | ID стикера (через `@idstickerbot`). Оставьте `""`, чтобы отключить. |
| `COOLDOWN_SECONDS` | Задержка перед повторным ответом (в секундах). |

---

## ⚠️ Дисклеймер
Использование юзерботов может привести к блокировке аккаунта, если вы злоупотребляете рассылками. Используйте скрипт ответственно.


# 🤖 Telegram Autoresponder (Userbot)

A lightweight and fast autoresponder for your personal Telegram account (Userbot, not a @BotFather bot), written in Python using the **Pyrogram** library.

The bot automatically replies to all incoming private messages when you are busy, sleeping, or away from your phone.

---

## ✨ Features

* 👤 **Userbot:** Runs on your personal account.
* ⏳ **Smart Anti-Spam:** Cooldown support. The bot won't spam someone if they send multiple messages in a row. The delay between repeated replies is configurable (default is 1 hour).
* 🛡️ **Self-Ignore:** The bot does not reply to your own messages or messages in "Saved Messages".
* 🖼️ **Sticker Support:** The bot can send a specific sticker before the text message.
* 💎 **Premium Emoji Support:** Replies are sent in HTML format, allowing the use of animated Premium emojis.
* ⚙️ **Bypass Spam Filters:** The session is masked as the official *Desktop Windows 10* app to prevent Telegram from blocking code requests during login.

---

## ⚙️ Preparation (Getting API Keys)

To allow the script to work with your account, you need developer keys:

1.  Go to [my.telegram.org](https://my.telegram.org) and log in.
2.  Open the **API development tools** section.
3.  Fill out the form (use any names, e.g., `MyAutoresponder`).
4.  You will receive an **API_ID** (numbers) and an **API_HASH** (long string). **Save them!**

---

## 📦 Installation & Setup

### Option 1: Locally on Windows
1.  Install **Python 3.8** or higher. Make sure to check **"Add Python to PATH"** during installation.
2.  Download the repository and extract the folder.
3.  Open a `.env` file in the script folder and enter your keys:
    ```env
    API_ID=12345678
    API_HASH=your_long_hash_here
    ```
4.  Open Command Prompt (cmd) in the folder and install dependencies:
    ```bash
    pip install -r requirements.txt
    ```
5.  Run the script:
    ```bash
    python main.py
    ```
6.  Enter your phone number and the SMS code sent to your Telegram app.

---

### Option 2: Running 24/7 on Linux VDS (Manual Login)

If you want to set everything up directly on the server without transferring session files from your computer:

1.  **Upload Files:** Transfer only three files to your VDS: `main.py`, `requirements.txt`, and `.env`. 
    > **Note:** The `autoresponder_session.session` file should NOT be on the server initially.
2.  **Connect via SSH:** Use PuTTY (Windows) or your terminal.
3.  **Setup Environment:**
    ```bash
    cd /path/to/script/folder
    sudo apt update && sudo apt install python3 python3-pip -y
    pip install -r requirements.txt
    ```
4.  **Run Manually for Authorization:**
    ```bash
    python3 main.py
    ```
5.  **Complete the Login Dialog in the Console:**
    * The console will prompt: `Enter phone number or bot token:`. Type your phone number (e.g., `+1234567890`) and press **Enter**.
    * Telegram will send a code to your app. The console will ask: `Enter confirmation code:`. Enter the 5-digit code and press **Enter**.
    * If you have **Two-Step Verification (Cloud Password)** enabled, it will ask: `Enter password:`. 
    * **Note:** Characters will not appear on the screen while typing your password — this is normal. Type it blindly and press **Enter**.

---

## 🚀 Background Execution (systemd)

To keep the bot running after you close the console, create a service:

1.  Create the service file: `sudo nano /etc/systemd/system/autotg.service`
2.  Paste the following config (replace `/opt/autotg` with your actual path):
    ```ini
    [Unit]
    Description=Telegram Autoresponder
    After=network.target

    [Service]
    User=root
    WorkingDirectory=/opt/autotg
    ExecStart=/usr/bin/python3 main.py
    Restart=always

    [Install]
    WantedBy=multi-user.target
    ```
3.  Start the service:
    ```bash
    sudo systemctl daemon-reload
    sudo systemctl enable autotg.service
    sudo systemctl start autotg.service
    ```

---

## 🛠️ Configuration (`main.py`)

You can customize the bot by editing the variables at the top of `main.py`:

| Parameter | Description |
| :--- | :--- |
| `AUTO_REPLY_TEXT` | The reply text. Supports HTML tags (e.g., `<tg-emoji>`). |
| `STICKER_ID` | The `file_id` of a sticker (get it via `@idstickerbot`). Leave as `""` to disable. |
| `COOLDOWN_SECONDS` | Delay between replies to the same person. Default is `3600` (1 hour). |

---

## ⚠️ Disclaimer
Using Userbots is technically against Telegram's Terms of Service. Use this script at your own risk. To avoid bans, do not set the cooldown to very short intervals.
