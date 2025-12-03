CHANGELOG – SEUP (Sustav Elektroničkog Uredskog Poslovanja)
1.0.0 – Initial Release

Prva funkcionalna verzija SEUP modula.

Osnovna struktura modula generirana putem Dolibarr ModuleBuilder-a.

Dodani početni modeli za Predmete, Akte i Priloge.

Postavljeni temeljni SQL predlošci i osnovna navigacija.

Hardkodirani testni sadržaji za interne potrebe razvoja.

2.0.0 – Core Stabilizacija

Potpuna reorganizacija direktorija (class/, pages/, lib/, sql/, langs/ itd.).

Implementirani modeli:

Predmet

Akt_helper

Prilog_helper

Suradnici_helper

Sortiranje_helper

Dodan osnovni workflow za kreiranje, prikaz i uređivanje predmeta.

Dodani backend alati za sortiranje, pretragu i filtriranje.

Počeci Nextcloud integracije – priprema API klase.

Prvi draft OnlyOffice integracije (bez potpune implementacije).

Dodan sustav tagova i osnovne administracijske stranice.

2.5.0 – DMS Ekspanzija

Uvedena napredna podrška za rad s prilozima i dokumentima.

Dovršena Nextcloud API integracija: kreiranje foldera, upload, strukture.

Nadograđen interface za rad s aktima, povezivanje akata na predmete.

Uvedeni helperi za generiranje dokumenata (PDF, DOCX).

Dodane interne klase za digitalni potpis i provjeru potpisa.

Dodan "Plan klasifikacijskih oznaka".

Prvi stabilni importer podataka.

3.0.0 – „Production Ready“ Refactor

Veliko čišćenje i refaktor kodne baze.

Uklanjanje starih placeholder datoteka i nepotrebnih skeleton fajlova.

Usklađivanje strukture s Dolibarr 22 standardima.

Optimiziran rad s bazom: novi SQL predlošci, bolja organizacija tablica.

Uređivanje svih stranica (pages/) – UX poboljšanja, layout stabilizacija.

Ujednačavanje PHP klasa i naming conventiona.

Uvedene dodatne funkcije za korisničke uloge i interne workflowe.

Dodano više sigurnosnih provjera i sanitizacije inputa.

Značajno brže učitavanje većih listi predmeta i akata.

3.0.1 – Licensing & Packaging Cleanup

Uklonjene sve GPL datoteke i naslijeđeni ModuleBuilder headeri.

Dodan novi proprietary LICENSE.md (8Core).

Kreiran novi info.xml kompatibilan s Dolibarr 22.

Usklađeni brojevi verzija i modul identificatori.

Čišćenje vendor-a: uklanjanje duplih JWT implementacija.

Priprema za stabilno izdanje i distribuciju prema klijentima.

Dokumentacija ažurirana: README, struktura, changelog.

---

## 3.1.0 – Zaprimanja i Otprema Fundamentals

**Datum:** Q1 2024

### Nove značajke
- ✉️ Dodan modul za zaprimanje pošte i dokumentacije
- 📤 Implementirana baza otpreme (`llx_a_otprema` tablica)
- 🔄 Osnovni workflow za registraciju primljene i poslane pošte
- 🔗 Povezivanje zaprimanja/otprema s predmetima

### Tehničke izmjene
- SQL migracije za nove tablice
- Backend struktura za evidentiranje ulazne/izlazne pošte

---

## 3.2.0 – Dizajn Modernizacija

**Datum:** Q1 2024

### UI/UX
- 🎨 Uveden moderan CSS dizajn sustav (`seup-modern.css`)
- 📱 Redizajnirane glavne stranice: predmeti, zaprimanja, otprema
- 📐 Poboljšan responsive layout i mobile experience
- 🧭 Dodan novi header i navigacijski sustav
- ✨ Vizualne optimizacije formi i tablica

---

## 3.3.0 – Zaprimanja Extended

**Datum:** Q2 2024

### Proširenja
- 🔍 Napredne funkcionalnosti za zaprimanja
- 🔎 Pretraga, filtriranje i sortiranje zaprimljenih dokumenata
- 🤖 Automatsko povezivanje zaprimanja s postojećim predmetima
- 📊 Dodani statusni indikatori i workflow kontrole
- 📥 Export funkcionalnosti za zaprimanja

---

## 3.4.0 – Otprema Advanced

**Datum:** Q2 2024

### Proširenja
- 📮 Proširene mogućnosti otpreme dokumenata
- 👥 Dodana integracija s adresarom (suradnici)
- 📍 Praćenje statusa otpreme i potvrde dostave
- 📦 Grupna otprema dokumenata
- 🏷️ Generiranje poštanskih oznaka i potvrda

