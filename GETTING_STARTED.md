# Getting Started: Construction Company Automation Guide

**Data-Driven Construction: От изолированных данных к автоматизации**

> "Если данные — это новая нефть, нам нужно научиться их определять, находить, добывать и перерабатывать, чтобы сделать их ценными." — Ralph Montague

---

## Ключевая идея

**Автоматизация строительства начинается не с BIM, а с понимания данных.**

BIM, ERP, Excel, PDF, фотографии — это всё **базы данных** в разных форматах. За каждым файлом Revit скрывается структурированная база данных. За каждым PDF — неструктурированный текст. Понимание типов данных и их связей — фундамент автоматизации.

```
┌─────────────────────────────────────────────────────────────────────┐
│                    ДАННЫЕ В СТРОИТЕЛЬСТВЕ                           │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│   СТРУКТУРИРОВАННЫЕ        ПОЛУСТРУКТУРИРОВАННЫЕ      НЕСТРУКТУРИРОВАННЫЕ
│   ─────────────────        ──────────────────────      ──────────────────
│   • Excel таблицы          • IFC модели               • PDF контракты
│   • Базы данных ERP        • JSON/XML файлы           • Фотографии
│   • CSV экспорты           • API ответы               • Письма и заметки
│   • Расписания P6          • BCF файлы                • Сканы документов
│                                                                      │
│   Легко обрабатывать       Требуют парсинга           Требуют AI/OCR
│   SQL запросы              Схема гибкая               Нет схемы
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Содержание

1. [Шаг 1: Оценка текущего состояния данных](#шаг-1-оценка-текущего-состояния-данных)
2. [Шаг 2: Обнаружение изолированных данных (Data Silos)](#шаг-2-обнаружение-изолированных-данных)
3. [Шаг 3: Классификация и инвентаризация данных](#шаг-3-классификация-и-инвентаризация-данных)
4. [Шаг 4: Построение ETL пайплайнов](#шаг-4-построение-etl-пайплайнов)
5. [Шаг 5: Автоматизация ключевых процессов](#шаг-5-автоматизация-ключевых-процессов)
6. [Кейсы из практики](#кейсы-из-практики)
7. [Дорожная карта по отделам](#дорожная-карта-по-отделам)

---

## Шаг 1: Оценка текущего состояния данных

**Источник:** DDC Book, Chapter 1.1 — "Эволюция использования данных в строительстве"

### Уровни цифровой зрелости

```python
from enum import Enum

class MaturityLevel(Enum):
    LEVEL_0_PAPER = 0      # Бумажный документооборот
    LEVEL_1_BASIC = 1      # Excel, email, файловые хранилища
    LEVEL_2_STRUCTURED = 2  # Специализированное ПО, базы данных
    LEVEL_3_INTEGRATED = 3  # Интегрированные системы (ERP + PM)
    LEVEL_4_AUTOMATED = 4   # Автоматические workflow, ML модели
    LEVEL_5_PREDICTIVE = 5  # Предиктивная аналитика, цифровые двойники
```

### Быстрая самооценка

| Вопрос | Да (1) | Нет (0) |
|--------|--------|---------|
| Есть единая база кодов работ (cost codes)? | | |
| Данные передаются между отделами автоматически? | | |
| Отчёты генерируются без ручного сбора данных? | | |
| Есть история изменений в данных (версионирование)? | | |
| Данные доступны с мобильных устройств на объекте? | | |

**Результат:**
- 0-1: Level 1 — Базовая цифровизация
- 2-3: Level 2-3 — Готовы к интеграции
- 4-5: Level 4+ — Готовы к AI автоматизации

### Практический кейс: Оценка компании

```python
# 2_DDC_Book/Chapter-1.1/data-evolution-analysis/SKILL.md

from dataclasses import dataclass
from typing import Dict, List

@dataclass
class DataFlowAssessment:
    category: str           # design, cost, schedule, quality
    source_systems: List[str]
    integration_level: float  # 0-1
    automation_level: float   # 0-1
    issues: List[str]

