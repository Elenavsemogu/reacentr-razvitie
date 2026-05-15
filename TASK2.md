# ТЗ-2: Устранение несоответствий по итогам аудита
> Проект: `/Users/elenapapina/Desktop/вся работа/my-company/reacentr-razvitie`  
> Выполнять только пункты 1–5. Пункт 6 (цены) — **ждёт ответа заказчицы, не трогать**.

---

## 1. Добавить «Специалисты» в десктоп-меню

Файл: `index.html`

Найти блок `<nav class="nav">` (строка ~536):
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

## 2. Дополнить legal.html блоками всех 13 специалистов

Файл: `legal.html`

В секции `<h2 id="specialists">Сведения о специалистах</h2>` уже есть 4 карточки (Алагян, Текутьева, Батареева, Катыкин). Добавить после них 9 недостающих — **только** для тех, у кого **нет** документов из `Специалисты.docx`:

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
    <h3>Пермякова Алёна Михайловна</h3>
    <div class="spec-role">Директор, учредитель</div>
</div>

<div class="spec-card">
    <h3>Акимова Лариса Анатольевна</h3>
    <div class="spec-role">Санитарка</div>
</div>
```

Также добавить в карточку Алагян атрибут `id="alagyan"`:
```html
<div class="spec-card" id="alagyan">
```

---

## 3. Добавить контакты надзорных органов в legal.html

Файл: `legal.html`

После блока `<h2>Нормативные документы</h2>` добавить новый раздел:

```html
<h2>Контакты надзорных органов</h2>
<div class="info-block">
    <h3>Федеральная служба по надзору в сфере здравоохранения (Росздравнадзор)</h3>
    <p>Сайт: <a href="https://roszdravnadzor.gov.ru" target="_blank" rel="noopener">roszdravnadzor.gov.ru</a></p>
    <p>Тел. горячей линии: <a href="tel:88002000054">8 800 200-00-54</a> (бесплатно)</p>
    <p>Email: <a href="mailto:info@roszdravnadzor.gov.ru">info@roszdravnadzor.gov.ru</a></p>
</div>
<div class="info-block">
    <h3>Управление Роспотребнадзора по Алтайскому краю</h3>
    <p>Сайт: <a href="https://22.rospotrebnadzor.ru" target="_blank" rel="noopener">22.rospotrebnadzor.ru</a></p>
    <p>Тел.: <a href="tel:+73852260056">+7 (3852) 26-00-56</a></p>
    <p>Адрес: 656010, Барнаул, ул. М. Горького, 28</p>
</div>
<div class="info-block">
    <h3>Министерство здравоохранения Алтайского края</h3>
    <p>Сайт: <a href="https://minzdrav.alregn.ru" target="_blank" rel="noopener">minzdrav.alregn.ru</a></p>
    <p>Тел.: <a href="tel:+73852677204">+7 (3852) 67-72-04</a></p>
</div>
```

---

## 4. Улучшить cookie-баннер

Файл: `index.html`

Найти блок `<div class="ck" id="ckBar">`. Заменить на:

```html
<div class="ck" id="ckBar">
    <h4>Cookie</h4>
    <p>Сайт использует cookie для корректной работы. <a href="privacy.html" style="color:var(--accent);text-decoration:underline">Политика конфиденциальности</a></p>
    <div style="display:flex;gap:10px;flex-wrap:wrap;margin-top:8px">
        <button onclick="document.getElementById('ckBar').style.display='none';localStorage.setItem('rc_ck','1')">Принять</button>
        <button onclick="document.getElementById('ckBar').style.display='none';localStorage.setItem('rc_ck','reject')" style="background:transparent;color:var(--gray);border:1px solid var(--gray);box-shadow:none">Отказаться</button>
    </div>
</div>
```

---

## 5. Добавить ответственного за ПДн в privacy.html

Файл: `privacy.html`

После блока `.operator` (с реквизитами) добавить:

```html
<div class="operator" style="margin-top:12px">
    <strong>Ответственный за организацию обработки персональных данных</strong>
    Пермякова Алёна Михайловна, директор<br>
    Email: <a href="mailto:r.c.razvitie@mail.ru">r.c.razvitie@mail.ru</a><br>
    Тел.: <a href="tel:+73852506146">+7 (3852) 50-61-46</a>
</div>
```

---

## 6. ⛔ НЕ ТРОГАТЬ — ждём решения заказчицы

Цены в `index.html` **не менять** до получения подтверждения о том, какой прайс актуален.

---

## 7. Итог работы

После всех пунктов:
1. Вывести список изменённых файлов
2. **Не делать push** — только по явному запросу
