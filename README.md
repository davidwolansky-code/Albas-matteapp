# Albas mattestudio

En mattelek för mobilen. Alba skriver en uträkning med fingret, till exempel `7 + 5`, och appen läser det hon skrivit. Sedan gissar hon svaret, också med handskrift. Är det fel får hon hjälp i små steg, och svaret ritas som prickar.

**Prova:** https://davidwolansky-code.github.io/Albas-mattestudio/

## Så funkar det
1. **Skriv en uträkning** (plus eller minus, tal upp till 99) eller tryck **Ge mig en uppgift** och välj tal upp till 10, 20 eller 100.
2. Appen visar vad den läste (`7 + 5`). Är något fel trycker man på tecknet och byter det.
3. **Gissa först.** Alba skriver sitt svar för hand. Appen visar inga prickar förrän hon har gissat.
4. **Rätt:** konfetti, ljud och ⭐ om det blev rätt på första försöket. Svaret visas med prickar (tiotal i ramar om tio).
5. **Fel:** inget rött kryss, bara hjälp i steg.
   - Första gången: "svaret är lite större/mindre än …" och prickarna visas.
   - Andra gången: appen räknar tillsammans med henne, tiotal för tiotal och sedan ett i taget, med en ton för varje steg.
   - Tredje gången: svaret visas och man går vidare.
   - Knappen **Hjälp mig** går att använda när som helst.
6. Appen frågar alltid "Stämmer det?" innan ett fel svar räknas. Då blir hon aldrig bedömd för att appen läste fel.

## "Hoppsan"-lektionen: så ritar man siffran
Rättar Alba ett tecken som appen läste fel, eller blir tecknet oläsligt, visar appen en liten lektion:
- **"Hoppsan, sådär ser inte en 9 ut, i alla fall inte för mig!"** och en förklaring i text av hur tecknet ser ut och hur man ritar det.
- En **animerad ritguide** som visar var man börjar (grön prick), vilken väg pennan går och i vilken ordning strecken ritas.
- **Spegelvända siffror** känns igen: då står det i stället "Hoppsan, din 3:a vänder åt fel håll!" och förklaringen säger hur den ska vända.
- **Prova själv:** hon ritar över en grå siffra och appen säger om det blev rätt ("Snyggt!") eller om den fortfarande vänder fel.
- Det finns lektioner för 0–9, plus och minus.

## Så läser appen handstil
- Allt sker i telefonen. Ingenting skickas någonstans och det finns ingen AI-tjänst bakom.
- Ett litet neuralt nätverk (82 kB, inbyggt i filen) läser siffrorna 0–9 samt +, − och =. Ett andra, ännu mindre nätverk (39 kB) avgör om en siffra är spegelvänd.
- Det är tränat på 60 000 riktiga handskrivna siffror (MNIST) och på egenproducerade tecken som liknar barnskrift: **spegelvända siffror**, lutande och ojämn stil, och flera sätt att skriva ettor, fyror, femmor, sjuor, nior och så vidare (ett eller flera streck, olika ordning).
- Streck som hör ihop (till exempel en nia med separat svans) grupperas till ett tecken innan de läses.

### Hur bra är det?
Uppmätt i den färdiga sidan, med syntetiska streck som aldrig använts i träningen:

| Test | Rätt |
|---|---|
| Enstaka tecken | 99 % |
| Bara spegelvända siffror | 99 % |
| Hela uträkningar (till exempel `46−18`) | 97 % |
| Riktig handskrift ur MNIST-testdelen | 97 % |
| Spegelvänd eller inte (riktiga siffror, MNIST, bara spegelvända siffror vänds) | 95 % hittas, 2 % falsklarm |

**Viktigt:** tre av de fyra mätningarna gjordes på egenproducerade tecken, så de är mer optimistiska än verkligheten. Ett barns riktiga handstil på en mobilskärm är ännu inte testad. Därför finns rättningsknapparna.

## Begränsningar
- Ett riktigt rejält kluddigt streck kan ändå läsas som en siffra med hög säkerhet. Då varnar appen inte, men Alba ser vad den läste och kan rätta.
- Bara plus och minus, tal upp till 99.
- Skriver man talen i fel ordning (21 i stället för 12) ser appen inte att det är fel.
- Tecken som klistrar ihop (siffror som nuddar varandra) kan läsas som ett tecken. Då visas ett `?` som man rättar.

## Tekniskt
- En enda fil, `index.html`, utan bibliotek. Funkar på GitHub Pages.
- Ljud görs live med Web Audio.
- Antal rätt, valt talområde och ljudval sparas i webbläsaren (`localStorage`).

## Lägg upp på GitHub
Nytt repo `Albas-mattestudio`, ladda upp `index.html` och `README.md`, Settings → Pages → Deploy from a branch → main / root.
