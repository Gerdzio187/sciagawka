===============================================================================
               ŚCIĄGAWKA: TERMINAL, SYSTEM LINUX ORAZ GIT
===============================================================================

-------------------------------------------------------------------------------
1. BUDOWA POLECENIA I POWŁOKA (SHELL)
-------------------------------------------------------------------------------
* Powłoka (Shell): Program interpretujący polecenia (np. sh, bash, zsh).
* Znak zachęty (Prompt):
    $  -> sesja zwykłego użytkownika
    #  -> sesja administratora (root)
* Anatomia polecenia: nazwa_polecenia [opcje] [argumenty]
    - Opcja: Zaczyna się od myślnika (np. -l). Można je łączyć (np. -l -a -> -la).
    - Argument: Wskazuje obiekt działania (np. nazwa pliku lub katalogu).
* ZASADA SPACJI: Wpisanie `ls-l` wywoła błąd "not found". Spacja rozdziela słowa!
* WIELKOŚĆ LITER: Linux ściśle rozróżnia wielkość liter (Plik.txt != plik.txt).
* type <nazwa> -> sprawdza typ polecenia (np. `type cd` -> shell builtin).


-------------------------------------------------------------------------------
2. NAWIGACJA PO SYSTEMIE PLIKÓW
-------------------------------------------------------------------------------
* Ścieżka bezwzględna: Zaczyna się od korzenia `/` (np. /home/student/zielnik).
* Ścieżka względna: Zaczyna się bez ukośnika (np. zielnik/laka).
* Znaki specjalne w ścieżkach:
    .   -> bieżący katalog
    ..  -> katalog nadrzędny (poziom wyżej)
    ~   -> katalog domowy użytkownika (/home/użytkownik)

POLECENIA NAWIGACYJNE:
  pwd                   - Wyświetla pełną ścieżkę bieżącego katalogu.
  cd <ścieżka>          - Zmienia katalog bieżący na wskazany.
  cd lub cd ~           - Powrót do katalogu domowego.
  cd -                  - Powrót do poprzednio odwiedzanego katalogu.


-------------------------------------------------------------------------------
3. LISTOWANIE ZAWARTOŚCI KATALOGU (ls)
-------------------------------------------------------------------------------
  ls                    - Wypisuje widoczną zawartość katalogu bieżącego.
  ls -F                 - Dodaje znaki typu na końcu nazwy (np. `/` = katalog).
  ls -a                 - Pokazuje WSZYSTKIE pliki (w tym ukryte z kropką `.`).
  ls -A                 - Pokazuje pliki ukryte (z wyłączeniem `.` oraz `..`).
  ls -l                 - Długi format (prawa, właściciel, rozmiar, data).
  ls -lh                - Długi format z rozmiarem w B/K/M/G.
  ls -ld <katalog>      - Pokazuje metadane samego katalogu.

SORTOWANIE W ls:
  ls -lS                - Sortuje wg rozmiaru (malejąco).
  ls -lt                - Sortuje wg czasu ostatniej modyfikacji (najnowsze).
  ls -lr                - Odwraca porządek sortowania (np. ls -lSr).


-------------------------------------------------------------------------------
4. TWORZENIE, EDYCJA I PODGLĄD PLIKÓW/KATALOGÓW
-------------------------------------------------------------------------------
TWORZENIE:
  mkdir <katalog>       - Tworzy nowy katalog.
  mkdir -p a/b/c        - Tworzy całą ścieżkę katalogów (w tym brakujące).
  touch <plik>          - Tworzy pusty plik (0 bajtów) lub odświeża datę.
  touch -d "YYYY-MM-DD HH:MM" <plik> - Ustawia konkretną datę modyfikacji.

PODGLĄD I ZAPIS TREŚCI:
  cat <plik>            - Wypisuje całą zawartość pliku na ekran.
  cat plik1 plik2       - Łączy i wypisuje zawartość kilku plików po kolei.
  echo "tekst"          - Wypisuje tekst w terminalu.
  echo -n "tekst"       - Wypisuje tekst bez znaku nowej linii na końcu.
  printf 'A\nB\n'       - Formatowane wypisywanie tekstu (z obsługą \n).