# Пример анализа типичной строительной компании
assessment = {
    "design": DataFlowAssessment(
        category="design",
        source_systems=["AutoCAD", "Revit"],
        integration_level=0.3,  # Данные передаются вручную
        automation_level=0.1,
        issues=["Нет связи с системой смет", "Ручной экспорт спецификаций"]
    ),
    "cost": DataFlowAssessment(
        category="cost",
        source_systems=["Excel", "1C"],
        integration_level=0.2,
        automation_level=0.0,
        issues=["Сметы в разных форматах", "Дублирование данных"]
    )
}

# Типичный результат: integration_level = 0.25 → Level 2
```

---

## Шаг 2: Обнаружение изолированных данных

**Источник:** DDC Book, Chapter 1.2 — "Технологии и системы управления в современном строительстве"

### Что такое Data Silos?

**Data Silo** — изолированный источник данных, не связанный с другими системами. Это главный враг автоматизации.

```
┌─────────────────────────────────────────────────────────────────────┐
│                         DATA SILOS                                   │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│    ┌──────────┐     ┌──────────┐     ┌──────────┐     ┌──────────┐ │
│    │  Excel   │     │   ERP    │     │   BIM    │     │  Photos  │ │
│    │  сметы   │     │   1C     │     │  Revit   │     │  объекта │ │
│    └──────────┘     └──────────┘     └──────────┘     └──────────┘ │
│         ↑                ↑                ↑                ↑        │
│         │                │                │                │        │
│         └────────────────┴────────────────┴────────────────┘        │
│                    НЕТ АВТОМАТИЧЕСКОЙ СВЯЗИ                         │
│                    Данные копируются вручную                        │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

### Практический кейс: Обнаружение silos

```python
# 2_DDC_Book/Chapter-1.2/data-silo-detection/SKILL.md

from dataclasses import dataclass
from typing import List
from enum import Enum

class SiloSeverity(Enum):
    CRITICAL = "critical"   # Критичное влияние на бизнес
    HIGH = "high"           # Значительная неэффективность
    MEDIUM = "medium"       # Заметные проблемы
    LOW = "low"             # Незначительные неудобства

@dataclass
class DataSource:
    name: str
    department: str
    data_entities: List[str]  # Какие данные содержит
    connections: List[str]    # С чем связан (пусто = silo!)
    has_api: bool             # Есть ли возможность интеграции

# Типичная картина в строительной компании
sources = [
    DataSource(
        name="Excel сметы",
        department="Сметный отдел",
        data_entities=["стоимость", "объёмы", "расценки"],
        connections=[],  # SILO! Ни с чем не связан
        has_api=False
    ),
    DataSource(
        name="1C Бухгалтерия",
        department="Бухгалтерия",
        data_entities=["счета", "платежи", "договора"],
        connections=["банк"],
        has_api=True  # Можно интегрировать!
    ),
    DataSource(
        name="Revit модели",
        department="Проектный отдел",
        data_entities=["геометрия", "спецификации", "объёмы"],
        connections=[],  # SILO! Данные не экспортируются автоматически
        has_api=True  # Но есть API для интеграции
    )
]

# Анализ: 2 из 3 источников — изолированные silos
# Рекомендация: связать Revit → Excel сметы → 1C
```

### Приоритеты устранения silos

| Severity | Пример | Действие |
|----------|--------|----------|
| CRITICAL | Сметы не связаны с фактическими затратами | ETL пайплайн |
| HIGH | BIM не экспортирует в сметную программу | API интеграция |
| MEDIUM | Фото объекта хранятся локально | Cloud синхронизация |
| LOW | Контакты подрядчиков в личных телефонах | CRM система |

---

## Шаг 3: Классификация и инвентаризация данных

**Источник:** DDC Book, Chapter 2.1 — "Типы данных в строительстве"

### Классификация по структуре

