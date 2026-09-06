# START_NOWEJ_SESJI.md

## P2P 60-24 OneClick EVO

**Data:** 2026-09-06  
**Status:** KAMIEŃ ZNACZNIK — FUNDAMENT KONCEPCYJNY  
**Wersja:** 0.1

---

## 1. Główna idea

P2P 60-24 ma stworzyć prosty i przyjazny sposób wejścia człowieka do nowego świata P2P.

Dla użytkownika:

**Pobierz → zezwól → kliknij → gotowe.**

Technologia może być bardzo zaawansowana wewnątrz, ale dla człowieka ma pozostać prosta.

---

## 2. Fundament systemu

Podstawą bezpieczeństwa nie jest sam algorytm.

Podstawą jest **człowiek, relacja i doświadczenie**.

Każda osoba ma wokół siebie najbliższy krąg około **5–6 osób**, którym rzeczywiście ufa.

Może zaprosić te osoby do systemu i przekazać im swoje zaufanie/rekomendację na podstawie własnego doświadczenia.

To jest pierwszy krok budowy sieci zaufania.

---

## 3. Dwa światy bezpieczeństwa

### Świat realny

```text
CZŁOWIEK
  ↓
RELACJA OSOBISTA
  ↓
DOŚWIADCZENIE
  ↓
ZAUFANIE
```

### Świat wirtualny

```text
TOŻSAMOŚĆ
  ↓
RELACJA
  ↓
REKOMENDACJA
  ↓
REPUTACJA
  ↓
ZAUFANIE
  ↓
AUTORYTET
  ↓
DOSTĘP / UPRAWNIENIE
```

**Świat wirtualny jest rozszerzeniem świata realnego, a nie jego zamiennikiem.**

---

## 4. Łańcuch zaufania

```text
DOŚWIADCZENIE
      ↓
ZAUFANIE
      ↓
REKOMENDACJA
      ↓
REPUTACJA
      ↓
PRZEKAZANIE ZAUFANIA
      ↓
AUTORYZACJA
      ↓
DOSTĘP
```

Najważniejsza zasada:

> **Reputacja musi mieć pochodzenie.**

System powinien móc odpowiedzieć:

- Kto przekazał zaufanie?
- Komu?
- Na jakiej podstawie?
- W jakim zakresie?
- Czy zaufanie nadal obowiązuje?

---

## 5. Prawda

Robocza definicja:

> **Prawda systemu to możliwy do prześledzenia zapis pochodzenia relacji, doświadczeń, rekomendacji i przekazanego zaufania.**

System nie powinien sam tworzyć „prawdy o człowieku”.

Powinien zapisywać **pochodzenie informacji i zaufania**.

Ważne:

**Reputacja ≠ prawda absolutna.**  
**Reputacja = dowody i historia relacji.**

---

## 6. Najważniejsze rozróżnienia

- **Tożsamość** — kim jest wirtualny uczestnik.
- **Uwierzytelnienie** — dowód tożsamości.
- **Relacja** — połączenie między osobami/węzłami.
- **Zaufanie** — poziom zaufania w konkretnej relacji i kontekście.
- **Reputacja** — historia i dowody wcześniejszych relacji/działań.
- **Autorytet** — przyznane uprawnienie do określonego działania.
- **Governance** — zasady przyznawania i odbierania autorytetu.

**Uwierzytelnienie ≠ zaufanie.**  
**Reputacja ≠ autorytet.**  
**Autorytet jest kontekstowy i może zostać cofnięty.**

---

## 7. Pierwszy Krąg Zaufania

Wzorzec:

```text
                    JA
                     │
          ┌──────────┼──────────┐
          ↓          ↓          ↓
       ZAUFANY     ZAUFANY    ZAUFANY
          │          │          │
          └──── około 5–6 ──────┘
                     │
              PRZEKAZANIE ZAUFANIA
                     ↓
                  REPUTACJA
```

Liczba 5–6 jest **wzorcem społecznym**, a nie sztywnym limitem protokołu.

Później można rozszerzać model o kolejne kręgi Dunbara.

---

## 8. Kręgi Dunbara — kierunek

```text
JA
 ↓
NAJBLIŻSI ~5–6
 ↓
BLISKI KRĄG ~15
 ↓
ROZSZERZONY KRĄG ~50
 ↓
SZERSZA SPOŁECZNOŚĆ ~150+
```

Wartości są orientacyjne. Nie powinny być automatycznie twardymi limitami technicznymi.

---

## 9. Zasady ochronne

1. Zaufanie jest relacyjne, nie uniwersalne.
2. Przekazane zaufanie ma zakres.
3. Zaufanie można cofnąć.
4. Autorytet jest kontekstowy.
5. Cyfrowa reputacja nie może automatycznie dowodzić relacji osobistej.
6. Prywatność i zgoda są podstawą.
7. System nie powinien tworzyć nadzoru nad ludźmi.
8. Nie ma jednej centralnej instancji, która decyduje, komu ufać.

---

## 10. Aktualny model P2P 60-24

```text
REAL WORLD
    │
    │ osobista relacja
    ↓
TRUST
    │
    │ rekomendacja
    ↓
REPUTATION
    │
    │ przekazanie
    ↓
VIRTUAL IDENTITY
    │
    ↓
AUTHORITY
    │
    ↓
ACCESS
    │
    ↓
P2P NODE
```

To łączy wcześniejszą architekturę techniczną z nową ontologią zaufania.

---

## 11. Stan projektu — kamień znacznik

### USTALONE

- OneClick jest wymaganiem architektonicznym.
- Minimalny cel techniczny: komunikacja dwóch niezależnych węzłów.
- System jest P2P, bez centralnego koordynatora.
- Tożsamość, transport, protokół, stan, zaufanie i autorytet są osobnymi pojęciami.
- Bezpieczeństwo ma wymiar techniczny i społeczny.
- Pierwszy krąg zaufania opiera się na realnych relacjach i doświadczeniu.
- Reputacja musi mieć pochodzenie.
- Zaufanie może być przekazywane i cofane.
- Autorytet jest ograniczony kontekstem.

### NASTĘPNY OBSZAR DO ZDEFINIOWANIA

**Model Pierwszego Kręgu Zaufania:**

- zaproszenie,
- przekazanie zaufania,
- zakres zaufania,
- zapis pochodzenia,
- cofnięcie zaufania,
- przejście od realnej relacji do wirtualnego uprawnienia.

---

## 12. Dokumenty źródłowe

- `docs/ontology/CORE_ONTOLOGY.md`
- `docs/architecture/SYSTEM_ARCHITECTURE.md`
- `docs/protocol/P2P_PROTOCOL_v0.1.md`
- `docs/engineering/REQUIREMENTS_v0.1.md`
- `docs/data/DATA_MODEL_v0.1.md`
- `docs/security/SECURITY_MODEL_v0.1.md`
- `P2P_60-24_Support_Circle.md`

Ten plik jest **punktem startowym następnej sesji** i streszcza aktualny stan koncepcyjny.
