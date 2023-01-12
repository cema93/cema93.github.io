---
title: Как удалять миграции в Laravel
layout: post
date: '2019-11-02 02:23:00'
category: Laravel
---

Если вы случайно создали файл миграции с  не правильным именем (команда  `php artisan migrate:make`) и хотите её удалить то:
## Если комаина php artisan migrate не выполнена
1. Вручную удаляете с диска файл миграции `app/database/migrations/my_migration_file_name.php`
2. Обновляете файл composer autoload командой: `composer dump-autoload`
3. Готово
## Если комаина php artisan migrate выполнена
a) Отменяете последнюю миграцию командой `migrate:rollback`

b) Если migrate:rollback не сработала, тогда делаете откат руками:

1. Вручную удаляете с диска файл миграции `app/database/migrations/my_migration_file_name.php`
2. Обновляете файл composer autoload командой: `composer dump-autoload`
3. Изменяете  базу данных, удаляя последнюю запись из таблицы миграции
