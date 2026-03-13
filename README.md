# HT-CT-62
HT-CT-62 - это один из возможных вариантов устройств на базе HT-CT62.
# Компиляция прошивки с помощью VS Code
Установка git
https://git-scm.com/install/windows
В окне установки нужно выбраать пункт `Add a Git Bash Profile to Windows Terminal`
img
Установка VS Code 
https://code.visualstudio.com/download
Скачиаем архив и открываем его в VS Code.
https://github.com/meshtastic/firmware/archive/refs/heads/develop.zip
Путь к прошивке .pio/build/heltec-ht62-esp32c3-sx1262
В поиске вкладки Extensions пишем PlatformIO и устанавливаем.
img
После установки пишем в терминал `pio run -e heltec-ht62-esp32c3-sx1262`
Путь к готовой прошивке: `.pio/build/heltec-ht62-esp32c3-sx1262/... .factory.bin`
Для прошивки используем исключительно файл с расширением .factory.bin
# Компиляция прошивки без VS Code
Все указаные действия расчитанны исключительно для linux дистрибутивов на основе Debian.
~~~
sudo apt install git
sudo apt install python3-venv #Установка пакета Venv.
python -m venv ~/.pio_venv #Создание окружения
source ~/.pio_venv/bin/activate #Активация окружения
pip install platformio #Установка PatformIO
git clone https://github.com/meshtastic/firmware && cd firmware #Установка репозитория
pio run -e heltec-ht62-esp32c3-sx1262
~~~
Путь к готовой прошивке: `~/firmware/.pio/build/heltec-ht62-esp32c3-sx1262/... .factory.bin`
Для прошивки используем исключительно файл с расширением .factory.bin
# Изменения в прошивке
В файле /src/power.h                                           
| Строчка    | Назначение                                     |
|-----------------|-----------------------------------------------|
| `#define OCV_ARRAY 4190, 4078, 4017, 3969, 3887, 3818, 3798, 3791, 3766, 3712, 3100` | 

В файле \variants\esp32c3\heltec_esp32c3\variant.h 
| Строчка    | Назначение                                     |
|-----------------|-----------------------------------------------|
| `#define HAS_SCREEN`     | Включение работы экрана          |
| `#define HAS_GPS`        | Включение работы GPS               |
| `#define GPS_RX_PIN`     | Пин приёма GPS данных                          |
| `#define GPS_TX_PIN`     | Пин передачи GPS данных                        |
| `#define BUTTON_PIN`     | Пин кнопки                                     |
| `#define I2C_SDA`        | Пин данных I2C                                |
| `#define I2C_SCL`        | Пин тактирования I2C                          |
| `#define BATTERY_PIN 2`  | Пин подключения акб к микроконтроллеру          |
| `#define ADC_CHANNEL ADC1_GPIO2_CHANNEL` | Определяет канал АЦП            |
| `#define ADC_MULTIPLIER 3.16`            | Коэффициент значения с АЦП      |
| `#define BATTERY_SENSE_SAMPLES 5`        | Кол-во измерений для усреднения |
|В файле /src/power.h                                             |
| `#define OCV_ARRAY 4190, 4078, 4017, 3969, 3887, 3818, 3798, 3791, 3766, 3712, 3100` | 
