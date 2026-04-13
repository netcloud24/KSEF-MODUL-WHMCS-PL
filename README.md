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


Szybka instalacja (kopiuj i wklej)

Instalacja modułu zajmuje około 2–3 minut. Wystarczy wykonać poniższe kroki na serwerze, gdzie działa WHMCS.

Na początku podmień wartości:

USER=twoj_user
WHMCS_PATH=/home/USER/domains/twojadomena.pl/public_html

Krok 1 — przejdź do katalogu WHMCS:

cd /home/USER/domains/twojadomena.pl/public_html

Krok 2 — pobierz moduł z GitHub:

wget https://github.com/netcloud24/KSEF-MODUL-WHMCS-PL/raw/main/ksefmodule-full-deploy.tar.gz

Krok 3 — rozpakuj paczkę:

tar -xzvf ksefmodule-full-deploy.tar.gz --strip-components=1

Po tym kroku pliki automatycznie trafią do odpowiednich katalogów:

modules/addons/ksefmodule
includes/hooks/ksefmodule.php

Krok 4 — ustaw uprawnienia:

chown -R USER:USER modules/addons/ksefmodule
chmod -R 755 modules/addons/ksefmodule

chown USER:USER includes/hooks/ksefmodule.php
chmod 644 includes/hooks/ksefmodule.php

Krok 5 — wyczyść cache WHMCS:

rm -rf templates_c/*

Krok 6 — aktywuj moduł:

Zaloguj się do panelu WHMCS i przejdź do:
System Settings → Addon Modules → KSeF Module → Activate

Krok 7 — konfiguracja:

W module uzupełnij:

NIP sprzedawcy
Token KSeF
Nazwę firmy i adres
Tryb (test lub production)

Następnie kliknij „Test połączenia”.

Krok 8 — dodaj cron:

Dodaj do crona (podmień ścieżkę):

*/5 * * * * php /home/USER/domains/twojadomena.pl/public_html/modules/addons/ksefmodule/cron/ksef_status.php

Jak to działa

Po poprawnej konfiguracji:

Faktura w WHMCS otrzymuje status Paid
Moduł dodaje ją do kolejki
Cron wysyła ją do KSeF
System zapisuje:
numer KSeF
XML
UPO
status operacji
Wymagania
klient w WHMCS musi mieć uzupełniony NIP
token KSeF musi odpowiadać trybowi (test / production)
Bezpieczeństwo i logika
brak duplikacji wysyłek
obsługa statusów: new, processing, sent, error
pełna kontrola z panelu WHMCS
możliwość ręcznej wysyłki lub pracy automatycznej
Autor

NETCLOUD24.COM / Łukasz Bodziony
