# Query

## Introduction
```php
$sigmie->newQuery(index: 'disney-movies')
        ->bool(function (Boolean $boolean) {

            $boolean->filter->matchAll();

            $boolean->filter()->multiMatch('goofy', ['name', 'description']);

            $boolean->must->term('is_active', true);

            $boolean->mustNot->term('is_active', false);

            $boolean->mustNot->wildcard('foo', '**/*');

            $boolean->should->bool(fn (Boolean $boolean) => $boolean->must->match('name', 'Mickey'));

        })
        ->sort('name.keyword', 'asc')
        ->fields(['name','description', 'stock', 'rating'])
        ->from(0)
        ->size(15)
        ->getDSL();
```

```php
$newQuery->get();
```

## Queries

### Boolean

```php
$newQuery->bool(function (Boolean $boolean) {

});
```

#### Must
```php
    $boolean->must()->term('is_active', true);
```
#### Must Not

```php
    $boolean->mustNot()->term('is_active', true);
```

#### Should

```php
    $boolean->should()->term('is_active', true);
```

#### Filter

```php
    $boolean->filter()->term('is_active', true);
```

### Range
```php
$newQuery->range('count', ['>=' => 233]);
```

### Term
```php
$newQuery->term('is_active', true);
```

### Match All
```php
$newQuery->matchAll();
```

### Match None
```php
$newQuery->matchNone();
```

### Multi Match
```php
$newQuery->multiMatch();
```

### Exists
```php
$newQuery->exists();
```

### Ids
```php
$newQuery->ids(['','','']);
```
### Fuzzy

```php
$newQuery($name)->fuzzy('name','lion');
```

### Terms
```php
$newQuery->terms(field:'category', values:['horror','action']);
```

### Regex
```php
$newQuery->regex('category','/(horror|action)/');
```

### Wildcard
```php
$newQuery->wildcard('name','john*');
```

## Sort
```php
$newQuery->sort('name.keyword', 'asc')
        ->sort('_score');
```

## From
```php
$newQuery->from(0);
```
## Size
```php
$newQuery->size(15);
```

## Boost
```php
$newQuery->matchAll(boost: 5)->get();
```