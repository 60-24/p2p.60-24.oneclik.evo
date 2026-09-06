# P2P 60-24 OneClick Evo
## Support Circle — Kręgi Wsparcia Społecznego

**Status:** PROPOSED  
**Typ dokumentu:** Ideologia / zasada architektoniczna  
**Projekt:** P2P 60-24 OneClick Evo  
**Wersja:** 0.1  
**Data:** 2026-09-06

---

## 1. Cel

P2P 60-24 OneClick Evo powinien być nie tylko siecią komunikacji i wymiany informacji, ale również **infrastrukturą wzajemnego wsparcia ludzi**.

System ma pomagać ludziom być bliżej osób, którym ufają, oraz ułatwiać poproszenie o pomoc wtedy, gdy samodzielne działanie staje się trudne.

Podstawowa idea:

> **Technologia ma wzmacniać ludzką solidarność, a nie ją zastępować.**

---

## 2. Support Circle — Krąg Wsparcia

**Support Circle** to dobrowolnie zdefiniowany krąg osób, które mogą wzajemnie oferować sobie pomoc, kontakt, obecność lub wsparcie.

Krąg może być zbudowany z:

- najbliższej rodziny,
- partnera lub partnerki,
- przyjaciół,
- sąsiadów,
- opiekunów,
- innych zaufanych osób,
- szerszej lokalnej społeczności P2P.

Członkostwo w kręgu wynika z relacji i zgody człowieka, a nie z automatycznej klasyfikacji algorytmicznej.

---

## 3. Powiązanie z kręgami Dunbara

Model Support Circle może wykorzystywać koncepcję warstw relacji społecznych Dunbara jako praktyczny model organizacji sieci zaufania.

### Core — najbliższy krąg

Około 1–5 osób.

Osoby, do których można zwrócić się z ważną lub pilną prośbą o pomoc.

### Close — bliski krąg

Do około 15 osób.

Przyjaciele, rodzina i inne osoby pozostające w bliskiej relacji.

### Extended — rozszerzony krąg

Do około 50 osób.

Szersza sieć osób znanych i godnych zaufania.

### Community — społeczność

Szersza społeczność P2P, w której możliwe jest poszukiwanie pomocy poza osobistymi kręgami.

**Liczby są orientacyjne i nie powinny być traktowane jako sztywne limity techniczne.**

---

## 4. Support Circle a TrustGraph

Support Circle powinien być jednym z zastosowań istniejącej koncepcji **TrustGraph**.

TrustGraph nie powinien oznaczać wyłącznie reputacji.

Może opisywać również:

- zaufanie,
- bliskość relacji,
- gotowość do pomocy,
- wzajemność,
- dostępność,
- historię dobrowolnie udzielonego wsparcia,
- przynależność do określonego kręgu.

Przykładowe relacje:

```text
A --trusts--> B
A --close_to--> B
A --can_ask_for_help--> B
B --willing_to_help--> A
A --support_contact--> B
```

Relacja powinna być **kontekstowa, kierunkowa i możliwa do zmiany**.

---

## 5. Mechanizm „Potrzebuję pomocy”

Podstawowym mechanizmem operacyjnym może być prosty komunikat:

> **POTRZEBUJĘ POMOCY**

System może następnie:

1. skierować prośbę do najbliższego odpowiedniego kręgu,
2. sprawdzić dobrowolnie zadeklarowaną dostępność,
3. umożliwić osobom z kręgu odpowiedź,
4. w razie potrzeby rozszerzyć poszukiwanie na kolejny krąg,
5. zakończyć proces po uzyskaniu wystarczającej pomocy.

Model:

```text
CZŁOWIEK
   ↓
POTRZEBUJĘ POMOCY
   ↓
CORE
   ↓
CLOSE
   ↓
EXTENDED
   ↓
COMMUNITY
```

Nie oznacza to automatycznego ujawniania informacji wszystkim kolejnym warstwom.

Każdy kolejny poziom powinien być uruchamiany zgodnie z zasadami prywatności, zgody i minimalizacji informacji.

---

## 6. Najważniejsza zasada: zgoda

P2P 60-24 **nie powinien samodzielnie definiować człowieka jako słabego, chorego, bezradnego czy potrzebującego**.

System może jedynie reagować na:

- świadomą prośbę o pomoc,
- wcześniej zdefiniowaną relację wsparcia,
- dobrowolnie ustawione reguły,
- sygnały, na których wykorzystanie użytkownik wcześniej wyraził zgodę.

### Zasada

> **System może pomagać człowiekowi poprosić o pomoc. Nie powinien odbierać mu prawa do samodzielnego określania, kiedy tej pomocy potrzebuje.**

