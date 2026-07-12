# NeurotraumaModik by Staili

[Русский](#русский) | [English](#english)

**Version / Версия:** `0.1.0`
**Plugin / Плагин:** `NeurotraumaModikByStaili.dll`
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
| `necrosis` | Некроз | тяжёлый столбняк/обморожение/сепсис/радиация | скальпель (дебридмент, < 70%) или пила (ампутация, ≥ 70%) |
| `tetanus` | Столбняк | ванильная инфекция раны (`infectionAmount` ≥ 40) | лечение инфекции; спадает сам |
| `pneumothorax` | Пневмоторакс | травма груди, взрывы | плевральный дренаж (chestdrain / ранорасширитель) |
| `lungdamage` | Повреждение лёгких | гемоторакс, травмы | O2-маска, покой (O2 > 94%) |
| `hyperventilation` | Гипервентиляция | стресс, адреналин, низкий O2 | успокоить пациента, малая доза морфина |
| `heartdamage` | Повреждение сердца | долгая фибрилляция, инсульт, экстремальное давление | хирургия: пересадка сердца |
| `seizure` | Судороги | падение здоровья мозга, гипоксия, радиация | противосудорожное, защита от травм |
| `kidneydamage` | Повреждение почек | радиация, септический шок, сильное обезвоживание, передоз, стойко низкое давление | время, плазмаферез |
| `kidneyfailure` | Почечная недостаточность | запущенное повреждение почек | хирургия: пересадка почки |
| `chronicpain` | Хроническая боль | давние травмы | морфин (осторожно с зависимостью) |
| `psychosis` | Психоз | радиация, травма, низкое настроение | время, седативные |
| `hallucinations` | Галлюцинации | высокий психоз, радиация | время, седативные |

## Особенности

- **Фантомные эффекты** при высоком психозе/галлюцинациях: призрачные пауки, фантомное кровотечение с красной виньеткой и жуткий шёпот на экране игрока. Чисто визуально и клиентски (отключается в настройках).
- **Иконки мода в ванильной панели статусов** — активные осложнения показываются снизу рядом с ванильными, размер подогнан под ванильный (отключается).
- **Своя хирургия** на предметы (скальпель / пила / ранорасширитель): дренаж, удаление шрапнели, удаление мёртвой ткани, ампутация, пересадка органа (сердце / лёгкие / почки). Для пересадки нужен ванильный предмет `internalorgans` (качество ≥40%) — один предмет на одну операцию.
- **Износ инструментов** — хирургические инструменты тратят состояние только при выполнении операции (не при открытии меню); расходники — при использовании.
- **Мультиплеер**: авторитет на хосте, синхронизация состояния, лечение союзников через окно ран, операции с указанием конкретной конечности.
- **Крафт**: рецепты завязаны на симптомы; сложные (критические) процедуры требуют дополнительных ингредиентов.
- **Совместимость с Herobrine's Prosthetics** (опционально): если у игрока установлен мод протезов, на конечности с `ProstheticLimb` не показываются necrosis/tetanus/frostbite/chronicpain, не предлагается ампутация через necrosis-picker, мод не бьёт `skinHealth` протеза обморожением. Body-wide аффликции (психоз, сердце, почки и т.д.) по-прежнему действуют на всё тело.

## Предметы

| ID | Предмет | Назначение |
|----|---------|-----------|
| `nt_o2_mask` | Кислородная маска | восполняет O2 в крови, снимает гипервентиляцию |
| `nt_scalpel` | Скальпель | открывает хирургию: удаление шрапнели, дебридмент некроза |
| `nt_bonesaw` | Костная пила | ампутация, пересадка (нужны `internalorgans` ≥40%) |
| `nt_retractor` | Ранорасширитель | плевральный дренаж, внутренние процедуры |
| `nt_cpr_mask` | Маска СЛР | пассивно повышает эффективность СЛР |

## Консольные команды

| Команда | Назначение |
|---------|-----------|
| `nt_list [игрок]` | список аффликций на цели |
| `nt_add <id> [кол-во=50] [игрок] [#конечность]` | добавить тяжесть |
| `nt_set <id> <кол-во> [игрок] [#конечность]` | задать тяжесть |
| `nt_clear [id] [игрок] [#конечность]` | снять одну/все |
| `nt_diag [игрок]` | диагностика цели/netid |
| `nt_limbs [игрок]` | список частей тела с индексами |

- **Цель**: явный `[игрок]` (частичное имя в MP или `@a`) → открытое окно ран на союзнике → локальный игрок.
- **Выбор конечности** токеном `#`: `#sel` (выделенная в UNI-HEALTH), `#<индекс>`, либо алиасы `#head #chest #abdomen #larm #rarm #lleg #rleg`, либо фрагмент имени. Работает для аффликций, привязанных к конечности (`necrosis`, `tetanus`, `frostbite`).
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
   [Info : NeurotraumaModikByStaili] NeurotraumaModik by Staili v0.1.0 loaded. ...
   ```

## Настройки

`Настройки → Mods` (при QoL.Unknown) или горячая клавиша **F9**. Файл: `BepInEx\config\NeurotraumaModikByStaili.cfg`.
Ключевые опции: `ShowModMoodles` (иконки в ванильной панели), `HallucinationVisuals` (фантомные эффекты), `HostAuthoritative` (авторитет хоста), `AddToLootPool` (спавн предметов в луте).

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
| `necrosis` | Necrosis | severe tetanus/frostbite/sepsis/radiation | scalpel (debridement, < 70%) or bonesaw (amputation, ≥ 70%) |
| `tetanus` | Tetanus | vanilla wound infection (`infectionAmount` ≥ 40) | clear the infection; fades on its own |
| `pneumothorax` | Pneumothorax | chest trauma, explosions | chest drain (chestdrain / retractor) |
| `lungdamage` | Lung damage | hemothorax, trauma | O2 mask, rest (O2 > 94%) |
| `hyperventilation` | Hyperventilation | stress, adrenaline, low O2 | calm the patient, low-dose morphine |
| `heartdamage` | Heart damage | prolonged fibrillation, stroke, BP extremes | surgery: heart transplant |
| `seizure` | Seizure | brain-health drops, hypoxia, radiation | anticonvulsant, protect from injury |
| `kidneydamage` | Kidney damage | radiation, septic shock, severe dehydration, overdose, sustained low BP | time, plasma exchange |
| `kidneyfailure` | Kidney failure | advanced kidney damage | surgery: kidney transplant |
| `chronicpain` | Chronic pain | long-standing injuries | morphine (mind dependency) |
| `psychosis` | Psychosis | radiation, trauma, low mood | time, sedatives |
| `hallucinations` | Hallucinations | high psychosis, radiation | time, sedatives |

## Features

- **Phantom effects** at high psychosis/hallucinations: phantom spiders, phantom bleeding with a red vignette, and creepy whispers on the player's screen. Purely cosmetic and client-side (toggleable).
- **Mod icons in the vanilla status bar** — active complications appear at the bottom next to vanilla ones, sized to match (toggleable).
- **Custom surgery** on tools (scalpel / bonesaw / retractor): drainage, shrapnel removal, dead-tissue removal, amputation, single-organ transplant (heart / lungs / kidneys). Each transplant consumes one vanilla `internalorgans` item (condition ≥40%).
- **Tool wear** — surgical tools lose condition only when an operation is performed (not on opening the menu); consumables wear on use.
- **Multiplayer**: host-authoritative, state sync, treating allies through the wound view, operations targeting a specific limb.
- **Crafting**: recipes tied to symptoms; complex (critical) procedures need extra ingredients.
- **Herobrine's Prosthetics support** (optional): when the prosthetics mod is installed, limbs with a `ProstheticLimb` component do not show necrosis/tetanus/frostbite/chronicpain icons, are excluded from the necrosis amputation picker, and are skipped by our frostbite skin-damage write. Body-wide afflictions (psychosis, heart, kidneys, etc.) still apply to the whole patient.

## Items

| ID | Item | Purpose |
|----|------|---------|
| `nt_o2_mask` | O2 mask | restores blood O2, clears hyperventilation |
| `nt_scalpel` | Scalpel | opens surgery: shrapnel removal, necrosis debridement |
| `nt_bonesaw` | Bone saw | amputation, transplant (requires `internalorgans` ≥40%) |
| `nt_retractor` | Retractor | pleural drainage, internal procedures |
| `nt_cpr_mask` | CPR mask | passively boosts CPR effectiveness |

## Console commands

| Command | Purpose |
|---------|---------|
| `nt_list [player]` | list afflictions on the target |
| `nt_add <id> [amount=50] [player] [#limb]` | add severity |
| `nt_set <id> <amount> [player] [#limb]` | set severity |
| `nt_clear [id] [player] [#limb]` | clear one/all |
| `nt_diag [player]` | target/netid diagnostics |
| `nt_limbs [player]` | list body parts with indices |

- **Target**: explicit `[player]` (MP partial name or `@a`) → open wound view on an ally → local player.
- **Limb selection** via a `#` token: `#sel` (highlighted in UNI-HEALTH), `#<index>`, aliases `#head #chest #abdomen #larm #rarm #lleg #rleg`, or a name fragment. Applies to limb-scoped afflictions (`necrosis`, `tetanus`, `frostbite`).
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
   [Info : NeurotraumaModikByStaili] NeurotraumaModik by Staili v0.1.0 loaded. ...
   ```

## Settings

`Settings → Mods` (with QoL.Unknown) or the **F9** hotkey. File: `BepInEx\config\NeurotraumaModikByStaili.cfg`.
Key options: `ShowModMoodles` (icons in the vanilla bar), `HallucinationVisuals` (phantom effects), `HostAuthoritative` (host authority), `AddToLootPool` (item loot spawning).

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
