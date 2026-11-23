# BEAST MODE

**Privatni, offline-first sistem za praćenje treninga** — jednostranična web aplikacija (single-page web app) na srpskom jeziku. Sve se čuva lokalno u pregledaču, bez slanja podataka na internet.

## Pregled

BEAST MODE je lagana aplikacija za lično praćenje treninga, opreme i napretka. Namenjena je korisnicima koji treniraju sa improvizovanom opremom i žele jednostavan alat koji radi na telefonu, bez naloga, bez cloud-a i bez dodatnih zavisnosti.

Ceo program je u jednom fajlu — [`index.html`](index.html) — i može se otvoriti direktno u pregledaču ili servirati sa bilo kog statičkog hosting-a.

## Funkcionalnosti

### Početna
- Pregled broja završenih treninga i komada opreme.
- Brzi prečac za pokretanje treninga.

### Trening
- Dodavanje vežbi sa nazivom, brojem serija (1–20) i ponavljanja (1–200).
- Označavanje pojedinačnih serija tokom treninga.
- Ugrađeni tajmer (pokreni/pauziraj) sa prikazom u formatu `MM:SS`.
- Čuvanje završenog treninga u istoriju jednim klikom.

### Oprema
- Katalog lične opreme sa nazivom, opisom i fotografijom.
- Fotografije se automatski smanjuju (max 900 px, JPEG kvalitet 0.65) pre čuvanja — čime se štedi lokalni prostor.

### Napredak
- Unos i istorija telesne težine (kg).
- Kalendar završenih treninga sa pregledom vežbi po danu.

### Više
- Mesto rezervisano za budućeg AI trenera (trenutno placeholder — ništa se ne šalje online).
- Galerija fotografija napretka.
- **Backup:** izvoz svih podataka u JSON datoteku i uvoz iz postojećeg backup-a (sa validacijom verzije).
- Informacije o privatnosti i lokalnom čuvanju podataka.

## Tehnologije

| Oblast | Detalj |
|---|---|
| Jezik | HTML5, CSS3, vanilla JavaScript (ES2020+) |
| Build alati | Nema — single-file aplikacija |
| Dependencies | Nijedna eksterna biblioteka |
| Čuvanje | `localStorage` pod ključem `beast-mode-v1` |
| Fotografije | `<canvas>` resize + `toDataURL('image/jpeg', 0.65)` |
| ID zapisa | `crypto.randomUUID()` |
| UI | Mobile-first, tamna tema sa crvenim akcentom, bottom-tab navigacija |
| PWA metadata | `theme-color`, `apple-mobile-web-app-*`, `viewport-fit=cover` |
| Jezik interfejsa | Srpski (`lang="sr"`) |

## Struktura podataka

Svi korisnički podaci čuvaju se u jednom `localStorage` ključu (`beast-mode-v1`) kao JSON objekat sa poljima:

- `equipment` — lista opreme
- `exercises` — aktivne vežbe trenutnog treninga
- `workouts` — istorija završenih treninga
- `weights` — merenja telesne težine
- `photos` — fotografije napretka

Backup fajl ima format:

```json
{
  "version": 1,
  "exportedAt": "YYYY-MM-DDTHH:mm:ss.sssZ",
  "data": { ... }
}
```

## Pokretanje

1. Preuzmi ili kloniraj repozitorijum.
2. Otvori [`index.html`](index.html) u pregledaču (Chrome, Safari, Firefox).
3. Dodaj aplikaciju na početni ekran telefona za iskustvo nalik nativnoj aplikaciji.

Nije potreban server, Node.js, niti bilo kakav build korak.

## Privatnost

- Svi podaci ostaju u pregledaču uređaja.
- Ništa se ne šalje na internet.
- Brisanje podataka sajta ili keša pregledača briše i korisničke podatke — zato se preporučuje redovan backup preko dugmeta **Izvezi backup**.

## Status projekta

Rana faza — jezgro funkcionalnosti (trening, oprema, napredak, backup) je implementirano. Sekcija AI trenera je pripremljena kao placeholder i biće povezana u narednoj fazi.
