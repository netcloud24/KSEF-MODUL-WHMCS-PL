<h1>KSEF-MODUL-WHMCS-PL</h1>

<p>
Darmowy moduł <strong>KSeF dla WHMCS</strong> w języku polskim.<br>
Integracja z <strong>Krajowym Systemem e-Faktur</strong> obejmująca:
</p>

<ul>
<li>konfigurację z panelu administratora WHMCS,</li>
<li>ręczną wysyłkę faktur WHMCS do KSeF,</li>
<li>automatyczne kolejkowanie faktur ze statusem <strong>Paid</strong>,</li>
<li>obsługę statusów wysyłki,</li>
<li>integrację z cronem,</li>
<li>zapis numeru KSeF,</li>
<li>zapis XML i UPO.</li>
</ul>

<p>
Projekt przygotowany przez <strong>NETCLOUD24.COM / Łukasz Bodziony</strong>.
</p>

<p>
👉 <strong>Sprawdź wydajne serwery pod WHMCS:</strong><br>
<a href="https://netcloud24.com" target="_blank">
https://netcloud24.com/
</a>
</p>

<hr>

<h2>🚀 Funkcje modułu</h2>

<ul>
<li>konfiguracja KSeF z panelu WHMCS,</li>
<li>obsługa trybu test / production,</li>
<li>automatyczna kolejka faktur,</li>
<li>integracja z hookiem InvoicePaid,</li>
<li>cron do wysyłki faktur,</li>
<li>zapis XML, UPO i numeru KSeF,</li>
<li>blokada duplikatów wysyłki,</li>
<li>lista faktur gotowych do wysłania,</li>
<li>logi i statusy operacji.</li>
</ul>

<hr>

<h2>⚙️ Wymagania</h2>

<ul>
<li>WHMCS 8 / 9</li>
<li>PHP 8.1+</li>
<li>token KSeF</li>
<li>dostęp do API KSeF</li>
</ul>

<hr>

<h2>📁 Struktura modułu</h2>

<pre>
modules/addons/ksefmodule/
├── ksefmodule.php
├── vendor/
├── lib/
│   ├── KsefConfig.php
│   ├── KsefService.php
│   └── KsefWhmcsMapper.php
└── cron/
    └── ksef_status.php

includes/hooks/ksefmodule.php
</pre>

<hr>

<h2>⚡ Szybka instalacja</h2>

<p>Podmień dane:</p>

<pre>
USER=twoj_user
WHMCS_PATH=/home/USER/domains/twojadomena.pl/public_html
</pre>

<h3>1. Wejdź do katalogu WHMCS</h3>

<pre>
cd /home/USER/domains/twojadomena.pl/public_html
</pre>

<h3>2. Pobierz moduł</h3>

<pre>
wget https://github.com/netcloud24/KSEF-MODUL-WHMCS-PL/raw/main/ksefmodule-full-deploy.tar.gz
</pre>

<h3>3. Rozpakuj</h3>

<pre>
tar -xzvf ksefmodule-full-deploy.tar.gz --strip-components=1
</pre>

<h3>4. Uprawnienia</h3>

<pre>
chown -R USER:USER modules/addons/ksefmodule
chmod -R 755 modules/addons/ksefmodule

chown USER:USER includes/hooks/ksefmodule.php
chmod 644 includes/hooks/ksefmodule.php
</pre>

<h3>5. Cache</h3>

<pre>
rm -rf templates_c/*
</pre>

<h3>6. Aktywacja</h3>

<p>
System Settings → Addon Modules → KSeF Module → Activate
</p>

<h3>7. Konfiguracja</h3>

<ul>
<li>NIP</li>
<li>Token KSeF</li>
<li>Nazwa firmy</li>
<li>Adres</li>
<li>Tryb (test / production)</li>
</ul>

<p>Kliknij: <strong>Test połączenia</strong></p>

<h3>8. Cron</h3>

<pre>
*/5 * * * * php /home/USER/domains/twojadomena.pl/public_html/modules/addons/ksefmodule/cron/ksef_status.php
</pre>

<hr>

<h2>🔄 Jak to działa</h2>

<ol>
<li>Faktura w WHMCS → status Paid</li>
<li>Dodanie do kolejki</li>
<li>Cron wysyła do KSeF</li>
<li>Zapis danych (KSeF, XML, UPO)</li>
</ol>

<hr>

<h2>📊 Statusy</h2>

<ul>
<li>new</li>
<li>processing</li>
<li>sent</li>
<li>error</li>
<li>hold</li>
<li>retry</li>
</ul>

<hr>

<h2>🔒 Bezpieczeństwo</h2>

<ul>
<li>brak duplikacji</li>
<li>kolejka + cron</li>
<li>kontrola statusów</li>
</ul>

<hr>

<h2>👨‍💻 Autor</h2>

<p>
<strong>NETCLOUD24.COM / Łukasz Bodziony</strong><br><br>

👉 <a href="https://netcloud24.com" target="_blank">
VPS Windows 
</a>
</p>

<hr>

<h2>📌 Licencja</h2>

<p>
Dodaj licencję (MIT / GPL) w repozytorium.
</p>
