---
type: slides
---

# Filtering

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

Filtering is probably one of the most frequent data manipulations you
will do in data analysis. Filtering is often used when we are either
trying to rid the dataframe of unwanted rows or analyze rows with a
particular column value.

Think of it as a sieve keeping only the rows matching conditions you
have set.

Let’s try to filter the `cereal.csv` dataset.

``` python
df = pd.read_csv('cereal.csv')
df.head()
```

```out
                        name mfr  type  calories  protein  fat  sodium  fiber  carbo  sugars  potass  vitamins  shelf  weight  cups     rating
0                  100% Bran   N  Cold        70        4    1     130   10.0    5.0       6     280        25      3     1.0  0.33  68.402973
1          100% Natural Bran   Q  Cold       120        3    5      15    2.0    8.0       8     135         0      3     1.0  1.00  33.983679
2                   All-Bran   K  Cold        70        4    1     260    9.0    7.0       5     320        25      3     1.0  0.33  59.425505
3  All-Bran with Extra Fiber   K  Cold        50        4    0     140   14.0    8.0       0     330        25      3     1.0  0.50  93.704912
4             Almond Delight   R  Cold       110        2    2     200    1.0   14.0       8       1        25      3     1.0  0.75  34.384843
```

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

## Conditions

Suppose you are trying to find the information for cereals with a
protein content greater than 4g per serving. Our first instinct would be
something along the line of

``` python
df['protein'] > 4
```

```out
0     False
1     False
2     False
3     False
4     False
      ...  
72    False
73    False
74    False
75    False
76    False
Name: protein, Length: 77, dtype: bool
```

This can be translated as "From the `protein` column in the dataframe
`df`, which have values greater than 4?

The output shows all the index labels and a column with True or False
values depending on if the row meets the condition. Cereals with `True`
have a protein content greater than 4 and `False` if they do not.

But we want a dataframe will all the information that only contains the
rows with protein above 4. How can that be achieved?

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

We wrap in within our dataframe similarly to how we slice.

``` python
df[df['protein'] > 4]
```

```out
              name mfr  type  calories  protein  fat  sodium  fiber  carbo  sugars  potass  vitamins  shelf  weight  cups     rating
11        Cheerios   G  Cold       110        6    2     290    2.0   17.0       1     105        25      1     1.0  1.25  50.764999
57  Quaker Oatmeal   Q   Hot       100        5    2       0    2.7    1.0       1     110         0      1     1.0  0.67  50.828392
67       Special K   K  Cold       110        6    0     230    1.0   16.0       3      55        25      1     1.0  1.00  53.131324
```

Normally we use `df['column name':'column name']` to select certain rows
by location, but now we are selecting based on if a condition results in
“True” columns.

The code can be translated to \> Only select the rows from the dataframe
`df` that from the `protein` column in the dataframe `df`, have values
greater than 4"

We can see from the output that only the rows meeting the condition as
displayed.

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

We can do this with equalities as well:

``` python
df[df['protein'] == 4]
```

```out
                                 name mfr  type  calories  protein  fat  sodium  fiber  carbo  sugars  potass  vitamins  shelf  weight  cups     rating
0                           100% Bran   N  Cold        70        4    1     130   10.0    5.0       6     280        25      3     1.0  0.33  68.402973
2                            All-Bran   K  Cold        70        4    1     260    9.0    7.0       5     320        25      3     1.0  0.33  59.425505
3           All-Bran with Extra Fiber   K  Cold        50        4    0     140   14.0    8.0       0     330        25      3     1.0  0.50  93.704912
41                               Life   Q  Cold       100        4    2     150    2.0   12.0       6      95        25      2     1.0  0.67  45.328074
43                              Maypo   A   Hot       100        4    1       0    0.0   16.0       3      95        25      2     1.0  1.00  54.850917
44   Muesli Raisins; Dates; & Almonds   R  Cold       150        4    3      95    3.0   16.0      11     170        25      3     1.0  1.00  37.136863
45  Muesli Raisins; Peaches; & Pecans   R  Cold       150        4    3     150    3.0   16.0      11     170        25      3     1.0  1.00  34.139765
56                 Quaker Oat Squares   Q  Cold       100        4    1     135    2.0   14.0       6     110        25      3     1.0  0.50  49.511874
```

Now we get all the cereals with a protein content of 4g per serving. The
key point to remember here is that we use **2** equal signs.

