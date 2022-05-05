# Prova con CRUDBooster
https://www.youtube.com/watch?v=jgOW-SEN-nw

Per funzionare correttamente, devi usare PHP 7.4.19 (anche sul server) e installare esattamente Laravel 8.0

    composer create-project laravel/laravel:8.0 start-lara-crudbooster
    php artisan migrate

# CRUDBooster
https://github.com/crocodic-studio/crudbooster/blob/v5.6/docs/en/installation.md

    composer require crocodicstudio/crudbooster=5.6.*
    php artisan crudbooster:install

### Se esce l'errore

    Illuminate\Contracts\Container\BindingResolutionException
    Target class [Database\Seeders\CBSeeder] does not exist.

devo andare in vendor\crocodicstudio\crudbooster\src\database\seeds\CBSeeder.php e aggiungere

    namespace Database\Seeders;

### Accesso
Vado in /admin/login per loggarmi con le credenziali della documentazione
- email : admin@crudbooster.com
- password : 123456

# Come creare i CRUD - esempio con Post

    php artisan make:model Post -m
    php artisan migrate

Vado in BE su Module Generator e seleziono la tabella posts: qui genero tutto

Una volta creati tutti i crud, posso creare dei permessi per i miei crud

# Ruoli e permessi con CRUDBooster

- Aggiungo almeno uno/due utenti nuovi e non li setto come superadmin
- Privileges Roles / List Privilege / Add Data : configuro i permessi di questo ruolo
  - I ruoli così creati li posso associare poi ai vari utenti che creo 
- Menu Management: associo i vari ruoli ai menu (di default ogni menu è associato solo a superadmin)
  - Altrimenti di default ogni utente non superadmin non può vedere niente
  - Tutti i menu che ci sono inizialmente son solo per il superadmin (giustamente perchè sono di amministrazionwe)

# API con CRUDBooster - esempio con Student

    php artisan make:model Student -mf

Faccio anche la factory giusto per popolare velocemente il DB
- LISTING = student.index
- CREATE/UPDATE/DELETE = student.store/update/destroy (metodo POST)

Ho solo i metodi GET e POST. Nelle POST devo inserire anche i parametri

Su Postman ho un 403 senza API secret key.
- La genero nella sua tab
- La inserisco in {POST} api/get-token come parametro chiamato **secret**
- Il token generato lo inserisco nei vari endpoint come Auth/Bearer token (non avrò più il 403)
