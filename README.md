# CarFactoryApi
Valt designmönster: Factory Pattern
Vi har valt Factory Pattern för att skapa olika typer av bilar (elbil, hybridbil, bensinbil) i vårt bil-API. Factory Pattern är ett välkänt designmönster där en "fabrik" ansvarar för att skapa objekt baserat på viss indata, i stället för att skapa dem direkt med new.

Varför vi valt detta mönster
Vi har flera biltyper som alla implementerar samma interface (ICar).

Factory Pattern gör det lätt att lägga till nya biltyper utan att behöva ändra i huvudlogiken.

Det förbättrar lösningen genom att:

Koden blir renare och mer underhållbar.

Det blir enklare att testa och utöka.

Det skapar lös koppling mellan delar i systemet.

Use Case: Skapa en bil
Namn: Skapa bil från användarinmatning
Aktör: Användare eller Admin
Beskrivning: En användare skickar in en typ av bil (t.ex. "electric") via ett API-anrop. Systemet använder fabriken för att skapa rätt typ av bil-objekt utan att resten av applikationen behöver veta exakt hur objektet skapas.

User Story
"Som administratör vill jag kunna skapa olika typer av bilar genom att bara skicka in biltyp som text, så att systemet automatiskt skapar rätt objekt."