---

## 3.5.0 – Code Cleanup Phase 1

**Datum:** Q2 2024

### Optimizacije
- ⚡ Refaktorirani helper classes za bolje performance
- 🧹 Uklonjen nekorišteni legacy kod
- 🗄️ Optimizacija SQL upita
- 📝 Standardizacija PHP dokumentacije i komentara
- 🛡️ Poboljšana error handling logika

---

## 3.6.0 – UI/UX Improvements

**Datum:** Q3 2024

### Poboljšanja korisničkog iskustva
- 🎯 Redesign predmet.php stranice
- 🪟 Novi modalni prozori za brže akcije
- 💡 Dodani tooltipovi i inline help
- 🔤 Poboljšan autocomplete za suradnike i oznake
- ⚡ Optimizacija ajax poziva za brže učitavanje

---

## 3.7.0 – Security & Validation

**Datum:** Q3 2024

### Sigurnost
- 🔐 Dodane dodatne sigurnosne provjere
- ✅ Input sanitizacija i validacija na svim formama
- 🛡️ CSRF zaštita na kritičnim akcijama
- 💉 SQL injection prevencija - prepared statements
- 🔑 Session management poboljšanja

---

## 4.0.0 – Major Architecture Update

**Datum:** Q4 2024

### Arhitekturne promjene
- 🏗️ Potpuna reorganizacija class strukture
- 🔧 Uvedeni novi pattern: DataLoader, ActionHandler, ViewHelper
- 📦 Refaktor `predmet.class.php` za modularnost
- 🎯 Bolja separacija logike i prikaza
- 🚀 Performance optimizacije na velikim bazama podataka

---

## 4.1.0 – OMAT Generator

**Datum:** Q4 2024

### Nova funkcionalnost
- 🔢 Implementiran sustav za generiranje OMAT brojeva
- ⚙️ Automatska alokacija brojeva prema pravilima
- 🎛️ Konfigurabilan format brojeva ustanove
- 🔗 Integracija s predmetima i aktima
- ✔️ Provjera duplikata i validacija

---

## 4.2.0 – Document Preview System

**Datum:** Q1 2025

### Nova funkcionalnost
- 👁️ Dodan sustav za pregled dokumenata
- 📄 PDF viewer integracija
- 📝 DOCX pretvorba u PDF za preview
- 🖼️ Thumbnails za brži pregled
- 🖥️ Full-screen mode za dokumente

---

## 4.2.5 – Omot & Stabilizacija

**Datum:** Q1 2025

### Finalizacija
- 📋 Implementiran sustav omota za predmete
- 🔍 Stranica za predpregled omota prije ispisa
- 🧹 Finalna čišćenja koda i optimizacije
- 🔧 Popravke funkcionalnosti u zaprimanjima i otpremama
- 🐛 Bugfixevi i stability improvements
- 🚀 Priprema za production deployment

---

## 4.2.6 – Database Auto-initialization

**Datum:** 27.11.2025

### Database Management
- 🔄 Sinkronizirana kreacija `llx_a_otprema` tablice između SQL filea i PHP metode
- 🔗 Dodani FOREIGN KEY constrainti u `createSeupDatabaseTables()` za konzistentnost
- ⚡ Tablice se automatski kreiraju pri prvom učitavanju stranice
- ✅ Ne zahtijeva ponovno aktiviranje/deaktiviranje modula
- 🛡️ Puni relacijski integritet - automatska CASCADE i RESTRICT pravila
- 🗄️ Optimizirano za clean instalacije - sve radi "out of the box"

### Tehničke izmjene
- Dodan `CONSTRAINT fk_otprema_predmet` s ON DELETE CASCADE
- Dodan `CONSTRAINT fk_otprema_ecm` s ON DELETE CASCADE
- Dodan `CONSTRAINT fk_otprema_potvrda` s ON DELETE SET NULL
- Dodan `CONSTRAINT fk_otprema_user` s ON DELETE RESTRICT
- Ujednačena struktura između `llx_a_otprema.sql` i `predmet_helper.class.php`

---

## 5.0.0 – Notification System (CURRENT)

**Datum:** 01.12.2025

### Nova funkcionalnost - Sustav obavjesti
- 🔔 **Notification Bell** - Dinamičko zvono u headeru s real-time brojem obavjesti
- 💬 **Admin modul za obavjesti** - Kreiranje, slanje i upravljanje obavjestima (`/admin/obavjesti.php`)
- 📊 **Sustav kategorija** - Info, Upozorenje, Nadogradnja, Hitno, Važno
- 🎯 **Ciljanje korisnika** - Slanje obavjesti svim korisnicima ili pojedinačnim userima
- 🔗 **Vanjski linkovi** - Mogućnost dodavanja vanjskih resursa u obavijesti
- ✅ **Status tracking** - Praćenje pročitanih/nepročitanih obavjesti po korisniku

