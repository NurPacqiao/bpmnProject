# SportBook — Architektura Procesowa BPMN 2.0

> **Projekt inżynierski:** _Zastosowanie BPMN do identyfikacji i ograniczania ryzyka w projektach informatycznych_  
> **Status:** 🟡 W trakcie realizacji  
> **Uczelnia:** Uniwersytet Komisji Edukacji Narodowej w Krakowie (Instytut Bezpieczeństwa i Informatyki)

---

## 📌 O projekcie

Projekt poświęcony jest analizie, modelowaniu oraz optymalizacji procesów biznesowych i technicznych w systemie **SportBook** — platformie służącej do rezerwacji infrastruktury sportowej (korty, hale, boiska) oraz zarządzania grafikami obiektów.

Głównym celem inżynierskim jest **identyfikacja punktów krytycznych, wąskich gardeł oraz podatności na awarie**, a następnie zaprojektowanie mechanizmów ich mitygacji w notacji BPMN 2.0 przy użyciu:

- wydzielonych kanałów obsługi zdarzeń awaryjnych (_Incident Management_),
- procesów uzgadniania spójności danych i rozliczeń finansowych (_Data & Financial Reconciliation_),
- przejścia z procesów manualnych (stan wyjściowy **AS-IS**) do zautomatyzowanych reguł decyzyjnych (stan docelowy **TO-BE**).

---

## 🏗️ Architektura procesów

System został zdekomponowany na 6 niezależnych domen procesowych (pule typu _Black-Box_), połączonych asynchronicznymi przepływami komunikatów (_Message Flows_):

| Identyfikator | Nazwa procesu                       | Rola w systemie                                                                              | Status                                   |
| :------------ | :---------------------------------- | :------------------------------------------------------------------------------------------- | :--------------------------------------- |
| **P1**        | Rezerwacje i anulowania | Główny obieg klienta: wybór terminu, blokowanie slotu, obsługa anulacji   | 🟡 W toku (draft AS-IS)                  |
| **P2**        | Płatności i zwroty     | Integracja z zewnętrznymi bramkami płatniczymi, zwroty środków             | 🟡 W toku (draft AS-IS)                  |
| **P3**        | Zarządzanie obiektami   | Konfiguracja parametrów obiektów, grafików i cenników przez zarządców        | 🟢 Zakończone (AS-IS)           |
| **P4**        | Obsługa incydentów      | Centralny punkt odbioru zgłoszeń awarii, błędów płatności i kolizji terminów    | 🟢 Zakończone (Architektura) |
| **P5**        | Przywracanie danych     | Procedury Disaster Recovery oraz uzgadnianie spójności baz danych i sald         | 🟢 Zakończone (Architektura) |
| **P6**        | Zmiana terminu          | Bezpieczna transakcyjnie modyfikacja slotów rezerwacji bez ryzyka utraty terminu | 🟢 Zakończone (Architektura) |

---

## 📁 Struktura repozytorium

```text
├── diagrams/                          # Pliki źródłowe modeli BPMN 2.0 (XML)
│   ├── schemat_procesow.bpmn          # Główny diagram współpracy P1–P6
│   ├── SportBook_P3_AS_IS.bpmn        # Szczegółowy model AS-IS zarządzania obiektami
│   └── drafts/                        # Robocze wersje dekompozycji P1 i P2
├── docs/                              # Dokumentacja projektu i raporty
│   ├── raport_nr_1/                   # Raport za okres 23.10.2026 – 06.11.2026 (kod LaTeX + PDF)
│   └── images/                        # Eksporty diagramów (PNG/SVG) na potrzeby dokumentacji
└── README.md
```
