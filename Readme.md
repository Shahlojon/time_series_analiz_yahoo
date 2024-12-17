1. Определение задачи и бизнес-целей проекта

  * Задача: Прогнозировать движение цены акций (рост или падение) на основе исторических данных.
  * Бизнес-цели:
    * Улучшить стратегию инвестирования.
    * Снизить риски, связанные с торговлей.
    * Разработать инструмент для автоматического принятия решений на основе прогноза.

2. ML System Design

*   Сбор данных: Исторические данные из Yahoo Finance.

* Предобработка:
    * Приведение данных к стандартному формату.
    * Добавление временных признаков (день недели, месяц, квартал).
    * Генерация признаков: скользящее среднее, волатильность.
* Разработка моделей:
    * Базовая модель (baseline) — ARIMA.
    * Классификация временных рядов: предсказание роста или падения (рост = 1, падение = 0).
    * Нейронные сети (LSTM/GRU).
* API для развертывания модели: Flask/Django API для получения прогнозов.
3. Этапы выполнения

* Подготовка baseline: Использовать ARIMA для предсказания цены закрытия (Adj Close) на следующий день.
* Метрика оценки — RMSE.
* Перевод задачи в классификацию:
   * Целевая переменная: target = 1 (если Adj Close_t > Adj Close_{t-1}), иначе 0.
   * Добавить временные признаки: день недели, месяц, квартал.
   * Добавить технические индикаторы: скользящее среднее (MA), индекс относительной силы (RSI), экспоненциальное среднее (EMA).
* Классификация временного ряда: Использовать данные с признаками для предсказания роста или падения (0 или 1).
* Метрики оценки: F1-score, Accuracy.
* Модель на основе НС: Разработать рекуррентную нейронную сеть (LSTM) для анализа временных рядов.
4. Выполнение анализа и подготовки

* Провести анализ корреляции признаков.
* Разделить данные на тренировочные и тестовые (например, 80% на тренировку, 20% на тест).
* Нормализовать данные для моделей НС.
* Проверить модели на переобучение.

Датасет представляет собой временной ряд финансовых данных акций:

1.   Дата наблюдения.
2.   Open, High, Low, Close*: Цены акций (на открытии, максимальная, минимальная и на закрытии торгов за день).
3.  Adj Close: Скорректированная цена закрытия (учитывает дивиденды и сплиты акций).
4.  Volume: Объем торговли.

В реальной жизни данные могут храниться в базе данных, например, в Postgres:


```
 CREATE TABLE stock_data (
    date DATE PRIMARY KEY,
    open FLOAT,
    high FLOAT,
    low FLOAT,
    close FLOAT,
    adj_close FLOAT,
    volume BIGINT
);

```




