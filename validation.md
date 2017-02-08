# Eloquent

## Find by if

```php
App\Model::Find($id);
```

## Fillable

```php
protected $fillable = ['name'];
$flight = App\Flight::create(['name' => 'Flight 10']);
// Si flight est déjà un model
$flight->fill(['name' => 'Flight 22']);

//Update
$flight = App\Flight::updateOrCreate(
    ['departure' => 'Oakland', 'destination' => 'San Diego'],
    ['price' => 99]
);
```

## Validation

```php
$this->validate($request, [
    'title' => 'required|min:3',
    'content' => 'required|min:5',
])
```

## Pagination

```php
// Controller
$models = App\Model::paginate($NbElementParPage);
// Ou
$models = App\Model::simplePaginate($NbElementParPage);
// View
{{ $models->links(['template']) }}
```

## Messages Flash

```php
//Controller
session()->flash($key, $value);
//View
@if(session()->has($key))
    {{ session()->get($key) }} 
    // Ou 
    {{ session($key) }}
@endif
```

## Routes

```php
{{ route('Name.route'[,$events]) }}
```

## Tips

```php
$lol = 'lol';
sprintf('Bonjour #%s', $lol) // Bonjour lol
```

```php
// Retenir la derniere valeur entrée dans un form
// old('title')
{{ old('title') ? old('title') : $event->title }}
// Ou
{{ old('title') ? : $event->title }}
```

```php
php artisan make:controller PhotoController --resource
```

```php
str_plural('Evenement', $event->count())
//Va mettre au pluriel si les evenement sont supérieur à deux
```