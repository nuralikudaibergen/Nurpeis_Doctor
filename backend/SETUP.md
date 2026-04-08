# Настройка Google Таблицы для заявок

## Шаг 1: Создайте Google Таблицу

1. Откройте [Google Таблицы](https://docs.google.com/spreadsheets/)
2. Создайте новую таблицу "Nurpeis Doctor - Заявки"
3. В первой строке добавьте заголовки:
   - A1: `Имя`
   - B1: `Телефон`
   - C1: `Услуга`
   - D1: `Дата`
   - E1: `Время`
   - F1: `Сообщение`
   - G1: `Тип` (Заявка/Отзыв)
   - H1: `Оценка`
   - I1: `Текст_отзыва`
   - J1: `Дата_создания`

## Шаг 2: Добавьте Apps Script

1. В таблице выберите **Расширения** → **Apps Script**
2. Удалите код `myFunction()` и вставьте нижеуказанный код:

```javascript
function doPost(e) {
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  const data = JSON.parse(e.postData.contents);

  const row = [
    data.name || '',
    data.phone || '',
    data.service || '',
    data.date || '',
    data.time || '',
    data.message || '',
    data.type || 'Заявка',
    data.rating || '',
    data.reviewText || '',
    new Date()
  ];

  sheet.appendRow(row);

  return ContentService.createTextOutput(JSON.stringify({success: true}))
    .setMimeType(ContentService.MimeType.JSON);
}

function doGet() {
  return ContentService.createTextOutput(JSON.stringify({status: 'ok'}))
    .setMimeType(ContentService.MimeType.JSON);
}
```

3. Нажмите **Сохранить** (дискета)
4. Нажмите **Развернуть** → **Новое развертывание**
5. Нажмите шестерёнку → **Веб-приложение**
6. Заполните:
   - Описание: `Nurpeis Doctor API`
   - Выполнить как: `Я`
   - Кто имеет доступ: `Все`
7. Нажмите **Развернуть**
8. Скопируйте **URL веб-приложения**

## Шаг 3: Обновите сайт

Скопируйте URL из предыдущего шага и сообщите мне, я обновлю код сайта.

---

## Просмотр заявок

1. Откройте вашу Google Таблицу
2. Все новые заявки будут появляться автоматически
3. Можно фильтровать, сортировать, создавать диаграммы