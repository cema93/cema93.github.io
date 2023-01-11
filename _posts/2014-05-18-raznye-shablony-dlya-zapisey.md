---
title: Разные шаблоны для записей в WordPress
layout: post
date: '2014-05-18 17:38:00'
category: WordPress
---

В этой статье вы узнаете как сделать для каждой записи или для какой-то отдельной свой уникальеый шаблон. Для этого вам нужно:

1. Создать файл шаблона и назвать его «single-slug.php» или «single-id.php» slug и id это ярлык и идентификатор поста;
2. Сделать копию файла «single.php» и назвать её, к примеру, «single-default.php» тем самым мы разграничим все посты по шаблонам для удобства.
3. Открыть файл «single.php», удалить все содержимое и вставить следующий код:

Если вы хотите всем записям из определенной категории(рубрики) сделать уникальный вид тогда это код для вас:
### Вариант 1 — ID категории(рубрики) в которой находится запись
```
<?php
  $post = $wp_query->post;
 
  if (in_category('32')) { //ID категории
      include(TEMPLATEPATH.'/single-portfolio.php');
  } else {
      include(TEMPLATEPATH.'/single-default.php');
  }
?>
```
### Вариант 2 — slug(Ярлык) категории(рубрики) в которой находится запись
```
<?php
  $post = $wp_query->post;
 
  if (in_category('portfolio')) { //slug  категории
      include(TEMPLATEPATH.'/single-portfolio.php');
  } else {
      include(TEMPLATEPATH.'/single-default.php');
  }
?>
```
Если надо использовать не 2, а 3 и больше вариантов то используем код по аналогии с примером:
```
if (in_category(‘portfolio’)) { //slug категории
	include(TEMPLATEPATH.’/single-portfolio.php’);
} elseif (in_category(‘news’)) { //slug категории
	include(TEMPLATEPATH.’/single-news.php’);
} else {
	include(TEMPLATEPATH.’/single-default.php’);
}
```
**Как видите, мы указываем WP**: если категория с ID=32 (или с названием «portfolio» — см. 2 вариант кода), тогда следует использовать шаблон для страниц записей «single-portfolio.php», но если категория имеет другой ID, тогда следует использовать шаблон «single-default.php».
И на этом также всё, Вам осталось только отверстать файл «single-portfolio.php» и все записи в указанной категории будут иметь свой вид.

Когда вы делаете отдельные шаблон для записи то, в отличии от рубрик, вы можете называть как хотите, **кроме «single.php»**.

Надеюсь, Вам все было понятно. Если что, спрашивайте в комментариях! ;)
