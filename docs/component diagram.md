# Component Diagram

## Purpose
Ten dokument opisuje wizualny model komponentów systemu oraz ich relacje.  
Stanowi graficzne uzupełnienie `architecture.md`, `modules.md` i `data-flow.md` — używany przez Architecture Agent, Refactor Agent i Pentest Agent do multi‑file reasoning.

---

## 1. High-level component diagram

```mermaid
flowchart TD
    U[User / External System] --> API[System Interface / Entry Point]

    API --> VAL[Validation Layer]
    VAL --> SAN[Sanitization Layer]
    SAN --> CORE[Core Module]

    CORE --> PROC[Processing Module]
    CORE --> ANALYSIS[Analysis Module]
    CORE --> SEC[Security Module]
    CORE --> LOG[Logging Module]
    CORE --> INTEGRATION[Integration Module]
    CORE --> PIPE[Pipeline / CI-CD Module]

    PROC --> ANALYSIS
    PROC --> INTEGRATION

    ANALYSIS --> SEC
    SEC --> LOG
    SEC --> PIPE

    PIPE --> OUT[Output / Responses / Artifacts]
    LOG --> OBS[Observability / Monitoring]
2. Component list
2.1 System Interface
Rola: punkt wejścia dla użytkownika i systemów zewnętrznych.

Odpowiedzialność: przyjmowanie żądań, przekazywanie ich do warstwy walidacji.

Powiązania: Validation Layer, Integration Module (dla webhooków/API).

2.2 Validation Layer
Rola: pierwsza linia obrony (zero‑trust).

Odpowiedzialność: schema/type/range/pattern validation.

Powiązania: Sanitization Layer, Security Module.

2.3 Sanitization Layer
Rola: oczyszczanie danych przed dalszym przetwarzaniem.

Odpowiedzialność: usuwanie niebezpiecznych znaków, normalizacja, strip HTML/JS.

Powiązania: Core Module, Logging Module.

2.4 Core Module
Rola: fundament systemu.

Odpowiedzialność: modele, utilsy, error handling, prymitywy walidacji/logowania.

Powiązania: wszystkie moduły funkcjonalne (Processing, Analysis, Security, Logging, Integration, Pipeline).

3. Functional components
3.1 Processing Module
Rola: główna logika biznesowa.

Odpowiedzialność: transformacje danych, workflowy, operacje domenowe.

Powiązania: Core, Analysis, Integration.

Granice: brak bezpośredniego logowania surowych danych, brak walidacji „na skróty”.

3.2 Analysis Module
Rola: analiza AI / heurystyczna.

Odpowiedzialność: wykrywanie wzorców, korelacja zdarzeń, scoring.

Powiązania: Core, Processing, Security, Logging.

Granice: tylko dane zwalidowane i zsanityzowane.

3.3 Security Module
Rola: mózg bezpieczeństwa.

Odpowiedzialność: walidacja zaawansowana, heurystyki pentestowe, scoring ryzyka.

Powiązania: Validation, Core, Logging, Pipeline.

Granice: nie modyfikuje logiki biznesowej, tylko ocenia i blokuje.

3.4 Logging Module
Rola: warstwa obserwowalności.

Odpowiedzialność: strukturalne logi, sanitizacja, standardy logowania.

Powiązania: wszystkie moduły, Security, Pipeline.

Granice: brak danych wrażliwych, brak surowych wejść.

3.5 Integration Module
Rola: komunikacja z zewnętrznymi API/systemami.

Odpowiedzialność: wywołania HTTP/API, mapowanie danych, obsługa błędów.

Powiązania: Core, Validation, Logging, Processing.

Granice: zawsze waliduje i sanitizuje odpowiedzi z zewnątrz.

3.6 Pipeline / CI-CD Module
Rola: automatyzacja, build, test, deploy.

Odpowiedzialność: pipeline’y, testy, audyty, artefakty.

Powiązania: Security, Logging, Core, repozytorium kodu.

Granice: brak logiki biznesowej, tylko orkiestracja.

4. Component interaction (sequence)
mermaid
sequenceDiagram
    participant U as User
    participant I as Interface
    participant V as Validation
    participant S as Sanitization
    participant C as Core
    participant P as Processing
    participant A as Analysis
    participant Sec as Security
    participant L as Logging
    participant Pipe as Pipeline
    participant O as Output

    U->>I: Request
    I->>V: Validate Input
    V->>S: Valid Data
    S->>C: Sanitized Data
    C->>P: Call Business Logic
    P->>A: Analysis Request
    A->>Sec: Security Evaluation
    Sec->>L: Security Log
    Sec->>Pipe: Security Event for CI/CD
    P->>O: Response Data
    O->>U: Response
5. Rules for component design
Brak cross‑module state sharing — komunikacja tylko przez jasno zdefiniowane API.

Walidacja na granicach — każdy komponent waliduje swoje wejścia.

Logowanie tylko przez Logging Module / Core.

Security Module nie zmienia logiki biznesowej, tylko ją ocenia/blokuje.

Pipeline nie wprowadza logiki domenowej, tylko orkiestruje.

Final notes
Ten diagram komponentów jest wizualnym „spoiwem” między architecture.md, modules.md i data-flow.md.
Każda zmiana architektury, modułów lub przepływów danych powinna być odzwierciedlona również tutaj, aby Copilot Agents miały zawsze aktualny obraz systemu.
