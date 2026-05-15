# ТЗ — Финальные правки сайта Реацентр Развитие
> Файл: `/Users/elenapapina/Desktop/вся работа/my-company/reacentr-razvitie`  
> Выполнять строго по порядку. После всех пунктов — вывести список изменённых файлов. Push только по запросу.

---

## 1. Обновить цены в прейскуранте (index.html)

Файл: `index.html`, секция `id="prices"`.

### 1.1 Колонка «Консультации»

Заменить весь блок `.price-col` с заголовком `Консультации`:
```html
<div class="price-col">
    <h3>Консультации</h3>
    <div class="pr"><span class="n">Консультация детского невролога</span><span class="v">1 700 ₽</span></div>
    <div class="pr"><span class="n">Повторная (в течение 3 мес.)</span><span class="v">1 500 ₽</span></div>
    <div class="pr"><span class="n">Консультация поведенческого невролога</span><span class="v">от 1 500 ₽</span></div>
    <div class="pr"><span class="n">Консультация логопеда</span><span class="v">от 1 600 ₽</span></div>
    <div class="pr"><span class="n">Консультация нейропсихолога</span><span class="v">1 700 ₽</span></div>
    <div class="pr"><span class="n">Консультация психолога</span><span class="v">от 1 600 ₽</span></div>
</div>
```
Строку «Тестирование на РАС» — **удалить** (нет в прайсе).

### 1.2 Колонка «Диагностика»

Заменить весь блок `.price-col` с заголовком `Диагностика`:
```html
<div class="price-col" style="margin-top:16px">
    <h3>Диагностика</h3>
    <div class="pr"><span class="n">ЭЭГ с компьютерной обработкой</span><span class="v">1 200 ₽</span></div>
    <div class="pr"><span class="n">Обследование с прибором «МЭКС»</span><span class="v">1 100 ₽</span></div>
</div>
```
Строки «ЭЭГ-мониторинг сна», «УЗДГ», «АСВП» — **удалить** (нет в прайсе).

### 1.3 Колонка «Микротоковая рефлексотерапия»

Заменить цены:
```html
<div class="price-col">
    <h3>Микротоковая рефлексотерапия</h3>
    <div class="pr"><span class="n">1 сеанс МТРТ (1-й курс)</span><span class="v">3 800 ₽</span></div>
    <div class="pr"><span class="n">Первый курс (15 сеансов)</span><span class="v">57 000 ₽</span></div>
    <div class="pr"><span class="n">Осмотр логопеда (по назначению)</span><span class="v">бесплатно</span></div>
    <div class="pr"><span class="n">Консультация психолога (по назн.)</span><span class="v">бесплатно</span></div>
</div>
```

### 1.4 Колонка «Занятия и процедуры»

Заменить весь блок:
```html
<div class="price-col" style="margin-top:16px">
    <h3>Занятия и процедуры</h3>
    <div class="pr"><span class="n">Занятие с логопедом (30 мин.)</span><span class="v">1 200 ₽</span></div>
    <div class="pr"><span class="n">Логопедический массаж</span><span class="v">1 200 ₽</span></div>
    <div class="pr"><span class="n">Занятие с нейропсихологом</span><span class="v">от 1 500 ₽</span></div>
    <div class="pr"><span class="n">Занятие с психологом (30 мин.)</span><span class="v">1 100 ₽</span></div>
    <div class="pr"><span class="n">Сенсорная интеграция (30 мин.)</span><span class="v">1 200 ₽</span></div>
    <div class="pr"><span class="n">ЛФК (30 мин.)</span><span class="v">1 200 ₽</span></div>
    <div class="pr"><span class="n">Массаж (30 мин.)</span><span class="v">1 200 ₽</span></div>
    <div class="pr"><span class="n">БАК (1 сеанс)</span><span class="v">1 100 ₽</span></div>
    <div class="pr"><span class="n">Курс БАК (10 сеансов)</span><span class="v">11 000 ₽</span></div>
</div>
```
Строки «АВА-терапия», «ВЧТ» — **удалить** (нет в прайсе).

