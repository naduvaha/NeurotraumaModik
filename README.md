# NeurotraumaModik by Staili

[Русский](#русский) | [English](#english)

**Version / Версия:** `2.2.2`  
**Plugin / Плагин:** `NeurotraumaModikByStaili.dll`  
**Nexus / Нексус:** [nexusmods.com/scavprototype/mods/440](https://www.nexusmods.com/scavprototype/mods/440)  
**Hard dependency / Жёсткая зависимость:** [CUCoreLib](https://www.nexusmods.com/scavprototype/mods/341)  
**Optional / Опционально:** [KrokoshaCasualtiesMP (KrokMP)](https://cucorelib.web.app/) (мультиплеер-синхронизация) · [QoL.Unknown](https://github.com/jimmyking9999999/QoL-Unknown/releases) · **Herobrine's Prosthetics** (протезы)

---

<a id="русский"></a>

<details open>
<summary><b>Русский</b></summary>

## Описание

Адаптация мода медицинского реализма **Neurotrauma** (из Barotrauma) для игры **Casualties Unknown**.  
Добавляет новый слой аффликций (осложнений) поверх ванильной системы «муддлов», не переписывая её — всё навешивается через аддитивные Harmony-патчи, собственную UI-панель и окно настроек.

**Иконки** (mood / heal / предметы / миниигра) **вшиты в DLL**. Рядом кладётся только `Content\Sound\`.

## Аффликции (осложнения)

Каждое имеет иконку, локализованные описание/подсказки лечения и, где нужно, отображается в нижней ванильной панели статусов.

| ID | RU | Как появляется | Как лечится |
|----|----|----|----|
| `frostbite` | Обморожение | холодная среда | тепло, согревание |
| `frostbite_amputation` | Обморожение — предампутация | конечность промёрзла до 100% | срочно: пила (ампутация) — иначе растёт некроз |
| `necrosis` | Некроз | тяжёлый столбняк/обморожение/сепсис/радиация, 100% обморожение | скальпель (дебридмент, < 70%) или пила (ампутация, ≥ 70%); при успехе инфекция на этой конечности сразу → 0 |
| `tetanus` | Столбняк | укусы, шип-ловушки, капканы и другие острые раны (не от инфекции) | время + обработка; до некроза (≥75%) |
| `fever` | Лихорадка | холод, болезнь, сепсис (~15 мин до 100%) | антибиотики / боевой инъектор / helluce; слабость и озноб, пока не спадёт |
| `wrongblood` | Реакция на переливание | несовместимая жёлтая кровь (~3 мин) | подождать; поддержка; не лить ту же группу снова |
| `pneumothorax` | Пневмоторакс | травма груди, взрывы | плевральный дренаж (chestdrain / ранорасширитель) |
| `lungdamage` | Повреждение лёгких | гемоторакс, травмы | кислородный конденсатор, покой (O2 > 94%) |
| `lungdamage_severe` | Повреждение лёгких — критично | `lungdamage` ≥ 70 | срочно кислородный конденсатор; снизить основное повреждение |
| `lung_overexpand` | Расширение лёгких | взрыв рядом / резкий перепад давления | покой, кислородный конденсатор |
| `lung_compress` | Сдавливание лёгких | тонешь в тяжёлой жидкости (нефть) без снаряжения | выйти из жидкости, снаряжение / конденсатор |
| `lung_wall_collapse` | Сдавление стенок лёгких | сильное внутреннее кровотечение | остановить кровотечение (повязка/шов/хирургия) |
| `hyperventilation` | Гипервентиляция | стресс, адреналин, низкий O2 | успокоить пациента, малая доза морфина |
| `heartdamage` | Повреждение сердца | долгая фибрилляция, инсульт, экстремальное давление | хирургия: пересадка сердца |
| `seizure` | Судороги | падение здоровья мозга, гипоксия, радиация | морфин (малая доза), защита от травм; **сильно портит прицел**; при >30% редко краткая потеря управления; сами по себе HP не снимают, медленно спадают |
| `kidneydamage` | Повреждение почек | радиация, септический шок, сильное обезвоживание, передоз, стойко низкое давление | время; УЛР (L.R.D.); антибиотики / combatpen (сепсис); пить воду; уйти от радиации |
| `kidneyfailure` | Почечная недостаточность | запущенное `kidneydamage` (≥ 70 накапливается) | хирургия: пересадка почки |
| `kidney_warning` | Тревога по почкам | `kidneydamage` 10–70 | УЛР; антибиотики / combatpen; пить воду; снизить радиацию |
| `kidney_deadlow` | Почки — критично | `kidneydamage` ≥ 70 | срочно: пила → пересадка почки |
| `liverdamage` | Повреждение печени | алкоголь (залп при глотке), передозировка, сепсис, радиация, токсины при отказе почек, антипаразитарное | бросить спирт; долгая трезвость; антибиотики / combatpen (сепсис); дождаться спада передоза и радиации |
| `pechen_warning` | Тревога по печени (стадия 1) | `liverdamage` 10–40 | бросить спирт; антибиотики / combatpen; дождаться спада передоза и радиации |
| `pechen_warning2` | Тревога по печени (стадия 2, переход) | `liverdamage` 40–70 | срочно бросить спирт; антибиотики / combatpen; дождаться спада передоза и радиации |
| `liverfailure` / `pechen_dead` | Отказ печени | `liverdamage` ≥ 70 | хирургия: пересадка печени + антипаразитарное (профилактика), без алкоголя |
| `platadead1/2/3stadia` | Сбой чипа (1–3) | радиация, травма, сепсис, передоз, экстрем. темп. (только чипированный режим; скаляр `chipdamage`) | крафт/применить `nt_important_chip` (плата ≥90% + нить×2) |
| `chronicpain` | Хроническая боль | давние травмы | морфин (малая доза, осторожно с зависимостью) |
| `psychosis` | Психоз | затяжные галлюцинации (>40) | время, сон, спирт |
| `hallucinations` | Галлюцинации | радиация, травма, низкое настроение | время, сон, спирт |
| `porez1` | Порез (степень 1) | разрез скальпелем; шанс от порезов/укусов | ванильные нити (`medicalsuture`) или само |
| `porez3` | Порез (степень 3, широкий) | расширение раны ранорасширителем | зашить после операции |
| `porez4_foreign` / `porez5_foreign` | Порез с инородным телом | попадание инородного тела (выше шанс при укусах) | извлечь ножницами, затем зашить |
| `parazite` | Паразиты | ~8 мин необработанного `porez4/5_foreign` (1–5 шт.); после извлечения — **10 мин** на ножницы, иначе снова заселятся | извлечь руками/пинцетом; затем ножницами убрать инородность; `nt_antiparasite` только профилактика |
| `fresh_suture` | Свежий шов | после наложения нитей (ваниль) | место защищено от повреждений, заживает само (100 → 0, ~2 мин) |

> Скрытые скаляры (не мудлы): `liver_graft` / `liver_sober`, `healthchip` / `chip_fuse`, `antiparasite_guard` — служебные таймеры/флаги.

## Особенности

- **Фантомные эффекты** при высоком психозе/галлюцинациях: призрачные пауки, фантомное кровотечение с красной виньеткой и жуткий шёпот на экране игрока. При **психозе > 30** — слуховые галлюцинации в духе Баратравмы на ванильных звуках: выстрелы, «вьетнамка» с сонаром, случайные звуки боли и крики персонажа. Чисто клиентски, без реального урона (отключается в настройках).
- **Иконки мода в ванильной панели статусов** — активные осложнения показываются снизу рядом с ванильными, размер подогнан под ванильный (отключается).
- **Иконки на силуэте UNI-HEALTH** привязаны к конечности (не ездят за курсором): некроз — на поражённой руке/ноге; сердце/лёгкие — только на груди; почки/печень — на животе/нижнем торсе. Печень показывает стадии `pechen_warning` → `pechen_warning2` → `pechen_dead`.
- **Своя хирургия** на предметы (скальпель / пила / ранорасширитель / ножницы): дренаж, удаление мёртвой ткани, ампутация, пересадка органа (сердце / лёгкие / почки / печень). Для пересадки нужен ванильный предмет `internalorgans` (качество ≥40%) — один предмет на одну операцию. После пересадки печени — окно риска инфекции (`liver_graft`): антипаразитарное ускоряет приживление; алкоголь бьёт по новому органу сильнее. **Операции не «в один клик»**: сначала разрез скальпелем (porez1) → расширение ранорасширителем (porez3) → и только затем внутренние процедуры; инородные тела извлекаются ножницами; закрытие — ванильными нитями (`medicalsuture`). Неверный инструмент не продвигает операцию, а лишь слегка вредит. Анестезия — через кислородный конденсатор с заряженной сывороткой. Дебридмент/ампутация некроза **сразу** обнуляет ванильную инфекцию на оперированной конечности.
- **Износ инструментов** — хирургические инструменты тратят состояние только при выполнении операции (не при открытии меню); расходники — при использовании. `nt_antiparasite` — **3 дозы** на флакон.
- **Паразиты**: заселяются в необработанный `porez4/5` (~8 мин). После извлечения — **10 минут**, чтобы убрать инородность ножницами, иначе паразиты вернутся. Пока сидят — сепсис начинает проявляться с **10%**. Мудл `parazite` на 100%, пока есть хотя бы один. Миниигра (окно ран / пинцет); в MP можно тянуть вместе. Антипаразитарное — только **профилактика** (~6 мин).
- **Мультиплеер**: авторитет на хосте; болезни привязаны к **Steam ID** (не «переезжают» на другого при перезаходе); синхронизация ран/паразитов/группы крови и per-limb трекеров; маска симптомов хоста; совместная хирургия и миниигра паразитов. Без KrokMP мод работает в **одиночке**. Игроки **без** Neurotrauma могут быть в лобби — у них нет симптомов/предметов мода; у остальных мод продолжает работать.
- **Группа крови (ABO+Rh)**: случайная при спавне в забеге; показывается в панели симптомов («У вас _ группа крови») и в описании ванильного пакета жёлтой крови. Сохраняется при переходе слоёв и в `save.sv` (Continue). **Несовместимое вливание** жёлтой крови → ~3 мин мудл `wrongblood`: к текущим пульсу/давлению **прибавляется** бонус (не фиксация на 120/160); растут лихорадка, нагрузка на почки/печень, тошнота.
- **Крафт / spawn `nt_*`**: инструменты и расходники во вкладке Medicine (через CUCore `RecipeRegistry`); типированные пакеты крови — `bloodbag` + 20 мл `alienblood`. Создание предметов — путь CUCore (`Utils.Create` → `CustomInstantiate`).
- **Сохранение аффликций**: статус мода пишется в блок `neurotrauma` внутри `save.sv` вместе с группой крови, счётчиками паразитов по конечностям и возрастом инородных ран.
- **Совместимость с Herobrine's Prosthetics** (опционально): если у игрока установлен мод протезов, на конечности с `ProstheticLimb` не показываются necrosis/tetanus/frostbite/chronicpain, не предлагается ампутация через necrosis-picker, мод не бьёт `skinHealth` протеза обморожением. Body-wide аффликции (психоз, сердце, почки и т.д.) по-прежнему действуют на всё тело.

## Предметы

| ID | Предмет | Назначение |
|----|---------|-----------|
| `nt_scalpel` | Скальпель | открывает хирургию: разрез (porez1), дебридмент некроза |
| `nt_bonesaw` | Костная пила | ампутация, пересадка (нужны `internalorgans` ≥40%) |
| `nt_retractor` | Ранорасширитель | расширяет рану (porez3), плевральный дренаж, внутренние процедуры |
| `nt_scissors` | Ножницы | крафт: 2× куб металлолома (`scrapcube`) + 20 мл биохим; извлечение инородных тел / сыворотки |
| `nt_antiparasite` | Антипаразитарное | **3 дозы**; профилактика новых паразитов (~6 мин); слегка помогает печени / сепсису — **не** извлекает уже засевших |
| `nt_serum_sleep` | Сыворотка для сна | заряжается в конденсатор (как батарейка) для анестезии |
| `nt_o2_condenser` | Кислородный конденсатор | пустой — кислородная маска (O2 + гипервентиляция); с сывороткой — усыпляет для операции |
| `nt_important_chip` | Важный чип | замена сбойной платы UNI-HEALTH (крафт: плата ≥90% + нить×2) |
| `nt_bloodtype_op` … `nt_bloodtype_abm` | Пакет крови (O+/O−/A+/…/AB−) | типированная жёлтая кровь для вливания; крафт: `bloodbag` + 20 мл инопланетной крови |

## Консольные команды

| Команда | Назначение |
|---------|-----------|
| `nt_list [игрок]` | список аффликций на цели |
| `nt_add <id> [кол-во=50] [игрок] [#конечность]` | добавить тяжесть |
| `nt_set <id> <кол-во> [игрок] [#конечность]` | задать тяжесть |
| `nt_clear [id] [игрок] [#конечность]` | снять одну/все |
| `nt_diag [игрок]` | диагностика цели/netid |
| `nt_limbs [игрок]` | список частей тела с индексами |
| `nt_bloodtype [A+\|random]` | показать / сменить свою группу крови (читы) |

- **Цель**: явный `[игрок]` (частичное имя в MP или `@a`) → открытое окно ран на союзнике → локальный игрок. Ник с пробелами пишется как есть: `nt_add frostbite 20 Staili Steyfer #lhand`.
- Алиасы стадий органов (`pechen_warning2`, `kidney_deadlow`, `lungdamage_severe`, …) пишут в базовый скаляр (`liverdamage` / `kidneydamage` / `lungdamage`).
- **Читы**: в мультиплеере все `nt_*` требуют включённый **`sv_cheats`** в правилах лобби (как `give` / `godmode`). Без него даже хост получит отказ.
- **Выбор конечности** токеном `#`: `#sel` (выделенная в UNI-HEALTH), `#<индекс>`, алиасы `#head #chest #lower #lhand #rhand #lfoot #rfoot #lthigh #rthigh ...`, либо фрагмент имени. Работает для аффликций, привязанных к конечности (`necrosis`, `tetanus`, `frostbite`, `parazite`). Без `#` конечность выбирается автоматически (для некроза — не голова). Иконка некроза **не показывается на голове**.
- **`parazite`**: `nt_set parazite 100 #larm` — случайно 1–5 шт. на конечности; `nt_set parazite 3 #larm` — ровно 3. Мудл всегда 100%, пока счётчик > 0.
- В командной строке для `id` и для `#конечность` работает **автозаполнение** (начните печатать `#`, чтобы увидеть список конечностей).

## Зависимости

| | |
|---|---|
| **Обязательно** | [BepInEx 5.4.x](https://github.com/BepInEx/BepInEx/releases) |
| **Обязательно** | [CUCoreLib](https://nexusmods.com/scavprototype/mods/341) — общая библиотека модов (регистрация предметов/контента) |
| **Опционально** | [KrokoshaCasualtiesMP (KrokMP)](https://cucorelib.web.app/) — синхронизация аффликций в мультиплеере (без него мод работает в одиночной игре) |
| **Опционально** | [QoL.Unknown](https://github.com/jimmyking9999999/QoL-Unknown/releases) — вкладка **«Нейротравма»** в настройках |
| **Опционально** | [MultyModik](https://www.nexusmods.com/scavprototype/mods/435) — источник тиков настроения/обнимашек |
| **Опционально** | **Herobrine's Prosthetics** (`prosthetics.dll`, GUID `com.HerobrinesProsthetics`) — протезы конечностей |

> Для одиночной игры достаточно BepInEx + CUCoreLib. Для MP с синхронизацией Neurotrauma нужен KrokMP; у всех с этим модом — одна версия плагина (+ CUCoreLib, и KrokMP если играете вместе). Игроки без Neurotrauma могут заходить в лобби.

## Установка

1. Установите BepInEx и **CUCoreLib** (для MP также **KrokoshaCasualtiesMP / KrokMP**) — см. https://cucorelib.web.app/
2. Скопируйте содержимое папки `NeurotraumaModik` в:
   ```
   Casualties Unknown\BepInEx\plugins\
   ```
   Должны оказаться:
   - `NeurotraumaModikByStaili.dll` (иконки уже внутри)
   - `NeurotraumaModik\Content\Sound\` (звуки; **без** `Sound\Voice`)
3. Запустите игру. В `BepInEx\LogOutput.log` появится строка:
   ```
   [Info : NeurotraumaModikByStaili] NeurotraumaModik by Staili v2.2.2 loaded. ... KrokMP: True/False ...
   ```

## Настройки

Вкладка **«Нейротравма»** в меню настроек (при QoL.Unknown) или горячая клавиша **F9** (окно мода). Файл: `BepInEx\config\NeurotraumaModikByStaili.cfg`.  
Ключевые опции: `ShowModMoodles` (иконки в ванильной панели), `HallucinationVisuals` (фантомные эффекты), `EnableParasites` (паразиты + миниигра), тогглы симптомов (печень / почки / лёгкие / …), `HostAuthoritative` (авторитет хоста), `AddToLootPool` (спавн предметов в луте).  
В MP (с KrokMP) клиенты **следуют маске симптомов хоста** (локальные галочки симптомов в F9 только для просмотра).  
На строке мода во вкладке **Mods** (при QoL.Unknown) есть кнопки **GIT** (релизы на GitHub) и **Nexus**.

## Совместимость

- Требует версию игры / CUCoreLib (и KrokMP для MP-синка), под которые собрана сборка.
- Возможны конфликты с модами, патчащими окно ран (`WoundView`), панель статусов (`MoodleManager`) или систему предметов.
- **RshLib**: его патч `Utils.Create` ломает CUCore-предметы (`nt_*`).
- **Herobrine's Prosthetics**: поддерживается опционально (runtime-детект `ProstheticLimb`). Протез не получает per-limb инфекцию/некроз/обморожение от нашего мода и не попадает под `nt_bonesaw` через necrosis-picker.

## Содержимое релиза

| Файл / папка | Описание |
|------|----------|
| `NeurotraumaModik\NeurotraumaModikByStaili.dll` | Плагин (иконки вшиты) — в `BepInEx\plugins\` |
| `NeurotraumaModik\NeurotraumaModik\Content\Sound\` | Звуки рядом с DLL (**без** `Voice`) |
| `NeurotraumaModik\README.md` | Этот файл |

</details>

---

<a id="english"></a>

<details>
<summary><b>English</b></summary>

## About

A Casualties Unknown adaptation of Barotrauma's medical-realism mod **Neurotrauma**.  
It layers a new set of afflictions (complications) on top of the vanilla moodle system without rewriting it — everything is bolted on with additive Harmony patches, a dedicated UI panel and a settings window.

**Icons** (mood / heal / items / minigame) are **embedded in the DLL**. Only `Content\Sound\` ships beside it (**no** `Voice` folder).

## Afflictions (complications)

Each has an icon, localized description/cure hints and, where relevant, shows in the vanilla bottom status bar.

| ID | EN | Trigger | Cure |
|----|----|----|----|
| `frostbite` | Frostbite | cold environment | warmth, rewarming |
| `frostbite_amputation` | Frostbite — pre-amputation | limb frozen to 100% | urgent: bonesaw (amputation) — otherwise necrosis grows |
| `necrosis` | Necrosis | severe tetanus/frostbite/sepsis/radiation, 100% frostbite | scalpel (debridement, < 70%) or bonesaw (amputation, ≥ 70%); on success, that limb's infection drops to 0 immediately |
| `tetanus` | Tetanus | bites, spike traps, bear traps and other sharp wounds (not from infection) | time + wound care; treat before necrosis (75%+) |
| `fever` | Fever | cold, sickness, sepsis (~15 min to 100%) | antibiotics / combat injector / helluce; weakness and chills until cleared |
| `wrongblood` | Transfusion reaction | incompatible yellow blood (~3 min) | wait it out; supportive care; do not re-transfuse mismatch |
| `pneumothorax` | Pneumothorax | chest trauma, explosions | chest drain (chestdrain / retractor) |
| `lungdamage` | Lung damage | hemothorax, trauma | O2 condenser, rest (O2 > 94%) |
| `lungdamage_severe` | Lung damage — critical | `lungdamage` ≥ 70 | O2 condenser urgently; reduce base damage |
| `lung_overexpand` | Lung over-expansion | nearby blast / rapid pressure change | rest, O2 condenser |
| `lung_compress` | Lung compression | drowning in heavy liquid (oil) without gear | leave the liquid, scuba gear / condenser |
| `lung_wall_collapse` | Lung wall collapse | severe internal bleeding | stop internal bleeding (bandage/suture/surgery) |
| `hyperventilation` | Hyperventilation | stress, adrenaline, low O2 | calm the patient, low-dose morphine |
| `heartdamage` | Heart damage | prolonged fibrillation, stroke, BP extremes | surgery: heart transplant |
| `seizure` | Seizure | brain-health drops, hypoxia, radiation | morphine (low dose), protect from injury; **heavy aim penalty**; above 30% rare brief control loss; does not deal HP damage; decays slowly |
| `kidneydamage` | Kidney damage | radiation, septic shock, severe dehydration, overdose, sustained low BP | time; L.R.D.; antibiotics / combatpen (sepsis); drink water; leave radiation |
| `kidneyfailure` | Kidney failure | advanced `kidneydamage` (builds at ≥ 70) | surgery: kidney transplant |
| `kidney_warning` | Kidney warning | `kidneydamage` 10–70 | L.R.D.; antibiotics / combatpen; drink water; leave radiation |
| `kidney_deadlow` | Kidney failure — critical | `kidneydamage` ≥ 70 | urgent: bonesaw → kidney transplant |
| `liverdamage` | Liver damage | alcohol (per-drink burst), overdose, sepsis, radiation, kidney toxins, anti-parasite | stop alcohol; long sobriety; antibiotics / combatpen (sepsis); wait out overdose & radiation |
| `pechen_warning` | Liver warning (stage 1) | `liverdamage` 10–40 | stop alcohol; antibiotics / combatpen; wait out overdose & radiation |
| `pechen_warning2` | Liver warning (stage 2, transition) | `liverdamage` 40–70 | urgently stop alcohol; antibiotics / combatpen; wait out overdose & radiation |
| `liverfailure` / `pechen_dead` | Liver failure | `liverdamage` ≥ 70 | surgery: liver transplant + anti-parasite prophylaxis; no alcohol |
| `platadead1/2/3stadia` | Chip fault (stages 1–3) | radiation, trauma, sepsis, overdose, extreme temp (chipped mode only; scalar `chipdamage`) | craft/apply `nt_important_chip` (circuit board ≥90% + string×2) |
| `chronicpain` | Chronic pain | long-standing injuries | morphine (low dose, mind dependency) |
| `psychosis` | Psychosis | prolonged hallucinations (>40) | time, sleep, alcohol |
| `hallucinations` | Hallucinations | radiation, trauma, low mood | time, sleep, alcohol |
| `porez1` | Cut (grade 1) | scalpel incision; chance from cuts/bites | vanilla thread (`medicalsuture`) or self-heal |
| `porez3` | Cut (grade 3, wide) | widened with a retractor | suture after operating |
| `porez4_foreign` / `porez5_foreign` | Cut with foreign body | embedded foreign object (higher chance on bites) | extract with scissors, then suture |
| `parazite` | Parasites | ~8 min untreated `porez4/5_foreign` (1–5); after pull — **10 min** to scissors-extract or they re-burrow | pull with hands/tweezers; then scissors; `nt_antiparasite` prophylaxis only |
| `fresh_suture` | Fresh suture | after applying thread (vanilla) | the spot is protected from re-injury, heals on its own (100 → 0, ~2 min) |

> Hidden scalars (not moodles): `liver_graft` / `liver_sober`, `healthchip` / `chip_fuse`, `antiparasite_guard` — timers/flags.

## Features

- **Phantom effects** at high psychosis/hallucinations: phantom spiders, phantom bleeding with a red vignette, and creepy whispers on the player's screen. At **psychosis > 30** — Barotrauma-style auditory flashbacks using vanilla game audio: gunshots, sonar/"Vietnam" jolts, random pain SFX, and character scream lines. Purely cosmetic, no real damage (toggleable).
- **Mod icons in the vanilla status bar** — active complications appear at the bottom next to vanilla ones, sized to match (toggleable).
- **UNI-HEALTH silhouette icons** are limb-anchored (they do not follow the cursor): necrosis on the affected arm/leg; heart/lungs on the chest only; kidneys/liver on the abdomen / lower torso. Liver shows stages `pechen_warning` → `pechen_warning2` → `pechen_dead`.
- **Custom surgery** on tools (scalpel / bonesaw / retractor / scissors): drainage, dead-tissue removal, amputation, organ transplant (heart / lungs / kidneys / liver). Each transplant consumes one vanilla `internalorgans` item (condition ≥40%). After a liver transplant — infection-risk window (`liver_graft`): anti-parasite speeds graft settling; alcohol hits the new organ harder. **Operations are not one-click**: incise with the scalpel (porez1) → widen with the retractor (porez3) → then internal procedures; foreign bodies are pulled with scissors; closing uses vanilla thread (`medicalsuture`). The wrong tool doesn't advance the operation — it just hurts a little. Anesthesia comes from the O2 condenser with a loaded serum charge. Necrosis debridement/amputation **immediately** clears vanilla infection on the operated limb.
- **Tool wear** — surgical tools lose condition only when an operation is performed (not on opening the menu); consumables wear on use. `nt_antiparasite` is a **3-dose** vial.
- **Parasites**: burrow into untreated `porez4/5` (~8 min). After extraction you have **10 minutes** to remove the foreign body with scissors or they return. While embedded, sepsis starts showing from **10%**. Minigame (wound view / tweezers); MP co-op pull. Anti-parasitic is prophylaxis only.
- **Multiplayer**: host-authoritative; afflictions bound to **Steam ID**; state sync including per-limb trackers; host FEATURES mask; shared surgery / parasite minigame. Without KrokMP the mod still runs in **single-player**. Players **without** Neurotrauma may join — they lack mod symptoms/items; everyone else keeps the mod.
- **Blood type (ABO+Rh)**: rolled randomly at spawn; shown on the symptoms panel (“You have blood type _”) and on vanilla yellow blood-bag tooltips. Persists across layers and in `save.sv` (Continue). **Incompatible yellow-blood transfusion** → ~3 min `wrongblood` moodle: **adds** to current pulse/BP (does not pin to 120/160); builds fever, kidney/liver stress, sickness.
- **Crafting / `nt_*` spawn**: tools and consumables under Medicine (CUCore `RecipeRegistry`); typed blood packs need a `bloodbag` + 20 mL `alienblood`. Spawning uses the CUCore path (`Utils.Create` → `CustomInstantiate`).
- **Save persistence**: mod status is written into a `neurotrauma` block inside `save.sv`, including blood type, per-limb parasite counts, and foreign-wound age.
- **Herobrine's Prosthetics support** (optional): when the prosthetics mod is installed, limbs with a `ProstheticLimb` component do not show necrosis/tetanus/frostbite/chronicpain icons, are excluded from the necrosis amputation picker, and are skipped by our frostbite skin-damage write. Body-wide afflictions (psychosis, heart, kidneys, etc.) still apply to the whole patient.

## Items

| ID | Item | Purpose |
|----|------|---------|
| `nt_scalpel` | Scalpel | opens surgery: incision (porez1), necrosis debridement |
| `nt_bonesaw` | Bone saw | amputation, transplant (requires `internalorgans` ≥40%) |
| `nt_retractor` | Retractor | widens the wound (porez3), pleural drainage, internal procedures |
| `nt_scissors` | Scissors | craft: 2× scrap cube + 20 mL biochem; extract foreign bodies / eject serum |
| `nt_antiparasite` | Anti-parasitic | **3 doses**; prophylaxis against new parasites (~6 min); mild liver/sepsis help — does **not** extract burrowed parasites |
| `nt_serum_sleep` | Anesthetic serum | loads into the condenser (like a battery) for anesthesia |
| `nt_o2_condenser` | O2 condenser | empty — oxygen mask (O2 + hyperventilation); with serum — puts the patient under for surgery |
| `nt_important_chip` | Important chip | replaces a failing UNI-HEALTH board (craft: circuit board ≥90% + string×2) |
| `nt_bloodtype_op` … `nt_bloodtype_abm` | Blood pack (O+/O−/A+/…/AB−) | typed yellow blood for transfusion; craft: `bloodbag` + 20 mL alien blood |

## Console commands

| Command | Purpose |
|---------|---------|
| `nt_list [player]` | list afflictions on the target |
| `nt_add <id> [amount=50] [player] [#limb]` | add severity |
| `nt_set <id> <amount> [player] [#limb]` | set severity |
| `nt_clear [id] [player] [#limb]` | clear one/all |
| `nt_diag [player]` | target/netid diagnostics |
| `nt_limbs [player]` | list body parts with indices |
| `nt_bloodtype [A+\|random]` | show / set your blood type (cheats) |

- **Target**: explicit `[player]` (MP partial name or `@a`) → open wound view on an ally → local player. Names with spaces work as-is: `nt_add frostbite 20 Staili Steyfer #lhand`.
- Organ-stage aliases (`pechen_warning2`, `kidney_deadlow`, `lungdamage_severe`, …) write into the base scalar (`liverdamage` / `kidneydamage` / `lungdamage`).
- **Cheats**: in multiplayer all `nt_*` commands require **`sv_cheats`** enabled in lobby rules (same as `give` / `godmode`). The host is blocked too when it is off.
- **Limb selection** via a `#` token: `#sel` (highlighted in UNI-HEALTH), `#<index>`, aliases `#head #chest #lower #lhand #rhand #lfoot #rfoot #lthigh #rthigh ...`, or a name fragment. Applies to limb-scoped afflictions (`necrosis`, `tetanus`, `frostbite`, `parazite`). Without `#`, a limb is picked automatically (necrosis never uses the head). The necrosis icon **does not appear on the head**.
- **`parazite`**: `nt_set parazite 100 #larm` rolls a random 1–5 on that limb; `nt_set parazite 3 #larm` sets exactly 3. Moodle stays at 100% while any remain.
- The command line offers **autocompletion** for both `id` and `#limb` (start typing `#` to see the limb list).

## Requirements

| | |
|---|---|
| **Required** | [BepInEx 5.4.x](https://github.com/BepInEx/BepInEx/releases) |
| **Required** | [CUCoreLib](https://www.nexusmods.com/scavprototype/mods/341) — shared modding library (item/content registration) |
| **Optional** | [KrokoshaCasualtiesMP (KrokMP)](https://cucorelib.web.app/) — multiplayer affliction sync (without it the mod runs in single-player) |
| **Optional** | [QoL.Unknown](https://github.com/jimmyking9999999/QoL-Unknown/releases) — **Neurotrauma** settings tab |
| **Optional** | [MultyModik](https://nexusmods.com/scavprototype/mods/435) — hug/mood tick source |
| **Optional** | **Herobrine's Prosthetics** (`prosthetics.dll`, GUID `com.HerobrinesProsthetics`) — limb prosthetics |

> Single-player only needs BepInEx + CUCoreLib. For MP sync, install KrokMP; everyone with Neurotrauma should use the same plugin version (+ CUCoreLib, and KrokMP when playing together). Players without this mod may still join.

## Install

1. Install BepInEx and **CUCoreLib** (for MP also **KrokoshaCasualtiesMP / KrokMP**) — see https://cucorelib.web.app/
2. Copy the contents of the `NeurotraumaModik` folder into:
   ```
   Casualties Unknown\BepInEx\plugins\
   ```
   You should have:
   - `NeurotraumaModikByStaili.dll` (icons already inside)
   - `NeurotraumaModik\Content\Sound\` (sounds; **no** `Sound\Voice`)
3. Launch the game. `BepInEx\LogOutput.log` should contain:
   ```
   [Info : NeurotraumaModikByStaili] NeurotraumaModik by Staili v2.2.2 loaded. ... KrokMP: True/False ...
   ```

## Settings

The **Neurotrauma** tab in the settings menu (with QoL.Unknown) or the **F9** hotkey (in-plugin window). File: `BepInEx\config\NeurotraumaModikByStaili.cfg`.  
Key options: `ShowModMoodles` (icons in the vanilla bar), `HallucinationVisuals` (phantom effects), `EnableParasites` (parasites + extract minigame), symptom toggles (liver / kidneys / lungs / …), `HostAuthoritative` (host authority), `AddToLootPool` (item loot spawning).  
In MP (with KrokMP), clients **follow the host symptom mask** (F9 symptom checkboxes are view-only for clients).  
The mod row on the **Mods** tab (with QoL.Unknown) has **GIT** (GitHub releases) and **Nexus** buttons.

## Compatibility

- Tied to the game / CUCoreLib (and KrokMP for MP sync) version this build targets. After a major game update the plugin needs a rebuild.
- May conflict with mods that patch the wound view (`WoundView`), the status bar (`MoodleManager`) or the item system.
- **RshLib**: its `Utils.Create` patch breaks CUCore items (`nt_*`).
- **Herobrine's Prosthetics**: optional integration (runtime `ProstheticLimb` detection). Prosthetic limbs are exempt from our per-limb infection/necrosis/frostbite effects and from necrosis-picker amputation via `nt_bonesaw`.

## Release contents

| File / folder | Purpose |
|------|---------|
| `NeurotraumaModik\NeurotraumaModikByStaili.dll` | Plugin (icons embedded) — place in `BepInEx\plugins\` |
| `NeurotraumaModik\NeurotraumaModik\Content\Sound\` | Sounds beside the DLL (**no** `Voice`) |
| `NeurotraumaModik\README.md` | This file |

</details>
