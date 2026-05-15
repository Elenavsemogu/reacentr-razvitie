# TASK3 — Реацентр Развитие: правки интерфейса и оптимизация

**Исполнитель:** авторежим (агент).  
**Дизайн-решения:** приняты заранее, строго следовать им. Никаких отступлений без согласования.  
**Важно:** перед началом прочитать `.context.md`. После выполнения всех задач — сформировать отчёт `WORK_REPORT.md` (см. п. 8).

---

## 1. Прейскурант — визуальный рефакторинг

**Проблема:** после автодобавления цен секция `#prices` превратилась в плоский длинный список — перегружает страницу.

**Дизайн-решение (принято):** аккордеон по категориям.

### Что сделать

В секции `#prices` заменить текущую `.price-grid` на **аккордеон-компонент** со следующей структурой:

```
[▼ Консультации]            — по умолчанию раскрыт
[▼ Диагностика]             — по умолчанию раскрыт
[▼ Микротоковая рефлексотерапия (МТРТ)]  — по умолчанию раскрыт
[▷ Занятия и процедуры]     — по умолчанию СВЁРНУТ (много строк)
```

**CSS-правила аккордеона:**
- Заголовок категории: фон `var(--accent-pale)`, левый бордюр 3px `var(--accent)`, padding 14px 20px, шрифт Geologica 600 15px, cursor pointer
- Стрелка-иконка справа: `▾` / `▴`, анимация rotate 0.2s
- Тело: фон белый, overflow hidden, transition max-height 0.3s ease
- Строки `.pr`: border-bottom `1px solid #F1F5F9`, padding 10px 20px
- Значение "бесплатно": цвет `#16a34a`, font-weight 700
- Значение числовое: цвет `var(--accent)`, font-weight 700
- На desktop: аккордеон в 2 колонки (CSS grid 1fr 1fr); «Занятия и процедуры» занимает обе колонки (grid-column: 1/-1)
- На mobile < 768px: 1 колонка, все аккордеоны по умолчанию свёрнуты

**Логика JS:** toggle класса `.open` на клик по заголовку. Простой ванильный JS, без библиотек.

**Содержимое аккордеонов — строго по прайсу (не менять цифры):** взять из текущего HTML строки `.pr` — они уже правильные после предыдущего обновления.

---

## 2. Страница legal.html — полный рефакторинг

**Проблема:** страница выглядит как голый текстовый документ. Ссылки на документы специалистов — просто текст, непонятно что это и как работает.

**Дизайн-решение (принято):**

### 2.1 Заголовочная часть и навигация

Добавить в `legal.html` такой же header и footer, как в `index.html` (скопировать блоки). Шрифты и CSS-переменные подключить из `index.html` (скопировать `:root` и базовые стили).

Под header — блок с якорными ссылками-навигацией:

```
Реквизиты · Лицензия · Специалисты · Контакты надзорных органов
```

Стиль — горизонтальные пилюли с border, как chip/badge. Padding 8px 18px, border-radius 100px, border 1.5px solid var(--accent), color var(--accent), hover: фон var(--accent-pale).

### 2.2 Секция «Документы клиники»

Карточки-плитки в сетке 3 колонки (на mobile 1-2):
- Карточка: белый фон, border-radius 16px, shadow-sm, padding 24px
- Иконка PDF (SVG, красная) + название документа (полужирный) + дата + кнопка «Открыть документ» → открывает pdf в новой вкладке (target="_blank")
- Уже есть: `docs/license.pdf`

### 2.3 Секция «Специалисты» — ключевая

**Принцип:** один специалист = одна карточка. Карточка закрытая по умолчанию. Клик на «▾ Документы об образовании» раскрывает список документов-кнопок.

**Разметка одной карточки:**
```html
<div class="spec-card">
  <div class="spec-card-head">
    <img src="img/team-[slug].jpg" class="spec-avatar" alt="...">
    <div class="spec-card-info">
      <strong class="spec-name">Фамилия Имя Отчество</strong>
      <span class="spec-role">Должность</span>
    </div>
    <button class="spec-docs-toggle" aria-expanded="false">
      <span>Документы</span>
      <svg ...><!-- chevron --></svg>
    </button>
  </div>
  <div class="spec-docs-body" hidden>
    <a href="specialist.html?id=slug" class="doc-chip">
      <svg ...><!-- pdf icon --></svg>
      Дипломы и сертификаты
    </a>
    <!-- если документов нет: -->
    <span class="doc-chip doc-chip--empty">Документы на оформлении</span>
  </div>
</div>
```

