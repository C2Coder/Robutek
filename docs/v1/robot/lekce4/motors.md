# Lekce 4 - Motory

V této lekci zkusíme točit motory a pohybovat robotem.

!!! tip "Polož si Robůtka na něco tak, aby se kola nedotýkala země a mohla se volně točit - tak můžeš kód otestovat bez toho, aby Robůtek sjel ze stolu."

Začneme opět s prázdným projektem, stáhni/nakopíruj si ho do nové složky pro tuto lekci:
[Stáhnout ZIP s prázdným projektem](../../lekce2/blank_project.zip){ .md-button .md-button--primary }

Otevři ve Visual Studiu Code a najdi `src/index.ts`, mělo by tam být něco jako:

```typescript
import * as colors from "./libs/colors.js";
import * as gpio from "gpio";
import { SmartLed, LED_WS2812 } from "smartled";
import { createRobutek } from "./libs/robutek.js"
const robutek = createRobutek("V1");
```

To je dobrý začátek - pokračovat budeme na konci souboru.

# Async main funkce
Motory jsou tzv. asynchroní, to znamená, se ovládají příkazem, který může trvat delší dobu, než se vykoná
(například "ujeď 50cm" bude trvat několik vteřin).

Abychom mohli motori používat, je třeba přidat tuto "kostru" s `async function()`. Klidně ji nakopíruj, patří na konec souboru `src/index.ts`.

```typescript
async function main() {
    // Tady bude kód na ovládání motorů

}

main().catch(console.error);
```

# Ježdění na vzdálenost

Ježdění má tři části - nastavení rychlosti, rampy, a samotný pohyb:

* `robutek.setSpeed(RYCHLOST)` - _RYCHLOST_ je číslo milimetrech za vteřinu, na Robůtkovi prakticky od 0 do 800 (záporné při značí couvání při
                                 nekonečné jízdě nebo jízdě na čas)
* `robutek.setRamp(RAMPA)` - _RAMPA_ je číslo udávající zrychlení Robůtka v mm/s^2. V případě, že je rovna nule, je zrychlení okamžité.
* `await robutek.move(SMĚR, { distance: VZDÁLENOST_V_MM })`
    * _SMĚR_ je desetinné číslo od -1 do 1, kdy
        * -1 je znamená úplně doleva,
        * 0 je rovně a
        * 1 je úplně doprava.
    * *VZDÁLENOST_V_MM* značí, jak daleko má robot jet

Zadávání parametrů rychlosti a rampy není potřeba opakovat při každém pohybu - knihovna si hodnotu pamatuje a při dalším volání funkce
`move` ji použije.

## Příklad
Patří dovnitř `async function main()`, pod komentář v přechozím kusu kódu:

```typescript
    robutek.setSpeed(100);  // Nastav rychlost na 100 mm/s
    robutek.setRamp(2000);  // Nastav zrychlení na 2000 mm/s^2
    await robutek.move(0, { distance: 100 });  // Ujeď 100 mm == 10 cm
```

**Úkol:** Zkus přidat kód, aby Robůtek dojel zase zpátky na stejné místo
??? note "Řešení"
    ```ts
    await robutek.move(0, { distance: -100 }) // Ujeď -100 mm == -10 cm
    ```


# Otáčení
Na otáčení má Robůtek připravenou funkci:

* `await robutek.rotate(ÚHEL)` - Otočí Robůtka o _ÚHEL_ stupňů rychlostí nastavenou přes `robutek.setSpeed`. Může být záporné číslo.

## Úkol
Napiš program tak, aby Robůtek popojel 10cm dopředu, otočil se čelem vzad (180 stupňů), a popojel zpátky na původní místo.
??? note "Řešení"

    ```ts
    import * as colors from "./libs/colors.js";
    import * as gpio from "gpio";
    import { SmartLed, LED_WS2812 } from "smartled";
    import { createRobutek } from "./libs/robutek.js"
    const robutek = createRobutek("V1");


    async function main() {
        // Tady bude kód na ovládání motorů

        robutek.setSpeed(100);  // Nastav rychlost na 100 mm/s
        robutek.setRamp(2000);  // Nastav zrychlení na 2000 mm/s^2

        await robutek.move(0, { distance: 100 });  // Ujeď 10 cm

        await robutek.rotate(180);  // Otoč se o 180 stupňů

        await robutek.move(0, { distance: 100 });  // Ujeď 10 cm
    }

    main().catch(console.error);
    ```

# Tvary
Kombinováním `robutek.move` a `robutek.rotate` můžeš s Robůtkem "vyjezdit" různé tvary.

**Úkol:** udělěj program tak, aby Robůtek objel čtverec a skončil zpátky na stejném místě.
??? note "Řešení"

    ```ts
    import * as colors from "./libs/colors.js";
    import * as gpio from "gpio";
    import { SmartLed, LED_WS2812 } from "smartled";
    import { createRobutek } from "./libs/robutek.js"
    const robutek = createRobutek("V1");

    async function main() {
        // Tady bude kód na ovládání motorů

        robutek.setSpeed(100);  // Nastav rychlost na 100 mm/s

        await robutek.move(0, { distance: 300 });  // Ujeď 30 cm
        await robutek.rotate(90);
        await robutek.move(0, { distance: 300 });
        await robutek.rotate(90);
        await robutek.move(0, { distance: 300 });
        await robutek.rotate(90);
        await robutek.move(0, { distance: 300 });
        await robutek.rotate(90);
    }

    main().catch(console.error);
    ```
