# Kamery online – założenia i ustalenia

Stan na: 12.11.2026

## Cel
Szybki podgląd wybranych publicznych kamer górskich z różnych portali, w jednym miejscu, na telefonie i na komputerze.

## Decyzje
- **Rozwiązanie:** statyczna strona HTML bez własnego serwera (`index.html`).
- **Serwer domowy:** na razie nie. Wrócimy do niego tylko wtedy, gdy będzie potrzebne archiwum kadrów, powiadomienia albo pośredniczenie dla zablokowanych kamer. Wtedy wyłącznie przez Tailscale lub WireGuard, bez otwierania portów na routerze. Ewentualnie Cloudflare Tunnel z logowaniem (Cloudflare Access).
- **Hosting:** GitHub Pages (darmowy, https, działa na telefonie i na komputerze). Artefakt Claude odpada, bo nie może wczytywać obrazu z zewnętrznych serwerów.
- **Wybór kamer:** 21 z 62 sprawdzonych, zaznaczonych w arkuszu „Kamery online – wybór kamer” (https://claude.ai/artifact/8MP8WFj3tjJbamdySi7ZD1).

## Działanie strony
- Zakładki: Wszystkie / Tatry / Beskid Żywiecki / Gorce / Pieniny.
- Zdjęcia (TOPR) odświeżają się co 5 minut i po powrocie do karty. Jest też przycisk „Odśwież”.
- Wideo i odtwarzacze startują dopiero po stuknięciu, żeby oszczędzać dane (strumień to ok. 2 Mb/s). Przełącznik „wideo w kafelkach” włącza odtwarzanie wszystkich naraz i jest zapamiętywany.
- Pełny ekran: strzałki, przesunięcie palcem (dla zdjęć), Esc. Link „źródło” prowadzi do strony właściciela kamery.
- Gdy strumienia nie da się odtworzyć, kafelek pokazuje komunikat i link do strony źródłowej.

## Źródła wybranych kamer
| Region | Kamera | Rodzaj | Źródło obrazu |
|---|---|---|---|
| Tatry | Morskie Oko – Mnich | zdjęcie | pogoda.topr.pl/download/current/momn.jpeg |
| Tatry | Hala Gąsienicowa – Granaty | zdjęcie | …/hala.jpeg |
| Tatry | Hala Gąsienicowa – Kasprowy Wierch | zdjęcie | …/hgkw.jpeg |
| Tatry | Kasprowy Wierch – Świnica | zdjęcie | …/kwgs.jpeg |
| Tatry | Kasprowy Wierch – Goryczkowa / Czerwone Wierchy | zdjęcie | …/kwgr.jpeg |
| Tatry | Kościelisko – Czerwone Wierchy | zdjęcie | …/kscw.jpeg |
| Beskid Żywiecki | Rysianka – w kierunku Tatr | wideo HLS | stream.arkomnet.eu/rysianka1 |
| Beskid Żywiecki | Rysianka – Hala Stopkowa | wideo HLS | stream.arkomnet.eu/rysianka2 |
| Beskid Żywiecki | Widok na Gminę Węgierska Górka | wideo HLS | stream.arkomnet.eu/wgwidok |
| Beskid Żywiecki | Cisiec – Wyciąg Za Groniem | wideo HLS | stream.arkomnet.eu/xxx_wyciag_III |
| Beskid Żywiecki | Żywiec – Rynek 1 i 3 | odtwarzacz | stream360.pl/v/Zywiec1/index1.php, index3.php |
| Beskid Żywiecki | Żywiec – Rynek 2, Średni Grojec | odtwarzacz | player.webcamera.pl (zywiec_cam_f0027b, zywiec_cam_1ce519) |
| Gorce | Suchy Groń, Magurki, Lubań, Gorc | wideo HLS | ochotnica.epicserv.pl/streams/cam5, cam1, cam3, cam4 |
| Pieniny | Schronisko Trzy Korony – Sromowce Niżne | odtwarzacz | static.webcamera.pl … schroniskapieninskie_cam_fb73aa |
| Pieniny | Jezioro Czorsztyńskie i zamek | odtwarzacz | static.webcamera.pl … niedzica_cam_a6aff0 |
| Pieniny | Stara Lubowla | odtwarzacz Windy | webcams.windy.com, webcamId=1621786379 |

## Ustalenia z testów
- **TOPR:** stara strona kamery.topr.pl działa tylko przez http. Strona na https (np. GitHub Pages) by jej nie wczytała, dlatego używamy obrazów z nowej strony pogoda.topr.pl (https, 1024×576).
- **arkomnet** (Rysianka, WGmedia): strumienie działają poza stronami źródłowymi.
- **Ochotnica (epicserv):** serwer wpuszcza tylko wybrane strony (działało z rysianka.pl, było blokowane z zywiec.pl). **Do sprawdzenia po publikacji na GitHub Pages.**
- **webcamera.pl / stream360 / Windy:** odtwarzacze ładują się na innych stronach. stream360 wymaga kliknięcia, webcamera.pl ma swój baner.
- Strona Trzy Korony błędnie opisuje odtwarzacze. Jezioro Czorsztyńskie to `niedzica_cam_a6aff0`, a `czorsztynski_cam_*` to stok Czorsztyn Ski.

## Do zrobienia
- [ ] Wrzucić `index.html` na GitHub Pages i dodać skrót na ekran główny telefonu.
- [ ] Sprawdzić kamery z Gorców (epicserv) pod docelowym adresem.
- [ ] Opcjonalnie: godziny wschodu i zachodu słońca, prognoza przy regionach, archiwum kadrów (wymaga serwera).

## Uwagi prawne
Do prywatnego podglądu wszystko jest w porządku. Przed publicznym udostępnianiem strony warto sprawdzić regulaminy portali, bo niektóre zabraniają osadzania obrazu bez zgody.