### UI/UX Komponente
- 🎨 **Moderni modal** - Elegantni popup s obavjestima, responsive dizajn
- 🖱️ **Interaktivne akcije** - "Označi pročitano", "Obriši", "Označi sve pročitanim"
- 🎭 **Vizualni feedback** - Promjena boje i stila kod oznake pročitano
- 🔕 **Pametno skrivanje** - Zvono se automatski skriva kad nema obavjesti
- 📱 **Responsive** - Optimiziran prikaz za desktop i mobile uređaje
- ⚡ **Auto-refresh** - Automatsko učitavanje novih obavjesti svakih 30 sekundi

### Database strukture
- 📋 **llx_seup_obavjesti** - Glavna tablica za pohranu obavjesti
  - `id`, `naslov`, `sadrzaj`, `subjekt`, `vanjski_link`
  - `target_user_ids` (JSON array), `kreirao`, `datum_kreiranja`

- 📋 **llx_seup_obavjesti_status** - Status pročitanosti po korisniku
  - `id`, `obavjest_id`, `user_id`, `procitano`, `datum_procitano`
  - Prati koji korisnik je pročitao koju obavijest

### Backend komponente
- 🔧 **obavjesti_helper.class.php** - Core logika za upravljanje obavjestima
- 🔌 **obavjesti_ajax.php** - AJAX endpoint za sve operacije
  - `get_notifications` - Dohvaćanje obavjesti za trenutnog korisnika
  - `mark_read` - Označavanje pojedinačne obavijesti kao pročitane
  - `mark_all_read` - Označavanje svih obavjesti kao pročitanih
  - `delete` - Brisanje pojedinačne obavijesti
  - `delete_all` - Brisanje svih obavjesti

### Frontend komponente
- 🎨 **notification-bell.css** - Stilovi za zvono, modal i obavijesti
- ⚡ **notification-bell.js** - JavaScript logika, event handling, AJAX
- 🧩 **Seup_modern.css integracija** - Ujednačen dizajn sustav

### Sigurnosne značajke
- 🔐 **User authentication** - Sve akcije verificiraju trenutnog korisnika
- 🛡️ **SQL injection zaštita** - Prepared statements u svim upitima
- 🧹 **XSS zaštita** - HTML escaping u prikazu sadržaja
- ✅ **Permission checks** - Admin stranica zaštićena korisničkim pravima

### Tehničke optimizacije
- ⚡ **Optimizirani SQL upiti** - JOIN operacije za brže dohvaćanje
- 💾 **Efficient data structure** - JSON format za target_user_ids
- 🔄 **Cascade brisanje** - Automatsko čišćenje statusa pri brisanju obavijesti
- 📊 **Indexi na ključnim poljima** - Brže pretraživanje i filtriranje

---

## 5.0.1 – Assignment System (Dodjela Predmeta)

**Datum:** 02.12.2025

### Nova funkcionalnost - Sustav dodjele predmeta
- 👥 **Assignment System** - Mogućnost dodjeljivanja predmeta određenim korisnicima
- 🔒 **Ograničen pristup** - Korisnici vide samo predmete dodijeljene njima ili svima
- 👨‍💼 **Admin override** - Administratori uvijek vide sve predmete bez obzira na dodjelu
- 🎯 **Ciljana dodjela** - Mogućnost odabira više korisnika za jedan predmet
- ✨ **Jednostavna selekcija** - Checkboxes za brz odabir korisnika

### UI/UX komponente
- 🎨 **Modal za dodjelu** - Elegantan popup s listom korisnika
- 🔘 **Checkbox selekcija** - Intuitivno odabiranje korisnika
- 💡 **"Svi korisnici" opcija** - Brzo dodjeljivanje svima jednim klikom
- 📝 **Prikaz dodijeljenih korisnika** - Lista s imenima korisnika u tablici predmeta
- 🔍 **Badge indikatori** - Vizualna oznaka broja dodijeljenih korisnika
- ⚡ **Live update** - Trenutna promjena bez osvježavanja stranice

### Database strukture
- 🗃️ **Dodani stupci u llx_a_predmeti**:
  - `assigned_user_ids` (TEXT) - JSON array s ID-jevima korisnika
  - `assigned_to_all` (TINYINT) - Flag za dodjelu svim korisnicima
  - `assigned_by` (INT) - Korisnik koji je dodjelio predmet
  - `assignment_date` (DATETIME) - Datum dodjele

