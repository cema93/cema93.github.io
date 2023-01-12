---
title: Вывод custom categories и custom post types в WordPress
layout: post
date: '2014-05-05 19:30:00'
category: WordPress
---

Небольшой пример, показывающий как можно получить из БД пользовательские категории, относящиеся к определенной таксономии, а также пользовательские посты для каждой из категорий.

```
<?php
$categories = get_categories(array(
	'type'                     => 'post',
	'child_of'                 => 0,
	'parent'                   => '',
	'orderby'                  => 'ID',
	'order'                    => 'ASC',
	'hide_empty'               => 0,
	'hierarchical'             => 1,
	'exclude'                  => '',
	'include'                  => '',
	'number'                   => '',
	'taxonomy'                 => 'cema93-faq-cat',
	'pad_counts'               => false )); 
foreach($categories as $category) {
	//Получаем категории
    echo '<div id="cat-'.$category->cat_ID.'">'.$category->cat_name.'</a></div>';
    //получаем пользовательские посты из данной категории
    $cat = $category->cat_ID;
 
	$args = array(
	'tax_query' => array(
		array(
			'taxonomy' => 'cema93-faq-cat',
			'field' => 'id',
			'terms' => $cat,
		)
	),
	'post_type' => 'cema93-faq',
	'posts_per_page' => -1
);
$posts = get_posts( $args );
	if($posts) {
		echo '<div id="cat-o-'.$category->cat_ID.'">';
		foreach( $posts as $post ) :	
			setup_postdata($post);
			echo the_title().'<br>';
			echo the_content();
		endforeach;
		echo '</div>';
	}
}
?>
```
Полезно почитать:
* get_categories [EN](http://codex.wordpress.org/Function_Reference/get_categories)  [RU](http://wp-kama.ru/function/get_categories)
* WP_Query [EN](http://codex.wordpress.org/Class_Reference/WP_Query) [RU](http://wp-kama.ru/function/wp_query)
* get_posts [EN](http://codex.wordpress.org/Template_Tags/get_posts) [RU](http://wp-kama.ru/function/get_posts)