```python
# 2_DDC_Book/Chapter-2.1/data-type-classifier/SKILL.md

class DataStructure(Enum):
    STRUCTURED = "structured"           # Таблицы, БД, Excel
    SEMI_STRUCTURED = "semi_structured" # JSON, XML, IFC
    UNSTRUCTURED = "unstructured"       # PDF, фото, видео
    GEOMETRIC = "geometric"             # CAD, BIM геометрия
    TEMPORAL = "temporal"               # Расписания, временные ряды
```

### Практический кейс: Инвентаризация данных

```python
# Проведите инвентаризацию всех источников данных в компании

data_inventory = [
    {
        "name": "Сметы проектов",
        "format": "Excel (.xlsx)",
        "structure": "STRUCTURED",
        "location": "Сетевой диск Z:",
        "volume": "500 файлов",
        "update_frequency": "Ежедневно",
        "owner": "Сметный отдел",
        "integration": "Ручной экспорт в 1C"
    },
    {
        "name": "BIM модели",
        "format": "Revit (.rvt), IFC",
        "structure": "SEMI_STRUCTURED",  # IFC = база данных!
        "location": "BIM360",
        "volume": "50 проектов",
        "update_frequency": "Еженедельно",
        "owner": "Проектный отдел",
        "integration": "Нет автоматической связи"
    },
    {
        "name": "Договоры",
        "format": "PDF, Word",
        "structure": "UNSTRUCTURED",
        "location": "SharePoint",
        "volume": "2000 документов",
        "update_frequency": "По необходимости",
        "owner": "Юридический отдел",
        "integration": "Ручной поиск"
    }
]

# Рекомендации по хранению
storage_recommendations = {
    "STRUCTURED": "Relational Database (PostgreSQL)",
    "SEMI_STRUCTURED": "Document Database (MongoDB) или Data Lake",
    "UNSTRUCTURED": "Object Storage (S3) + Vector DB для поиска",
    "GEOMETRIC": "File System + IFC сервер",
    "TEMPORAL": "Time Series DB (InfluxDB)"
}
```

### Ключевой инсайт: IFC = База данных

```
┌─────────────────────────────────────────────────────────────────────┐
│                    IFC ≠ Просто 3D модель                           │
│                    IFC = Структурированная база данных              │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│   IFC файл содержит:                                                │
│   ├── IfcProject (проект)                                           │
│   │   ├── IfcSite (участок)                                         │
│   │   │   ├── IfcBuilding (здание)                                  │
│   │   │   │   ├── IfcBuildingStorey (этаж)                          │
│   │   │   │   │   ├── IfcWall (стена)                               │
│   │   │   │   │   │   ├── Pset_WallCommon (свойства)                │
│   │   │   │   │   │   │   ├── IsExternal: True                      │
│   │   │   │   │   │   │   ├── FireRating: "2 hour"                  │
│   │   │   │   │   │   ├── BaseQuantities (объёмы)                   │
│   │   │   │   │   │   │   ├── NetVolume: 15.5 m³                    │
│   │   │   │   │   │   │   ├── NetArea: 45.2 m²                      │
│                                                                      │
│   Можно извлечь: объёмы, площади, материалы, связи                  │
│   И автоматически передать в сметную программу!                     │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Шаг 4: Построение ETL пайплайнов

**Источник:** DDC Book, Chapter 4.2 — "ETL и автоматизация процессов"

> "ETL: переход от ручного управления к автоматизации позволяет компаниям обрабатывать данные без постоянного человеческого вмешательства."

### Что такое ETL?

```
┌─────────┐    ┌───────────┐    ┌────────┐
│ EXTRACT │ -> │ TRANSFORM │ -> │  LOAD  │
│ Извлечь │    │ Преобразов│    │ Загруз │
└─────────┘    └───────────┘    └────────┘
     │               │               │
     ▼               ▼               ▼
  Источники      Обработка       Выходы
  - Excel        - Очистка       - Excel отчёт
  - PDF          - Валидация     - PDF отчёт
  - BIM/IFC      - Расчёты       - База данных
  - API          - Агрегация     - API
