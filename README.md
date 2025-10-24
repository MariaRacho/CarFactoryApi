# SmartCar Workshop Booking System Api
## Val av mönster: Strategy Pattern (”Strategi”)

Problem i domänen: I ett verkstadsbokningssystem finns flera sätt att avgöra om en tid är bokningsbar:
- enkel regel (är sloten ledig?),
- kapacitet per mekaniker/lyft,
- prioritet för VIP/företagskunder,
- buffertar före/efter vissa servicetyper,
- öppettider/helg-regler, osv.

Om vi hårdkodar all logik i en och samma metod blir koden svår att underhålla och ändra.

**Lösning:** Med Strategy kapslar vi in varianta algoritmer för ”tillgänglighetskontroll” bakom ett gemensamt gränssnitt. Då kan vi byta strategi (eller kombinera dem) utan att röra resten av systemet.

**Vinster:**
- **Öppen–stängd principen (OCP):** Lägg till en ny regel/algoritm genom en ny klass, i stället för att ändra gammal kod.
- **Testbarhet:** Varje strategi testas isolerat.
- **Konfigurerbarhet:** Välj strategi per verkstad, kundtyp eller servicetyp via config/DI.

**Kort Use Case (kopplat till Strategy)**
- **UC-12:** Kontrollera tidslucka för servicebokning
- **Primär aktör:** Kund (via webb/app)
- **Mål:** Avgöra om vald bil, servicetyp, datum och tid kan bokas.
- **Förutsättningar:** Verkstad, resurser (mekaniker/lyftar), öppettider finns definierade.
- **Huvudflöde:**
1. Kunden väljer servicetyp, datum och tid.
2. Systemet hämtar aktiv tillgänglighetsstrategi för aktuell verkstad/servicetyp.
3. Strategin körs med indata (bil, servicetyp, tid, varaktighet, resurser).
4. Systemet visar resultat: ”Tillgänglig” eller ”Inte tillgänglig” med orsak.

- **Eftervillkor:** Om tillgänglig markeras sloten som preliminärt reserverad inför bekräftelse.

**Koppling till designmönster:** Steg 2–3 anropar Strategy-gränssnittet för tillgänglighetskontroll.

**Kort User Story (kopplat till Strategy)**

Som kund vill jag att systemet ska korrekt avgöra om min valda tid går att boka (enligt verkstadens regler) så att jag slipper dubbelbokningar och kan välja en fungerande tid direkt.

**Acceptanskriterier (urval):**
1. Systemet använder rätt strategi beroende på servicetyp och verkstad.
2. Regler för buffert/kapacitet/öppettider respekteras.
3. Svaret ska vara deterministiskt och testbart.

**Klassdiagram:** BookingService → använder (dependency) → IAvailabilityStrategy;
SimpleAvailabilityStrategy, CapacityAwareAvailabilityStrategy → realiserar IAvailabilityStrategy.

**Sekvens/aktivitet (UC-12):** Steget ”Hämta strategi” → ”IsSlotAvailable()” → beslut ”Tillgänglig?” → fortsätt/avbryt.
