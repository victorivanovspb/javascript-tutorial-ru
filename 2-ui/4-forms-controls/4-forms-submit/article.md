# Формы: отправка, событие и метод submit

Событие `submit` возникает при отправке формы. Наиболее частое его применение -- это *валидация* (проверка) формы перед отправкой. 

Метод `submit` позволяет инициировать отправку формы из JavaScript, без участия пользователя. Далее мы рассмотрим их важные детали использования.
[cut]
## Событие submit

Чтобы отправить форму на сервер, у посетителя есть два способа:

<ol>
<li>**Первый -- это нажать кнопку `<input type="submit">` или `<input type="image">`.**</li>
<li>**Второй -- нажать Enter, находясь на каком-нибудь поле.**</li>
</ol>

Какой бы способ ни выбрал посетитель -- будет сгенерировано событие `submit`. Обработчик в нём может проверить данные и, если они неверны, то вывести ошибку и сделать `event.preventDefault()` -- тогда форма не отправится на сервер.

Посмотрим это на живом примере. 

Оба способа выдадут сообщение, форма не будет отправлена:

```html
<!--+ autorun height=80 -->
<form onsubmit="alert('submit!');return false">
  Первый: Enter в текстовом поле <input type="text" value="Текст"><br>
  Второй: Нажать на "Отправить": <input type="submit" value="Отправить">
</form>

</button>
```

Ожидаемое поведение:

<ol><li>Перейдите в текстовое поле и нажмите Enter, будет событие, но форма не отправится на сервер благодаря `return false` в обработчике.</li>
<li>То же самое произойдет при клике на `<input type="submit">`.</li>
</ol>

[smart header="Взаимосвязь событий `submit` и `click`"]

**При отправке формы путём нажатия Enter на текстовом поле, на элементе `<input type="submit">` везде, кроме IE<9, генерируется событие `click`.**

Это довольно забавно, учитывая что клика-то и не было.

```html
<!--+ autorun height=80 -->
<form onsubmit="alert('submit');return false">
 <input type="text" size="30" value="Нажми здесь Enter">
 <input type="submit" value="Submit" *!*onclick="alert('click')"*/!*>
</form>
```

[/smart]

[warn header="В IE<9 событие `submit` не всплывает"]
В IE<9 событие `submit` не всплывает. Впрочем, если вешать обработчик `submit` на сам элемент формы, без использования делегирования, то это не создаёт проблем.
</li>
</ul>
[/warn]


## Метод submit

Чтобы отправить форму на сервер из JavaScript -- нужно вызвать на элементе формы метод `form.submit()`.

При этом само событие `submit` не генерируется. Предполагается, что если программист вызывает метод `form.submit()`, то он выполнил все проверки.

Это используют, в частности, для искусственной генерации и отправки формы. 