---

## 7. Wsparcie zamiast kontroli

Support Circle nie jest mechanizmem nadzoru.

Nie powinien służyć do:

- śledzenia człowieka,
- oceniania jego wartości,
- automatycznego tworzenia hierarchii społecznej,
- wymuszania pomocy,
- publicznego ujawniania problemów,
- budowania „punktacji słabości”.

Jego funkcją jest **ułatwianie dobrowolnej wzajemnej pomocy**.

---

## 8. Wzajemność

Wsparcie nie powinno być rozumiane wyłącznie jako relacja:

```text
silny → słaby
```

Lepszym modelem jest:

```text
człowiek ↔ człowiek
```

Każdy może w jednym momencie potrzebować pomocy, a w innym jej udzielać.

Dlatego wartość relacji nie powinna być uzależniona od bilansu:

> „ile dałeś” kontra „ile otrzymałeś”.

Pomoc może być nierównomierna w czasie.

---

## 9. Prywatność i minimalizacja informacji

Informacja o potrzebie pomocy powinna być przekazywana **tylko tym osobom, które muszą ją otrzymać, aby móc pomóc**.

Domyślna zasada:

> **Minimum informacji → maksimum użytecznego wsparcia.**

Przykładowo zamiast udostępniać szczegóły problemu:

```text
„Anna potrzebuje dziś kontaktu i pomocy.”
```

można przekazać:

```text
„Anna prosi o kontakt.”
```

Szczegóły pozostają pomiędzy osobami, których dotyczą.

---

## 10. Brak uzależnienia od jednego człowieka

Jedna osoba nie powinna być jedynym elementem całego systemu wsparcia.

Jeżeli członek Core jest niedostępny, system może — za zgodą użytkownika — poszukać alternatywy w Close lub Extended.

Model:

```text
        CORE
      /  |       A   B   C
         |
       CLOSE
      /  |       D   E   F
```

W ten sposób sieć może zwiększać odporność społeczną bez tworzenia jednego „opiekuna centralnego”.

---

## 11. Relacja z Trust Infrastructure

Support Circle powinien być częścią szerszej **Trust Infrastructure** projektu.

Można wyróżnić:

```text
Trust Infrastructure
│
├── Identity Trust
├── Relationship Trust
├── Social Trust
├── Support Circle
├── TrustGraph
└── Community Trust
```

Trust nie jest tutaj walutą.

Nie powinien być kupowany, wydobywany ani zamieniany na token.

Jest właściwością relacji społecznych, budowaną przez rzeczywiste interakcje, doświadczenie i dobrowolne potwierdzenie.

---

## 12. Granice systemu

Support Circle nie jest:

- służbą ratunkową,
- systemem medycznym,
- terapeutą,
- opiekunem prawnym,
- systemem przymusu,
- zamiennikiem profesjonalnej pomocy.

W sytuacjach wymagających profesjonalnej lub natychmiastowej interwencji system powinien ułatwiać dotarcie do właściwej pomocy, a nie próbować jej zastępować.

---

## 13. Zasada ideologiczna P2P 60-24

Proponowana zasada do Constitution:

> **P2P 60-24 OneClick Evo powinien wzmacniać naturalne sieci ludzkiego wsparcia. Każdy człowiek powinien mieć możliwość dobrowolnego utworzenia własnego kręgu zaufanych osób, zwrócenia się do niego o pomoc oraz — w miarę możliwości — udzielenia pomocy innym. Technologia ma ułatwiać kontakt, nie zastępować człowieka.**

---

## 14. Zasada „nikt nie musi być sam”

Docelową ideą tej części projektu jest:

> **Jeżeli człowiek potrzebuje pomocy, powinien mieć możliwość łatwego dotarcia do ludzi, którym ufa.**

Nie oznacza to obietnicy, że pomoc zawsze będzie dostępna.

Oznacza stworzenie infrastruktury, która **zmniejsza barierę pomiędzy potrzebą a drugim człowiekiem**.

---

## 15. Status koncepcyjny

Ten dokument jest **propozycją ideologiczną i architektoniczną**.

Nie definiuje jeszcze:

- konkretnego protokołu,
- schematu danych,
- API,
- algorytmu wyboru kontaktów,
- mechanizmu eskalacji,
- interfejsu użytkownika.

Te elementy powinny zostać zaprojektowane dopiero po zaakceptowaniu zasady przez człowieka.

### Następny etap

Po akceptacji:

**Support Circle → model ontologiczny → relacje TrustGraph → scenariusze → wymagania → testy → implementacja.**
