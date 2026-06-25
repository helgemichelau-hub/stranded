# Gestrandet — Monetarisierungs-Setup

## Supporter Pack (2,99 €) — kosmetisch, kein Pay-to-Win

Schaltet 3 exklusive Outfits frei: Schattenwandler, Sonnenuntergang, Tiefsee.
Diese geben **keinen Spielvorteil** — rein optisch.

## Code-System

Gültige Unlock-Codes (NICHT im Quelltext, nur ihre Hashes):
- `ISLAND-HERO`
- `SURVIVOR-99`
- `CASTAWAY-PRO`
- `OCEAN-BOUND`

Im Quellcode liegen nur die djb2-Hashes dieser Codes. Ein Angreifer kann
die Codes nicht durch bloßes Lesen des Quelltexts gewinnen.

## Stripe-Einrichtung (TODO vor Launch)

1. **Stripe Payment Link erstellen**: dashboard.stripe.com → Payment Links → 2,99 € Einmalzahlung
2. **Success-URL setzen** auf: `https://DEINE-DOMAIN/?supporter=ISLAND-HERO`
   (das schaltet nach Kauf automatisch frei)
3. **Den Link** in `index.html` ersetzen: Suche `https://buy.stripe.com/test_placeholder`

### Wichtige ehrliche Einschränkung

Bei einer **statischen PWA ohne Backend** ist der Unlock clientseitig.
Technisch versierte Nutzer können `META.supporter = true` in der Browser-
Konsole setzen. Das ist bei reinen Web-Spielen normal und akzeptabel, weil:

- Der Kauf **freiwilliger Support** ist (kosmetisch, kein Vorteil)
- Die Mehrheit der Nutzer keine DevTools öffnet
- Echte Sicherheit nur mit Server möglich wäre (Vercel Function + Stripe Webhook)

**Empfehlung für echten Schutz** (falls gewünscht):
Eine kleine Vercel Serverless Function, die den Stripe Webhook empfängt
und pro Kauf einen einmaligen, signierten Code generiert. ~30 Zeilen Code.
