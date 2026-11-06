# SportBook — Architektura Procesowa BPMN 2.0

> **Projekt inżynierski:** _Zastosowanie BPMN do identyfikacji i ograniczania ryzyka w projektach informatycznych_  
> **Status:** 🟡 W trakcie realizacji  
> **Uczelnia:** Uniwersytet Komisji Edukacji Narodowej w Krakowie (Instytut Bezpieczeństwa i Informatyki)

---

## 📌 O projekcie

Projekt poświęcony jest analizie, modelowaniu oraz optymalizacji procesów biznesowych i technicznych w systemie **SportBook** — platformie służącej do rezerwacji infrastruktury sportowej (korty, hale, boiska) oraz zarządzania grafikami obiektów[cite: 2, 3].

Głównym celem inżynierskim jest **identyfikacja punktów krytycznych, wąskich gardeł oraz podatności na awarie**, a następnie zaprojektowanie mechanizmów ich mitygacji w notacji BPMN 2.0 przy użyciu:

- wydzielonych kanałów obsługi zdarzeń awaryjnych (_Incident Management_)[cite: 1, 3],
- procesów uzgadniania spójności danych i rozliczeń finansowych (_Data & Financial Reconciliation_)[cite: 1, 3],
- przejścia z procesów manualnych (stan wyjściowy **AS-IS**) do zautomatyzowanych reguł decyzyjnych (stan docelowy **TO-BE**)[cite: 2].

---

## 🏗️ Architektura procesów

System został zdekomponowany na 6 niezależnych domen procesowych (pule typu _Black-Box_), połączonych asynchronicznymi przepływami komunikatów (_Message Flows_)[cite: 1, 3]:

| Identyfikator | Nazwa procesu                       | Rola w systemie                                                                              | Status                                   |
| :------------ | :---------------------------------- | :------------------------------------------------------------------------------------------- | :--------------------------------------- |
| **P1**        | Rezerwacje i anulowania[cite: 1, 3] | Główny obieg klienta: wybór terminu, blokowanie slotu, obsługa anulacji[cite: 1, 3]          | 🟡 W toku (draft AS-IS)                  |
| **P2**        | Płatności i zwroty[cite: 1, 3]      | Integracja z zewnętrznymi bramkami płatniczymi, zwroty środków[cite: 1, 3]                   | 🟡 W toku (draft AS-IS)                  |
| **P3**        | Zarządzanie obiektami[cite: 1, 3]   | Konfiguracja parametrów obiektów, grafików i cenników przez zarządców[cite: 1, 2, 3]         | 🟢 Zakończone (AS-IS)[cite: 2]           |
| **P4**        | Obsługa incydentów[cite: 1, 3]      | Centralny punkt odbioru zgłoszeń awarii, błędów płatności i kolizji terminów[cite: 1, 3]     | 🟢 Zakończone (Architektura)[cite: 1, 3] |
| **P5**        | Przywracanie danych[cite: 1, 3]     | Procedury Disaster Recovery oraz uzgadnianie spójności baz danych i sald[cite: 1, 3]         | 🟢 Zakończone (Architektura)[cite: 1, 3] |
| **P6**        | Zmiana terminu[cite: 1, 3]          | Bezpieczna transakcyjnie modyfikacja slotów rezerwacji bez ryzyka utraty terminu[cite: 1, 3] | 🟢 Zakończone (Architektura)[cite: 1, 3] |

---

## 📁 Struktura repozytorium

```text
├── diagrams/                          # Pliki źródłowe modeli BPMN 2.0 (XML)
│   ├── schemat_procesow.bpmn          # Główny diagram współpracy P1–P6
│   ├── SportBook_P3_AS_IS.bpmn        # Szczegółowy model AS-IS zarządzania obiektami[cite: 2]
│   └── drafts/                        # Robocze wersje dekompozycji P1 i P2[cite: 1, 3]
├── docs/                              # Dokumentacja projektu i raporty
│   ├── raport_nr_1/                   # Raport za okres 23.10.2026 – 06.11.2026 (kod LaTeX + PDF)
│   └── images/                        # Eksporty diagramów (PNG/SVG) na potrzeby dokumentacji
└── README.md
```
