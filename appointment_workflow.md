# Sequence Diagram: Запись на прием к врачу

```mermaid
sequenceDiagram
    participant Patient as Пациент
    participant Frontend as Frontend (React)
    participant Backend as Backend (FastAPI)
    participant DB as База данных
    participant Bot as Telegram Bot
    participant Doctor as Врач

    Patient->>Frontend: 1. Ищет врача
    Frontend->>Backend: 2. GET /api/doctors
    Backend->>DB: 3. Запрос списка врачей
    DB-->>Backend: 4. Данные врачей
    Backend-->>Frontend: 5. Список врачей
    Frontend-->>Patient: 6. Отображение результатов
    
    Patient->>Frontend: 7. Выбирает врача и время
    Frontend->>Backend: 8. POST /api/appointments
    Backend->>DB: 9. Создание записи
    DB-->>Backend: 10. Подтверждение
    Backend->>Bot: 11. Уведомление врачу
    Bot->>Doctor: 12. "Новая запись!"
    Backend-->>Frontend: 13. Подтверждение записи
    Frontend-->>Patient: 14. "Вы записаны!"
    
    Note over Patient,Doctor: Пациент получает подтверждение<br/>Врач получает уведомление