---

## 2. Удалить карточку услуги ВЧТ из блока «Услуги» (index.html)

Файл: `index.html`, секция `id="services"`.

Найти и **удалить** карточку `openSvc(7)` целиком:
```html
<div class="srv" onclick="openSvc(7)">
    <div class="srv-icon">...</div>
    <h3>Речевая терапия (ВЧТ)</h3>
    <p>Высокочастотная речевая терапия...</p>
    <div class="price-tag">от 2 200 ₽</div>
    <div class="srv-arrow">→</div>
</div>
```

Также удалить запись `services[7]` из массива JS (строка ~1363, объект с `title:'Высокочастотная речевая терапия (ВЧТ)'`). После удаления исправить индексы: `openSvc(8)` → `openSvc(7)`, `openSvc(9)` → `openSvc(8)`.

---

## 3. Обновить цены в карточках услуг и модальных окнах (index.html)

После изменения массива `services[]` (строки ~1348–1369) обновить цены в `sm-price` внутри `body` каждого объекта:

- `services[0]` (МТРТ): `Сеанс — от 3 800 ₽ · Курс (15 сеансов) — от 57 000 ₽`
- `services[1]` (Детская неврология): `Первичная — 1 700 ₽ · Повторная — 1 500 ₽ · Обследование МЭКС — 1 100 ₽`
- `services[2]` (Диагностика): `ЭЭГ — 1 200 ₽ · МЭКС — 1 100 ₽` (убрать УЗДГ, АСВП)
- `services[3]` (Логопедия): `Занятие с логопедом — 1 200 ₽ · Логомассаж — 1 200 ₽ · Аудиотренажёр — 1 200 ₽`
- `services[4]` (Психология): удалить упоминание АВА-терапии из `<ul>` и `sm-price`; `Нейропсихолог — 1 700 ₽ · Психолог — от 1 100 ₽`
- `services[5]` (Массаж и ЛФК): `Массаж — 1 200 ₽ · ЛФК — 1 200 ₽`
- `services[6]` (БАК): `1 сеанс — 1 100 ₽ · Курс (10 сеансов) — 11 000 ₽`

Также обновить `price-tag` в карточках услуг на странице:
- Карточка МТРТ (`openSvc(0)`): `от 3 800 ₽ / сеанс`
- Карточка Диагностика (`openSvc(2)`): `от 1 200 ₽`
- Карточка Лечебный массаж (`openSvc(5)`): `от 1 200 ₽`

---

## 4. Добавить «Специалисты» в десктоп-меню (index.html)

Найти `<nav>` в хедере (строка ~537):
```html
<a href="#about">О центре</a>
<a href="#services">Услуги</a>
<a href="#prices">Цены</a>
<a href="#reviews">Отзывы</a>
<a href="#contacts">Контакты</a>
```
Добавить после «Цены»:
```html
<a href="#team">Специалисты</a>
```

---

## 5. Дополнить legal.html — 9 недостающих специалистов

Файл: `legal.html`, после последней карточки `</div>` блока Катыкина (строка ~175) добавить:

