# CLAUDE.md — P2P 60-24 OneClick Evo
> Wersja: 4.0 · Sesja 15 · Dla agentów AI i deweloperów

## 0. INSTRUKCJA DLA AGENTA AI

Przed działaniem przeczytaj ten plik w całości.
To jest **jedyne źródło prawdy** o architekturze projektu.
Zmiany architektury = zmiany logiki — nie rozdzielaj tych pojęć.

---

## 1. ZASADY ABSOLUTNE

```
1. ZERO centralnego serwera
2. ZERO Docker / Kubernetes
3. UDP (P2P) + HTTP tylko fenotyp (:8024)
4. ZERO chmury
5. ZERO npm/pip/zewnętrznych dependencji
6. Minimalność ekologiczna
7. Fenotyp != Genotyp — prywatne NIGDY przez HTTP/logi
8. System SUGERUJE · Człowiek DECYDUJE (Governance)
```

---

## 2. STACK

```
Go 1.21+  ·  UDP :6024/:6025  ·  HTTP :8024
BadgerDB  ·  ed25519  ·  SHA256
Linux/macOS/ARM/Windows (bez zewnętrznych binarek)
```

---

## 3. STRUKTURA PLIKÓW (28 plików Go)

```
RDZEŃ:
  main.go              punkt wejścia · sekwencja startu VIII · flagi CLI
  node.go              Kernel #01: Node · PeerInfo · AccessThreshold
  db.go                BadgerDB wrapper · Get/Set/Delete/Scan/GC
  p2p.go               UDP gossip · ed25519 signing · broadcast · ping
  go.mod               moduł Go · tylko BadgerDB jako zewnętrzna dep

BEZPIECZEŃSTWO:
  trust.go             Kernel #17/#18 · TrustPeerEdge · InviteToken
  reputation.go        Kernel #06 · ReputationRecord · LOCAL_REP_WEIGHT=0.7
  governance.go        Kernel #09 · GovernanceRecord · 5 inwariantów · ed25519

LOGGER (sesja 15):
  logger.go            JSON logger · zero deps · ModuleLogger · HealthMetrics
                       EventConstants (18) · EmergenceLevel()

SYSTEM MODUŁÓW:
  module.go            Module interface · ModuleRegistry · PublicItem · Broadcast
  module_health.go     S/I/R/E · stability · 14 MergeSignals · tipping points
  module_base.go       BaseModule · DefaultModules() → 16 modułów
                       Announcements · LocalSupport · Ecology (pełne)
  module_catalog.go    22 manifesty · keywords · merge signals · OMF forms

MODUŁY DOMENOWE (8 plików):
  rod_module.go        działki · plony · prace
  health_module.go     fizjo/psycho/relax · zero PII pacjenta
  motors_module.go     BlaBlaCar P2P · RouteMatch · serwis
  education_module.go  korepetycje · barter wiedzy · warsztaty
  tasks_module.go      Kernel #07 · HPC lifecycle · blokada→wypłata
  gastronomy_module.go farm-to-table MergeSignal · przepisy · warsztaty
  sport_module.go      wydarzenia · grupy · sprzęt · find-partner
  remaining_modules.go ArtCulture · TechInnovation · RolAgra ·
                       Tourism · BauBud · Immobil

OMF (4 pliki):
  omf.go               Kernel #19: OMFAtom · 22 relacje · 4 stany · konstruktory
  omf_graph.go         OMFGraph · CrossMap (7 PL) · gossip · transitions
  omf_query.go         OMFEngine · Query · 35+ formularzy seed
  omf_field.go         OMFField · 4 stany · AliasResolver (kolor=color=barwa)

PODSYSTEMY:
  territorial.go       TerritorialOntology · 5 regionów · PL/EN/DE/UK
  inspiration_engine.go Warstwa 12 · joy_index · 12 wzorców · ZERO PRESJI
  sleep.go             SleepManager · watchdog · 30min idle threshold
  stemcell.go          Kernel #14-16: Epigenome · ModuleRole · ApoptosisConfig
  need.go              Kernel #03: NeedEntity · Post/Fulfill/ListOpen
  ogloszenie.go        Kernel #02: ServiceEntity · persistence layer

INTERFEJS HTTP:
  webnode.go           HTTP :8024 · SEO · /join · /modules · fenotyp
  webnode_api.go       /api/modules · /api/health · /api/status (JSON)

INSTALACJA:
  install.sh           Linux/macOS/ARM · systemd/launchd · firewall
  install.ps1          Windows · sc.exe · firewall rules
```

