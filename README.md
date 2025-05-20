# Интеграция Figma с GitHub Issues через Make.com

## 📌 Описание проекта

В рамках практического задания была реализована интеграция проекта, разработанного в Figma, с системой управления задачами GitHub.  
Целью интеграции является автоматическое создание Issue в GitHub при фиксации новых изменений в макете Figma.

---

## Интерфейс пользователя
![2025-05-20_17-20-10](https://github.com/user-attachments/assets/a339e30a-b0cd-4e6a-940b-65ca41379eec)

---

## Интерфейс курьера
![2025-05-20_17-20-20](https://github.com/user-attachments/assets/7f5b9ef8-f95e-446a-aa0f-30f50cd7dd76)

---

## Интерфейс оператора
![2025-05-20_17-20-34](https://github.com/user-attachments/assets/5cd98d06-e9d3-4ab9-bf22-d259f4ee9005)

---

## 🔧 Используемые технологии

- [Figma](https://figma.com) — среда проектирования интерфейсов
- [Make.com](https://www.make.com/) — no-code платформа для автоматизации
- GitHub REST API — создание задач (`issues`)
- Figma REST API (частично) — получение информации о версии макета

---

## 🔗 Связь между Figma и GitHub

1. **Figma** → модуль `List File Version History` запрашивает последнюю версию
2. **Make.com** → сравнивает текущую версию с предыдущей
3. Если версия **новая**:
   - создаётся Issue в GitHub с описанием изменений
   - сохраняется текущий `Version ID` в `Data Store`

---

## ⚙️ Логика сценария

| Шаг | Модуль                                  | Описание                                               |
|-----|-----------------------------------------|--------------------------------------------------------|
| 1   | Figma → List File Version History       | Получение последней версии макета                     |
| 2   | Data Store → Get a Record               | Получение сохранённого `last_version_id`              |
| 3   | Filter                                   | Сравнение: если `Version ID ≠ last_version_id`        |
| 4   | GitHub → Create an Issue                | Создание задачи с информацией о версии                |
| 5   | Data Store → Update a Record            | Сохранение нового `Version ID` для следующей итерации |

---

## 💬 Пример создаваемого Issue

Обнаружено обновление в Figma-макете. Дата обновления: 2025-05-20T13:53:48.000Z.Пользователь: Yaroslav, https://www.gravatar.com/avatar/b29b75354662fb6929774ff4fbbe2df6?size=240&default=https%3A%2F%2Fs3-alpha.figma.com%2Fstatic%2Fuser_y_v2.png, 947565866700752763. Открыть макет:(https://www.figma.com/design/Cl1V4R7yjTmGkQFHIja31L/%D0%9F%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B5-%D0%B4%D0%BE%D1%81%D1%82%D0%B0%D0%B2%D0%BA%D0%B8?node-id=0-1&m=dev&t=HlQfzCCmrHLgLCe2-1)

---

## 🛠 Возможности для расширения

- Отслеживание изменений в структуре проекта (страницы/фреймы)
- Подключение Pull Request вместо Issue
- Сравнение содержимого узлов Figma через `GET /v1/files`

---

## 📝 Примечания

> Figma API имеет ограничения для бесплатных аккаунтов.  
> Доступ к структуре макета через `/v1/files/{file_key}` возможен только при наличии **рабочего File Key** из команды с планом Pro.

---

## 👨‍💻 Автор

Yaroslav  
Группа БСБО-03-23  
2025 г.