**CSS карточки:**
- `.spec-card`: background white, border-radius 16px, border 1px solid #E2E8F0, padding 0, overflow hidden, transition box-shadow .2s
- `.spec-card-head`: display flex, align-items center, gap 16px, padding 20px
- `.spec-avatar`: width 52px, height 52px, border-radius 50%, object-fit cover
- `.spec-name`: font Geologica 600 15px, color var(--black)
- `.spec-role`: font-size 13px, color var(--gray)
- `.spec-docs-toggle`: margin-left auto, display flex, align-items center, gap 8px, padding 8px 14px, background var(--accent-pale), border 1px solid var(--accent), border-radius 100px, font-size 13px, font-weight 600, color var(--accent), cursor pointer; chevron rotate при [aria-expanded="true"]
- `.spec-docs-body`: padding 0 20px 20px, display flex, flex-wrap wrap, gap 8px
- `.doc-chip`: inline-flex, align-items center, gap 6px, padding 8px 16px, background #FEF2F2, border 1px solid #FECACA, border-radius 100px, font-size 13px, color #991b1b, font-weight 600; hover: background #FEE2E2
- `.doc-chip--empty`: background #F8FAFC, border-color #E2E8F0, color var(--gray-light)

**Сетка карточек:** CSS grid, `grid-template-columns: repeat(auto-fill, minmax(340px, 1fr))`, gap 16px

**JS:** клик на `.spec-docs-toggle` → toggle `hidden` на `.spec-docs-body` + toggle `aria-expanded` + поворот chevron.

### 2.4 Контакты надзорных органов

Сохранить текущий контент, оформить как простой список с иконками, в отдельной секции.

---

## 3. Оптимизация изображений

**Задача:** конвертировать изображения в `img/` (кроме `team-*.jpg`) в WebP с двумя размерами для srcset.

**Список файлов для обработки** (проверить наличие в `img/`):
- `hero-*.jpg` (капсулы в hero)
- `method-procedure.jpg`
- `gan-*.jpg`

**Команда для конвертации** (запустить в папке проекта):
```bash
for f in img/hero-*.jpg img/method-procedure.jpg img/gan-*.jpg; do
  [ -f "$f" ] || continue
  base="${f%.jpg}"
  # 800px wide version
  sips -z 0 800 "$f" --out "${base}-800.jpg" 2>/dev/null
  # WebP 85% quality (если есть cwebp)
  if command -v cwebp &>/dev/null; then
    cwebp -q 85 "$f" -o "${base}.webp"
    cwebp -q 85 "${base}-800.jpg" -o "${base}-800.webp"
  fi
done
```

**Если cwebp недоступен** — пропустить WebP, сделать только сжатые JPEG через `sips`.

**В HTML** заменить `<img src="img/foo.jpg">` на:
```html
<picture>
  <source srcset="img/foo.webp" type="image/webp">
  <source srcset="img/foo.jpg" type="image/jpeg">
  <img src="img/foo.jpg" alt="..." loading="lazy">
</picture>
```

Для hero-капсул добавить `loading="eager"` (они выше fold), остальные — `loading="lazy"`.

---

## 4. Hero-секция — sticky-скролл текстовой колонки

**Проблема:** капсулы с фото выше текстовой части. При прокрутке hero текст уходит из вида раньше, чем капсулы.

**Дизайн-решение (принято):** `position: sticky` на `.hero-copy`.

**Изменить CSS:**

```css
/* Было: */
.hero-inner { align-items: start; }
.hero-copy { padding-top: 6px; }

/* Стало: */
.hero-inner { align-items: start; min-height: 620px; }
.hero-copy {
  padding-top: 6px;
  position: sticky;
  top: 100px;         /* отступ от верха вьюпорта, ниже header */
  align-self: start;  /* обязательно для sticky в grid */
}
```

На mobile (< 768px) — убрать sticky (он там не нужен, т.к. колонки вертикально):
```css
@media (max-width: 767px) {
  .hero-copy { position: static; }
}
```

---

## 5. Favicon

**Дизайн-решение (принято):** Скруглённый квадрат с брендовым градиентом, белая буква «Р».

**Создать файл `img/favicon.svg`:**
```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 64 64">
  <defs>
    <linearGradient id="g" x1="0%" y1="0%" x2="100%" y2="100%">
      <stop offset="0%" stop-color="#1D4CAA"/>
      <stop offset="100%" stop-color="#0EA5E9"/>
    </linearGradient>
  </defs>
  <rect width="64" height="64" rx="16" fill="url(#g)"/>
  <text x="32" y="46" text-anchor="middle" font-family="Georgia,serif"
        font-size="38" font-weight="700" fill="#fff">Р</text>
</svg>
```