In Python, a single `=` is used as an assignment operator. We are
setting objects equal to something. Double equal signs, `==`, is used
for comparison. We check if certain values are equivalent to one
another.

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

We can filter categorical columns too. In this example, I only want
cereals from the manufacturer “Q” (For Quaker):

``` python
df[df['mfr'] == 'Q']
```

```out
                  name mfr  type  calories  protein  fat  sodium  fiber  carbo  sugars  potass  vitamins  shelf  weight  cups     rating
1    100% Natural Bran   Q  Cold       120        3    5      15    2.0    8.0       8     135         0      3     1.0  1.00  33.983679
10        Cap'n'Crunch   Q  Cold       120        1    2     220    0.0   12.0      12      35        25      2     1.0  0.75  18.042851
35    Honey Graham Ohs   Q  Cold       120        1    2     220    1.0   12.0      11      45        25      2     1.0  1.00  21.871292
41                Life   Q  Cold       100        4    2     150    2.0   12.0       6      95        25      2     1.0  0.67  45.328074
54         Puffed Rice   Q  Cold        50        1    0       0    0.0   13.0       0      15         0      3     0.5  1.00  60.756112
55        Puffed Wheat   Q  Cold        50        2    0       0    1.0   10.0       0      50         0      3     0.5  1.00  63.005645
56  Quaker Oat Squares   Q  Cold       100        4    1     135    2.0   14.0       6     110        25      3     1.0  0.50  49.511874
57      Quaker Oatmeal   Q   Hot       100        5    2       0    2.7    1.0       1     110         0      1     1.0  0.67  50.828392
```

Here we are using the double equal signs we saw in the last slide.

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

## Multiple Condition Filtering - “and”

We now know how to filter on one condition but how do we filter if we
have many? Perhaps we only want cereals with protein content between 4
to 5 grams? The cereals that meet protein contents greater or equal to 4
are the following:

``` python
df[df['protein'] >= 4]
```

```out
                                 name mfr  type  calories  protein  fat  sodium  fiber  carbo  sugars  potass  vitamins  shelf  weight  cups     rating
0                           100% Bran   N  Cold        70        4    1     130   10.0    5.0       6     280        25      3     1.0  0.33  68.402973
2                            All-Bran   K  Cold        70        4    1     260    9.0    7.0       5     320        25      3     1.0  0.33  59.425505
3           All-Bran with Extra Fiber   K  Cold        50        4    0     140   14.0    8.0       0     330        25      3     1.0  0.50  93.704912
11                           Cheerios   G  Cold       110        6    2     290    2.0   17.0       1     105        25      1     1.0  1.25  50.764999
41                               Life   Q  Cold       100        4    2     150    2.0   12.0       6      95        25      2     1.0  0.67  45.328074
43                              Maypo   A   Hot       100        4    1       0    0.0   16.0       3      95        25      2     1.0  1.00  54.850917
44   Muesli Raisins; Dates; & Almonds   R  Cold       150        4    3      95    3.0   16.0      11     170        25      3     1.0  1.00  37.136863
45  Muesli Raisins; Peaches; & Pecans   R  Cold       150        4    3     150    3.0   16.0      11     170        25      3     1.0  1.00  34.139765
56                 Quaker Oat Squares   Q  Cold       100        4    1     135    2.0   14.0       6     110        25      3     1.0  0.50  49.511874
57                     Quaker Oatmeal   Q   Hot       100        5    2       0    2.7    1.0       1     110         0      1     1.0  0.67  50.828392
67                          Special K   K  Cold       110        6    0     230    1.0   16.0       3      55        25      1     1.0  1.00  53.131324
```

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

And the cereals that meet the condition of protein content below or
equal to 5 grams are the following:

``` python
df[df['protein'] <= 5]
```

