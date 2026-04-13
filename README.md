<h1>KSEF-MODUL-WHMCS-PL</h1>

<p>
<strong>Darmowy moduł KSeF dla WHMCS</strong> w języku polskim, umożliwiający pełną integrację z 
<strong>Krajowym Systemem e-Faktur (KSeF – Ministerstwo Finansów)</strong>.
</p>

<p>
Projekt został stworzony przez <strong>NETCLOUD24.COM / Łukasz Bodziony</strong> i jest 
<strong>w 100% darmowy dla wszystkich</strong> — zarówno do użytku prywatnego, jak i komercyjnego.
</p>

<p>
Możesz go dowolnie używać, modyfikować i wdrażać u klientów bez żadnych opłat licencyjnych.
</p>

<p>
👉 Infrastruktura pod WHMCS i KSeF:
</p>

<ul>
<li><a href="https://netcloud24.com/" target="_blank">VPS Windows</a></li>
<li><a href="https://netcloud24.com/serwer-vps/" target="_blank">Serwery VPS Linux</a></li>
<li><a href="https://netcloud24.com/hosting/" target="_blank">Hosting WWW</a></li>
</ul>

<hr>

<h2>📌 Opis projektu</h2>

<p>
KSEF-MODUL-WHMCS-PL to kompletny moduł integracyjny, który pozwala automatycznie wysyłać faktury z WHMCS do KSeF.
</p>

<p>
Został zaprojektowany w taki sposób, aby wdrożenie było maksymalnie proste — bez konieczności pisania własnej integracji,
bez znajomości API KSeF i bez użycia podpisu kwalifikowanego.
</p>

<p>
Moduł wykorzystuje <strong>oficjalne API KSeF</strong> oraz autoryzację tokenem Ministerstwa Finansów.
</p>

<p>
Dzięki temu możesz w kilka minut uruchomić pełną automatyzację fakturowania zgodną z wymogami KSeF.
</p>

<hr>

<h2>💸 100% darmowy</h2>

<ul>
<li>✔ brak opłat licencyjnych</li>
<li>✔ brak abonamentu</li>
<li>✔ brak ograniczeń</li>
<li>✔ open source</li>
<li>✔ do użytku komercyjnego</li>
</ul>

<p>
Projekt powstał jako narzędzie dla społeczności WHMCS i firm wdrażających KSeF.
</p>

<hr>

<h2>🚀 Funkcjonalność</h2>

<ul>
<li>konfiguracja z panelu WHMCS</li>
<li>obsługa trybu test i production</li>
<li>autoryzacja tokenem MF</li>
<li>automatyczne kolejkowanie faktur (Paid)</li>
<li>cron do wysyłki</li>
<li>statusy: new / processing / sent / error</li>
<li>zapis numeru KSeF</li>
<li>zapis XML faktury</li>
<li>zapis UPO</li>
<li>blokada duplikatów</li>
<li>panel historii wysyłek</li>
</ul>

<hr>

<h2>🔑 Autoryzacja (Token KSeF – Ministerstwo Finansów)</h2>

<p>
Moduł działa wyłącznie na <strong>tokenie KSeF</strong> generowanym w systemie MF.
</p>

<p>
Nie wymagane:
</p>

<ul>
<li>podpis kwalifikowany</li>
<li>certyfikat</li>
</ul>

<p>
Generowanie tokenu:
</p>

<ul>
<li>Test: https://ksef-test.mf.gov.pl</li>
<li>Produkcja: https://ksef.mf.gov.pl</li>
</ul>

<p>
Format tokenu:
</p>

<pre>
20260402-EC-XXXXXXXXXX|nip-1234567890|HASH
</pre>

<p><strong>Ważne:</strong></p>

<ul>
<li>token musi pasować do trybu (test / production)</li>
<li>NIP musi być zgodny z tokenem</li>
</ul>

<hr>

<h2>📦 Composer / vendor (KLUCZOWE)</h2>

<p>
Moduł korzysta z bibliotek PHP (guzzle, ksef-client).
</p>

<p>
✔ W paczce <strong>ksefmodule-full-deploy.tar.gz</strong> katalog <strong>vendor</strong> jest już zawarty  
➡️ NIE trzeba używać composera
</p>

<p>
✔ Jeśli instalujesz ręcznie:
</p>

<pre>
cd modules/addons/ksefmodule
composer install
</pre>

<p>
❌ Brak vendor = moduł NIE zadziała
</p>

<hr>

<h2>⚡ Instalacja (2 minuty)</h2>

<pre>
cd /home/USER/domains/twojadomena.pl/public_html

wget https://github.com/netcloud24/KSEF-MODUL-WHMCS-PL/raw/main/ksefmodule-full-deploy.tar.gz

tar -xzvf ksefmodule-full-deploy.tar.gz --strip-components=1

chown -R USER:USER modules/addons/ksefmodule
chmod -R 755 modules/addons/ksefmodule

chown USER:USER includes/hooks/ksefmodule.php
chmod 644 includes/hooks/ksefmodule.php

rm -rf templates_c/*
</pre>

<p>
Aktywacja:
</p>

<p>
System Settings → Addon Modules → Activate
</p>

<hr>

<h2>⚙️ Konfiguracja</h2>

<ul>
<li>NIP</li>
<li>Token KSeF</li>
<li>Nazwa firmy</li>
<li>Adres</li>
<li>Tryb (test / production)</li>
</ul>

<p>
Kliknij: <strong>Test połączenia</strong>
</p>

<hr>

<h2>⏱ Cron</h2>

<pre>
*/5 * * * * php /home/USER/domains/twojadomena.pl/public_html/modules/addons/ksefmodule/cron/ksef_status.php
</pre>

<hr>

<h2>🔄 Jak działa</h2>

<ol>
<li>Faktura → Paid</li>
<li>Dodanie do kolejki</li>
<li>Cron wysyła do KSeF</li>
<li>KSeF nadaje numer</li>
<li>Zapis XML + UPO</li>
</ol>

<hr>

<h2>🔒 Stabilność</h2>

<ul>
<li>brak duplikatów</li>
<li>kolejka przetwarzania</li>
<li>retry błędów</li>
<li>kontrola statusów</li>
</ul>

<hr>

<h2>🎯 Zastosowanie</h2>

<ul>
<li>firmy hostingowe</li>
<li>WHMCS</li>
<li>SaaS</li>
<li>software house</li>
<li>biura księgowe</li>
</ul>

<hr>

<h2>👨‍💻 Autor</h2>

<p>
<strong>NETCLOUD24.COM / Łukasz Bodziony</strong>
</p>

<p>
👉 Oferta:
</p>

<ul>
<li><a href="https://netcloud24.com/">VPS Windows</a></li>
<li><a href="https://netcloud24.com/serwer-vps/">VPS Linux</a></li>
<li><a href="https://netcloud24.com/hosting/">Hosting WWW</a></li>
</ul>

<hr>