**Добавить в `<head>` всех HTML-файлов** (`index.html`, `legal.html`, `privacy.html`, `specialist.html`):
```html
<link rel="icon" href="img/favicon.svg" type="image/svg+xml">
<link rel="icon" href="img/favicon-32.png" sizes="32x32">
<link rel="apple-touch-icon" href="img/favicon-180.png">
```

Сгенерировать `favicon-32.png` и `favicon-180.png` из SVG через `sips` или `rsvg-convert` если доступен. Если нет — оставить только SVG-фавикон (поддерживается всеми современными браузерами).

---

## 6. Подвал — контрастность текста

**Файлы:** `index.html`, `legal.html`, `privacy.html`

**Изменить CSS-правила для footer:**

```css
/* Было */
footer { color: rgba(255,255,255,.65); }
.ft-links a { color: rgba(255,255,255,.55); }
.ft-bottom span { color: rgba(255,255,255,.5); }
.ft-disclaimer { color: rgba(255,255,255,.45); }

/* Стало */
footer { color: rgba(255,255,255,.85); }
.ft-links a { color: rgba(255,255,255,.75); }
.ft-links a:hover { color: #fff; }
.ft-bottom { color: rgba(255,255,255,.8); }
.ft-disclaimer { color: rgba(255,255,255,.7); }
```

Найти все вхождения `rgba(255,255,255,.4` и `rgba(255,255,255,.5` в footer-блоке и поднять прозрачность до `.7`–`.85`.

---

## 7. Логотип в подвале

**Логотип:** `/Users/elenapapina/Desktop/вся работа/papina-icon.svg`  
Скопировать как `img/papina-icon.svg` в папку проекта.

**В блоке `.ft-bottom`** заменить текущую строку `<a href="https://papina.team" ...>сайт от ПАПИНА</a>` на:

```html
<a href="https://papina.team" target="_blank" rel="noopener" class="ft-maker">
  <img src="img/papina-icon.svg" alt="ПАПИНА конструкторская" class="ft-maker-logo">
  <span>Сайт сделан в <strong>ПАПИНА конструкторская</strong></span>
</a>
```

**CSS:**
```css
.ft-maker {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  color: rgba(255,255,255,.7);
  font-size: 13px;
  transition: color .2s;
}
.ft-maker:hover { color: #fff; }
.ft-maker strong { font-weight: 600; }
.ft-maker-logo {
  width: 24px;
  height: 24px;
  opacity: .75;
  filter: brightness(10);   /* делаем белым на синем фоне */
  transition: opacity .2s;
}
.ft-maker:hover .ft-maker-logo { opacity: 1; }
```

---

## 8. Отчёт по выполненным работам

После завершения всех задач создать файл `WORK_REPORT.md` в корне проекта:

```markdown
# Отчёт о выполненных работах — Реацентр Развитие
Дата: [дата выполнения]

## Статус задач

| # | Задача | Статус | Файлы изменены |
|---|--------|--------|----------------|
| 1 | Прейскурант — аккордеон | ✅/⚠️/❌ | index.html |
| 2 | legal.html — рефакторинг | ✅/⚠️/❌ | legal.html |
| 3 | Оптимизация изображений | ✅/⚠️/❌ | img/ |
| 4 | Hero sticky-скролл | ✅/⚠️/❌ | index.html |
| 5 | Favicon | ✅/⚠️/❌ | img/favicon.svg, *.html |
| 6 | Контрастность footer | ✅/⚠️/❌ | index.html, legal.html, privacy.html |
| 7 | Лого в footer | ✅/⚠️/❌ | index.html, img/papina-icon.svg |

## Что проверить вручную

- [ ] Открыть сайт в браузере, прокрутить hero — текст должен "плыть" вниз
- [ ] Открыть прейскурант — аккордеоны должны раскрываться по клику
- [ ] Открыть legal.html — карточки специалистов, документы по клику
- [ ] Проверить favicon во вкладке браузера
- [ ] Проверить подвал — лого ПАПИНА, контрастность текста

## Незакрытые задачи (если есть)

[Описать что не удалось и почему]

## Для главного разработчика

[Технические заметки: что сделано нестандартно, на что обратить внимание]
```

---

## Правила для авторежима

1. **Не менять цены** — они уже правильные после предыдущего обновления
2. **Не изобретать дизайн** — все дизайн-решения описаны выше
3. **Не трогать** `specialist.html`, `js/`, `docs/`
4. **Делать commit только если явно попросят** — после выполнения всех задач написать итог и ждать
5. При ошибке в одном пункте — не останавливаться, переходить к следующему, отметить в отчёте