```

### Практический кейс: ETL для сметных данных

```python
# 2_DDC_Book/Chapter-4.2/etl-pipeline/SKILL.md

import pandas as pd
from pathlib import Path

class ConstructionETLPipeline:
    """ETL пайплайн для строительных данных"""

    def __init__(self, config):
        self.config = config
        self.data = None
        self.errors = []

    def extract(self):
        """EXTRACT: Извлечение из разных источников"""
        print("Извлечение данных...")

        all_data = []

        # Из Excel файлов
        for file in Path(self.config['input_folder']).glob("*.xlsx"):
            df = pd.read_excel(file)
            df['_source'] = file.name
            all_data.append(df)
            print(f"  Извлечено: {file.name}")

        self.data = pd.concat(all_data, ignore_index=True)
        print(f"  Всего записей: {len(self.data)}")
        return self

    def transform(self):
        """TRANSFORM: Очистка и преобразование"""
        print("Преобразование данных...")

        # Удаление пустых строк
        self.data = self.data.dropna(how='all')

        # Стандартизация названий
        if 'Категория' in self.data.columns:
            self.data['Категория'] = self.data['Категория'].str.strip().str.title()

        # Расчёт итогов
        if 'Количество' in self.data.columns and 'Цена' in self.data.columns:
            self.data['Сумма'] = self.data['Количество'] * self.data['Цена']

        # Валидация
        invalid = self.data[self.data['Количество'] <= 0]
        if len(invalid) > 0:
            self.errors.append(f"Найдено {len(invalid)} строк с некорректным количеством")

        print(f"  Обработано записей: {len(self.data)}")
        print(f"  Ошибок валидации: {len(self.errors)}")
        return self

    def load(self):
        """LOAD: Сохранение результатов"""
        print("Загрузка результатов...")

        # Сводный отчёт
        summary = self.data.groupby('Категория').agg({
            'Сумма': 'sum',
            'Количество': 'sum'
        }).round(2)

        # Сохранение в Excel
        output_path = self.config['output_file']
        with pd.ExcelWriter(output_path, engine='openpyxl') as writer:
            self.data.to_excel(writer, sheet_name='Данные', index=False)
            summary.to_excel(writer, sheet_name='Сводка')

        print(f"  Сохранено: {output_path}")
        return self

    def run(self):
        """Запуск полного пайплайна"""
        return self.extract().transform().load()

# Использование
config = {
    'input_folder': './сметы/',
    'output_file': './отчёты/сводная_смета.xlsx'
}

pipeline = ConstructionETLPipeline(config)
pipeline.run()
```

### Автоматизация с n8n

```json
// 3_DDC_Insights/Automation-Workflows/n8n-daily-report/SKILL.md

{
  "workflow": "Ежедневный отчёт",
  "trigger": "Каждый день в 17:00",
  "nodes": [
    {
      "name": "Получить данные о погоде",
      "type": "HTTP Request",
      "url": "api.openweathermap.org"
    },
    {
      "name": "Получить данные из Excel",
      "type": "Spreadsheet File",
      "operation": "read"
    },
    {
      "name": "Обработать данные",
      "type": "Code",
      "code": "// Агрегация и форматирование"
    },
    {
      "name": "Сгенерировать PDF",
      "type": "HTTP Request",
      "url": "pdf-service/generate"
    },
    {
      "name": "Отправить email",
      "type": "Email Send",
      "to": "management@company.ru"
    }
  ]
}
```

---

## Шаг 5: Автоматизация ключевых процессов

### Процесс 1: Автоматическое составление смет

**Источник:** DDC Book, Chapter 3.1 — "Расчёт стоимости и составление смет"

```python
# 2_DDC_Book/Chapter-3.1/estimate-builder/SKILL.md

from dataclasses import dataclass
from enum import Enum
from typing import List

