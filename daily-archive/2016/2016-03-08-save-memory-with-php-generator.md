---
layout: post
summary: "Save memory by switching to PHP Generator"
tags: programming php
---
> Source: [https://evertpot.com/switching-to-generators/](https://evertpot.com/switching-to-generators/)
>
> Read more: [http://php.net/manual/en/language.generators.overview.php](http://php.net/manual/en/language.generators.overview.php)

### The memory problem

If our articles table contains a lot of records, we’re storing each one of those in the $articles variable. This means that your “peak memory usage” is dependent on how many records there are. For many smaller use-cases this might not really be an issue, but sometimes you do have to work with a lot of data.

It’s not uncommon in complex applications for the result of a function like our getArticles to be passed to multiple functions that mangle or modify the data further.

Each of these functions tend to have a (foreach) loop and will grow in memory usage as the amount of data goes up.

```php

<?php

function getArticles() {

   $articles = [];
   $result = $this->db->query('SELECT * FROM articles');

   while($record = $result->fetch(PDO::FETCH_ASSOC)) {

       $articles[] = $this->mapToObject($record);

   }

   return $articles;

}

```

### Generators to the rescue

A generator allows you to return an ‘array-like result’ from a function, but only return one record at a time.

```php

<?php

function getArticles() {

   $result = $this->db->query('SELECT * FROM articles');

   while($record = $result->fetch(PDO::FETCH_ASSOC)) {

       yield $this->mapToObject($record);

   }

}

```

The difference? Every time the getArticles() method ‘generates’ a new record, the function effectively ‘pauses’, and for every iteration of the foreach loop, the function is continued until it hits another yield.