### Backend komponente
- 🔧 **assignment_helper.class.php** - Core logika za upravljanje dodjelama
  - `assignPredmetToUsers()` - Dodjeljivanje predmeta korisnicima
  - `getAssignedUsers()` - Dohvaćanje dodijeljenih korisnika
  - `isUserAssignedToPredmet()` - Provjera pristupa korisnika
  - `unassignPredmet()` - Uklanjanje dodjela

- 📄 **predmeti.php** - Ažuriran za filtriranje predmeta po dodjelama
  - WHERE uvjet za ograničen pristup
  - Admin bypass logika
  - Prikaz dodijeljenih korisnika u tablici

- 🔌 **request_handler.class.php** - Proširena AJAX logika
  - `assign_predmet` action - Spremanje dodjela
  - Integracija s assignment_helper classom

### Frontend komponente
- 🎨 **predmeti.css** - Stilovi za modal, checkboxove i badge
- ⚡ **predmeti.js** - JavaScript logika
  - `openAssignModal()` - Otvaranje modala za dodjelu
  - `toggleAllUsers()` - Kontrola "Svi korisnici" opcije
  - `saveAssignment()` - AJAX spremanje dodjela
  - Event handling za checkboxove

### Sigurnosne značajke
- 🔐 **Permission checks** - Samo vlasnik ili admin može dodjeljivati
- 🛡️ **Data validation** - Validacija korisničkih ID-ova
- 🧹 **XSS zaštita** - Sanitizacija svih inputa
- ✅ **SQL injection zaštita** - Prepared statements

### Dokumentacija
- 📚 **ASSIGNMENT_IMPLEMENTATION.md** - Detaljna tehnička dokumentacija
  - Database design
  - Business rules
  - Security considerations
  - API referenca

---

## 5.0.2 – Access Control & UI Improvements

**Datum:** 03.12.2025

### Access Control (Kontrola pristupa)
- 🔒 **Disabled action cards** - Ne-admin korisnici ne mogu pristupiti osjetljivim funkcijama
- 🎯 **Role-based UI** - Vizualno razlikovanje dostupnih i nedostupnih opcija
- 👁️ **Transparency & visibility** - Korisnici vide što postoji, ali znaju da nemaju pristup

### Ograničen pristup za ne-admin korisnike
- 🚫 **Novi Predmet** - Disabled za obične korisnike
- 🚫 **Plan Klasifikacijskih Oznaka** - Disabled za obične korisnike
- 🚫 **Postavke** - Disabled za obične korisnike
- ✅ **Predmeti** - Uvijek dostupno svim korisnicima

### UI/UX komponente
- 🎨 **Disabled card styling** - Siva kartica, opacity 0.6
- 🏷️ **Admin badge** - "Samo za administratore" oznaka
- 🖱️ **Cursor feedback** - `cursor: not-allowed` za disabled kartice
- 🎭 **Icon styling** - Sive ikone umjesto plavih za disabled
- 🚫 **Pointer events** - `pointer-events: none` za potpuno onemogućavanje klika

### CSS implementacija
- 📐 **`.seup-action-card-disabled`** - Novi CSS class za disabled kartice
  - Smanjena vidljivost (opacity: 0.6)
  - Onemogućeni hover efekti
  - Siva ikona umjesto gradient plave
  - Pozicionirani badge u gornjem desnom kutu

- 🎨 **Badge styling** - Žuta pozadina (warning paleta)
  - `var(--warning-100)` background
  - `var(--warning-800)` text color
  - `var(--warning-300)` border
  - Zaobljeni kutovi i padding

### Backend logika
- 🔧 **seupindex.php** - Ažuriran za dinamičko dodavanje disabled klase
  - `$is_admin = ($user->admin == 1)` - Admin provjera
  - Conditional class assignment
  - `href="#"` za disabled kartice (bez navigacije)
  - Predmeti kartica uvijek aktivna

### User Experience princip
- 💡 **Opcija 2 implementirana** - Disabled s vizualnim indikatorom
- ✨ **Prednost over Opcija 3** - Bez iritantnih pop-upa
- 👍 **User-friendly pristup** - Jasno komunicirano, bez frustracije
- 📱 **Consistent experience** - Ujednačeno iskustvo na svim uređajima

### Prednosti implementacije
- ⚡ **Instant feedback** - Korisnik odmah zna što može/ne može
- 🎯 **Clear communication** - Nema dvojbi o razlozima nedostupnosti
- 🚀 **Performance** - Bez dodatnih AJAX poziva ili modalnih prozora
- ♿ **Accessibility** - Jasno označeno za screen readere

---
