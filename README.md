# KSEF-MODUL-WHMCS-PL

Darmowy moduł **KSeF dla WHMCS** w języku polskim.  
Integracja z **Krajowym Systemem e-Faktur** obejmująca:

- konfigurację z panelu administratora WHMCS,
- ręczną wysyłkę faktur WHMCS do KSeF,
- automatyczne kolejkowanie faktur ze statusem **Paid**,
- obsługę statusów wysyłki,
- integrację z cronem,
- zapis numeru KSeF,
- zapis XML i UPO.

Projekt przygotowany przez **NETCLOUD24.COM / Łukasz Bodziony**.

---

## Funkcje modułu

Moduł umożliwia:

- konfigurację KSeF bezpośrednio z panelu WHMCS,
- zapis:
  - trybu `test` / `production`,
  - NIP sprzedawcy,
  - tokenu KSeF,
  - pełnych danych adresowych firmy,
  - waluty domyślnej,
  - ustawień crona,
- test połączenia z KSeF,
- ręczne dodanie faktury WHMCS do kolejki wysyłki,
- listę faktur WHMCS ze statusem **Paid**, gotowych do wysłania,
- listę ostatnich wysyłek z informacją o:
  - statusie,
  - numerze KSeF,
  - NIP nabywcy,
  - komunikacie błędu,
- integrację z hookiem `InvoicePaid`,
- przetwarzanie kolejki przez cron,
- blokadę duplikatów wysyłki.

---

## Wymagania

Przed instalacją upewnij się, że serwer spełnia wymagania:

- WHMCS 8/9
- PHP 8.1 lub nowsze
- aktywny dostęp do KSeF
- poprawny token KSeF
- moduł działa z biblioteką:
  - `n1ebieski/ksef-php-client`
  - `guzzlehttp/guzzle`

---

## Struktura modułu

Po instalacji katalog modułu powinien wyglądać tak:

BASH
modules/addons/ksefmodule/
├── ksefmodule.php
├── vendor/
├── lib/
│   ├── KsefConfig.php
│   ├── KsefService.php
│   └── KsefWhmcsMapper.php
└── cron/
    └── ksef_status.php
