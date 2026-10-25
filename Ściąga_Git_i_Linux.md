===============================================================================
                       ŚCIĄGA: GIT & LINUX TERMINAL
===============================================================================

-------------------------------------------------------------------------------
1. GIT — KONFIGURACJA POCZĄTKOWA
-------------------------------------------------------------------------------
Te polecenia wykonujesz raz po instalacji Gita na swoim koncie:

  git config --global user.name "Imię Nazwisko"
  git config --global user.email "email@example.com"
  git config --global init.defaultBranch main
  git config --global pull.rebase false

* Podgląd wszystkich ustawień:  cat ~/.gitconfig
* Ustawienia tylko dla 1 repo:  git config user.name "Inne Imie" (bez --global)


-------------------------------------------------------------------------------
2. GIT — TRZY OBSZARY I PRZEPŁYW PRACY
-------------------------------------------------------------------------------
  [Katalog roboczy]  --- git add --->  [Poczekalnia / Index]
  (pliki na dysku)                       (przygotowane do zapisu)
                                                   |
                                              git commit
                                                   |
                                                   v
  [Serwer GitHub]   <--- git push ---  [Repozytorium Lokalne]
  (origin/main)                          (historia w katalogu .git)


-------------------------------------------------------------------------------
3. GIT — PODSTAWOWE POLECENIA
-------------------------------------------------------------------------------
* git clone <adres_repo>    - Pobiera repozytorium z serwera (robi się RAZ!).
* git status                - Pokazuje stan plików (zawsze warto sprawdzić).
* git add <plik>            - Dodaje konkretny plik do poczekalni.
* git add .                 - Dodaje WSZYSTKIE nowe i zmienione pliki.
* git commit -m "Opis"     - Zapisuje poczekalnię w historii repozytorium.
* git log --oneline         - Wyświetla skróconą historię commitów (wyjście: q).


-------------------------------------------------------------------------------
4. GIT — SYNCHRONIZACJA Z SERWEREM (GITHUB)
-------------------------------------------------------------------------------
* git push                  - Wysyła lokalne commity na serwer.
* git push -u origin main   - Pierwsze wysłanie nowej gałęzi (łączy z origin).
* git pull                  - Pobiera nowe commity z serwera i scala je z Twoimi.

CYKL PRACY W ZESPOLE / NA POLECENTACH:
  1. git status          (sprawdź czy katalog jest czysty)
  2. git pull            (pobierz pracę innych przed rozpoczęciem własnej)
  3. [edycja plików]
  4. git add .           (dodaj zmiany)
  5. git commit -m "..." (zapisz wersję)
  6. git push            (wyślij na serwer)

ODRZUCONY PUSH (REJECTED / FETCH FIRST):
  Jeśli ktoś wysłał pracę przed Tobą, Twój `git push` zostanie odrzucony.
  Rozwiązanie: Wykonaj `git pull` -> zapisz komunikat scalenia (Ctrl+O, Ctrl+X w nano) -> wykonaj `git push`.


-------------------------------------------------------------------------------
5. LINUX — PRAWA DOSTĘPU (PERMISSIONS)
-------------------------------------------------------------------------------
ATRYBUTY W `ls -l` (np. -rw-r--r--):
  Typ | Właściciel (u) | Grupa (g) | Inni (o)
   -       r w -          r - -       r - -

OPIS UPRAWNIEŃ:
  Prawo          | Dla pliku                    | Dla katalogu
  ---------------+------------------------------+----------------------------
  r (read, 4)    | Odczyt treści pliku          | Wyświetlenie listy plików
  w (write, 2)   | Zmiana treści pliku          | Tworzenie/usuwanie plików
  x (execute, 1) | Uruchomienie jako program    | Wejście do katalogu (cd)

TYPOWE TRYBY CYFROWE (chmod):
  * 644 (rw-r--r--) - Domyślny plik: właściciel edytuje, reszta czyta.
  * 600 (rw-------) - Plik prywatny: tylko właściciel ma dostęp.
  * 755 (rwxr-xr-x) - Domyślny katalog lub skrypt wykonywalny.
  * 700 (rwx------) - Katalg/program prywatny dla właściciela.

ZAMIANA ZAPISU (chmod):
  * Zapis symboliczny (literowy):
      chmod u+x skrypt.sh     -> dodaje prawo wykonania dla właściciela
      chmod go-rw plik.txt    -> zabiera odczyt i zapis grupie i innym
  * Zapis cyfrowy (bezwzględny):
      chmod 755 skrypt.sh     -> ustawia rwxr-xr-x
      chmod 600 tajne.txt     -> ustawia rw-------


-------------------------------------------------------------------------------
6. LINUX — SKRYPTY BASH
-------------------------------------------------------------------------------
1. Pierwsza linia (Shebang):
   #!/bin/bash

2. Komentarze:
   Linie zaczynające się od # są ignorowane przez powłokę.

3. Nadanie praw i uruchomienie:
   chmod +x moj_skrypt.sh     -> nadaje bit wykonywalności (x)
   ./moj_skrypt.sh            -> uruchamia skrypt w bieżącym katalogu

   (Uruchomienie przez `bash moj_skrypt.sh` nie wymaga prawa +x ani shebanga).

4. Warto pamiętać:
   * Skrypt uruchamia się w OSOBNYM procesie — zmiana katalogu (`cd`)
     wewnątrz skryptu NIE ZMIENI Twojego katalogu po jego zakończeniu.
   * Git śledzi z praw dostępu TYLKO bit wykonywalności:
     100644 = zwykły plik | 100755 = plik wykonywalny (+x)

===============================================================================