```out
                         name mfr  type  calories  protein  fat  sodium  fiber  carbo  sugars  potass  vitamins  shelf  weight  cups     rating
0                   100% Bran   N  Cold        70        4    1     130   10.0    5.0       6     280        25      3     1.0  0.33  68.402973
1           100% Natural Bran   Q  Cold       120        3    5      15    2.0    8.0       8     135         0      3     1.0  1.00  33.983679
2                    All-Bran   K  Cold        70        4    1     260    9.0    7.0       5     320        25      3     1.0  0.33  59.425505
3   All-Bran with Extra Fiber   K  Cold        50        4    0     140   14.0    8.0       0     330        25      3     1.0  0.50  93.704912
4              Almond Delight   R  Cold       110        2    2     200    1.0   14.0       8       1        25      3     1.0  0.75  34.384843
..                        ...  ..   ...       ...      ...  ...     ...    ...    ...     ...     ...       ...    ...     ...   ...        ...
72                    Triples   G  Cold       110        2    1     250    0.0   21.0       3      60        25      3     1.0  0.75  39.106174
73                       Trix   G  Cold       110        1    1     140    0.0   13.0      12      25        25      2     1.0  1.00  27.753301
74                 Wheat Chex   R  Cold       100        3    1     230    3.0   17.0       3     115        25      1     1.0  0.67  49.787445
75                   Wheaties   G  Cold       100        3    1     200    3.0   17.0       3     110        25      1     1.0  1.00  51.592193
76        Wheaties Honey Gold   G  Cold       110        2    1     200    1.0   16.0       8      60        25      1     1.0  0.75  36.187559

[75 rows x 16 columns]
```

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

We add the 2 conditions together in code that looks like this:

``` python
df[(df['protein'] >= 4) & (df['protein'] <= 5)]
```

```out
                                 name mfr  type  calories  protein  fat  sodium  fiber  carbo  sugars  potass  vitamins  shelf  weight  cups     rating
0                           100% Bran   N  Cold        70        4    1     130   10.0    5.0       6     280        25      3     1.0  0.33  68.402973
2                            All-Bran   K  Cold        70        4    1     260    9.0    7.0       5     320        25      3     1.0  0.33  59.425505
3           All-Bran with Extra Fiber   K  Cold        50        4    0     140   14.0    8.0       0     330        25      3     1.0  0.50  93.704912
41                               Life   Q  Cold       100        4    2     150    2.0   12.0       6      95        25      2     1.0  0.67  45.328074
43                              Maypo   A   Hot       100        4    1       0    0.0   16.0       3      95        25      2     1.0  1.00  54.850917
44   Muesli Raisins; Dates; & Almonds   R  Cold       150        4    3      95    3.0   16.0      11     170        25      3     1.0  1.00  37.136863
45  Muesli Raisins; Peaches; & Pecans   R  Cold       150        4    3     150    3.0   16.0      11     170        25      3     1.0  1.00  34.139765
56                 Quaker Oat Squares   Q  Cold       100        4    1     135    2.0   14.0       6     110        25      3     1.0  0.50  49.511874
57                     Quaker Oatmeal   Q   Hot       100        5    2       0    2.7    1.0       1     110         0      1     1.0  0.67  50.828392
```

Code Explained:  
We need to use the special symbol `&` indicating “and”. This means that
both conditions must hold to be returned in the new dataframe. Each
condition is wrapped with parentheses to distinguish the conditions from
one another.

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

That means that only rows present in **both** dataframes will be
selected.

<img src='/module2/condition_and.png'  alt="404 image" />

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

Next, we will look at a case where we filter on 2 different columns.
Let’s say we only want cereals from the Quaker manufacturer, with a
protein content greater than 4.

``` python
df[(df['mfr'] == 'Q') & (df['protein'] > 4)]
```

```out
              name mfr type  calories  protein  fat  sodium  fiber  carbo  sugars  potass  vitamins  shelf  weight  cups     rating
57  Quaker Oatmeal   Q  Hot       100        5    2       0    2.7    1.0       1     110         0      1     1.0  0.67  50.828392
```

The same coding syntax can be applied to two different column
conditions.

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

## Multiple Condition Filtering - “or”

Suppose that we are interested in cereals that either are made from the
Quaker manufacturer **OR** a protein content above 4.  
We only need one of these conditions to hold to return a row.

``` python
df[(df['mfr'] == 'Q') | (df['protein'] > 4)]
```