class CostCategory(Enum):
    LABOR = "labor"           # Работы
    MATERIAL = "material"     # Материалы
    EQUIPMENT = "equipment"   # Механизмы
    SUBCONTRACTOR = "subcontractor"  # Субподряд

@dataclass
class EstimateLineItem:
    code: str           # Код работы (из CWICR базы)
    description: str
    quantity: float
    unit: str
    unit_cost: float
    category: CostCategory

    @property
    def total(self) -> float:
        return round(self.quantity * self.unit_cost, 2)

class EstimateBuilder:
    """Построение смет из структурированных данных"""

    def __init__(self, project_name: str):
        self.project_name = project_name
        self.items: List[EstimateLineItem] = []
        self.markups = {'overhead': 0.15, 'profit': 0.10, 'contingency': 0.05}

    def add_item(self, code, description, quantity, unit, unit_cost, category):
        item = EstimateLineItem(code, description, quantity, unit, unit_cost, category)
        self.items.append(item)
        return item

    def get_direct_cost(self) -> float:
        return sum(item.total for item in self.items)

    def get_total_cost(self) -> float:
        direct = self.get_direct_cost()
        markup_total = sum(self.markups.values())
        return direct * (1 + markup_total)

    def import_from_ifc(self, ifc_path: str, price_database: dict):
        """Импорт объёмов из IFC и расценок из базы"""
        import ifcopenshell

        model = ifcopenshell.open(ifc_path)

        for wall in model.by_type("IfcWall"):
            # Извлекаем объём из IFC
            volume = self._get_quantity(wall, "NetVolume")

            # Находим расценку в базе
            material = self._get_material(wall)
            price_info = price_database.get(material, {})

            self.add_item(
                code=price_info.get('code', 'N/A'),
                description=f"Стена: {wall.Name}",
                quantity=volume,
                unit="м³",
                unit_cost=price_info.get('unit_cost', 0),
                category=CostCategory.MATERIAL
            )

# Пример использования
estimate = EstimateBuilder("Офисное здание")

# Добавление позиций
estimate.add_item("03.30.00", "Бетон фундамента", 500, "м³", 180, CostCategory.MATERIAL)
estimate.add_item("03.30.01", "Работы по бетонированию", 500, "м³", 50, CostCategory.LABOR)
estimate.add_item("05.12.00", "Металлоконструкции", 50, "т", 4500, CostCategory.SUBCONTRACTOR)

print(f"Прямые затраты: {estimate.get_direct_cost():,.0f} руб")
print(f"Итого с накладными: {estimate.get_total_cost():,.0f} руб")
```

### Процесс 2: Автоматический контроль отклонений

```python
# Связка: Плановые данные (смета) ↔ Фактические данные (ERP)

class BudgetVarianceAnalyzer:
    """Анализ отклонений факт vs план"""

    def __init__(self, planned_df, actual_df):
        self.planned = planned_df
        self.actual = actual_df

    def calculate_variance(self):
        """Расчёт отклонений по каждой позиции"""
        merged = self.planned.merge(
            self.actual,
            on='Код работы',
            suffixes=('_план', '_факт')
        )

        merged['Отклонение'] = merged['Сумма_факт'] - merged['Сумма_план']
        merged['Отклонение_%'] = (merged['Отклонение'] / merged['Сумма_план']) * 100

        return merged

    def get_alerts(self, threshold=10):
        """Позиции с отклонением > threshold%"""
        variance = self.calculate_variance()
        return variance[abs(variance['Отклонение_%']) > threshold]

# Автоматическая проверка каждую неделю
# n8n workflow: ERP → Analyzer → Email руководству
```

### Процесс 3: Автоматическая генерация отчётов

```python
# 3_DDC_Insights/Automation-Workflows/n8n-daily-report/SKILL.md

