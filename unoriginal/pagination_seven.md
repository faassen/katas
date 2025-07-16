# Kata: Pagination Seven

Pagination can be found in many websites on the Internet. Most of the time you
can see the current page and going to the previous and the next page. Sometimes
you can go to the first and the last page. Some information like total pages
number can be shown.

Aware of the need for all these contraints, we found a lot of pagination
example like:

Simple pagination:

```
< 42 >
```

Advanced pagination:

```
<< < Page 42 of 100 > >>
```

Pagination Seven:

But the advanced pagination is really verbose, so we had the idea to represent
first, last, next, previous and current page at the same time. We decided to
use a "Pagination Seven" representation:

```
1 … 41 (42) 43 … 100
```

## Part I

To start, we need to represent all pages up to 7. The goal is to show the
current page between `(` and `)`, as examples:

Page 2 of 5:

```
1 (2) 3 4 5
```

Page 6 of 7:

```
1 2 3 4 5 (6) 7
```

## Part II

Now we need to see the first, last, previous and next page, but we want to use
only 7 slots when total number of pages is above 7. So we need to replace a
group of pages with `…`. Here are some examples:

Page 42 of 100:

```
1 … 41 (42) 43 … 100
```

Page 5 of 9:

```
1 … 4 (5) 6 … 9
```

## Part III

Sometimes we don’t need to show `…` because we are in the first part of the
pagination, so we have:

Page 2 of 9:

```
1 (2) 3 4 5 … 9
```

Page 4 of 9:

```
1 2 3 (4) 5 … 9
```

## Part IV

And now the same idea but for the last part of the pagination:

Page 8 of 9:

```
1 … 5 6 7 (8) 9
```

Page 6 of 9:

```
1 … 5 (6) 7 8 9
```