PRZEKIEROWANIE WYJŚCIA (>):
  echo "tekst" > plik.txt - Zapisuje tekst do pliku. 
                            UWAGA: Operator > NADPISUJE zawartość pliku!


-------------------------------------------------------------------------------
5. KOPIOWANIE, PRZENOSZENIE I USUWANIE
-------------------------------------------------------------------------------
KOPIOWANIE (cp):
  cp plik1 plik2        - Kopiuje plik1 pod nazwę plik2.
  cp plik1 plik2 kat/   - Kopiuje pliki do wskazanego katalogu.
  cp -r zrodlo cel      - KOPIOWANIE REKURENCYJNE katalogu z zawartością.

PRZENOSZENIE / ZMIANA NAZWY (mv):
  mv stara nowa         - Zmienia nazwę pliku lub katalogu.
  mv plik katalog/      - Przenosi plik do katalogu.

USUWANIE (rm, rmdir):
  UWAGA: W TERMINALU NIE MA KOSZA! USUWANIE JEST TRWAŁE!
  rm <plik>             - Usuwa zwykły plik.
  rm -r <katalog>       - REKURENCYJNIE usuwa katalog z zawartością.
  rm -rf <katalog>      - Wymusza usunięcie bez pytania i błędów.
  rmdir <katalog>       - Usuwa katalog WYŁĄCZNIE wtedy, gdy jest pusty.


-------------------------------------------------------------------------------
6. PRAWA DOSTĘPU W LINUKSIE (chmod)
-------------------------------------------------------------------------------
FORMAT ls -l (np. -rw-r--r--):
  Typ (-) | Właściciel (rw-) | Grupa (r--) | Inni (r--)

OPIS UPRAWNIEŃ:
  r (read, 4)    - Odczyt pliku / wyświetlenie listy w katalogu.
  w (write, 2)   - Edycja pliku / tworzenie i usuwanie w katalogu.
  x (execute, 1) - Uruchomienie programu / wejście do katalogu (cd).

TYPOWE TRYBY CYFROWE:
  644 (rw-r--r--) - Domyślny plik tekstowy.
  600 (rw-------) - Plik prywatny.
  755 (rwxr-xr-x) - Domyślny katalog / skrypt wykonywalny.
  700 (rwx------) - Katalog prywatny.

ZMIANA PRAW (chmod):
  chmod u+x skrypt.sh   - Dodaje bit wykonania dla właściciela.
  chmod go-rw plik.txt  - Zabiera odczyt i zapis grupie i innym.
  chmod 755 skrypt.sh   - Ustawia rwxr-xr-x.


-------------------------------------------------------------------------------
7. GIT — PRACA Z REPOZYTORIUM I GITHUBEM
-------------------------------------------------------------------------------
KONFIGURACJA (wykonujesz raz):
  git config --global user.name "Imię Nazwisko"
  git config --global user.email "email@example.com"
  git config --global init.defaultBranch main
  git config --global pull.rebase false

PODSTAWOWE POLECENIA:
  git clone <url>       - Pobiera repozytorium z serwera (RAZ na projekt).
  git status            - Pokazuje stan plików i poczekalni.
  git add .             - Dodaje wszystkie zmiany do poczekalni (staging).
  git commit -m "Opis"  - Zapisuje poczekalnię w historii lokalnej.
  git log --oneline     - Skrócona historia commitów (wyjście: q).

SYNCHRONIZACJA Z GITHUBEM:
  git push              - Wysyła lokalne commity na serwer.
  git push -u origin main - Pierwsze wysłanie nowej gałęzi na serwer.
  git pull              - Pobiera nowe commity z serwera i je scala.

CYKL PRACY:
  1. git status
  2. git pull
  3. [edycja plików]
  4. git add .
  5. git commit -m "opis"
  6. git push

TRYBY PLIKÓW W GIT:
  100644 -> zwykły plik
  100755 -> plik wykonywalny (po `chmod +x`)


-------------------------------------------------------------------------------
8. POMOC I DOKUMENTACJA
-------------------------------------------------------------------------------
  <polecenie> --help    - Wyświetla opis składni i opcji danej wersji.
  man <polecenie>       - Otwiera podręcznik ekranowy (manual page).
===============================================================================