```html
<div class="spec-card">
    <h3>Такова Наталья Юрьевна</h3>
    <div class="spec-role">Заместитель директора</div>
</div>

<div class="spec-card">
    <h3>Киселева Лариса Валентиновна</h3>
    <div class="spec-role">Детский психолог</div>
    <p class="spec-docs"><a href="specialist.html?id=kiseleva">Документы об образовании (защищённый просмотр)</a></p>
</div>

<div class="spec-card">
    <h3>Полежаева Елена Николаевна</h3>
    <div class="spec-role">Детский психолог</div>
    <p class="spec-docs"><a href="specialist.html?id=polezhaeva">Документы об образовании (защищённый просмотр)</a></p>
</div>

<div class="spec-card">
    <h3>Чуприна Елена Сергеевна</h3>
    <div class="spec-role">Логопед</div>
    <p class="spec-docs"><a href="specialist.html?id=chuprina">Документы об образовании (защищённый просмотр)</a></p>
</div>

<div class="spec-card">
    <h3>Стаценко Алла Анатольевна</h3>
    <div class="spec-role">Администратор</div>
</div>

<div class="spec-card">
    <h3>Острых Светлана Сергеевна</h3>
    <div class="spec-role">Медицинская сестра по массажу</div>
    <p class="spec-docs"><a href="specialist.html?id=ostrykh">Документы об образовании (защищённый просмотр)</a></p>
</div>

<div class="spec-card">
    <h3>Серёдкина Олеся Анатольевна</h3>
    <div class="spec-role">Медицинская сестра</div>
    <p class="spec-docs"><a href="specialist.html?id=seredkina">Документы об образовании (защищённый просмотр)</a></p>
</div>

<div class="spec-card">
    <h3>Акимова Лариса Анатольевна</h3>
    <div class="spec-role">Санитарка</div>
</div>

<div class="spec-card">
    <h3>Пермякова Алёна Михайловна</h3>
    <div class="spec-role">Директор, учредитель</div>
</div>
```

Также добавить `id="alagyan"` к первой карточке:
```html
<div class="spec-card" id="alagyan">
```

---

## 6. Добавить контакты надзорных органов в legal.html

Добавить перед `<h2>Нормативные документы</h2>`:
```html
<h2>Контакты надзорных органов</h2>
<div class="info-block">
    <h3>Росздравнадзор</h3>
    <p>Сайт: <a href="https://roszdravnadzor.gov.ru" target="_blank" rel="noopener">roszdravnadzor.gov.ru</a></p>
    <p>Горячая линия: <a href="tel:88002000054">8 800 200-00-54</a> (бесплатно)</p>
</div>
<div class="info-block">
    <h3>Роспотребнадзор по Алтайскому краю</h3>
    <p>Сайт: <a href="https://22.rospotrebnadzor.ru" target="_blank" rel="noopener">22.rospotrebnadzor.ru</a></p>
    <p>Тел.: <a href="tel:+73852260056">+7 (3852) 26-00-56</a></p>
</div>
<div class="info-block">
    <h3>Министерство здравоохранения Алтайского края</h3>
    <p>Сайт: <a href="https://minzdrav.alregn.ru" target="_blank" rel="noopener">minzdrav.alregn.ru</a></p>
    <p>Тел.: <a href="tel:+73852677204">+7 (3852) 67-72-04</a></p>
</div>
```

---

## 7. Улучшить cookie-баннер (index.html)

Найти `<div class="ck" id="ckBar">`. Заменить содержимое:
```html
<div class="ck" id="ckBar">
    <h4>Cookie</h4>
    <p>Сайт использует cookie для корректной работы. <a href="privacy.html" style="color:var(--accent);text-decoration:underline">Политика конфиденциальности</a></p>
    <div style="display:flex;gap:10px;flex-wrap:wrap;margin-top:8px">
        <button onclick="document.getElementById('ckBar').style.display='none';localStorage.setItem('rc_ck','1')">Принять</button>
        <button onclick="document.getElementById('ckBar').style.display='none';localStorage.setItem('rc_ck','reject')" style="background:transparent;color:var(--gray);border:1px solid currentColor;box-shadow:none">Отказаться</button>
    </div>
</div>
```

---

## 8. Добавить ответственного за ПДн в privacy.html

Найти блок `.operator` (строка ~33) и добавить **после него** (не внутри):
```html
<div class="operator" style="margin-top:12px">
    <strong>Ответственный за организацию обработки персональных данных</strong>
    Пермякова Алёна Михайловна, директор<br>
    Email: <a href="mailto:r.c.razvitie@mail.ru">r.c.razvitie@mail.ru</a> · Тел.: <a href="tel:+73852506146">+7 (3852) 50-61-46</a>
</div>
```

---

## Итог

После выполнения всех пунктов:
1. Вывести список изменённых файлов
2. **Push не делать** — только по явному запросу заказчицы
