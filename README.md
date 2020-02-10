# Functionalities to increase your python powers! 💥

![](power.jpg)

## Table of Contents

- [Built-in functionalities](#built-in-functionalities)
  - [Indexing](#indexing)
    - [Reverse string](#reverse-string)
  - [Comprehensions](#comprehensions)
    - [List Comprehensions](#list-comprehensions)
    - [Dictionary Comprehensions](#dictionary-comprehensions)
    - [Set Comprehensions](#set-comprehensions)
    - [if/else and nested Comprehensions](#ifelse-and-nested-comprehensions)
- [Built-in functions](#built-in-functions)
  - [zip()](#zip)
  - [map()](#map)
  - [filter()](#filter)
  - [enumerate()](#enumerate)
- [Standard libraries](#standard-libraries)
  - [collections](#collections)
    - [Counter()](#counter)
- [Numpy functions](#numpy-functions)
  - [np.where()](#npwhere)
  - [np.arg*()](#nparg)
- [Smaller libraries](#smaller-libraries)
  - [holidays](#holidays)


## Built-in functionalities

### Indexing

#### Reverse string

Reverse a string with this simple slicing:

```python
name = 'Sheldon'
name[::-1]
> 'nodlehS'
```

But how does this work? When you are slicing a string you can also specify the step `your_string[start:end:step]`, when you set step as -1, it will go backwards (so to speak), and when you don't specify start and end slicing arguments, it will take the whole string. That's why the `[::-1]` slicing will reverse your string.


### Comprehensions

Comprehensions are the compact form of for loops.

#### List Comprehensions

Instead of:

```python
squared = []
for i in range(11):
    squared.append(i**2)

print(squared)
> [0, 1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

You could write:

```python
squared = [i**2 for i in range(11)]
print(squared)
> [0, 1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```

#### Dictionary Comprehensions

Instead of:

```python
len_of_names = {}
names = ['Sheldon', 'Howard', 'Leonard', 'Raj', 'Penny', 'Bernadette', 'Amy']
for name in names:
    len_of_names[name] = len(name)

print(len_of_names)
> {'Sheldon': 7, 'Howard': 6, 'Leonard': 7, 'Raj': 3, 'Penny': 5, 'Bernadette': 10, 'Amy': 3}
```

You could write:

```python
names = ['Sheldon', 'Howard', 'Leonard', 'Raj', 'Penny', 'Bernadette', 'Amy']
len_of_names = {name: len(name) for name in names}
print(len_of_names)
> {'Sheldon': 7, 'Howard': 6, 'Leonard': 7, 'Raj': 3, 'Penny': 5, 'Bernadette': 10, 'Amy': 3}
```

#### Set Comprehensions

Instead of:

```python
integers = [0, 0, 1, 2, 2, 3, 4, 5, 6, 6, 7, 8, 9, 10]
equal_numbers = set()

for elem in integers:
    if elem % 2 == 0:
        equal_numbers.add(elem)

print(equal_numbers)
> {0, 2, 4, 6, 8, 10}
```

You could write:

```python
integers = [0, 0, 1, 2, 2, 3, 4, 5, 6, 6, 7, 8, 9, 10]
equal_numbers = {elem for elem in integers if elem % 2 == 0}
print(equal_numbers) 
> {0, 2, 4, 6, 8, 10}
```

#### if/else and nested Comprehensions
If you want to include an if/else-statement in your comprehension, follow the schema:

```python
[f(x) if condition else g(x) for x in sequence]
```

If you only need an if-statement:

```python
[f(x) for x in sequence if condition]
```

You can also nest multiple loops with comprehensions:

```python
[a for a in sequence_A for b in sequence_B]
```

Where A is the outer loop and B is the inner loop. This makes the nested comprehension equivalent to:

```python
for a in sequence_A:
    for b in sequence_B:
        print(a)
```


## Built-in functions

For easy explanation of `zip()`, `map()`, `filter()` and `enumerate()` I'll use the following lists:

```python
color_names = ['red', 'blue', 'teal', 'orange', 'yellow', 'gray']
color_hex = ['#ff0000', '#0000ff', '#008080', '#ff6600', '#ff9900', '#808080']
random_colors = ['blue', 'teal', 'red', 'gray', 'orange', 'blue', 'yellow', 'teal', 'red', 'blue']
```

### zip()
Make an iterator that aggregates elements from each of the iterables.

By using zip you can construct a new iterator out of two or more iterables, in this case `color_names` and `color_hex`. With this you could for example make a dictionary:
```python
name2hex = dict(zip(color_names, color_hex))
print(name2hex)
> {'red': '#ff0000', 'blue': '#0000ff', 'teal': '#008080', 'orange': '#ff6600', 'yellow': '#ff9900', 'gray': '#808080'}
```

### map()
Return an iterator that applies function to every item of iterable, yielding the results.

In this case, we would like to map the color names in `random_colors` into the corresponding hexadecimal value. The `map()` takes a function to apply to an iterator (the list of color names `random_colors`). The function can be created as a lambda function from your dictionary:

```python
name2hex_foo = lambda x: name2hex[x]
print(name2hex_foo('red'))
> '#ff0000'
```

All you have to do now is apply (read: map) the function `name2hex_foo` onto the iterator `random_colors`:

```python
random_colors_hex = list(map(name2hex_foo, random_colors))
print(random_colors_hex)
> ['#0000ff', '#008080', '#ff0000', '#808080', '#ff6600', '#0000ff', '#ff9900', '#008080', '#ff0000', '#0000ff']
```

### filter()
Construct an iterator from those elements of iterable for which function returns true.

In the hexadecimal system, F is known as the highest value. Every hexadecimal number beginning with FF, has the maximum amount of red in the color. For the sake of this example, we assume that all warm colors starts with FF. We would like to filter all warm colors out of the list `random_colors`:

```python
warm_colors = lambda x: 'ff' == name2hex[x][1:3]
print(list(filter(warm_colors, random_colors)))
> ['red', 'orange', 'yellow', 'red']
```

### enumerate()
Often you'll see, that python developers use the `range()` function in combination with the `len()` function to create an index in a `for` loop:

```python
for i in range(len(color_names)):
    print(i, color_names[i])
> 0 red
> 1 blue
> 2 teal
> 3 orange
> 4 yellow
> 5 gray
```



We're actually not taking advantage of the fact, that the list `color_names` is an iterater but rather making a fake index. Use `enumerate()` instead, which return an enumerate object, which itself is an iterator:

```python
for i, color_name in enumerate(color_names):
    print(i, color_name)
> 0 red
> 1 blue
> 2 teal
> 3 orange
> 4 yellow
> 5 gray
```

You can also set the argument `start` to specify the starting number of the index, which is extremely helpful instead of the often seen `i+1` index:

```python
for i, color_name in enumerate(color_names, start=1):
    print(i, color_name)
> 1 red
> 2 blue
> 3 teal
> 4 orange
> 5 yellow
> 6 gray
```

How about if the iterator is a dictionary? Well, you just need to unpack it with `.items()`:

```python
for i, (clr_name, clr_hex) in enumerate(name2hex.items()):
    print(i, clr_name, clr_hex)
> 0 red #ff0000
> 1 blue #0000ff
> 2 teal #008080
> 3 orange #ff6600
> 4 yellow #ff9900
> 5 gray #808080
```

## Standard libraries

### collections

#### Counter()

You probably already know the `.value_counts()` function you can apply to a pandas series. But did you know, that the `Counter()` function from the collections library can do (pretty much) the same thing without converting a list to a pandas series and use their built-in function? Check this out:

```python
from collections import Counter

random_colors = ['blue', 'teal', 'red', 'gray', 'orange', 'blue', 'yellow', 'teal', 'red', 'blue']
clr_counts = Counter(random_colors)
print(clr_counts.most_common())
> [('blue', 3),
>  ('teal', 2),
>  ('red', 2),
>  ('gray', 1),
>  ('orange', 1),
>  ('yellow', 1)]
```

And you can even update your Counter object with more values:

```python
clr_counts.update(['teal', 'teal'])
print(clr_counts.most_common())
> [('teal', 4),
>  ('blue', 3),
>  ('red', 2),
>  ('gray', 1),
>  ('orange', 1),
>  ('yellow', 1)]
```

Maybe you only want the top three colors in the Counter object:

```python
print(clr_counts.most_common(3))
> [('teal', 4),
>  ('blue', 3),
>  ('red', 2)]
```

Or maybe you were wondering, how many times red appeared in the Counter object:

```python
print(clr_counts['red'])
> 2
```


## Numpy functions

For easy explanation of `np.where()` and `np.arg*()` I'll use the following arrays:

```python
integers = np.array([1, 2, 3, 4, 9, 10, 42, 73, 5, 6, 7, 8, 1337, 0])
equal_numbers = integers % 2 == 0
print(equal_numbers)
> [False, True, False, True, False, True, True, False, False, True, False, True, False, True]
```

### np.where()
If you want the values of the equal numbers you would subset `integers` by `equal_numbers`:

```python
print(integers[equal_numbers])
> [2, 4, 10, 42, 6, 8, 0]
```

but often you would want the indices of the `equal_numbers` in `integers`, this is where `np.where()` is powerful:

```python
print(np.where(equal_numbers)[0])
> [1, 3, 5, 6, 9, 11, 13]
```

### np.arg*()
If you want the minimum and maximum value of `integers` you would use `min()` and `max()`:

```python
print(min(integers))
> 0
print(max(integers))
> 1337
```

but if you need the index, `np.argmin()` and `np.argmax()` are your friends:

```python
print(np.argmin(integers))
> 13
print(np.argmax(integers))
> 12
```

Another arg-function worth mentioning is the `np.argsort()`, which gives you the indices of the sorted array:

```python
print(np.argsort(integers))
> [13, 0, 1, 2, 3, 8, 9, 10, 11, 4, 5, 6, 7, 12]
print(integers[np.argsort(integers)])
> [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 42, 73, 1337]
```

## Smaller libraries

### holidays
Ever working with dates? You can do all sort of feature engineering on dates, one of them are the binary question; is it a holiday?

```python
import holidays

print(holidays.Denmark(years=2019))
> {datetime.date(2019, 1, 1): 'Nytårsdag',
>  datetime.date(2019, 4, 14): 'Palmesøndag',
>  datetime.date(2019, 4, 18): 'Skærtorsdag',
>  datetime.date(2019, 4, 19): 'Langfredag',
>  datetime.date(2019, 4, 21): 'Påskedag',
>  datetime.date(2019, 4, 22): 'Anden påskedag',
>  datetime.date(2019, 5, 17): 'Store bededag',
>  datetime.date(2019, 5, 30): 'Kristi himmelfartsdag',
>  datetime.date(2019, 6, 9): 'Pinsedag',
>  datetime.date(2019, 6, 10): 'Anden pinsedag',
>  datetime.date(2019, 12, 25): 'Juledag',
>  datetime.date(2019, 12, 26): 'Anden juledag'}
```

You can easily create a function, in this case `is_holiday()` to lookup up, if a given `datetime` object is a holiday:

```python
def is_holiday(dt):
    try:
        if holidays.Denmark(years=dt.year)[dt]:
            return True
    except KeyError:
        return False
```

And say you have a pandas dataframe with dates:

```python
start = datetime(year=2019, month=1, day=1)
end = datetime(year=2019, month=12, day=31)
df = pd.DataFrame()
df['date'] = pd.date_range(start, end)
print(df.head())
>         date
> 0 2019-01-01
> 1 2019-01-02
> 2 2019-01-03
> 3 2019-01-04
> 4 2019-01-05
```

It's pretty straight-forward to enrich your dataset:

```python
df['holiday'] = df.date.apply(is_holiday)
print(df.head())
>         date  holiday
> 0 2019-01-01     True
> 1 2019-01-02    False
> 2 2019-01-03    False
> 3 2019-01-04    False
> 4 2019-01-05    False
```


