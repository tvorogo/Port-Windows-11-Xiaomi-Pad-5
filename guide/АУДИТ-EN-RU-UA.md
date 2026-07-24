# Аудит гайдов: изъяны в версиях EN / RU / UA

Проверены все файлы папок `English`, `Russian`, `Ukrainian`. Ниже находки, сгруппированные по серьёзности. 🔴 — может сломать устройство/шаг, 🟠 — расхождение перевода или битая навигация, 🟡 — опечатка/язык/форматирование.

---

## 🔴 Критические технические ошибки

1. **UA `disable-secureboot-uk.md` — команды diskpart переведены на украинский и работать НЕ будут.**
   - `assign letter y` → превратилось в `присвоїти букву у` (ещё и «у» кириллическое).
   - `select volume <number>` → `sel vol <номер>`.
   - Заголовок «Виберіть **гучність** esp» — «volume» переведено как «громкость» (звук), а не «том/розділ».
   - Пользователь скопирует `присвоїти букву у` в diskpart и получит ошибку. Нужно вернуть оригинальные англ. команды.

2. **UA `fixgpt.md` — опечатка в команде.** `adb reboot bootloder` вместо `adb reboot bootloader` — команда не выполнится.

3. **RU `1-partition-ru.md` — неверная команда в конце ручной разметки.** Шаг называется «Перезагрузите, чтобы проверить, запускается ли Android», но команда `adb reboot recovery` (грузит в recovery, а не в систему). В EN и UA правильно — `adb reboot`.

4. **UA `fixgpt.md` и `re-root-uk.md` — испорченный placeholder пути.** `fastboot boot fastboot\до\recovery.img` — слово `fastboot` вставлено туда, где должен быть `шлях`. Должно быть `fastboot boot шлях\до\recovery.img`.

---

## 🔴 Фактические расхождения в данных

5. **Кабель зарядки (`troubleshooting`).** EN: «оригинальный кабель Xiaomi 33W» + кабель Samsung. RU: «оригинальный кабель **Poco X3 Pro**» и без Samsung — другое устройство, вероятно ошибка перевода.

6. **Срок ожидания разблокировки (`unlock-bootloader`).** EN и RU: `168 hrs / 7 days`. UA: `72 години / 3 дні` — другое число. Нужно свести к одному значению.

7. **Версия UEFI в команде прошивки (`disable-secureboot`).** Файл в разделе «Требования» у всех — `nabu-uefi-v4-fixed_NOSB.img`, но в команде: EN и UA прошивают `...NoSecureboot-v3.img` (v3), RU — `XXXnabu-NoSecureboot-v4.img` (v4 + мусорный префикс `XXX`). Имя не совпадает с реальным файлом ни в одной версии.

---

## 🟠 Пропущенные шаги и устаревшее содержимое

8. **UA `unlock-bootloader-uk.md` устарел** — нет метода **HyperSploit** (обход дневной квоты), который в EN и RU идёт как «Способ 1 (рекомендуется)». В UA также отсутствует ссылка на скачивание HyperSploit в требованиях.

9. **UA `uninstall-uk.md` неполный** — только 1 способ (`adb shell restore`). В EN и RU три способа (adb restore, `gpt_both0.bin`, Nabu Fastboot Tool).

10. **RU и UA `reinstall` — пропущен шаг бэкапа + предупреждение.** В EN есть шаг «Back up your boot.img» (`dd ...`) и `[!Warning]` про наличие Android boot.img перед началом. В RU и UA оба отсутствуют.

11. **UA `update-uk.md` — другая процедура.** Вместо DriveLetterAssigner (как в EN/RU) вставлены ручные шаги diskpart; в требованиях нет DriveLetterAssigner и ADB&Fastboot.

12. **RU `Re-rooting-ru.md` — иной финал.** EN/UA: «BACKUP BOOT IMAGE → Windows → готово». RU расписывает ручное монтирование и удаление boot.img — расходится с оригиналом.

13. **UA `troubleshooting-uk.md` сильно урезан** — нет разделов: перенос файлов в папку Windows, зарядка в Windows, «устройство не определяется в fastboot» (а именно на этот якорь ведёт ссылка из `1-partition-uk.md`!).

14. **UA `troubleshooting` BSOD fsa4480** — вместо удаления строки `<DriverPackageFile .../>` из NABU.xml (как в EN) сказано удалить целую папку — сомнительная инструкция.