def generate_daily_report(project_data: dict) -> str:
    """Генерация ежедневного отчёта"""

    report = f"""
# Ежедневный отчёт: {project_data['name']}
**Дата:** {project_data['date']}

## Погода
- Температура: {project_data['weather']['temp']}°C
- Условия: {project_data['weather']['condition']}

## Рабочая сила
| Профессия | Человек | Часы |
|-----------|---------|------|
"""
    for labor in project_data['labor']:
        report += f"| {labor['trade']} | {labor['count']} | {labor['hours']} |\n"

    report += f"""
## Прогресс
- Выполнено: {project_data['progress']}%
- Отклонение от графика: {project_data['schedule_variance']} дней

## Проблемы
"""
    for issue in project_data.get('issues', []):
        report += f"- {issue}\n"

    return report
```

---

## Кейсы из практики

### Кейс 1: От 2 дней к 2 часам — автоматизация сметы

**Проблема:** Сметчик тратит 2 дня на составление сметы, вручную перенося данные из спецификаций Revit в Excel.

**Решение:**
1. Экспорт данных из Revit в IFC
2. Парсинг IFC с помощью ifcopenshell
3. Автоматическое сопоставление с базой расценок CWICR
4. Генерация Excel сметы

**Результат:** 2 часа вместо 2 дней. Экономия 80% времени.

```python
# Упрощённый пример
import ifcopenshell

def ifc_to_estimate(ifc_path, price_db):
    model = ifcopenshell.open(ifc_path)
    estimate_items = []

    for element in model.by_type("IfcBuildingElement"):
        # Извлекаем объёмы
        quantities = get_element_quantities(element)

        # Классифицируем элемент
        category = classify_element(element)

        # Находим расценку
        price = price_db.get(category)

        estimate_items.append({
            'description': element.Name,
            'quantity': quantities.get('volume'),
            'unit': 'm³',
            'unit_cost': price['unit_cost'],
            'total': quantities.get('volume') * price['unit_cost']
        })

    return estimate_items
```

### Кейс 2: Единая база работ вместо хаоса

**Проблема:** В компании 5 сметчиков, каждый использует свои названия работ. "Бетонирование фундамента", "Устройство ж/б фундамента", "Бетонные работы (фундамент)" — одна и та же работа с разными названиями.

**Решение:** CWICR Database — 55,719 стандартизированных позиций работ на 9 языках.

```python
# 1_DDC_Toolkit/CWICR-Database/semantic-search-cwicr/SKILL.md

from qdrant_client import QdrantClient

def search_cwicr(query: str) -> list:
    """Семантический поиск по базе работ"""
    client = QdrantClient("localhost", port=6333)

    # Векторный поиск (понимает синонимы!)
    results = client.search(
        collection_name="ddc_cwicr_ru",
        query_vector=get_embedding(query),
        limit=5
    )

    return [
        {
            'code': r.payload['code'],
            'description': r.payload['description'],
            'unit': r.payload['unit'],
            'confidence': r.score
        }
        for r in results
    ]

# Теперь любой запрос найдёт правильную позицию
search_cwicr("бетонирование фундамента")
# → [{'code': '03.30.00', 'description': 'Бетонные работы - фундаменты', ...}]

search_cwicr("concrete foundation pour")
# → [{'code': '03.30.00', 'description': 'Concrete works - foundations', ...}]
```

### Кейс 3: Автоматический контроль сроков

**Проблема:** Отклонения в графике обнаруживаются слишком поздно.

**Решение:** ETL пайплайн, который ежедневно сравнивает план и факт.

```python
# Ежедневная проверка (запускается через n8n или Airflow)

def check_schedule_variance(project_id):
    # Извлекаем данные
    planned = get_planned_schedule(project_id)  # Из P6/MS Project
    actual = get_actual_progress(project_id)     # Из Procore/фото

    # Анализируем
    for task in planned:
        actual_progress = actual.get(task['id'], {})

        if actual_progress['completion'] < task['planned_completion']:
            variance = task['planned_completion'] - actual_progress['completion']

            if variance > 5:  # Отклонение > 5%
                send_alert(
                    to="pm@company.ru",
                    subject=f"Отставание: {task['name']}",
                    body=f"Отклонение: {variance}%. Требуется корректировка."
                )
