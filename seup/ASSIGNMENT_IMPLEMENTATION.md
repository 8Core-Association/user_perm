# 🎯 Assignment System Implementation Guide

## 📋 **ŠTO JE IMPLEMENTIRANO**

Implementiran je **Assignment-Based Permission System** koji omogućava:
- ✅ **Admini** vide SVE predmete
- ✅ **Regular useri** vide SAMO dodijeljene predmete
- ✅ **1 korisnik po predmetu** (1:1 odnos)
- ✅ Admin može dodijeliti/ukloniti dodjelu
- ✅ UI za dodjeljivanje s modalnom

---

## 📁 **KREIRANE DATOTEKE**

### **1. SQL Migracija**
```
seup/sql/add_assignment_columns.sql
```

**Što radi:**
- Dodaje 3 nova stupca u `llx_a_predmet`:
  - `fk_user_assigned` - ID dodijeljenog korisnika
  - `date_assigned` - Datum dodjele
  - `assigned_by` - ID admina koji je dodjelio
- Dodaje indexe i foreign key constrainte

**Kako pokrenuti:**
```bash
# Opcija 1: Kroz Dolibarr SQL konzolu
# Admin panel → Tools → Execute SQL

# Opcija 2: Direktno MySQL
mysql -u username -p database_name < seup/sql/add_assignment_columns.sql
```

---

### **2. Assignment Helper Klasa**
```
seup/class/assignment_helper.class.php
```

**Metode:**

| Metoda | Opis |
|--------|------|
| `ensureAssignmentColumns($db)` | Osigurava da stupci postoje |
| `assignUser($db, $predmet_id, $user_id, $assigned_by)` | Dodijeli predmet korisniku |
| `unassignUser($db, $predmet_id)` | Ukloni dodjelu |
| `getAssignedUser($db, $predmet_id)` | Dohvati dodijeljenog korisnika |
| `getActiveUsers($db, $conf)` | Dohvati sve aktivne korisnike |
| `userHasAccess($db, $user, $predmet_id)` | Provjeri ima li korisnik pristup |
| `getAccessiblePredmetiIds($db, $user)` | Dohvati ID-eve dostupnih predmeta |
| `getAssignmentStats($db)` | Statistike dodjela |
| `getPredmetiByUser($db, $user_id)` | Dohvati predmete korisnika |

---

### **3. Modificirani `predmeti.php`**

**Dodano:**
1. **Permission filter** u SQL query
2. **Nova kolona** "Dodijeljeno" u tablici
3. **Novi action button** za dodjeljivanje (samo za admina)
4. **3 nova AJAX handlera:**
   - `assign_user` - Dodijeli korisnika
   - `unassign_user` - Ukloni dodjelu
   - `get_assigned_user` - Dohvati trenutnu dodjelu
5. **Assignment modal** s user selectom
6. **JavaScript logika** za modal i AJAX pozive
7. **CSS stilovi** za nove elemente

---

## 🔐 **KAKO PERMISSION SISTEM RADI**

### **Za ADMINA (`$user->admin == 1`):**
```php
// SQL query BEZ filtera
SELECT * FROM llx_a_predmet
WHERE ID_predmeta NOT IN (SELECT ID_predmeta FROM llx_a_arhiva WHERE status_arhive = 'active')
ORDER BY ...
```
**Rezultat:** Vidi SVE predmete

### **Za REGULAR USERA (`$user->admin == 0`):**
```php
// SQL query SA filterom
SELECT * FROM llx_a_predmet
WHERE ID_predmeta NOT IN (...)
AND fk_user_assigned = 5  -- ID trenutnog korisnika
ORDER BY ...
```
**Rezultat:** Vidi SAMO predmete dodijeljene njemu

---

## 🎨 **UI/UX FLOW**

### **1. Tablica Predmeta**

Dodana nova kolona **"Dodijeljeno"** nakon kolone "Otvoreno":

| ID | Klasa | Naziv | ... | Otvoreno | **Dodijeljeno** | Akcije |
|----|-------|-------|-----|----------|----------------|--------|
| 1  | 010-05/25... | Predmet 1 | ... | 03.12.2025 | **John D.** | 👁️ ✏️ 🗄️ **👤** |
| 2  | 011-06/25... | Predmet 2 | ... | 02.12.2025 | *Nije dodijeljeno* | 👁️ ✏️ 🗄️ **👤** |

- **Zeleni badge** → Prikazuje dodijeljenog korisnika
- **"Nije dodijeljeno"** → Grey text za nedodijeljene

### **2. Action Button**

**Novi button** (samo za admina):
```html
<button class="seup-action-btn seup-btn-assign">
    <i class="fas fa-user-plus"></i>
</button>
```

- **Zeleni button** s iconom
- Prikazuje se SAMO ako je `$user->admin`

### **3. Assignment Modal**

**Otvara se kad admin klikne na 👤 button:**

