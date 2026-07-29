<img align="right" src="https://raw.githubusercontent.com/erdilS/Port-Windows-11-Xiaomi-Pad-5/main/nabu.png" width="425" alt="Windows 11 Running On A Xiaomi Pad 5">

# Запуск Windows на Xiaomi Pad 5

## Видалення

### Чому потрібне видалення?
> Якщо ви хочете повторно заблокувати завантажувач, вам знадобиться, щоб таблиця розділів була стандартною.

> [!Warning]
> **Усі ваші дані буде видалено! Зробіть резервну копію, якщо потрібно.**

### Перемкніться на Android
> Якщо останнім разом ви завантажувалися в Windows, спочатку перемкніться на Android перед початком процесу видалення.

#### Перезавантаження в режим fastboot
- Завантажте свій NABU в **режим fastboot**, утримуючи кнопку **`volume down`** під час перезавантаження через USB-кабель.
- Або, якщо у вас увімкнено USB Debugging, виконайте команду нижче, перебуваючи в Android.
```cmd
adb reboot bootloader
```

> [!NOTE]
>
> ▶️ Натисніть, щоб розгорнути меню.

<details>
  <summary><strong>Спосіб 1 - Видалення за допомогою adb shell restore</strong></summary>

### Передумови
- [```Android platform tools```](troubleshooting-uk.md#adb-fastboot-not-recognized-uk)

- [```Модифікований образ recovery```](https://github.com/ArKT-7/twrp_device_xiaomi_nabu/releases/tag/mod-win) 

#### Завантаження в модифікований recovery
> Відкрийте вікно CMD у папці platform-tools, а потім (поки ваш планшет у режимі fastboot) виконайте
```cmd
fastboot boot шлях\до\recovery.img
```

### Відновлення схеми розділів
> [!Warning]
> Це видалить ваші файли в Android. Спочатку зробіть резервну копію, якщо потрібно.

```cmd
adb shell restore
```

#### Перезавантаження в Android
```cmd
adb reboot 
```

## Готово!

</details>

<details>
  <summary><strong>Спосіб 2 - Видалення в fastboot</strong></summary>

### Передумови
- [```Android platform tools```](troubleshooting-uk.md#adb-fastboot-not-recognized-uk)

- [```gpt_both0.bin```](https://github.com/erdilS/Port-Windows-11-Xiaomi-Pad-5/releases/download/Files/gpt_both0.bin) 

### Відновлення таблиці розділів
> Замініть ```шлях\до\gpt_both0.bin``` на фактичний шлях до файлу gpt_both0.bin.
```cmd
fastboot flash partition:0 шлях\до\gpt_both0.bin
```

#### Стерти userdata
> Щоб уникнути bootloop і відновити розмір FS
```cmd
fastboot -w
```

#### Перезавантаження в Android
```cmd
fastboot reboot
```

## Готово!

</details>

<details>
  <summary><strong>Спосіб 3 - Видалення за допомогою "Nabu Fastboot Tool"</strong></summary>

### Передумови
 `Кабель` для підключення вашого **`Xiaomi Pad 5`** до **`іншого пристрою`**

 **`Будь-який інший пристрій (Android, Windows, Mac або Linux)`**

### Підключення до Fastboot Tool на сайті
- Відкрийте **[Nabu Fastboot Tool](https://arkt-7.github.io/nabu/)** у браузері будь-якого пристрою.
- Натисніть кнопку **`Connect Device Fastboot`**.
- Виберіть **`Android`** зі списку, що з’явиться, і **`дозвольте`** дозволи.

### Форматування та повернення розділів до stock
- Прокрутіть вниз до розділу **`Format/wipe make Partition Stock`**.
- У полі введення введіть **`format`**.
- Нарешті натисніть кнопку **`Format/Wipe`** і натисніть **`OK`**, коли з’явиться попередження.
- Після завершення форматування з’явиться вікно успіху. Натисніть **`OK`**, щоб закрити його.
- Прокрутіть вгору і натисніть кнопку **`Reboot Device`**, щоб перезавантажити пристрій.

## Готово!

</details>

> [!NOTE]
> Якщо ваш пристрій **перезавантажився в recovery** після видалення Windows, виконайте такі дії:
> 1. Виберіть **Wipe Data/Factory reset**
> 2. **Wipe All Data**
> 3. Після успішного стирання даних натисніть **Back To Main Menu**
> 4. Натисніть **Reboot**
> 5. Перезавантажтеся в System
