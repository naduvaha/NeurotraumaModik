# NeurotraumaModik by Staili

[Русский](#русский) | [English](#english)

**Version / Версия:** `2.1.1`
**Plugin / Плагин:** `NeurotraumaModikByStaili.dll`
**Nexus / Нексус:** [nexusmods.com/scavprototype/mods/440](https://www.nexusmods.com/scavprototype/mods/440)
**Hard dependency / Жёсткая зависимость:** [KrokoshaCasualtiesMP (KrokMP)](https://cucorelib.web.app/) · [CUCoreLib](https://www.nexusmods.com/scavprototype/mods/341)
**Optional / Опционально:** [QoL.Unknown](https://github.com/jimmyking9999999/QoL-Unknown/releases) · **Herobrine's Prosthetics** (протезы)

---

<a id="русский"></a>

<details open>
<summary><b>Русский</b></summary>

## Описание

Адаптация мода медицинского реализма **Neurotrauma** (из Barotrauma) для игры **Casualties Unknown**.
Добавляет новый слой аффликций (осложнений) поверх ванильной системы «муддлов», не переписывая её — всё навешивается через аддитивные Harmony-патчи, собственную UI-панель и окно настроек.

## Аффликции (осложнения)

Каждое имеет иконку, локализованные описание/подсказки лечения и, где нужно, отображается в нижней ванильной панели статусов.

| ID | RU | Как появляется | Как лечится |
|----|----|----|----|
| `frostbite` | Обморожение | холодная среда | тепло, согревание |
| `frostbite_amputation` | Обморожение — предампутация | конечность промёрзла до 100% | срочно: пила (ампутация) — иначе растёт некроз |
| `necrosis` | Некроз | тяжёлый столбняк/обморожение/сепсис/радиация, 100% обморожение | скальпель (дебридмент, < 70%) или пила (ампутация, ≥ 70%); при успехе инфекция на этой конечности сразу → 0 |
| `tetanus` | Столбняк | укусы, шип-ловушки, капканы и другие острые раны (не от инфекции) | время + обработка; до некроза (≥75%) |
| `pneumothorax` | Пневмоторакс | травма груди, взрывы | плевральный дренаж (chestdrain / ранорасширитель) |
| `lungdamage` | Повреждение лёгких | гемоторакс, травмы | кислородный конденсатор, покой (O2 > 94%) |
| `lungdamage_severe` | Повреждение лёгких — критично | `lungdamage` ≥ 65 | срочно кислородный конденсатор; снизить основное повреждение |
| `lung_overexpand` | Расширение лёгких | взрыв рядом / резкий перепад давления | покой, кислородный конденсатор |
| `lung_compress` | Сдавливание лёгких | тонешь в тяжёлой жидкости (нефть) без снаряжения | выйти из жидкости, снаряжение / конденсатор |
| `lung_wall_collapse` | Сдавление стенок лёгких | сильное внутреннее кровотечение | остановить кровотечение (повязка/шов/хирургия) |
| `hyperventilation` | Гипервентиляция | стресс, адреналин, низкий O2 | успокоить пациента, малая доза морфина |
| `heartdamage` | Повреждение сердца | долгая фибрилляция, инсульт, экстремальное давление | хирургия: пересадка сердца |
| `seizure` | Судороги | падение здоровья мозга, гипоксия, радиация | морфин (малая доза), защита от травм; ухудшает точность стрельбы (разброс) |
| `kidneydamage` | Повреждение почек | радиация, септический шок, сильное обезвоживание, передоз, стойко низкое давление | время; убрать причину; УЛР (L.R.D.) |
| `kidneyfailure` | Почечная недостаточность | запущенное повреждение почек | хирургия: пересадка почки |
| `kidney_warning` | Тревога по почкам | `kidneyfailure` ≥ 40 | снизить радиацию/сепсис/обезвоживание |
| `kidney_deadlow` | Почки — критично | `kidneyfailure` ≥ 80 | срочно: пила → пересадка почки |
| `liverdamage` | Повреждение печени | алкоголь, передозировка, сепсис, радиация, токсины при отказе почек, антипаразитарное | бросить спирт; лечить причину |
| `liverfailure` / `pechen_dead` | Отказ печени | `liverdamage` ≥ 70 | хирургия: пересадка печени + антипаразитарное (профилактика), без алкоголя |
| `pechen_warning` | Тревога по печени | `liverdamage` 10–70 | бросить пить; сепсис / передозировка / радиация |
| `platadead1/2/3stadia` | Сбой чипа (1–3) | радиация, травма, сепсис, передоз, экстрем. темп. (только чипированный режим) | крафт/применить `nt_important_chip` (плата ≥90% + нить×2) |
| `chronicpain` | Хроническая боль | давние травмы | морфин (малая доза, осторожно с зависимостью) |
| `psychosis` | Психоз | затяжные галлюцинации (>40) | время, сон, спирт |
| `hallucinations` | Галлюцинации | радиация, травма, низкое настроение | время, сон, спирт |
| `porez1` | Порез (степень 1) | разрез скальпелем; шанс от порезов/укусов | ванильные нити (`medicalsuture`) или само |
| `porez3` | Порез (степень 3, широкий) | расширение раны ранорасширителем | зашить после операции |
| `porez4_foreign` / `porez5_foreign` | Порез с инородным телом | попадание инородного тела (выше шанс при укусах) | извлечь ножницами, затем зашить |
| `parazite` | Паразиты | ~6 мин необработанного `porez4/5_foreign` (1–5 шт.); после извлечения — **10 мин** на ножницы, иначе снова заселятся | извлечь руками/пинцетом; затем ножницами убрать инородность; `nt_antiparasite` только профилактика |
| `fresh_suture` | Свежий шов | после наложения нитей (ваниль) | место защищено от повреждений, заживает само (100 → 0, ~2 мин) |

## Особенности

- **Фантомные эффекты** при высоком психозе/галлюцинациях: призрачные пауки, фантомное кровотечение с красной виньеткой и жуткий шёпот на экране игрока. При **психозе > 30** — слуховые галлюцинации в духе Баратравмы на ванильных звуках: выстрелы, «вьетнамка» с сонаром, случайные звуки боли и крики персонажа. Чисто клиентски, без реального урона (отключается в настройках).
- **Иконки мода в ванильной панели статусов** — активные осложнения показываются снизу рядом с ванильными, размер подогнан под ванильный (отключается).
- **Иконки на силуэте UNI-HEALTH** привязаны к конечности (не ездят за курсором): некроз — на поражённой руке/ноге; сердце/лёгкие — только на груди; почки/печень — на животе/нижнем торсе.
- **Своя хирургия** на предметы (скальпель / пила / ранорасширитель / ножницы): дренаж, удаление мёртвой ткани, ампутация, пересадка органа (сердце / лёгкие / почки / печень). Для пересадки нужен ванильный предмет `internalorgans` (качество ≥40%) — один предмет на одну операцию. После пересадки печени — окно риска инфекции (`liver_graft`): антипаразитарное ускоряет приживление; алкоголь бьёт по новому органу сильнее. **Операции не «в один клик»**: сначала разрез скальпелем (porez1) → расширение ранорасширителем (porez3) → и только затем внутренние процедуры; инородные тела извлекаются ножницами; закрытие — ванильными нитями (`medicalsuture`). Неверный инструмент не продвигает операцию, а лишь слегка вредит. Анестезия — через кислородный конденсатор с заряженной сывороткой. Дебридмент/ампутация некроза **сразу** обнуляет ванильную инфекцию на оперированной конечности.
- **Износ инструментов** — хирургические инструменты тратят состояние только при выполнении операции (не при открытии меню); расходники — при использовании.
- **Паразиты**: заселяются в необработанную рану с инородным телом (~6 мин). После извлечения — **10 минут**, чтобы убрать инородность ножницами, иначе паразиты вернутся. Мудл `parazite` на 100%, пока есть хотя бы один. Миниигра (окно ран / пинцет); в MP можно тянуть вместе. Антипаразитарное — только **профилактика** (~6 мин).
- **Мультиплеер**: авторитет на хосте; болезни привязаны к **Steam ID** (не «переезжают» на другого при перезаходе); синхронизация ран/паразитов/группы крови и per-limb трекеров; маска симптомов хоста; совместная хирургия и миниигра паразитов. Игроки **без** Neurotrauma могут быть в лобби — у них нет симптомов/предметов мода; у остальных мод продолжает работать.
- **Группа крови (ABO+Rh)**: случайная при спавне в забеге; показывается в панели симптомов («У вас _ группа крови») и в описании ванильного пакета жёлтой крови. Сохраняется при переходе слоёв и в `save.sv` (Continue). **Несовместимое вливание** жёлтой крови → ~3 мин повышенное давление (~160) и пульс 120.
- **Крафт / spawn `nt_*`**: инструменты и расходники в вкладке Medicine (через CUCore `RecipeRegistry`); типированные пакеты крови — `bloodbag` + 20 мл `alienblood`. Создание предметов — путь CUCore (`Utils.Create` → `CustomInstantiate`).
- **Сохранение аффликций**: статус мода пишется в блок `neurotrauma` внутри `save.sv` вместе с группой крови, счётчиками паразитов по конечностям и возрастом инородных ран.
- **Совместимость с Herobrine's Prosthetics** (опционально): если у игрока установлен мод протезов, на конечности с `ProstheticLimb` не показываются necrosis/tetanus/frostbite/chronicpain, не предлагается ампутация через necrosis-picker, мод не бьёт `skinHealth` протеза обморожением. Body-wide аффликции (психоз, сердце, почки и т.д.) по-прежнему действуют на всё тело.

## Предметы

| ID | Предмет | Назначение |
|----|---------|-----------|
| `nt_scalpel` | Скальпель | открывает хирургию: разрез (porez1), дебридмент некроза |
| `nt_bonesaw` | Костная пила | ампутация, пересадка (нужны `internalorgans` ≥40%) |
| `nt_retractor` | Ранорасширитель | расширяет рану (porez3), плевральный дренаж, внутренние процедуры |
| `nt_scissors` | Ножницы | крафт: 2× куб металлолома (`scrapcube`) + 20 мл биохим; извлечение инородных тел / сыворотки |
| `nt_antiparasite` | Антипаразитарное | профилактика новых паразитов (~6 мин); слегка помогает печени / сепсису — **не** извлекает уже засевших |
| `nt_serum_sleep` | Сыворотка для сна | заряжается в конденсатор (как батарейка) для анестезии |
| `nt_o2_condenser` | Кислородный конденсатор | пустой — кислородная маска (O2 + гипервентиляция); с сывороткой — усыпляет для операции |
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

- **Цель**: явный `[игрок]` (частичное имя в MP или `@a`) → открытое окно ран на союзнике → локальный игрок. Ник с пробелами пишется как есть: `nt_add frostbite 20 name name #lhand`.
- **Читы**: в мультиплеере все `nt_*` требуют включённый **`sv_cheats`** в правилах лобби (как `give` / `godmode`). Без него даже хост получит отказ.
- **Выбор конечности** токеном `#`: `#sel` (выделенная в UNI-HEALTH), `#<индекс>`, алиасы `#head #chest #lower #lhand #rhand #lfoot #rfoot #lthigh #rthigh ...`, либо фрагмент имени. Работает для аффликций, привязанных к конечности (`necrosis`, `tetanus`, `frostbite`, `parazite`). Без `#` конечность выбирается автоматически (для некроза — не голова). Иконка некроза **не показывается на голове**.
- **`parazite`**: `nt_set parazite 100 #larm` — случайно 1–5 шт. на конечности; `nt_set parazite 3 #larm` — ровно 3. Мудл всегда 100%, пока счётчик > 0.
- В командной строке для `id` и для `#конечность` работает **автозаполнение** (начните печатать `#`, чтобы увидеть список конечностей).

## Зависимости

| | |
|---|---|
| **Обязательно** | [BepInEx 5.4.x](https://github.com/BepInEx/BepInEx/releases) |
| **Обязательно** | [KrokoshaCasualtiesMP (KrokMP)](https://cucorelib.web.app/) — мультиплеер и синхронизация |
| **Обязательно** | [CUCoreLib](https://www.nexusmods.com/scavprototype/mods/341) — общая библиотека модов (регистрация предметов/контента, netcode) |
| **Опционально** | [QoL.Unknown](https://github.com/jimmyking9999999/QoL-Unknown/releases) — вкладка настроек мода |
| **Опционально** | [MultyModik](https://github.com/naduvaha/MultyModik/releases) — источник тиков настроения/обнимашек |
| **Опционально** | **Herobrine's Prosthetics** (`prosthetics.dll`, GUID `com.HerobrinesProsthetics`) — протезы конечностей |

> У кого установлен Neurotrauma — одна и та же версия плагина (+ KrokMP / CUCoreLib). Игроки без этого мода могут заходить в лобби; симптомы/предметы Neurotrauma у них не работают, у остальных мод не отключается.

## Установка

1. Установите BepInEx, **KrokoshaCasualtiesMP (KrokMP)** и **CUCoreLib** — см. https://cucorelib.web.app/
2. Скопируйте содержимое папки `NeurotraumaModik` в:
   ```
   Casualties Unknown\BepInEx\plugins\
   ```
   (`NeurotraumaModikByStaili.dll` и папку `NeurotraumaModik\Content` с иконками/звуками)
3. Запустите игру. В `BepInEx\LogOutput.log` появится строка:
   ```
   [Info : NeurotraumaModikByStaili] NeurotraumaModik by Staili v2.1.1 loaded. ...
   ```

## Настройки

`Настройки → Mods` (при QoL.Unknown) или горячая клавиша **F9**. Файл: `BepInEx\config\NeurotraumaModikByStaili.cfg`.
Ключевые опции: `ShowModMoodles` (иконки в ванильной панели), `HallucinationVisuals` (фантомные эффекты), `EnableParasites` (паразиты + миниигра), тогглы остальных симптомов, `HostAuthoritative` (авторитет хоста), `AddToLootPool` (спавн предметов в луте).
В MP клиенты **следуют маске симптомов хоста** (локальные галочки симптомов в F9 только для просмотра).
На строке мода во вкладке **Mods** (при QoL.Unknown) есть кнопки **GIT** (страница релизов на GitHub) и **Nexus** (страница мода на Nexus).

## Совместимость

- Требует версию игры / KrokMP / CUCoreLib, под которые собрана сборка.
- Возможны конфликты с модами, патчащими окно ран (`WoundView`), панель статусов (`MoodleManager`) или систему предметов.
- **RshLib**: его патч `Utils.Create` ломает CUCore-предметы (`nt_*`).
- **Herobrine's Prosthetics**: поддерживается опционально (runtime-детект `ProstheticLimb`). Протез не получает per-limb инфекцию/некроз/обморожение от нашего мода и не попадает под `nt_bonesaw` через necrosis-picker.

## Содержимое релиза

| Файл / папка | Описание |
|------|----------|
| `NeurotraumaModik\NeurotraumaModikByStaili.dll` | Плагин — кладётся в `BepInEx\plugins\` |
| `NeurotraumaModik\NeurotraumaModik\Content\` | Иконки и звуки — рядом с DLL |

</details>

---

<a id="english"></a>

<details>
<summary><b>English</b></summary>

## About

A Casualties Unknown adaptation of Barotrauma's medical-realism mod **Neurotrauma**.
It layers a new set of afflictions (complications) on top of the vanilla moodle system without rewriting it — everything is bolted on with additive Harmony patches, a dedicated UI panel and a settings window.

## Afflictions (complications)

Each has an icon, localized description/cure hints and, where relevant, shows in the vanilla bottom status bar.

| ID | EN | Trigger | Cure |
|----|----|----|----|
| `frostbite` | Frostbite | cold environment | warmth, rewarming |
| `frostbite_amputation` | Frostbite — pre-amputation | limb frozen to 100% | urgent: bonesaw (amputation) — otherwise necrosis grows |
| `necrosis` | Necrosis | severe tetanus/frostbite/sepsis/radiation, 100% frostbite | scalpel (debridement, < 70%) or bonesaw (amputation, ≥ 70%); on success, that limb's infection drops to 0 immediately |
| `tetanus` | Tetanus | bites, spike traps, bear traps and other sharp wounds (not from infection) | time + wound care; treat before necrosis (75%+) |
| `pneumothorax` | Pneumothorax | chest trauma, explosions | chest drain (chestdrain / retractor) |
| `lungdamage` | Lung damage | hemothorax, trauma | O2 condenser, rest (O2 > 94%) |
| `lungdamage_severe` | Lung damage — critical | `lungdamage` ≥ 65 | O2 condenser urgently; reduce base damage |
| `lung_overexpand` | Lung over-expansion | nearby blast / rapid pressure change | rest, O2 condenser |
| `lung_compress` | Lung compression | drowning in heavy liquid (oil) without gear | leave the liquid, scuba gear / condenser |
| `lung_wall_collapse` | Lung wall collapse | severe internal bleeding | stop internal bleeding (bandage/suture/surgery) |
| `hyperventilation` | Hyperventilation | stress, adrenaline, low O2 | calm the patient, low-dose morphine |
| `heartdamage` | Heart damage | prolonged fibrillation, stroke, BP extremes | surgery: heart transplant |
| `seizure` | Seizure | brain-health drops, hypoxia, radiation | morphine (low dose), protect from injury; worsens weapon accuracy (spread) |
| `kidneydamage` | Kidney damage | radiation, septic shock, severe dehydration, overdose, sustained low BP | time; treat cause; L.R.D. |
| `kidneyfailure` | Kidney failure | advanced kidney damage | surgery: kidney transplant |
| `kidney_warning` | Kidney warning | `kidneyfailure` ≥ 40 | reduce radiation/sepsis/dehydration |
| `kidney_deadlow` | Kidney failure — critical | `kidneyfailure` ≥ 80 | urgent: bonesaw → kidney transplant |
| `liverdamage` | Liver damage | alcohol, overdose, sepsis, radiation, kidney toxins, anti-parasite | stop alcohol; treat cause |
| `liverfailure` / `pechen_dead` | Liver failure | `liverdamage` ≥ 70 | surgery: liver transplant + anti-parasite prophylaxis; no alcohol |
| `pechen_warning` | Liver warning | `liverdamage` 10–70 | stop drinking; sepsis / overdose / radiation |
| `chronicpain` | Chronic pain | long-standing injuries | morphine (low dose, mind dependency) |
| `psychosis` | Psychosis | prolonged hallucinations (>40) | time, sleep, alcohol |
| `hallucinations` | Hallucinations | radiation, trauma, low mood | time, sleep, alcohol |
| `porez1` | Cut (grade 1) | scalpel incision; chance from cuts/bites | vanilla thread (`medicalsuture`) or self-heal |
| `porez3` | Cut (grade 3, wide) | widened with a retractor | suture after operating |
| `porez4_foreign` / `porez5_foreign` | Cut with foreign body | embedded foreign object (higher chance on bites) | extract with scissors, then suture |
| `parazite` | Parasites | ~6 min untreated foreign wound (1–5); after pull — **10 min** to scissors-extract or they re-burrow | pull with hands/tweezers; then scissors; `nt_antiparasite` prophylaxis only |
| `fresh_suture` | Fresh suture | after applying thread (vanilla) | the spot is protected from re-injury, heals on its own (100 → 0, ~2 min) |

## Features

- **Phantom effects** at high psychosis/hallucinations: phantom spiders, phantom bleeding with a red vignette, and creepy whispers on the player's screen. At **psychosis > 30** — Barotrauma-style auditory flashbacks using vanilla game audio: gunshots, sonar/"Vietnam" jolts, random pain SFX, and character scream lines. Purely cosmetic, no real damage (toggleable).
- **Mod icons in the vanilla status bar** — active complications appear at the bottom next to vanilla ones, sized to match (toggleable).
- **UNI-HEALTH silhouette icons** are limb-anchored (they do not follow the cursor): necrosis on the affected arm/leg; heart/lungs on the chest only; kidneys/liver on the abdomen / lower torso.
- **Custom surgery** on tools (scalpel / bonesaw / retractor / scissors): drainage, dead-tissue removal, amputation, single-organ transplant (heart / lungs / kidneys). Each transplant consumes one vanilla `internalorgans` item (condition ≥40%). **Operations are not one-click**: incise with the scalpel (porez1) → widen with the retractor (porez3) → then internal procedures; foreign bodies are pulled with scissors; closing uses vanilla thread (`medicalsuture`). The wrong tool doesn't advance the operation — it just hurts a little. Anesthesia comes from the O2 condenser with a loaded serum charge. Necrosis debridement/amputation **immediately** clears vanilla infection on the operated limb.
- **Tool wear** — surgical tools lose condition only when an operation is performed (not on opening the menu); consumables wear on use.
- **Parasites**: burrow into untreated foreign wounds (~6 min). After extraction you have **10 minutes** to remove the foreign body with scissors or they return. Minigame (wound view / tweezers); MP co-op pull. Anti-parasitic is prophylaxis only.
- **Multiplayer**: host-authoritative; afflictions bound to **Steam ID**; state sync including per-limb trackers; host FEATURES mask; shared surgery / parasite minigame. Players **without** Neurotrauma may join — they lack mod symptoms/items; everyone else keeps the mod.
- **Blood type (ABO+Rh)**: rolled randomly at spawn; shown on the symptoms panel (“You have blood type _”) and on vanilla yellow blood-bag tooltips. Persists across layers and in `save.sv` (Continue). **Incompatible yellow-blood transfusion** → ~3 min elevated BP (~160) and heart rate 120.
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
| `nt_antiparasite` | Anti-parasitic | prophylaxis against new parasites (~6 min); mild liver/sepsis help — does **not** extract burrowed parasites |
| `nt_serum_sleep` | Anesthetic serum | loads into the condenser (like a battery) for anesthesia |
| `nt_o2_condenser` | O2 condenser | empty — oxygen mask (O2 + hyperventilation); with serum — puts the patient under for surgery |
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

- **Target**: explicit `[player]` (MP partial name or `@a`) → open wound view on an ally → local player. Names with spaces work as-is: `nt_add frostbite 20 name name #lhand`.
- **Cheats**: in multiplayer all `nt_*` commands require **`sv_cheats`** enabled in lobby rules (same as `give` / `godmode`). The host is blocked too when it is off.
- **Limb selection** via a `#` token: `#sel` (highlighted in UNI-HEALTH), `#<index>`, aliases `#head #chest #lower #lhand #rhand #lfoot #rfoot #lthigh #rthigh ...`, or a name fragment. Applies to limb-scoped afflictions (`necrosis`, `tetanus`, `frostbite`, `parazite`). Without `#`, a limb is picked automatically (necrosis never uses the head). The necrosis icon **does not appear on the head**.
- **`parazite`**: `nt_set parazite 100 #larm` rolls a random 1–5 on that limb; `nt_set parazite 3 #larm` sets exactly 3. Moodle stays at 100% while any remain.
- The command line offers **autocompletion** for both `id` and `#limb` (start typing `#` to see the limb list).

## Requirements

| | |
|---|---|
| **Required** | [BepInEx 5.4.x](https://github.com/BepInEx/BepInEx/releases) |
| **Required** | [KrokoshaCasualtiesMP (KrokMP)](https://cucorelib.web.app/) — multiplayer and sync |
| **Required** | [CUCoreLib](https://www.nexusmods.com/scavprototype/mods/341) — shared modding library (item/content registration, netcode) |
| **Optional** | [QoL.Unknown](https://github.com/jimmyking9999999/QoL-Unknown/releases) — mod settings tab |
| **Optional** | [MultyModik](https://github.com/naduvaha/MultyModik/releases) — hug/mood tick source |
| **Optional** | **Herobrine's Prosthetics** (`prosthetics.dll`, GUID `com.HerobrinesProsthetics`) — limb prosthetics |

> Anyone running Neurotrauma should use the same plugin version (+ KrokMP / CUCoreLib). Players without this mod may still join; they just won't get Neurotrauma symptoms/items, and the mod keeps working for the rest.

## Install

1. Install BepInEx, **KrokoshaCasualtiesMP (KrokMP)** and **CUCoreLib** — see https://cucorelib.web.app/
2. Copy the contents of the `NeurotraumaModik` folder into:
   ```
   Casualties Unknown\BepInEx\plugins\
   ```
   (`NeurotraumaModikByStaili.dll` and the `NeurotraumaModik\Content` folder with icons/sounds)
3. Launch the game. `BepInEx\LogOutput.log` should contain:
   ```
   [Info : NeurotraumaModikByStaili] NeurotraumaModik by Staili v2.1.1 loaded. ...
   ```

## Settings

`Settings → Mods` (with QoL.Unknown) or the **F9** hotkey. File: `BepInEx\config\NeurotraumaModikByStaili.cfg`.
Key options: `ShowModMoodles` (icons in the vanilla bar), `HallucinationVisuals` (phantom effects), `EnableParasites` (parasites + extract minigame), other symptom toggles, `HostAuthoritative` (host authority), `AddToLootPool` (item loot spawning).
In MP, clients **follow the host symptom mask** (F9 symptom checkboxes are view-only for clients).
The mod row on the **Mods** tab (with QoL.Unknown) has **GIT** (GitHub releases page) and **Nexus** (mod page on Nexus) buttons.

## Compatibility

- Tied to the game / KrokMP / CUCoreLib version this build targets. After a major game update the plugin needs a rebuild.
- May conflict with mods that patch the wound view (`WoundView`), the status bar (`MoodleManager`) or the item system.
- **RshLib**: its `Utils.Create` patch breaks CUCore items (`nt_*`).
- **Herobrine's Prosthetics**: optional integration (runtime `ProstheticLimb` detection). Prosthetic limbs are exempt from our per-limb infection/necrosis/frostbite effects and from necrosis-picker amputation via `nt_bonesaw`.

## Release contents

| File / folder | Purpose |
|------|---------|
| `NeurotraumaModik\NeurotraumaModikByStaili.dll` | The plugin — place in `BepInEx\plugins\` |
| `NeurotraumaModik\NeurotraumaModik\Content\` | Icons and sounds — next to the DLL |

</details>