15. **RU `uninstall-ru.md`, Способ 3 — copy-paste ошибка.** Блок «если устройство перезагрузилось в recovery» повторяет шаги FORMAT вместо инструкции Wipe Data/Factory reset (как в EN). Плюс в список устройств добавлен «iOS», который WebUSB-инструмент не поддерживает.

---

## 🟠 Битые и неверные ссылки

16. `Russian/reinstall-ru.md` → `/guide/Russian/partition-ru.md` — файла нет (нужно `1-partition-ru.md`).
17. `Ukrainian/reinstall-uk.md` → `/guide/Ukrainian/install-uk.md` — файла нет (нужно `1-partition-uk.md`).
18. `Ukrainian/UEFI-updating-uk.md` → `/guide/Ukrainian/dualboot-uk.md` — файла нет (нужно `4-dualboot-uk.md`).
19. `English/fix-gpt-en.md` → `selection-en.md` — файла нет (в EN он называется `installation-selection-en.md`).
20. `Ukrainian/1-partition-uk.md` → `troubleshooting-en.md#...` — ведёт на английский файл (нужно `troubleshooting-uk.md`), причём нужного якоря в UA-версии всё равно нет.
21. `Russian/Additional-materials-ru.md` → `Re-rooting-en.md` — ссылка на английский файл вместо `Re-rooting-ru.md`.
22. `Ukrainian/README-uk.md`: пункт «Налаштування подвійного завантаження» ведёт прямо на `4-dualboot-uk.md` минуя страницу выбора `dualboot-selection-uk.md` — пользователь не видит вариант DBKP.
23. `Ukrainian/README-uk.md`: «Гайд з оновлення» ведёт на внешний репозиторий `Kumar-Jy/...DriverUpdate.md`, хотя рядом есть локальный `update-uk.md`; «Гайд з перевстановлення» ведёт на английский `reinstall-en.md`.
24. `Russian/dualboot-selection-ru.md`: `<a href>` картинок ведут на `4-dualboot-en.md` и `dbkp-en.md` (английские) вместо `-ru`.
25. Ссылки WinInstaller в `selection`: RU → русский `Installation-ru.md`, UA → корень репозитория (без файла) в картинке и англ. `Installation.md` в тексте, EN → `Installation.md`. Несогласованно.

---

## 🟡 Опечатки, язык, форматирование

26. EN `1-partition-en.md`: заголовок `#### Reboot into fastboot mkde` → `mode`.
27. EN `unlock-bootloader-en.md`: `Add platfrom tools` → `platform`; `while appling` → `applying`. Та же `platfrom` в RU `unlock-bootloader-ru.md`.
28. UA `update-uk.md`: 4 блока кода закрыты четырьмя бэктиками ` ```` ` вместо трёх — ломает разметку.
29. UA `unlock-bootloader-uk.md`: блоки `<details>` закрыты `</summary></details>` (лишний `</summary>`) — структура сломана.
30. UA `disable-secureboot-uk.md`: «Ви не можете **оновлювати робити** великі оновлення» — задвоённый глагол.
31. RU опечатки: `достачно` → достаточно (`README-RU.md`), `Androis` → Android (`reinstall-ru.md`), `реквавери` → рекавери (`fix-gpt-ru.md`), `Моддифицированый` → модифицированный (`uninstall-ru.md`), `приоложения` → приложения (`dualboot-selection-ru.md`), `Перевдите` → переведите (`troubleshooting-ru.md`), `Разблокироанный` → разблокированный (`edl-ru.md`), `УМРЕТЬ` → умереть (`README-RU.md`).
32. RU `edl-ru.md`: `USB_BULK_CID` вместо `QUSB_BULK_CID` (потерян Q).
33. UA `update-uk.md`: «як каже **мейнтейнера**» → мейнтейнер; `Драйвері` → Драйвери; «розділ Windows на **телефоні**» — устройство планшет.
34. Требование `Brain`/`Мозг` (шутка) есть в EN и RU, но выпало из UA в `1-partition` и `2-rootguide`.
35. RU `3-install-ru.md` содержит `[!Tip]` про пропуск входа в Microsoft, которого нет в EN на этом шаге (в EN он в `4-dualboot`). UA — вверху `3-install-uk.md` предупреждение про YouTube, которого нет в EN/RU этого файла. Контент разъезжается между файлами.

---

### Приоритет исправлений
Сначала пункты 1–4 (сломанные команды у пользователя) и 5–7 (неверные данные), затем битые ссылки 16–25, потом язык.
