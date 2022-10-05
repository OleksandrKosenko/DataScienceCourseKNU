<!DOCTYPE html>

<html>

<head>

<meta charset="utf-8" />
<meta name="generator" content="pandoc" />
<meta http-equiv="X-UA-Compatible" content="IE=EDGE" />



<meta name="date" content="2022-10-05" />


<!-- code folding -->




</head>

<body>


<div class="container-fluid main-container">




<div id="header">



<h1 class="title toc-ignore">Lab1 - Kosenko Oleksandr UP-11</h1>
<h4 class="date">2022-10-05</h4>

</div>


<div id="лабораторна-робота-1" class="section level1">
<h1>Лабораторна робота №1</h1>
<ol style="list-style-type: decimal">
<li><p>Створити змінні базових (atomic) типів. Базові типи: character,
numeric, integer, complex, logical.</p>
<pre class="r"><code>some_character &lt;- &quot;a&quot;
print(class(some_character))</code></pre>
<pre><code>## [1] &quot;character&quot;</code></pre>
<pre class="r"><code>some_numeric &lt;- 1.0
print(class(some_numeric))</code></pre>
<pre><code>## [1] &quot;numeric&quot;</code></pre>
<pre class="r"><code>some_integer &lt;- 1L
print(class(some_integer))</code></pre>
<pre><code>## [1] &quot;integer&quot;</code></pre>
<pre class="r"><code>some_coplex &lt;- 1 + 2i
print(class(some_coplex))</code></pre>
<pre><code>## [1] &quot;complex&quot;</code></pre>
<pre class="r"><code>some_logical &lt;- TRUE
print(class(some_logical))</code></pre>
<pre><code>## [1] &quot;logical&quot;</code></pre></li>
<li><p>Створити вектори, які: містить послідовність з 5 до 75; містить
числа 3.14, 2.71, 0, 13; 100 значень TRUE.</p>
<pre class="r"><code>first_vector &lt;- c(5:75)
second_vector &lt;- c(3.14,2.72,0,13)
third_vector &lt;- rep(c(TRUE), times = 100)</code></pre></li>
<li><p>Створити наступну матрицю за допомогою <strong>matrix</strong>,
та за допомогою <strong>cbind</strong> або <strong>rbind</strong></p>
<table>
<tbody>
<tr class="odd">
<td align="center">0.5</td>
<td align="center">1.3</td>
<td align="center">3.5</td>
</tr>
<tr class="even">
<td align="center">3.9</td>
<td align="center">131</td>
<td align="center">2.8</td>
</tr>
<tr class="odd">
<td align="center">0</td>
<td align="center">2.2</td>
<td align="center">4.6</td>
</tr>
<tr class="even">
<td align="center">2</td>
<td align="center">7</td>
<td align="center">5.1</td>
</tr>
</tbody>
</table>
<pre class="r"><code>vector_for_matrix &lt;- c(0.5, 1.3, 3.5, 3.9, 131, 2.8, 0, 2.2, 4.6, 2, 7, 5.1)
matrix(vector_for_matrix, nrow = 4, ncol = 3, byrow = TRUE)</code></pre>
<pre><code>##      [,1]  [,2] [,3]
## [1,]  0.5   1.3  3.5
## [2,]  3.9 131.0  2.8
## [3,]  0.0   2.2  4.6
## [4,]  2.0   7.0  5.1</code></pre>
<pre class="r"><code>v_cbind_1 &lt;- c(0.5, 3.9, 0, 2)
v_cbind_2 &lt;- c(1.3, 131, 2.2, 7)
v_cbind_3 &lt;- c(3.5, 2.8, 4.6, 5.1)
cbind(v_cbind_1, v_cbind_2, v_cbind_3)</code></pre>
<pre><code>##      v_cbind_1 v_cbind_2 v_cbind_3
## [1,]       0.5       1.3       3.5
## [2,]       3.9     131.0       2.8
## [3,]       0.0       2.2       4.6
## [4,]       2.0       7.0       5.1</code></pre></li>
<li><p>Створити довільний список (list), в який включити всі базові
типи.</p>
<pre class="r"><code>some_list &lt;- list(some_character, some_coplex, some_integer, some_logical, some_numeric)
for (item in some_list) {
    print(item)
    print(class(item))
}</code></pre>
<pre><code>## [1] &quot;a&quot;
## [1] &quot;character&quot;
## [1] 1+2i
## [1] &quot;complex&quot;
## [1] 1
## [1] &quot;integer&quot;
## [1] TRUE
## [1] &quot;logical&quot;
## [1] 1
## [1] &quot;numeric&quot;</code></pre></li>
<li><p>Створити фактор з трьома рівнями «baby», «child», «adult»</p>
<pre class="r"><code>some_factor &lt;- factor(c(&quot;baby&quot;, &quot;child&quot;, &quot;adult&quot;, &quot;child&quot;, &quot;adult&quot;), levels = c(&quot;baby&quot;, &quot;child&quot;, &quot;adult&quot;))
some_factor</code></pre>
<pre><code>## [1] baby  child adult child adult
## Levels: baby child adult</code></pre></li>
<li><p>Знайти індекс першого значення NA в векторі 1, 2, 3, 4, NA, 6, 7,
NA, 9, NA, 11. Знайти кількість значень NA.</p>
<pre class="r"><code>new_vector &lt;- c(1, 2, 3, 4, NA, 6, 7, NA, 9, NA, 11)
cat(&#39;Index of first &quot;NA&quot; in vector is&#39;,match(NA,new_vector))</code></pre>
<pre><code>## Index of first &quot;NA&quot; in vector is 5</code></pre>
<pre class="r"><code>count &lt;- 0
for (item in new_vector) {
    if(is.na(item)) {
      count &lt;- count + 1
    }
}
cat(&#39;Quantity of NA in vector is&#39;,count)</code></pre>
<pre><code>## Quantity of NA in vector is 3</code></pre></li>
<li><p>Створити довільний data frame та вивести в консоль.</p>
<pre class="r"><code>dataframe_of_students &lt;- data.frame (
  Name = c(&quot;Alex&quot;, &quot;Andriy&quot;, &quot;Olesya&quot;),
  Age = c(22, 22, 23),
  HasCar = c(FALSE, TRUE, FALSE)
)
dataframe_of_students</code></pre>
<pre><code>##     Name Age HasCar
## 1   Alex  22  FALSE
## 2 Andriy  22   TRUE
## 3 Olesya  23  FALSE</code></pre></li>
<li><p>Змінити імена стовпців цього data frame.</p>
<pre class="r"><code>colnames(dataframe_of_students)[3] &lt;- &quot;HasPlaystation&quot;
dataframe_of_students</code></pre>
<pre><code>##     Name Age HasPlaystation
## 1   Alex  22          FALSE
## 2 Andriy  22           TRUE
## 3 Olesya  23          FALSE</code></pre></li>
</ol>
</div>




</div>


<!-- code folding -->


<!-- dynamically load mathjax for compatibility with self-contained -->

</body>
</html>
