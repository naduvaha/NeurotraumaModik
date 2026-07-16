# NeurotraumaModik by Staili

[Русский](#русский) | [English](#english)

**Version / Версия:** `2.0.0`
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
| `necrosis` | Некроз | тяжёлый столбняк/обморожение/сепсис/радиация, 100% обморожение | скальпель (дебридмент, < 70%) или пила (ампутация, ≥ 70%) |
| `tetanus` | Столбняк | ванильная инфекция раны (`infectionAmount` ≥ 40) | лечение инфекции; спадает сам |
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
| `chronicpain` | Хроническая боль | давние травмы | морфин (малая доза, осторожно с зависимостью) |
| `psychosis` | Психоз | затяжные галлюцинации (>40) | время, сон, спирт |
| `hallucinations` | Галлюцинации | радиация, травма, низкое настроение | время, сон, спирт |
| `porez1` | Порез (степень 1) | разрез скальпелем; шанс от порезов/укусов | ванильные нити (`medicalsuture`) или само |
| `porez3` | Порез (степень 3, широкий) | расширение раны ранорасширителем | зашить после операции |
| `porez4_foreign` / `porez5_foreign` | Порез с инородным телом | попадание инородного тела (выше шанс при укусах) | извлечь ножницами, затем зашить |
| `fresh_suture` | Свежий шов | после наложения нитей (ваниль) | место защищено от повреждений, заживает само (100 → 0, ~2 мин) |

## Особенности

- **Фантомные эффекты** при высоком психозе/галлюцинациях: призрачные пауки, фантомное кровотечение с красной виньеткой и жуткий шёпот на экране игрока. При **психозе > 30** — слуховые галлюцинации в духе Баратравмы на ванильных звуках: выстрелы, «вьетнамка» с сонаром, случайные звуки боли и крики персонажа. Чисто клиентски, без реального урона (отключается в настройках).
- **Иконки мода в ванильной панели статусов** — активные осложнения показываются снизу рядом с ванильными, размер подогнан под ванильный (отключается).
- **Своя хирургия** на предметы (скальпель / пила / ранорасширитель / ножницы): дренаж, удаление мёртвой ткани, ампутация, пересадка органа (сердце / лёгкие / почки). Для пересадки нужен ванильный предмет `internalorgans` (качество ≥40%) — один предмет на одну операцию. **Операции не «в один клик»**: сначала разрез скальпелем (porez1) → расширение ранорасширителем (porez3) → и только затем внутренние процедуры; инородные тела извлекаются ножницами; закрытие — ванильными нитями (`medicalsuture`). Неверный инструмент не продвигает операцию, а лишь слегка вредит. Анестезия — через кислородный конденсатор с заряженной сывороткой.
- **Износ инструментов** — хирургические инструменты тратят состояние только при выполнении операции (не при открытии меню); расходники — при использовании.
- **Мультиплеер**: авторитет на хосте, синхронизация состояния (включая раны по конечностям и группу крови), лечение союзников через окно ран, операции с указанием конкретной конечности.
- **Группа крови (ABO+Rh)**: случайная при спавне в забеге; показывается в панели симптомов («У вас _ группа крови») и в описании ванильного пакета жёлтой крови. Сохраняется при переходе слоёв и в `save.sv` (Continue). **Несовместимое вливание** жёлтой крови → ~3 мин повышенное давление (~160) и пульс 120.
- **Крафт**: инструменты и расходники в вкладке Medicine; типированные пакеты крови — `bloodbag` + 20 мл `alienblood` (не меняют вашу группу, нужны для переливания с меткой ABO).
- **Сохранение аффликций**: статус мода пишется в блок `neurotrauma` внутри `save.sv` вместе с группой крови.
- **Совместимость с Herobrine's Prosthetics** (опционально): если у игрока установлен мод протезов, на конечности с `ProstheticLimb` не показываются necrosis/tetanus/frostbite/chronicpain, не предлагается ампутация через necrosis-picker, мод не бьёт `skinHealth` протеза обморожением. Body-wide аффликции (психоз, сердце, почки и т.д.) по-прежнему действуют на всё тело.

## Предметы

| ID | Предмет | Назначение |
|----|---------|-----------|
| `nt_scalpel` | Скальпель | открывает хирургию: разрез (porez1), дебридмент некроза |
| `nt_bonesaw` | Костная пила | ампутация, пересадка (нужны `internalorgans` ≥40%) |
| `nt_retractor` | Ранорасширитель | расширяет рану (porez3), плевральный дренаж, внутренние процедуры |
| `nt_scissors` | Ножницы | извлечение инородных тел, извлечение сыворотки из конденсатора |
| `nt_antiparasite` | Антипаразитарное | убирает паразитов/бактерий в крови |
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
- **Выбор конечности** токеном `#`: `#sel` (выделенная в UNI-HEALTH), `#<индекс>`, алиасы `#head #chest #lower #lhand #rhand #lfoot #rfoot #lthigh #rthigh ...`, либо фрагмент имени. Работает для аффликций, привязанных к конечности (`necrosis`, `tetanus`, `frostbite`). Без `#` конечность выбирается автоматически (для некроза — не голова). Иконка некроза **не показывается на голове**.
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

> Все игроки в лобби (хост и клиенты) должны иметь одинаковую версию плагина, KrokMP и CUCoreLib.

## Установка

1. Установите BepInEx, **KrokoshaCasualtiesMP (KrokMP)** и **CUCoreLib** — см. https://cucorelib.web.app/
2. Скопируйте содержимое папки `NeurotraumaModik` в:
   ```
   Casualties Unknown\BepInEx\plugins\
   ```
   (`NeurotraumaModikByStaili.dll` и папку `NeurotraumaModik\Content` с иконками/звуками)
3. Запустите игру. В `BepInEx\LogOutput.log` появится строка:
   ```
   [Info : NeurotraumaModikByStaili] NeurotraumaModik by Staili v2.0.0 loaded. ...
   ```

## Настройки

`Настройки → Mods` (при QoL.Unknown) или горячая клавиша **F9**. Файл: `BepInEx\config\NeurotraumaModikByStaili.cfg`.
Ключевые опции: `ShowModMoodles` (иконки в ванильной панели), `HallucinationVisuals` (фантомные эффекты), `HostAuthoritative` (авторитет хоста), `AddToLootPool` (спавн предметов в луте).
На строке мода во вкладке **Mods** (при QoL.Unknown) есть кнопки **GIT** (страница релизов на GitHub) и **Nexus** (страница мода на Nexus).

## Совместимость

- Требует версию игры / KrokMP / CUCoreLib, под которые собрана сборка.
- Возможны конфликты с модами, патчащими окно ран (`WoundView`), панель статусов (`MoodleManager`) или систему предметов.
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
| `necrosis` | Necrosis | severe tetanus/frostbite/sepsis/radiation, 100% frostbite | scalpel (debridement, < 70%) or bonesaw (amputation, ≥ 70%) |
| `tetanus` | Tetanus | vanilla wound infection (`infectionAmount` ≥ 40) | clear the infection; fades on its own |
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
| `chronicpain` | Chronic pain | long-standing injuries | morphine (low dose, mind dependency) |
| `psychosis` | Psychosis | prolonged hallucinations (>40) | time, sleep, alcohol |
| `hallucinations` | Hallucinations | radiation, trauma, low mood | time, sleep, alcohol |
| `porez1` | Cut (grade 1) | scalpel incision; chance from cuts/bites | vanilla thread (`medicalsuture`) or self-heal |
| `porez3` | Cut (grade 3, wide) | widened with a retractor | suture after operating |
| `porez4_foreign` / `porez5_foreign` | Cut with foreign body | embedded foreign object (higher chance on bites) | extract with scissors, then suture |
| `fresh_suture` | Fresh suture | after applying thread (vanilla) | the spot is protected from re-injury, heals on its own (100 → 0, ~2 min) |

## Features

- **Phantom effects** at high psychosis/hallucinations: phantom spiders, phantom bleeding with a red vignette, and creepy whispers on the player's screen. At **psychosis > 30** — Barotrauma-style auditory flashbacks using vanilla game audio: gunshots, sonar/"Vietnam" jolts, random pain SFX, and character scream lines. Purely cosmetic, no real damage (toggleable).
- **Mod icons in the vanilla status bar** — active complications appear at the bottom next to vanilla ones, sized to match (toggleable).
- **Custom surgery** on tools (scalpel / bonesaw / retractor / scissors): drainage, dead-tissue removal, amputation, single-organ transplant (heart / lungs / kidneys). Each transplant consumes one vanilla `internalorgans` item (condition ≥40%). **Operations are not one-click**: incise with the scalpel (porez1) → widen with the retractor (porez3) → then internal procedures; foreign bodies are pulled with scissors; closing uses vanilla thread (`medicalsuture`). The wrong tool doesn't advance the operation — it just hurts a little. Anesthesia comes from the O2 condenser with a loaded serum charge.
- **Tool wear** — surgical tools lose condition only when an operation is performed (not on opening the menu); consumables wear on use.
- **Multiplayer**: host-authoritative, state sync (including per-limb wounds and blood type), treating allies through the wound view, operations targeting a specific limb.
- **Blood type (ABO+Rh)**: rolled randomly at spawn; shown on the symptoms panel (“You have blood type _”) and on vanilla yellow blood-bag tooltips. Persists across layers and in `save.sv` (Continue). **Incompatible yellow-blood transfusion** → ~3 min elevated BP (~160) and heart rate 120.
- **Crafting**: tools and consumables under Medicine; typed blood packs need a `bloodbag` + 20 mL `alienblood` (they do not change your innate type — they are for labeled transfusion).
- **Save persistence**: mod status is written into a `neurotrauma` block inside `save.sv`, including blood type.
- **Herobrine's Prosthetics support** (optional): when the prosthetics mod is installed, limbs with a `ProstheticLimb` component do not show necrosis/tetanus/frostbite/chronicpain icons, are excluded from the necrosis amputation picker, and are skipped by our frostbite skin-damage write. Body-wide afflictions (psychosis, heart, kidneys, etc.) still apply to the whole patient.

## Items

| ID | Item | Purpose |
|----|------|---------|
| `nt_scalpel` | Scalpel | opens surgery: incision (porez1), necrosis debridement |
| `nt_bonesaw` | Bone saw | amputation, transplant (requires `internalorgans` ≥40%) |
| `nt_retractor` | Retractor | widens the wound (porez3), pleural drainage, internal procedures |
| `nt_scissors` | Scissors | extract foreign bodies, eject serum ampoule from the condenser |
| `nt_antiparasite` | Anti-parasitic | wipes parasites/bacteria in the blood |
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
- **Limb selection** via a `#` token: `#sel` (highlighted in UNI-HEALTH), `#<index>`, aliases `#head #chest #lower #lhand #rhand #lfoot #rfoot #lthigh #rthigh ...`, or a name fragment. Applies to limb-scoped afflictions (`necrosis`, `tetanus`, `frostbite`). Without `#`, a limb is picked automatically (necrosis never uses the head). The necrosis icon **does not appear on the head**.
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

> Every player in the lobby (host and clients) must run the same plugin, KrokMP and CUCoreLib version.

## Install

1. Install BepInEx, **KrokoshaCasualtiesMP (KrokMP)** and **CUCoreLib** — see https://cucorelib.web.app/
2. Copy the contents of the `NeurotraumaModik` folder into:
   ```
   Casualties Unknown\BepInEx\plugins\
   ```
   (`NeurotraumaModikByStaili.dll` and the `NeurotraumaModik\Content` folder with icons/sounds)
3. Launch the game. `BepInEx\LogOutput.log` should contain:
   ```
   [Info : NeurotraumaModikByStaili] NeurotraumaModik by Staili v2.0.0 loaded. ...
   ```

## Settings

`Settings → Mods` (with QoL.Unknown) or the **F9** hotkey. File: `BepInEx\config\NeurotraumaModikByStaili.cfg`.
Key options: `ShowModMoodles` (icons in the vanilla bar), `HallucinationVisuals` (phantom effects), `HostAuthoritative` (host authority), `AddToLootPool` (item loot spawning).
The mod row on the **Mods** tab (with QoL.Unknown) has **GIT** (GitHub releases page) and **Nexus** (mod page on Nexus) buttons.

## Compatibility

- Tied to the game / KrokMP / CUCoreLib version this build targets. After a major game update the plugin needs a rebuild.
- May conflict with mods that patch the wound view (`WoundView`), the status bar (`MoodleManager`) or the item system.
- **Herobrine's Prosthetics**: optional integration (runtime `ProstheticLimb` detection). Prosthetic limbs are exempt from our per-limb infection/necrosis/frostbite effects and from necrosis-picker amputation via `nt_bonesaw`.

## Release contents

| File / folder | Purpose |
|------|---------|
| `NeurotraumaModik\NeurotraumaModikByStaili.dll` | The plugin — place in `BepInEx\plugins\` |
| `NeurotraumaModik\NeurotraumaModik\Content\` | Icons and sounds — next to the DLL |

</details>
