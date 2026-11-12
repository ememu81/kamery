# Kamery online – założenia i ustalenia

Stan na: 12.11.2026 (wieczór)

## Cel
Szybki podgląd wybranych publicznych kamer górskich z różnych portali, w jednym miejscu, na telefonie i na komputerze.

## Decyzje
- **Rozwiązanie:** statyczna strona HTML bez własnego serwera (`index.html`).
- **Serwer domowy:** na razie nie. Wrócimy do niego tylko wtedy, gdy będzie potrzebne archiwum kadrów, powiadomienia albo pośredniczenie dla zablokowanych kamer. Wtedy wyłącznie przez Tailscale lub WireGuard, bez otwierania portów na routerze. Ewentualnie Cloudflare Tunnel z logowaniem (Cloudflare Access).
- **Hosting:** GitHub Pages, https://ememu81.github.io/kamery/, repozytorium `ememu81/kamery` (darmowy, https, działa na telefonie i na komputerze). Artefakt Claude odpada, bo nie może wczytywać obrazu z zewnętrznych serwerów.
- **Wybór kamer:** 21 z 62 sprawdzonych + Koniaków – Centrum (Ochodzita) dodany 12.11; 22 kamery, zaznaczonych w arkuszu „Kamery online – wybór kamer” (https://claude.ai/artifact/8MP8WFj3tjJbamdySi7ZD1).

## Działanie strony
- Zakładki: Wszystkie / Beskidy / Tatry / Gorce / Pieniny / Pogoda (w tej kolejności są też sekcje na stronie).
- **Prognozy:** nad kamerami regionu jest zwijany pasek „Prognoza” z wyborem punktu i źródła (yr.no / ICM UM). Zakładka „Pogoda” pokazuje wszystkie punkty z oboma źródłami obok siebie. Prognozy odświeżają się co godzinę. W widoku „Wszystkie” paski są domyślnie zwinięte, a stan zwinięcia, wybrany punkt i źródło są zapamiętywane.
- **Mapa (zakładka „Pogoda”, na górze):** widżet Windy wyśrodkowany na 49.40, 19.70 (zoom 7) z przełącznikiem Radar opadów / Satelita / Chmury (prognoza); wybór jest zapamiętywany. RainViewer odpada: od 1.01.2026 darmowe API nie ma satelity i ma maks. zoom 7 na kafelkach radaru.
- Zdjęcia (TOPR) odświeżają się co 5 minut i po powrocie do karty. Jest też przycisk „Odśwież”.
- Wideo i odtwarzacze startują dopiero po stuknięciu, żeby oszczędzać dane (strumień to ok. 2 Mb/s). Przełącznik „wideo w kafelkach” włącza odtwarzanie wszystkich naraz i jest zapamiętywany.
- Przełącznik „miniatury wideo” (domyślnie włączony na komputerze, wyłączony na telefonie): z każdego strumienia HLS pobierana jest jedna klatka, odświeżana co 10 min (ok. 1 MB na kamerę), a odtwarzacze webcamera.pl i Windy ładują się w kafelku i pokazują swój podgląd. Żywiec Rynek 1 i 3 (stream360) nie mają podglądu, bo ich odtwarzacz przed kliknięciem pokazuje tylko herb.
- Wideo odtwarzane jest przez hls.js. Natywny odtwarzacz HLS jest tylko zapasem, bo w nowszym Chrome nie radził sobie z częścią strumieni.
- Przy zdjęciach TOPR jest napis „sprawdzono HH:MM”, czyli godzina pobrania. Godzina wykonania zdjęcia jest wypalona w jego rogu.
- Pełny ekran: strzałki, przesunięcie palcem (dla zdjęć), Esc. Link „źródło” prowadzi do strony właściciela kamery.
- Gdy strumienia nie da się odtworzyć, kafelek pokazuje komunikat i link do strony źródłowej.

## Źródła wybranych kamer
| Region | Kamera | Rodzaj | Źródło obrazu |
|---|---|---|---|
| Tatry | Morskie Oko – Mnich | zdjęcie | kamery.topr.pl/moko_TPN/moko_02.jpg (zapas: pogoda.topr.pl/download/current/momn.jpeg) |
| Tatry | Hala Gąsienicowa – Granaty | zdjęcie | kamery.topr.pl/hala/hala.jpg (zapas: …/hala.jpeg) |
| Tatry | Hala Gąsienicowa – Kasprowy Wierch | zdjęcie | kamery.topr.pl/hala2/hala2.jpg (zapas: …/hgkw.jpeg) |
| Tatry | Kasprowy Wierch – Świnica | zdjęcie | kamery.topr.pl/gasienicowa/gasie.jpg (zapas: …/kwgs.jpeg) |
| Tatry | Kasprowy Wierch – Goryczkowa / Czerwone Wierchy | zdjęcie | kamery.topr.pl/goryczkowa/gorycz.jpg (zapas: …/kwgr.jpeg) |
| Tatry | Kościelisko – Czerwone Wierchy | zdjęcie | kamery.topr.pl/czwierchy/czwierchy.jpg (nie działa od 29.09) |
| Beskidy | Koniaków – Centrum (Ochodzita) | wideo HLS | polineo.pl:5443/LiveApp/streams/480833538014407854235726.m3u8 (strona: istebna.eu) |
| Beskidy | Rysianka – w kierunku Tatr | wideo HLS | stream.arkomnet.eu/rysianka1 |
| Beskidy | Rysianka – Hala Stopkowa | wideo HLS | stream.arkomnet.eu/rysianka2 |
| Beskidy | Widok na Gminę Węgierska Górka | wideo HLS | stream.arkomnet.eu/wgwidok |
| Beskidy | Cisiec – Wyciąg Za Groniem | wideo HLS | stream.arkomnet.eu/xxx_wyciag_III |
| Beskidy | Żywiec – Rynek 1 i 3 | odtwarzacz | stream360.pl/v/Zywiec1/index1.php, index3.php |
| Beskidy | Żywiec – Rynek 2, Średni Grojec | odtwarzacz | player.webcamera.pl (zywiec_cam_f0027b, zywiec_cam_1ce519) |
| Gorce | Suchy Groń, Magurki, Lubań, Gorc | wideo HLS | ochotnica.epicserv.pl/streams/cam5, cam1, cam3, cam4 |
| Pieniny | Schronisko Trzy Korony – Sromowce Niżne | odtwarzacz | static.webcamera.pl … schroniskapieninskie_cam_fb73aa |
| Pieniny | Jezioro Czorsztyńskie i zamek | odtwarzacz | static.webcamera.pl … niedzica_cam_a6aff0 |
| Pieniny | Stara Lubowla | odtwarzacz Windy | webcams.windy.com, webcamId=1621786379 |

## Punkty prognozy
| Punkt | Region | Współrzędne |
|---|---|---|
| Hala Rysianka | Beskidy | 49.5409, 19.1306 |
| Babia Góra | Beskidy | 49.5732, 19.5294 |
| Ochodzita | Beskidy | 49.5456, 18.9551 |
| Kasprowy Wierch | Tatry | 49.2318, 19.9817 |
| Lubań | Gorce | 49.4878, 20.3420 |
| Trzy Korony | Pieniny | 49.4147, 20.4122 |

- **yr.no:** gotowy meteogram SVG na 48 h: `https://www.yr.no/en/content/<lat>,<lon>/meteogram.svg`.
- **ICM (meteo.pl), model UM 4 km, 60 h (`um4_60`, najnowszy przebieg, jak domyślnie w aplikacji):** stare obrazki `mgram_pict.php` zwracają już tylko reklamę nowej aplikacji, więc meteogram jest rysowany na stronie (SVG) w układzie aplikacji Meteo ICM (https://app.meteo.pl/meteogram/<lat>,<lon>). Ma 8 paneli: temperatura (powietrze, odczuwalna, punkt rosy, rozrzut), opad według rodzaju z wilgotnością, szansa opadu, ciśnienie, wiatr z porywami, kierunek wiatru, podstawy i wierzchołki chmur z widzialnością, zachmurzenie w oktantach z mgłą. Dane pochodzą z API aplikacji: `GET https://devmgramapi.meteo.pl/meteorograms/available` oraz `POST …/meteorograms/um4_60` (albo `um4_120` dla 5 dni) z `{point:{lat,lon}, date:<przebieg>}`. Działa z ememu81.github.io (CORS), ale to **nieoficjalne API aplikacji**, które może się zmienić. Pod wykresem jest wymagany przez ICM podpis źródła; strona nie może mieć reklam.

Zdjęcia TOPR idą przez pośrednik: `https://images.weserv.nl/?url=kamery.topr.pl/<ścieżka>`.

## Ustalenia z testów
- **TOPR:** nowa strona pogoda.topr.pl (`/download/current/`) przestała się aktualizować 10.11. Nieaktualne kadry widać też na samej stronie TOPR. Aktualne zdjęcia ma stara strona kamery.topr.pl, ale działa ona tylko przez http, więc strona pobiera je przez darmowy pośrednik https **images.weserv.nl**. Przy błędzie przełącza się na zapas z pogoda.topr.pl.
- **Kościelisko – Czerwone Wierchy:** kamera nie działa od 29.09.2026 (ostatni kadr ma tę datę w obu źródłach).
- **arkomnet** (Rysianka, WGmedia): strumienie działają poza stronami źródłowymi.
- **Ochotnica (epicserv):** serwer wpuszcza tylko wybrane strony (blokuje np. zywiec.pl), ale z ememu81.github.io działa (sprawdzone 12.11).
- **webcamera.pl / stream360 / Windy:** odtwarzacze ładują się na innych stronach. stream360 wymaga kliknięcia, webcamera.pl ma swój baner.
- Strona Trzy Korony błędnie opisuje odtwarzacze. Jezioro Czorsztyńskie to `niedzica_cam_a6aff0`, a `czorsztynski_cam_*` to stok Czorsztyn Ski.

## Do zrobienia
- [x] Strona na GitHub Pages: https://ememu81.github.io/kamery/ (repozytorium ememu81/kamery, zmiany commituje Claude).
- [x] Kamery z Gorców działają pod docelowym adresem.
- [ ] Dodać skrót na ekran główny telefonu.
- [x] Nieaktualne zdjęcia TOPR: źródło zmienione na kamery.topr.pl przez images.weserv.nl (12.11).
- [ ] Zdecydować, czy zostawić Kościelisko (nie działa od 29.09) albo zamienić je na inną kamerę.
- [x] Prognozy yr.no + ICM dla 6 punktów (12.11).
- [x] Gorce: punkt prognozy Lubań (12.11).
- [ ] Opcjonalnie: archiwum kadrów (wymaga serwera).

## Uwagi prawne
Do prywatnego podglądu wszystko jest w porządku. Przed publicznym udostępnianiem strony warto sprawdzić regulaminy portali, bo niektóre zabraniają osadzania obrazu bez zgody.