```out
                  name mfr  type  calories  protein  fat  sodium  fiber  carbo  sugars  potass  vitamins  shelf  weight  cups     rating
1    100% Natural Bran   Q  Cold       120        3    5      15    2.0    8.0       8     135         0      3     1.0  1.00  33.983679
10        Cap'n'Crunch   Q  Cold       120        1    2     220    0.0   12.0      12      35        25      2     1.0  0.75  18.042851
11            Cheerios   G  Cold       110        6    2     290    2.0   17.0       1     105        25      1     1.0  1.25  50.764999
35    Honey Graham Ohs   Q  Cold       120        1    2     220    1.0   12.0      11      45        25      2     1.0  1.00  21.871292
41                Life   Q  Cold       100        4    2     150    2.0   12.0       6      95        25      2     1.0  0.67  45.328074
54         Puffed Rice   Q  Cold        50        1    0       0    0.0   13.0       0      15         0      3     0.5  1.00  60.756112
55        Puffed Wheat   Q  Cold        50        2    0       0    1.0   10.0       0      50         0      3     0.5  1.00  63.005645
56  Quaker Oat Squares   Q  Cold       100        4    1     135    2.0   14.0       6     110        25      3     1.0  0.50  49.511874
57      Quaker Oatmeal   Q   Hot       100        5    2       0    2.7    1.0       1     110         0      1     1.0  0.67  50.828392
67           Special K   K  Cold       110        6    0     230    1.0   16.0       3      55        25      1     1.0  1.00  53.131324
```

Instead of using the `&` symbol, we use `|` which is called the “pipe
operator”. This means “or” in the Python programming language.

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

This time, filtering using “or” resulted in 10 cereals that met either
of the conditions. When we filtered using “and”, only 1 cereal met both
conditions.

<img src='/module2/condition_or.png'  alt="404 image" />

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

## Tilde

We saw that all our filtering are expressed with an underlying column
with `True` or `False` values indicating if the rows meet the
conditions:

``` python
df['protein'] > 4
```

```out
0     False
1     False
2     False
3     False
4     False
      ...  
72    False
73    False
74    False
75    False
76    False
Name: protein, Length: 77, dtype: bool
```

But what if I wanted the rows that were the complement of this?

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

Of course we could do `df['protein'] <= 4` in this situation, but
sometimes the inverse equation is not so straightforward. This is where
*Tilde* (`~`) can be helpful.

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

*Tilde* (`~`) gives us the ability to return the complement of the code
following it.

``` python
(df['protein'] > 4).head()
```

```out
0    False
1    False
2    False
3    False
4    False
Name: protein, dtype: bool
```

Tilda converts all the `True` values to `False` and all the `False`
values, to `True.`

``` python
(~(df['protein'] > 4)).head()
```

```out
0    True
1    True
2    True
3    True
4    True
Name: protein, dtype: bool
```

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

We can obtain the complete dataframe by putting the entire condition
within our square brackets like we did before:

``` python
df[~(df['protein'] > 4)]
```

```out
                         name mfr  type  calories  protein  fat  sodium  fiber  carbo  sugars  potass  vitamins  shelf  weight  cups     rating
0                   100% Bran   N  Cold        70        4    1     130   10.0    5.0       6     280        25      3     1.0  0.33  68.402973
1           100% Natural Bran   Q  Cold       120        3    5      15    2.0    8.0       8     135         0      3     1.0  1.00  33.983679
2                    All-Bran   K  Cold        70        4    1     260    9.0    7.0       5     320        25      3     1.0  0.33  59.425505
3   All-Bran with Extra Fiber   K  Cold        50        4    0     140   14.0    8.0       0     330        25      3     1.0  0.50  93.704912
4              Almond Delight   R  Cold       110        2    2     200    1.0   14.0       8       1        25      3     1.0  0.75  34.384843
..                        ...  ..   ...       ...      ...  ...     ...    ...    ...     ...     ...       ...    ...     ...   ...        ...
72                    Triples   G  Cold       110        2    1     250    0.0   21.0       3      60        25      3     1.0  0.75  39.106174
73                       Trix   G  Cold       110        1    1     140    0.0   13.0      12      25        25      2     1.0  1.00  27.753301
74                 Wheat Chex   R  Cold       100        3    1     230    3.0   17.0       3     115        25      1     1.0  0.67  49.787445
75                   Wheaties   G  Cold       100        3    1     200    3.0   17.0       3     110        25      1     1.0  1.00  51.592193
76        Wheaties Honey Gold   G  Cold       110        2    1     200    1.0   16.0       8      60        25      1     1.0  0.75  36.187559

[74 rows x 16 columns]
```

This gives us more versatility when filtering, especially when we want
the inverse of more complicated conditions and verbs (you’ll see this in
Module 3).

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>

---

# Let’s apply what we learned\!

Notes: Script here

<html>

<audio controls >

<source src="/placeholder_audio.mp3" />

</audio>

</html>
