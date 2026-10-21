# Kody ICD-9 do skierowań

Wyszukiwarka kodów procedur ICD-9 PL (słownik NFZ) do wpisywania na skierowaniach.
Lekarz otwiera link do strony, wpisuje np. „usg tarczycy” i dotyka kodu, żeby go skopiować.

Adres strony: `https://TWOJ-LOGIN.github.io/kody-icd9/`

## Jak to działa

- Cała aplikacja to zwykła strona (`index.html`) i plik ze słownikiem (`data/icd9.json`).
- Po pierwszym otwarciu strona zapisuje się w telefonie i działa także bez internetu.
- Codziennie rano automat GitHub (zakładka **Actions**) sprawdza stronę NFZ. Gdy jest nowa wersja słownika,
  pobiera ją, sprawdza i publikuje na stronie.
- Aplikacja nie ma przycisku sprawdzania i nie wysyła zapytań o aktualność. Przy publikacji automat wpisuje w stronę
  datę i godzinę ostatniego sprawdzenia oraz nazwę najnowszego pliku z NFZ, a aplikacja pokazuje je na dole:
  „Baza sprawdzona: … Ostatnia nazwa pliku na stronie NFZ: …”.
- Gdy strona zawiera nowszą wersję niż ta zapisana w telefonie, aplikacja pobiera ją sama, tylko wtedy.
- Źródło danych: [słownik ICD-9 PL CM na nfz.gov.pl](https://www.nfz.gov.pl/dla-swiadczeniodawcy/slowniki/pliki-icd-9-pl/).

## Gdy automat nie może pobrać pliku z NFZ

Zakładka Actions pokaże czerwony znaczek, a GitHub wyśle e-mail. Strona dalej działa na dotychczasowych kodach.
Wtedy dodaj plik ręcznie: instrukcja jest w pliku `incoming/CZYTAJ.txt`.

## Ręczne uruchomienie sprawdzenia

Zakładka **Actions** → **Aktualizacja kodów NFZ i publikacja strony** → **Run workflow**.

## Pliki

| Plik | Do czego służy |
| --- | --- |
| `index.html` | cała aplikacja |
| `data/icd9.json` | słownik (10 059 kodów w wersji 5.90) |
| `data/meta.json` | numer wersji i data ostatniego sprawdzenia NFZ |
| `sw.js`, `manifest.webmanifest`, ikony | instalacja na telefonie i praca bez internetu |
| `scripts/update.py`, `scripts/convert.py` | pobranie i przekonwertowanie słownika z NFZ |
| `.github/workflows/update.yml` | harmonogram automatu i publikacja strony |
| `incoming/` | awaryjne, ręczne wgranie pliku z NFZ |

Kod zawsze dobiera lekarz. Aplikacja tylko ułatwia znalezienie kodu w słowniku NFZ.