```
┌─────────────────────────────────────┐
│ 👤 Dodijeli Predmet Korisniku       │
├─────────────────────────────────────┤
│ ℹ️ Predmet: 010-05/25-12/4          │
│    Naziv predmeta...                │
│                                     │
│ 👤 Odaberite korisnika *            │
│ ┌────────────────────────────────┐  │
│ │ [Dropdown sa svim korisnicima] │  │
│ └────────────────────────────────┘  │
│                                     │
│ ✓ Trenutno dodijeljeno              │
│ ┌────────────────────────────────┐  │
│ │ [JD] John Doe                  │  │
│ │      Dodijeljeno: 01.12.2025   │  │
│ │                    [✕ Ukloni]  │  │
│ └────────────────────────────────┘  │
│                                     │
│          [Odustani]  [👤 Dodijeli] │
└─────────────────────────────────────┘
```

**Features:**
- Dropdown sa svim aktivnim korisnicima iz `llx_user`
- Prikazuje trenutno dodijeljenog (ako postoji)
- Button za uklanjanje dodjele
- Validacija prije spremanja

---

## 🔄 **WORKFLOW DIJAGRAM**

```
┌──────────┐
│  ADMIN   │ Login
└─────┬────┘
      │
      v
┌────────────────────────────────┐
│  predmeti.php                  │
│  ✅ Vidi SVE predmete          │
└────────────┬───────────────────┘
             │
             │ Klikne 👤 button
             v
┌────────────────────────────────┐
│  Assignment Modal              │
│  1. Odabere korisnika          │
│  2. Klikne "Dodijeli"          │
└────────────┬───────────────────┘
             │
             │ AJAX: assign_user
             v
┌────────────────────────────────┐
│  Assignment_Helper             │
│  assignUser($db, ...)          │
│  UPDATE llx_a_predmet          │
│  SET fk_user_assigned = X      │
└────────────┬───────────────────┘
             │
             │ Reload page
             v
┌────────────────────────────────┐
│  Regular User Login            │
│  ✅ Vidi SAMO svoje predmete   │
└────────────────────────────────┘
```

---

## 📊 **BAZA PODATAKA**

### **Schema: `llx_a_predmet`**

```sql
CREATE TABLE llx_a_predmet (
    ID_predmeta INT AUTO_INCREMENT PRIMARY KEY,
    -- ... postojeća polja ...

    -- NOVI STUPCI (dodani migracijom)
    fk_user_assigned INT DEFAULT NULL COMMENT 'Dodijeljeni korisnik',
    date_assigned DATETIME DEFAULT NULL COMMENT 'Datum dodjele',
    assigned_by INT DEFAULT NULL COMMENT 'Admin koji je dodjelio',

    -- Indeksi
    KEY idx_assigned (fk_user_assigned),
    KEY idx_assigned_by (assigned_by),

    -- Foreign keys
    CONSTRAINT fk_predmet_assigned_user
        FOREIGN KEY (fk_user_assigned)
        REFERENCES llx_user(rowid)
        ON DELETE SET NULL
        ON UPDATE CASCADE,

    CONSTRAINT fk_predmet_assigned_by
        FOREIGN KEY (assigned_by)
        REFERENCES llx_user(rowid)
        ON DELETE SET NULL
        ON UPDATE CASCADE
);
```

### **Primjer podataka:**

| ID_predmeta | naziv_predmeta | fk_user_assigned | date_assigned | assigned_by |
|-------------|----------------|------------------|---------------|-------------|
| 1 | Predmet 1 | 5 | 2025-12-03 10:30:00 | 1 |
| 2 | Predmet 2 | NULL | NULL | NULL |
| 3 | Predmet 3 | 7 | 2025-12-02 15:45:00 | 1 |

**Objašnjenje:**
- **Predmet 1** → Dodijeljen korisniku ID=5, dodijelio admin ID=1
- **Predmet 2** → Nije dodijeljen nikome
- **Predmet 3** → Dodijeljen korisniku ID=7

---

## 🧪 **TESTIRANJE**

### **Test Scenariji:**

#### **Scenario 1: Admin pristup**
1. Login kao admin
2. Otvori `predmeti.php`
3. **Očekivano:** Vidiš SVE predmete (i dodijeljene i nedodijeljene)

#### **Scenario 2: Regular user bez dodjela**
1. Login kao regular user (npr. ID=5)
2. Otvori `predmeti.php`
3. **Očekivano:** Vidiš PRAZAN popis (nema dodijeljenih predmeta)

#### **Scenario 3: Admin dodijeli predmet**
1. Login kao admin
2. Otvori `predmeti.php`
3. Klikni 👤 button na nekom predmetu
4. Odaberi korisnika (npr. "John Doe")
5. Klikni "Dodijeli"
6. **Očekivano:** Toast "Korisnik uspješno dodijeljen!", reload stranice, vidiš zeleni badge