---

## 4. KERNEL — 19 STRUKTUR

```
#01 Node              node.go       ID · PubKey · Peers · Thresholds
#02 ServiceEntity     ogloszenie.go ogłoszenie/usługa w sieci
#03 NeedEntity        need.go       potrzeba węzła
#04 Relation          omf.go        OMFRelation (22 typy)
#05 FieldSignal       omf_field.go  OMFField · historia
#06 ReputationRecord  reputation.go score · local*0.7 + global*0.3
#07 Task              tasks_module  HPC lifecycle · blokada→wypłata
#08 EnergyLedger      module_health energy flow w stability formula
#09 GovernanceRecord  governance.go ed25519 signed · human-only
#10 NetworkState      node.go       PeerCount · Readiness
#11 CulturalEntity    omf.go        OMFAtom w domenie artculture
#12 SocialCognition   inspiration_engine joy_index · ZERO PRESJI
#13 SocialPhysics     module_health stability = match*0.6 + energy*0.4
#14 ModuleEpigenome   stemcell.go   trait expressions · generations
#15 ModuleRole        stemcell.go   producer|consumer|mediator|catalyst
#16 ApoptosisConfig   stemcell.go   min_stability · max_idle
#17 TrustPeerEdge     trust.go      score · signed · LastUpdate
#18 NodeAdmissionGate trust.go      RequireToken · MinReputation
#19 OMFAtom           omf.go        label · domain · 22 relacje · 4 stany
```

---

## 5. SEKWENCJA STARTU (dokument VIII)

```go
// main.go — kolejność OBOWIĄZKOWA:
db.Open()                           // 1
trustMgr.ValidateInviteToken()      // 2
p2p.Start()          // UDP :6024   // 3
sleepMgr.Start()     // watchdog    // 4
stemCell.Start()     // epigenome   // 5
registry.HealthMonitor.Start()      // 6  S/I/R/E monitor
registry.Activate(DefaultModules()) // 7  16 modułów
omfGraph.Start()                    // 8  graph+forms+transitions
inspiration.Start()                 // 9  Warstwa 12
web.Start()          // HTTP :8024  // 10 OSTATNI
```

---

## 6. OMF — ARCHITEKTURA

```
22 typy relacji: is_a · part_of · compatible_with · requires ·
  offered_by · needs · exchanged_for · lent_by · same_as ·
  opposite_of · caused_by · leads_to · used_for · located_in ·
  owned_by · created_by · belongs_to · similar_to · depends_on ·
  produced_from · transformed_to · associated_with

4 stany OMFAtom:
  WILD → EMERGING (≥5%)  → STABLE (≥20%) → CORE (≥50%+trust≥0.7)

AliasResolver:
  kolor = color = barwa = Farbe = colour → jeden OMFField

CrossMap (7 wbudowanych PL):
  eclass↔pkwiu dla: tynkowanie · stolarka · naprawa pojazdów ·
  uprawa zbóż · uprawa warzyw · korepetycje · gastronomia

35+ formularzy seed (omf_query.go seedForms)
```

---

## 7. 16 MODUŁÓW + DefaultModules()

```go
// module_base.go DefaultModules():
CORE (3):   announcements · localsupport · ecology
ŻYCIE (7):  rod · health · motors · education · tasks · gastronomy · sport
KULTURA (2): artculture · techinnovation
GOSPODARKA (4): rolagra · tourism · baubud · immobil
```

---

## 8. MONITOR EWOLUCYJNY (S/I/R/E)

