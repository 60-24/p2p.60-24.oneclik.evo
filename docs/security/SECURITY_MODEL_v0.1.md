# P2P 60-24 OneClick EVO — Security Model v0.1

**Status:** PROPOSED / PRE-CODING  
**Version:** 0.1

## 1. Cel

Zdefiniować minimalne granice bezpieczeństwa dla pierwszego Minikernelu P2P: dwóch niezależnych Node'ów, które potrafią się rozpoznać, nawiązać komunikację i wymienić zweryfikowane wiadomości.

## 2. Zasady bezpieczeństwa

1. Tożsamość prywatna pozostaje lokalnie na Node.
2. Każda wiadomość protokołu musi przejść walidację.
3. Nieznany Peer nie jest automatycznie zaufany.
4. Błędny pakiet nie może zakończyć procesu Node.
5. Bezpieczeństwo nie może zależeć od AI.
6. System działa bez centralnego serwera bezpieczeństwa.
7. Użytkownik OneClick nie powinien konfigurować technicznych mechanizmów bezpieczeństwa, jeśli można je wykonać automatycznie.

## 3. Najważniejsze zagrożenia v0.1

- sfałszowana wiadomość,
- zmodyfikowana wiadomość,
- ponowne wysłanie starej wiadomości (replay),
- niepoprawny lub zbyt duży pakiet,
- podszywanie się pod inny Node,
- niezgodność Node ID z kluczem publicznym,
- podstawowy flood pakietów UDP,
- ujawnienie klucza prywatnego w logach, HTTP lub komunikacji P2P.

## 4. Mechanizmy ochronne

### 4.1 Tożsamość

Node posiada lokalną tożsamość kryptograficzną opartą o Ed25519.

**Klucz prywatny:** nigdy nie opuszcza Node.  
**Klucz publiczny:** może być przekazywany w ramach protokołu.

Node ID musi być jednoznacznie związany z przyjętą definicją tożsamości.

### 4.2 Podpis wiadomości

Wiadomości są podpisywane przez nadawcę i weryfikowane przez odbiorcę.

Podpis zapewnia przede wszystkim:
- autentyczność źródła,
- integralność danych.

**Ed25519 nie zapewnia szyfrowania.** Nie wolno nazywać samego podpisu „bezpiecznym kanałem”.

### 4.3 Świeżość i replay

Każda wiadomość musi posiadać mechanizm pozwalający wykryć ponowne użycie starej wiadomości, np. Message ID/nonce oraz informację o świeżości.

Dokładne okno czasowe i sposób przechowywania wykorzystanych identyfikatorów pozostają decyzją projektową przed implementacją.

### 4.4 Walidacja protokołu

Odbiorca sprawdza co najmniej:

- wersję protokołu,
- typ wiadomości,
- nadawcę i odbiorcę,
- podpis,
- świeżość,
- stan połączenia,
- rozmiar danych.

Niepoprawna wiadomość jest odrzucana.

## 5. Ważne rozróżnienie

```text
AUTHENTICATION ≠ AUTHORIZATION ≠ TRUST ≠ ENCRYPTION
```

- **Authentication** — kim jest nadawca?
- **Authorization** — co wolno mu zrobić?
- **Trust** — jaki poziom zaufania przypisujemy Peerowi?
- **Encryption** — kto może odczytać dane?

Te pojęcia nie mogą być łączone w jeden mechanizm.

## 6. Trust

Podstawowa zasada:

> KNOWN ≠ TRUSTED

Samo poznanie klucza publicznego lub adresu Peer'a nie oznacza zaufania.

Rozbudowany TrustGraph, reputacja i governance są poza zakresem Minikernelu v0.1.

## 7. Prywatność

Domyślna zasada:

> Jeśli informacja nie musi opuścić Node, nie opuszcza Node.

Nie wolno umieszczać kluczy prywatnych ani danych wrażliwych w:
- logach,
- publicznym HTTP,
- komunikacji P2P bez wyraźnej potrzeby,
- komunikatach błędów.

HTTP pozostaje warstwą phenotype i nie może stać się ukrytym kanałem wycieku prywatnego stanu.

## 8. Zachowanie w przypadku błędu

Node musi bezpiecznie obsługiwać:

- błędny podpis → odrzuć,
- zmienioną wiadomość → odrzuć,
- replay → odrzuć,
- zły format → odrzuć,
- zbyt duży pakiet → odrzuć,
- nieznanego Peer'a → zachowaj zdefiniowaną politykę, bez automatycznego zaufania,
- timeout → obsłuż bez awarii procesu.

**Błąd danych wejściowych nie może powodować crash Node.**

## 9. OneClick

Bezpieczeństwo jest częścią architektury OneClick.

Użytkownik powinien widzieć prosty rezultat:

`START → READY → CONNECTED`

Techniczne operacje — generowanie tożsamości, podpisy, walidacja, timeouty i ochrona stanu — powinny być wykonywane wewnętrznie.

## 10. Niezmienniki bezpieczeństwa

1. Klucz prywatny nigdy nie opuszcza Node.
2. Niezweryfikowana wiadomość nie może być uznana za poprawną wiadomość protokołu.
3. Niepoprawny pakiet nie może wyłączyć Node.
4. `KNOWN ≠ TRUSTED`.
5. Dane wrażliwe nie trafiają do logów ani publicznego HTTP.
6. Nie deklarujemy szyfrowania, dopóki mechanizm szyfrowanego kanału nie zostanie osobno zaprojektowany i zweryfikowany.

## 11. Otwarte decyzje przed implementacją

- sposób bezpiecznego przechowywania klucza prywatnego,
- dokładna definicja Node ID,
- okno świeżości wiadomości,
- mechanizm replay cache,
- protokół szyfrowanego kanału,
- polityka autoryzacji Peerów,
- podstawowe ograniczenie flood/rate limiting.

**Nie wolno rozstrzygać tych punktów przypadkowo w kodzie.**

## 12. Minimalne testy akceptacyjne

Minikernel powinien potwierdzić, że:

1. poprawnie podpisana wiadomość jest przyjęta,
2. zmodyfikowana wiadomość jest odrzucona,
3. wiadomość podpisana innym kluczem jest odrzucona,
4. replay jest odrzucony,
5. błędny format nie powoduje crash Node,
6. zbyt duży pakiet jest odrzucony,
7. zachowanie wobec nieznanego Peer'a jest zgodne z polityką,
8. klucz prywatny nie pojawia się w logach ani HTTP,
9. timeout nie powoduje awarii procesu.

## 13. Zakres poza v0.1

- pełny TrustGraph,
- reputacja i ekonomia,
- governance/DAO,
- AI podejmujące decyzje,
- Support Circle jako protokół,
- autonomiczna ewolucja,
- zaawansowany discovery,
- pełny system szyfrowania.

## 14. Następny krok

`docs/resilience/FAILURE_RESILIENCE_MODEL_v0.1.md`

Najpierw określamy, **jak Node ma zachować się podczas awarii, utraty pakietów, restartu i błędów Peer'a**.

**Nie kodujemy jeszcze.**