#### **Scenario 4: Regular user vidi svoj predmet**
1. Admin dodijeli predmet ID=1 korisniku ID=5
2. Logout admin, login kao user ID=5
3. Otvori `predmeti.php`
4. **Očekivano:** Vidiš SAMO predmet ID=1

#### **Scenario 5: Admin ukloni dodjelu**
1. Login kao admin
2. Otvori `predmeti.php`
3. Klikni 👤 button na dodijeljenom predmetu
4. Klikni "✕ Ukloni" button
5. **Očekivano:** Toast "Dodjela uklonjena!", reload, badge nestaje

---

## 🐛 **TROUBLESHOOTING**

### **Problem: Regular user vidi SVE predmete**

**Uzrok:** SQL migracija nije pokrenuta ili stupci ne postoje

**Rješenje:**
```bash
# 1. Provjeri postoje li stupci
SHOW COLUMNS FROM llx_a_predmet LIKE 'fk_user_assigned';

# 2. Ako ne postoje, pokreni migraciju
mysql -u root -p dolibarr_db < seup/sql/add_assignment_columns.sql
```

---

### **Problem: Admin ne vidi 👤 button**

**Uzrok:** PHP condition `if ($user->admin)` ne radi

**Provjera:**
```php
// Dodaj na vrh predmeti.php (privremeno)
var_dump($user->admin); // Trebalo bi biti 1 ili 0
exit;
```

**Rješenje:**
- Provjeri je li korisnik stvarno admin u `llx_user` tablici
- `admin` column mora biti `1`

---

### **Problem: AJAX error pri dodjeljivanju**

**Uzrok:** Foreign key constraint ili permission issue

**Debug:**
```javascript
// Otvori Browser Console (F12) i gledaj network tab
// Request payload:
{
  action: "assign_user",
  predmet_id: 1,
  user_id: 5
}

// Response (error):
{
  success: false,
  error: "Samo admin može dodijeljivati predmete"
}
```

**Provjera:**
- Jesi li admin?
- Postoje li korisnik ID=5 u `llx_user`?
- Postoji li predmet ID=1?

---

### **Problem: Dropdown prazan (nema korisnika)**

**Uzrok:** `llx_user` tablica nema aktivnih korisnika

**Provjera:**
```sql
SELECT rowid, firstname, lastname, statut
FROM llx_user
WHERE statut = 1;
```

**Rješenje:**
- Kreiraj korisnike kroz Dolibarr admin panel
- Ili aktiviraj postojeće (`statut = 1`)

---

## 📈 **BUDUĆA PROŠIRENJA**

Ako želiš dodati:

### **1. Multiple users po predmetu**

**Trenutno:** 1 predmet → 1 korisnik
**Buduće:** 1 predmet → više korisnika

**Implementacija:**
- Kreirati novu tablicu `llx_a_predmet_korisnici` (many-to-many)
- Dodati role system (assigned, collaborator, observer)
- Modificirati `Assignment_Helper` za multiple assignments

---

### **2. Notifikacije**

**Dodati:**
- Email notifikaciju kad se dodijeli predmet
- In-app obavijest (Dolibarr notifications)

**Implementacija:**
```php
// U Assignment_Helper::assignUser()
require_once DOL_DOCUMENT_ROOT . '/core/class/notify.class.php';

$notif = new Notify($db);
$notif->send(
    $user_id,
    'Dodijeljen vam je novi predmet: ' . $predmet->naziv,
    'seup_assignment'
);
```

---

### **3. Dashboard widget**

**Prikaži:**
- "Moji predmeti" widget na home page
- Broj dodijeljenih predmeta
- Brzi pristup

---

## 📝 **FINALNA CHECKLIST**

Prije puštanja u produkciju:

- [ ] Pokrenuta SQL migracija
- [ ] Testirano: Admin vidi sve
- [ ] Testirano: User vidi samo svoje
- [ ] Testirano: Dodjeljivanje radi
- [ ] Testirano: Uklanjanje dodjele radi
- [ ] Testirano: Modal validacije
- [ ] Provjereno: Foreign keys postoje
- [ ] Provjereno: Nema SQL errora u logovima
- [ ] Backup baze prije migracije!

---

## 🎉 **ZAVRŠENO!**

Assignment system je potpuno implementiran i spreman za upotrebu.

**Kreirano:**
- 1 SQL migracija
- 1 PHP Helper klasa
- Modificiran `predmeti.php` (400+ linija koda)
- 9 novih funkcija
- 3 AJAX endpointa
- Kompletna UI/UX s modalom
- CSS styling

**Total lines added:** ~600 linija

---

## 💬 **Podrška**

Za pitanja ili probleme:
- Email: info@8core.hr
- Tel: +385 099 851 0717

---

**Verzija:** 1.0.0
**Datum:** 2025-12-03
**Autor:** 8Core Association