```
stability = match(I↔R) * 0.6 + energyFlow * 0.4

≥ 0.60 → StateStable   (S) · replikuje się
0.30–0.59 → StateIll   (I) lub StateRecovery (R)
< 0.30 → CRITICAL      → Collapse|Adapt|Merge (wymaga podpisu)

14 MergeSignals (module_health.go KnownMergeSignals):
  rod+gastronomy → farm-to-table
  rod+health → wellness-garden
  motors+tasks → courier-local
  ... (14 łącznie)
```

---

## 9. GOVERNANCE — 5 INWARIANTÓW

```go
// governance.go
const (
    NoGlobalAdmin       = true   // brak globalnego admina
    DecisionRequireSign = true   // ed25519 dla każdej decyzji
    LocalRepWeight      = 0.7    // waga lokalnej reputacji
    EpochLengthBlocks   = 1000
    NoPIIOnChain        = true   // zero PII
)
```

---

## 10. PROGI DOSTĘPU (dokument IX)

```
peers ≥ 1          → gossip · LOCAL
peers ≥ 3          → task_access · HPC
peers ≥ 5 + rep≥0.3 → governance
rep ≥ 0.2          → wystawia InviteTokeny
rep ≥ 0.5          → CITY · GLOBAL · Immobil
rep ≥ 0.85         → genesis
```

---

## 11. HIERARCHIA EMERGENCJI

```
N-0: 1–20   N-1: 20–100   N-2: 100–300
N-3: 300+   → Vector Memory · AI Tutor · Emergence Engine
N-4: 1000+  N-5: 10 000+

network_readiness = (nodes/300) × (avg_peers/12) × (modules/20)
```

---

## 12. API ENDPOINTS (webnode_api.go)

```
GET /api/status   → {status, version, node_id}
GET /api/modules  → lista 16 modułów z S/I/R/E, stability, scope
GET /api/health   → metrics: peers, emergence, module_states, omf_atoms
                    HTTP 503 gdy status=critical
GET /api/         → SEO HTML fenotypu
GET /modules      → HTML lista modułów
GET /join         → JSON info jak dołączyć
```

---

## 13. ZASADY KODOWANIA

```
✓ Każda funkcja publiczna ma komentarz doc
✓ Brak PII w logach, DB, HTTP — weryfikuj każdy fmt.Sprintf
✓ thread-safe: sync.RWMutex lub sync/atomic
✓ Fallback na stderr w loggerze — nigdy nie blokuj systemu
✓ Deterministyczna kolejność (sort) w odpowiedziach API
✓ ed25519 podpisuje każdą decyzję governance
✓ CloseDB/Stop w defer — zawsze sprzątaj zasoby
✓ Zero zewnętrznych importów poza BadgerDB
```

---

## 14. CZEGO NIE ROBIĆ

```
✗ Nie eksponuj PrivKey, InviteToken przez HTTP
✗ Nie loguj danych pacjenta (health_module)
✗ Nie dodawaj centralnego serwera koordynującego
✗ Nie używaj Docker/npm/pip
✗ Nie pomijaj kolejności startu z dokumentu VIII
✗ Nie zmieniaj logiki bez zrozumienia impaktu na OMFAtom lifecycle
✗ Nie traktuj propozycji zewnętrznych LLM jako gotowych do wdrożenia
```

---

## 15. HISTORIA SESJI

```
Sesja 01–11: budowa rdzenia, P2P, modułów, OMF
Sesja 12:    OMFAtom (Kernel #19) · 22 relacje · 4 stany · formularze
Sesja 13:    cluster_test.go · WCAG dashboard spec · Ecology panel widget
Sesja 14:    ocena propozycji zewnętrznych (regresja odrzucona)
Sesja 15:    logger.go · webnode_api.go · pełne repo (28 plików) · verify.sh
```

---

*P2P 60-24 OneClick Evo · CLAUDE.md v4.0 · Sesja 15*
*~14 000 linii Go · 16 modułów · 19 struktur kernela · zero Docker*
