<h1>KSEF-MODUL-WHMCS-PL</h1>

<p>
<strong>Darmowy moduł KSeF dla WHMCS</strong> w języku polskim, udostępniony publicznie jako projekt open source.
</p>

<p>
Projekt został stworzony przez <strong>NETCLOUD24.COM / Łukasz Bodziony</strong> i jest <strong>całkowicie bezpłatny dla wszystkich</strong> — zarówno do użytku prywatnego, jak i komercyjnego.
</p>

<p>
Możesz go używać w swojej firmie, wdrażać u klientów, modyfikować oraz rozwijać według własnych potrzeb — bez opłat licencyjnych.
</p>

<p>
👉 <strong>Serwery pod WHMCS / KSeF:</strong><br>
<a href="https://netcloud24.com" target="_blank">
</a>
</p>

<hr>

<h2>📌 Czym jest ten moduł</h2>

<p>
KSEF-MODUL-WHMCS-PL to kompletny system integracji WHMCS z Krajowym Systemem e-Faktur (KSeF), który umożliwia automatyczne i ręczne przesyłanie faktur do systemu Ministerstwa Finansów.
</p>

<p>
Został zaprojektowany tak, aby maksymalnie uprościć wdrożenie KSeF w firmach korzystających z WHMCS — bez konieczności pisania własnych integracji, bez kombinowania z API i bez ręcznej obsługi faktur.
</p>

<p>
Moduł działa w pełni niezależnie od core WHMCS i wykorzystuje oficjalne API KSeF oraz autoryzację tokenem Ministerstwa Finansów.
</p>

<p>
Dzięki temu możesz w ciągu kilku minut przejść od braku integracji do pełnej automatyzacji wysyłki faktur zgodnie z wymogami KSeF.
</p>

<hr>

<h2>💸 100% darmowy</h2>

<p>
Ten moduł jest:
</p>

<ul>
<li>✔ darmowy do użytku prywatnego</li>
<li>✔ darmowy do użytku komercyjnego</li>
<li>✔ darmowy dla firm hostingowych</li>
<li>✔ darmowy dla wdrożeń u klientów</li>
<li>✔ open source – możesz go rozwijać</li>
</ul>

<p>
Nie ma żadnych ukrytych opłat, subskrypcji ani licencji.
</p>

<p>
To świadoma decyzja — zamiast sprzedawać moduł, projekt ma budować ekosystem i ułatwiać wdrożenia KSeF.
</p>

<hr>

<h2>🚀 Funkcjonalność</h2>

<p>Moduł oferuje kompletny zestaw funkcji produkcyjnych:</p>

<ul>
<li>pełna konfiguracja z panelu WHMCS</li>
<li>obsługa trybu test i production</li>
<li>integracja z API KSeF</li>
<li>autoryzacja tokenem Ministerstwa Finansów</li>
<li>automatyczne kolejkowanie faktur po statusie Paid</li>
<li>cron do przetwarzania i wysyłki</li>
<li>obsługa statusów faktur</li>
<li>zapis numeru KSeF</li>
<li>zapis XML faktury</li>
<li>zapis UPO (urzędowe potwierdzenie odbioru)</li>
<li>blokada duplikatów</li>
<li>logika retry i kontrola błędów</li>
<li>panel podglądu wysyłek</li>
</ul>

<hr>

<h2>🔑 Autoryzacja – token Ministerstwa Finansów</h2>

<p>
Moduł wykorzystuje <strong>oficjalny token KSeF</strong> generowany w systemie Ministerstwa Finansów.
</p>

<p>
Nie jest wymagany:
</p>

<ul>
<li>podpis kwalifikowany</li>
<li>certyfikat</li>
<li>profil zaufany</li>
</ul>

<p>
Token generujesz tutaj:
</p>

<ul>
<li>Test: https://ksef-test.mf.gov.pl</li>
<li>Produkcja: https://ksef.mf.gov.pl</li>
</ul>

<p>
Token ma postać:
</p>

<pre>
20260402-EC-XXXXXXXXXX|nip-1234567890|HASH
</pre>

<p><strong>Ważne:</strong></p>

<ul>
<li>token jest powiązany z NIP-em</li>
<li>token testowy działa tylko w trybie test</li>
<li>token produkcyjny działa tylko w production</li>
<li>NIP musi być zgodny z tokenem</li>
</ul>

<hr>

<h2>⚡ Instalacja (bardzo prosta)</h2>

<p>Podmień dane:</p>

<pre>
USER=twoj_user
WHMCS_PATH=/home/USER/domains/twojadomena.pl/public_html
</pre>

<p><strong>Krok 1:</strong></p>

<pre>
cd /home/USER/domains/twojadomena.pl/public_html
</pre>

<p><strong>Krok 2:</strong></p>

<pre>
wget https://github.com/netcloud24/KSEF-MODUL-WHMCS-PL/raw/main/ksefmodule-full-deploy.tar.gz
</pre>

<p><strong>Krok 3:</strong></p>

<pre>
tar -xzvf ksefmodule-full-deploy.tar.gz --strip-components=1
</pre>

<p><strong>Krok 4:</strong></p>

<pre>
chown -R USER:USER modules/addons/ksefmodule
chmod -R 755 modules/addons/ksefmodule

chown USER:USER includes/hooks/ksefmodule.php
chmod 644 includes/hooks/ksefmodule.php
</pre>

<p><strong>Krok 5:</strong></p>

<pre>
rm -rf templates_c/*
</pre>

<p><strong>Krok 6:</strong></p>

<p>System Settings → Addon Modules → Activate</p>

<p><strong>Krok 7:</strong></p>

<p>Wprowadź NIP, token, dane firmy i kliknij Test połączenia</p>

<p><strong>Krok 8 (cron):</strong></p>

<pre>
*/5 * * * * php /home/USER/domains/twojadomena.pl/public_html/modules/addons/ksefmodule/cron/ksef_status.php
</pre>

<hr>

<h2>🔄 Jak działa system</h2>

<ol>
<li>Faktura WHMCS → status Paid</li>
<li>Dodanie do kolejki</li>
<li>Cron wysyła do KSeF</li>
<li>KSeF nadaje numer</li>
<li>Zapis XML + UPO + status</li>
</ol>

<hr>

<h2>🔒 Stabilność i bezpieczeństwo</h2>

<ul>
<li>brak duplikacji faktur</li>
<li>kontrola statusów</li>
<li>kolejka przetwarzania</li>
<li>retry błędów</li>
<li>pełna kontrola z panelu</li>
</ul>

<hr>

<h2>🎯 Dla kogo jest ten moduł</h2>

<ul>
<li>firmy hostingowe (WHMCS)</li>
<li>SaaS</li>
<li>software house</li>
<li>biura księgowe</li>
<li>integratorzy systemów</li>
</ul>

<hr>

<h2>👨‍💻 Autor</h2>

<p>
<strong>NETCLOUD24.COM / Łukasz Bodziony</strong><br><br>

👉 <a href="https://netcloud24.com/" target="_blank">
VPS Windows 
</a>
</p>

<hr>

<h2>📌 Licencja</h2>

<p>
Projekt open source – zalecana licencja MIT lub GPL.
</p>