```

---

## Дорожная карта по отделам

### Сметный отдел

| Неделя | Действие | Скилл |
|--------|----------|-------|
| 1 | Внедрение единой базы расценок | `semantic-search-cwicr` |
| 2 | Автоматический импорт объёмов из IFC | `bim-qto` |
| 3-4 | ETL пайплайн: IFC → Смета | `etl-pipeline` |
| 5+ | Автоматическая генерация смет | `estimate-builder` |

### Производственный отдел

| Неделя | Действие | Скилл |
|--------|----------|-------|
| 1 | Цифровизация ежедневных отчётов | `n8n-daily-report` |
| 2 | Автоматический сбор фото с объекта | `n8n-photo-report` |
| 3-4 | Связь графика и факта | `schedule-delay-analyzer` |
| 5+ | Предиктивная аналитика сроков | `duration-prediction` |

### Финансовый отдел

| Неделя | Действие | Скилл |
|--------|----------|-------|
| 1 | Автоматический контроль бюджета | `budget-variance-analyzer` |
| 2 | Прогноз cash flow | `cash-flow-forecaster` |
| 3-4 | Интеграция с ERP | `erp-data-extractor` |
| 5+ | ML модель прогноза затрат | `cost-prediction` |

### Руководство

| Неделя | Действие | Скилл |
|--------|----------|-------|
| 1 | Оценка цифровой зрелости | `data-evolution-analysis` |
| 2 | Обнаружение data silos | `data-silo-detection` |
| 3-4 | KPI дашборд | `kpi-dashboard` |
| 5+ | Стратегия цифровой трансформации | `digital-maturity-assessment` |

---

## ROI автоматизации

### Экономия времени по процессам

| Процесс | Ручное время | Автоматизация | Экономия |
|---------|--------------|---------------|----------|
| Составление сметы | 16 часов | 2 часа | 87% |
| Ежедневный отчёт | 2 часа | 10 мин | 92% |
| Контроль бюджета | 4 часа/неделя | 30 мин | 87% |
| Поиск расценки | 15 мин/позиция | 10 сек | 99% |

### Пример расчёта

```
Компания: 30 сотрудников, 5 активных проектов

Экономия времени:
- Сметы: 5 смет/мес × 14 ч = 70 ч/мес
- Отчёты: 5 проектов × 1.8 ч × 22 дня = 198 ч/мес
- Контроль: 5 проектов × 3.5 ч × 4 недели = 70 ч/мес

Итого: 338 часов/месяц

При средней ставке 2000 руб/час: 676,000 руб/мес
Консервативная оценка (50%): 338,000 руб/мес

Затраты на внедрение: 150,000 руб (разово)
Окупаемость: < 1 месяца
```

---

## Быстрый старт

### День 1: Установка

```bash
pip install pandas openpyxl ifcopenshell pdfplumber qdrant-client
git clone https://github.com/datadrivenconstruction/DDC_Skills.git
```

### День 2-3: Инвентаризация данных

```python
# Составьте список всех источников данных
# Используйте data-silo-detection для анализа
python analyze_data_sources.py
```

### День 4-5: Первый ETL пайплайн

```python
# Свяжите хотя бы 2 источника данных
# Например: Excel сметы → Сводный отчёт
python run_etl.py
```

### Неделя 2+: Масштабирование

```python
# Добавляйте новые источники
# Автоматизируйте новые процессы
# Измеряйте ROI
```

---

## Ресурсы

- **Книга:** "Data-Driven Construction" by Artem Boiko (ISBN 978-3-9826255-9-1)
- **Сайт:** https://datadrivenconstruction.io
- **CWICR база:** https://openconstructionestimate.com
- **GitHub:** https://github.com/datadrivenconstruction

---

**Начните сегодня. Автоматизация строительства — это автоматизация данных.**
