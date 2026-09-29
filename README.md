# 🛡️ SafeGuard AntiFish Defense

`<strong>`{=html}Android Cybersecurity & Anti-Phishing
Platform`</strong>`{=html}`<br>`{=html} Защита от фишинга,
интернет-мошенничества и потенциально опасных сетевых ресурсов.
```{=html}
</p>
```

------------------------------------------------------------------------

## О проекте

**SafeGuard AntiFish Defense** --- Android-проект в области
кибербезопасности для анализа ссылок, QR-кодов, доменов и доступных
сетевых индикаторов, выявления признаков фишинга и
интернет-мошенничества и понятного объяснения уровня риска.

Проект развивается с упором на **privacy by design**, локальную
обработку там, где это возможно, прозрачные результаты анализа и
отсутствие фиктивных показателей защиты.

> SafeGuard не заявляет абсолютную защиту от всех киберугроз. Результаты
> анализа являются индикаторами риска.

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

Проект не предусматривает обход certificate pinning, отключение TLS
validation, root/Frida/Xposed для обхода защиты сторонних приложений или
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

Эвристические и YARA-сигналы используются как часть общей корреляции
угроз. Одно совпадение не должно автоматически классифицировать объект
как malware.

``` text
YARA + IOC + Heuristics + Threat Intelligence
                    |
           Threat Correlation
                    |
               Risk Engine
```

## Privacy by Design

SafeGuard проектируется так, чтобы без необходимости не хранить пароли,
PIN, OTP, CVV, банковские данные, cookies, authentication/session
tokens, содержимое приватных сообщений и форм авторизации.

## Technology Stack

  Technology                      Purpose
  ------------------------------- --------------------------
  Kotlin                          Main language
  Jetpack Compose                 UI
  Material 3                      Design system
  MVVM / Clean Architecture       Architecture
  Coroutines / Flow / StateFlow   Async & reactive state
  Hilt                            Dependency Injection
  Room                            Local database
  DataStore                       Settings
  WorkManager                     Background jobs
  CameraX / ML Kit                QR workflow
  Android VpnService              Local network protection
  Android Keystore                Local key protection

## Сборка

Требуются Android Studio, JDK 17 и Android SDK.

``` bash
git clone YOUR_REPOSITORY_URL
cd SafeGuard-AntiFish-Defense
./gradlew clean
./gradlew test
./gradlew lint
./gradlew assembleDebug
```

Windows:

``` powershell
gradlew.bat clean
gradlew.bat test
gradlew.bat lint
gradlew.bat assembleDebug
```

Debug APK:

`app/build/outputs/apk/debug/app-debug.apk`

## Releases

Готовые APK рекомендуется публиковать через **GitHub Releases**, а не
коммитить в основной репозиторий. Для релиза указывайте версию/build,
дату, changelog, SHA-256, известные ограничения и APK.

## 🤝 Участие в разработке

SafeGuard открыт для участия Android/Kotlin и
cybersecurity-разработчиков, тестировщиков и специалистов по
локализации.

Особенно полезна помощь в направлениях:

-   URL/domain security и homograph detection
-   Android networking
-   IOC / Threat Intelligence
-   YARA
-   Unit / integration testing
-   False-positive reduction
-   Kotlin / Jetpack Compose
-   Қазақша / English localization
-   Documentation

Для простых задач используйте labels `good first issue`, `help wanted`,
`testing`, `documentation`, `localization`.

## Сообщить об ошибке

В Issue укажите версию SafeGuard, Android, шаги воспроизведения,
ожидаемый и фактический результат. Не публикуйте пароли, OTP, токены,
API-ключи, приватные сертификаты, банковскую информацию или другие
секретные данные.

## Security Vulnerabilities

Потенциальные уязвимости, способные подвергнуть пользователей риску, не
следует сразу раскрывать в публичном Issue. Используйте процесс
ответственного сообщения, описанный в `SECURITY.md`.

## Roadmap

Отмечайте `[x]` только после фактической реализации и проверки.

-   [ ] URL & Domain Protection
-   [ ] Homograph / Punycode Detection
-   [ ] QR Protection
-   [ ] Scam Text Analyzer
-   [ ] Local VPN Protection
-   [ ] DNS / Domain / IP Filtering
-   [ ] IOC Database
-   [ ] Threat Intelligence
-   [ ] Heuristic Engine
-   [ ] YARA Detection
-   [ ] Application Security Scanner
-   [ ] Critical Apps Protection
-   [ ] Advanced HTTPS Protection
-   [ ] Security Center
-   [ ] RU / KK / EN localization
-   [ ] Deepfake media research
-   [ ] Voice-clone detection research

## Disclaimer

SafeGuard AntiFish Defense --- defensive cybersecurity project. Ни один
инструмент безопасности не может гарантировать обнаружение или
предотвращение всех фишинговых, мошеннических или вредоносных действий.
Результаты SafeGuard являются оценкой риска на основании доступных
сигналов, а не абсолютным доказательством вредоносности сайта, файла,
приложения или человека.

## Developer

**Куанышгали Ишимбаев**

SafeGuard AntiFish Defense\
Email: `kuanishgalii@gmail.com`

------------------------------------------------------------------------

```{=html}
<p align="center">
```
`<strong>`{=html}🛡️ SafeGuard AntiFish
Defense`</strong>`{=html}`<br>`{=html} Think Before You
Trust.`<br>`{=html}`<br>`{=html} © 2026 SafeGuard AntiFish Defense
```{=html}
</p>
```
