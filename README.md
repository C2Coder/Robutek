TES

# 🖍️ Robůtek

Robůtek je robotická platforma založená na čipu ESP32-S3. Je velice rozšitiřelný, ale ze základu umí jezdit, kreslit fixou, jezdit po čáře, pohybovat se bludištěm. Programování je přes [Jaculus](https://jaculus.org).

---

## 🔧 Vlastnosti

- Diferenciální pohon
- Enkodéry na kolech pro přesný pohyb (V2 - lepší přesnost)
- Držák na **fixu** pro kreslení na papír
- **IR senzory** pro sledování čáry
- **RGB senzor** pro detekování barev na podlaze (V2)
- **RGB podsvícení** pro hezčí vzhled Robůtka (V2)
- **Rozšiřující paluba** s:
  - Servem pro zvedání fixy
  - Adresovatelný RGB pásek
  - Laserový senzorem vzdálenosti (VL53L0X)
  - Přídavný RGB senzor (V2)

---

## 📅 Historie

| Rok | Verze | Popis |
|-----|-------|-------|
| 2024 | v1    | První plnohodnotný robůtek |
| 2025 | v2    | Opravené chyby na desce, rgb senzor, větší přesnost motorů |

---

##  🙌 Jak přispívat

### HW
- HW složka nechaná tak jak je beze změn

### DEV
- -> DEVELOPMENT.md

### Robutek library
- Knihovna přesunuta do `robutekLibrary`
- Funguje jako referenční projekt pro ostatní projekty v dokumentaci (kopírují se `@types` a `src/libs`)

- TODO? - rozdělení do `robutek-v1.ts` a `robutek-v2.ts`?

### Další verze dokumentace
- Zkopírovat poslední verzi dokumentace jako reference
- Zkopírovat `mkdocs-vx.yml` a upravit
- Upravit `.github/workflows/deploy-ghpages.yml` a `.github/workflows/test-ghpages.yml`



<!-- ## elektro
* 1x 18650 ve slotu
* nabíjení z USB-C z 5V - avšak je potřeba rozpoznávat proudové schopnosti portu 0,5/1,5/víc?
* stepup na předběžně 6V pro motory a serva
* stepup na 5V pro PMOD
* LDO na 3,3V pro ESP
* vypínač před stepupy (mechanický)
* 2x H mosty, motorové výstupy (+ enkodér vstupy)
* 8x senzory jízdy po čáře (viz obrázek)
* 8x LEDky + konektor
* 1x servo konektor
* pípák
* nx kde n € N && n <= 5 User tlačítko, Reset tlačítko, Boot tlačítko
* 3x lidar
* 1x PMOD konektor (muxovaný na ROM boot UART pinech?), asi s napájecím napětím volitelným jumperem
* uprostřed díra na fixu

### nabíječka
* MAX77757

### Stepup 5V
* ???

### Stepup 6V
* ???

### LDO 3.3V
* LD39200

### čárasenzor
* ??? ITR8307/S17/TR8(B)

### pípák
* viz ELKS

### servo
* SG90

### H-most
* DRV8833

# mecha
* uchycení paluby a lidarů
* zvedání fixi

# TODO

## Jarek M
- evaluace motorů

## Jirka
- kritika pro zábavu

## Patrik
- seznámit se s datasheety od vybraných součástek
    * MAX77757
    * LD39200
    * DRV8833
    * ITR8307/S17/TR8(B) -->
