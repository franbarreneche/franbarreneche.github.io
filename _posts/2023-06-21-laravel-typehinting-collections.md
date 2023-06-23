---
layout: post
title:  Laravel typehinting collections
date:   2023-06-21 23:30:00
description: A small tip to help you IDE
tags: laravel php collections array
categories: code
---
As it has become popular lately, it is very common nowadays to add type hints to class attributes, function parameters, and return types.

Since PHP currently doesn't have support for generics, we can only indicate that a variable is of type "Collection" but there is no way with the current type system to specify what type of data is contained within that collection.

One way to avoid this language limitation is to provide data type annotations using PHP Doc comments, in order to provide additional information to the IDE about the data type. 

Here's an example:

```php
class Test
{
    protected Collection $dontKnowWhatIsInside;
    /** @var Collection<int,CustomType1> */
    protected Collection $knowWhatIsInside1;
    /** @var Collection<string,CustomType2> */
    protected Collection $knowWhatIsInside2;
}
```


The same problem arises when trying to provide information about the data type contained within a regular PHP array, and similarly, PHP Doc comments can be used to provide this information even allowing the use of data types that are unions.

Here's an example:

```php
class Test
{
    protected array $dontKnowWhatIsInside;
    /** @var CustomType1[] */
    protected array $knowWhatIsInside1;
    /** @var array<CustomType2|null> */
    protected array $knowWhatIsInside2;
}
```
