# 🛡️ SafeGuard AntiFish Defense
    Android Cybersecurity & Anti-Phishing
Защита от фишинга,интернет-мошенничества и потенциально опасных сетевых ресурсов.

------------------------------------------------------------------------

## О проекте

**SafeGuard AntiFish Defense** - Android-проект в области
кибербезопасности для анализа ссылок, QR-кодов, доменов и доступных
сетевых индикаторов, выявления признаков фишинга и
интернет-мошенничества и понятного объяснения уровня риска.

Проект развивается с упором на **privacy by design**, локальную
обработку там, где это возможно, прозрачные результаты анализа и
отсутствие фиктивных показателей защиты.

> SafeGuard не заявляет абсолютную защиту от всех киберугроз.
> Результаты анализа являются индикаторами риска.

## Основные направления

-   🔗 URL & Domain Protection
-   🧬 IDN / Punycode / Homograph Detection
-   📱 QR Security Scanner
-   💬 Scam Text Analyzer
-   🛡️ Local VPN Protection (`VpnService`)
-   🌐 DNS / Domain / IP Analysis
-   🗃️ IOC & Threat Intelligence
-   🔬 Heuristic Analysis
-   🧪 YARA Detection
-   📲 Application Security Scanner
-   🏦 Critical Apps Protection
-   📊 Security Center & History
-   🌍 Қазақша / Русский / English

## Архитектура анализа

``` text
URL / QR / Text / App / Network
              |
              v
        Normalization
              |
      +-------+-------+
      |       |       |
     IOC   Threat DB  Heuristics
      |       |       |
      +-------+-------+
              |
              v
      Threat Correlation
              |
              v
          Risk Engine
              |
      +-------+-------+
      |       |       |
    ALLOW    WARN    BLOCK
```

`BLOCKED` используется только тогда, когда действие действительно было
технически заблокировано. `DETECTED`, `WARNED` и `BLOCKED` --- разные
состояния.

## Link & Phishing Protection

Анализ может включать HTTP/HTTPS, hostname, IP-based URL, subdomains,
ports, redirects, URL shorteners, encoded characters,
Unicode/IDN/Punycode, mixed scripts, homograph-признаки, brand
impersonation, IOC/Threat Database и Allowlist/Blocklist.

## QR Protection

``` text
SCAN -> PARSE -> SHOW URL -> ANALYZE -> SHOW RISK -> USER DECIDES
```

QR-код не должен автоматически открывать URL после распознавания.

## Scam Text Analyzer

Модуль предназначен для обнаружения признаков социальной инженерии:
искусственной срочности, угроз блокировки аккаунта, просьб сообщить
пароль/OTP/CVV, перевести деньги, установить APK, предоставить удалённый
доступ или перейти по подозрительной ссылке.

SafeGuard не предназначен для скрытого чтения личных сообщений.

## Local VPN Protection

``` text
Android Apps
    |
SafeGuard Local VPN
    |
DNS / Domain / IP Analysis
    |
IOC + Threat Database
    |
Risk Engine
    |
Policy Engine
    |
ALLOW / WARN / BLOCK
```

SafeGuard не заявляет возможность видеть полный URL или содержимое
каждого HTTPS-соединения.

## Advanced HTTPS Protection

Расширенная HTTPS-проверка является дополнительной возможностью только
для совместимого трафика и включается пользователем явно.

Проект не предусматривает обход certificate pinning, отключение TLS validation, root/Frida/Xposed для обхода защиты сторонних приложений или
модификацию сторонних APK.

## IOC Database

Типы индикаторов:

`DOMAIN` · `IP` · `URL` · `URL_PATTERN` · `SHA256` ·
`CERTIFICATE_FINGERPRINT` · `PACKAGE_INDICATOR`

Категории:

`PHISHING` · `SCAM` · `MALWARE` · `FAKE_LOGIN` · `BRAND_IMPERSONATION` ·
`SPYWARE` · `TROJAN` · `SUSPICIOUS` · `NETWORK_THREAT` · `USER_BLOCKED`

Неизвестный hash или indicator не означает, что объект вредоносный.

## Heuristic & YARA Detection

Эвристические и YARA-сигналы используются как часть общей корреляции угроз. 

Одно совпадение не должно автоматически классифицировать объект как malware.

``` text
YARA + IOC + Heuristics + Threat Intelligence
                    |
           Threat Correlation
                    |
               Risk Engine
```


## Disclaimer

SafeGuard AntiFish Defense Defensive Cybersecurity Project. 
Ни один инструмент безопасности не может гарантировать обнаружение или предотвращение всех фишинговых, мошеннических или вредоносных действий.
Результаты SafeGuard являются оценкой риска на основании доступных сигнатур,а не абсолютным доказательством вредоносности сайта, файла,приложения или человека.

## Developer

**Куанышгали Ишимбаев**

SafeGuard AntiFish Defense\
Email: `kuanishgalii@gmail.com`

------------------------------------------------------------------------


</p>
```
