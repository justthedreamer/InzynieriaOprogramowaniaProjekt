# PIRS - Parcel Issue Reporting System

Aplikacja dająca możliwość raportowania nieprawidłowości związanych z transportem przesyłek, automatami składującymi
przesyłki oraz aplikacją mobilną.<br>
Aplikacja ma na celu ułatwienie procesu zgłaszania, oraz procesowania zgłoszeń w firmie kurierskiej.
Jako źródło danych o przesyłkach, klientach oraz aplikacji mobilnej, system integruje się
z istniejącymi systemami firmy.

## Architektura

Architektura systemu opiera się na podejściu mikroserwisowym, co pozwala na niezależne skalowanie i rozwijanie
poszczególnych komponentów systemu. Wykorzystanie wzorca CQRS (Command Query Responsibility Segregation) oraz Event
Sourcing pozwala na efektywne zarządzanie stanem aplikacji, oraz zapewnia wysoką dostępność i spójność danych w
rozproszonym środowisku.

## Mikro serwisy

### Parcel Issue Reporting Service

> Odpowiedzialny za zgłoszenia problemów dotyczących procesowania przesyłek.

- **Adapter**: Aby komunikować się z zewnętrznymi systemami firmy.

### Parcel Device Issue Reporting Service

> Odpowiedzialny za zgłaszanie problemów dotyczących automatów paczkowych.

- **Adapter**: Aby komunikować się z zewnętrznymi systemami firmy.

### Software Issue Reporting Service

> Odpowiedzialny za zgłaszanie problemów dotyczących aplikacji mobilnej.

- **Adapter**: Aby komunikować się z zewnętrznymi systemami firmy.

### Ticket Management Service

> Odpowiedzialny za procesowanie oraz odczyt zgłoszeń przez pracowników.

**Design Patterns**

- **CQRS**: Aby zapewnić logiczną separację między zadaniami modyfikującymi stan systemu a pobieraniem danych.
- **State**: Aby kontrolować stan zgłoszenia i przeciwdziałać niepożądanym modyfikacjom.

### Authentication and Authorization Service

> Odpowiedzialny za logowanie i rejestracje użytkowników oraz określanie dostępu do zasobów.

**Design Patterns**

- **Adapter**: Aby komunikować się z zewnętrznymi systemami firmy.

### Notification Service

> Odpowiedzialny za wysyłanie powiadomień na podstawie zmian dokonanych w systemie.

**Design Patterns**

- **Strategy**: Aby w odpowiedni sposób wysyłać powiadomienia, bazując na zmianie dokonanej w systemie.

## Wymagania funkcjonalne

| **ID**  | **Opis wymagania**                                                                                                                                                                                               | **Priorytet** |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|
| FUNC-01 | System musi umożliwiać przypisanie zgłoszenia do maksymalnie jednego pracownika w danej chwili, aby uniknąć konfliktów.                                                                                          | Wysoki        |
| FUNC-02 | Tylko użytkownicy z odpowiednimi uprawnieniami (osoby autoryzowane) mogą przydzielać pracowników do realizacji zgłoszeń.                                                                                         | Wysoki        |
| FUNC-03 | Po zakończeniu pracy nad zgłoszeniem, pracownik musi zainicjować proces oceny i zatwierdzenia zgłoszenia przez osobę autoryzowaną.                                                                               | Średni        |
| FUNC-04 | Wszystkie działania podejmowane przez pracowników w ramach realizacji zgłoszeń muszą być rejestrowane w systemie jako zdarzenia z odpowiednimi metadanymi (np. czas, identyfikator użytkownika, opis działania). | Wysoki        |
| FUNC-05 | System powinien umożliwiać osobom szczebla kierowniczego przydzielanie odpowiednich uprawnień dla pracowników.                                                                                                   | Wysoki        |

## Wymagania niefunkcjonalne

| **ID**   | **Opis wymagania**                                                                                        | **Priorytet** |
|----------|-----------------------------------------------------------------------------------------------------------|---------------|
| NFUNC-01 | System musi być skalowalny, aby obsłużyć wzrost liczby użytkowników i zgłoszeń bez degradacji wydajności. | Wysoki        |
| NFUNC-02 | System powinien zapewniać wysoki poziom bezpieczeństwa danych, w tym szyfrowanie danych wrażliwych.       | Wysoki        |
| NFUNC-03 | Czas odpowiedzi systemu na zapytania użytkowników nie powinien przekraczać 2 sekund.                      | Wysoki        |
| NFUNC-04 | System powinien być dostępny z poziomem SLA (Service Level Agreement) na poziomie 99.9% uptime.           | Wysoki        |
| NFUNC-05 | System powinien być zgodny z obowiązującymi przepisami o ochronie danych osobowych (np. GDPR w Europie).  | Wysoki        |

## Use Case diagram

<img src="./img/UseCase.drawio.svg"/>

## Ticket Life Cycle

<img src="./img/TicketLifeCycle.drawio.svg"/>

## Example Infrastructure

<img src="./img/Infrastructure.drawio.svg"/>

