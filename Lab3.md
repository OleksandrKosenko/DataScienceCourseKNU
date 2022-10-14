<!DOCTYPE html>

<html>

<head>

<meta charset="utf-8" />
<meta name="generator" content="pandoc" />
<meta http-equiv="X-UA-Compatible" content="IE=EDGE" />


<meta name="author" content="Kosenko Oleksandr" />

<meta name="date" content="2022-10-14" />


<!-- code folding -->


</head>

<body>


<div class="container-fluid main-container">




<div id="header">



<h1 class="title toc-ignore">Lab3</h1>
<h4 class="author">Kosenko Oleksandr</h4>
<h4 class="date">2022-10-14</h4>

</div>


<ol style="list-style-type: decimal">
<li>Функція add2(x, y), яка повертає суму двох чисел.</li>
</ol>
<pre class="r"><code>add &lt;-  function(x, y) {
  x + y
}
add(2, 2)</code></pre>
<pre><code>## [1] 4</code></pre>
<ol start="2" style="list-style-type: decimal">
<li>Функція above(x, n), яка приймає вектор та число n, та повертає всі
елементі вектору, які більше n. По замовчуванню n = 10.</li>
</ol>
<pre class="r"><code>above &lt;-  function(x, n) {
  x[x&gt;n]
}
vector &lt;- c(9,10,12,13,14,15,16,17,18,19,20)
above(vector, 4)</code></pre>
<pre><code>##  [1]  9 10 12 13 14 15 16 17 18 19 20</code></pre>
<ol start="3" style="list-style-type: decimal">
<li>Функція my_ifelse(x, exp, n), яка приймає вектор x, порівнює всі
його елементи за допомогою exp з n, та повертає елементи вектору, які
відповідають умові expression. Наприклад, my_ifelse(x, “&gt;”, 0)
повертає всі елементи x, які більші 0. Exp може дорівнювати “&lt;”,
“&gt;”, “&lt;=”, “&gt;=”, “==”. Якщо exp не співпадає ні з одним з цих
виразів, повертається вектор x.</li>
</ol>
<pre class="r"><code>my_ifelse &lt;-  function(x, exp, n) {
  result = switch(  
    exp,  
    &quot;&lt;&quot;= x[x&lt;n],  
    &quot;&gt;&quot;= x[x&gt;n],  
    &quot;&lt;=&quot;= x[x&lt;=n],  
    &quot;&gt;=&quot;= x[x&gt;=n],
    &quot;==&quot;= x[x==n],
    x
  )
}
print(my_ifelse(vector, &quot;&gt;&quot;, 10))</code></pre>
<pre><code>## [1] 12 13 14 15 16 17 18 19 20</code></pre>
<pre class="r"><code>print(my_ifelse(vector, &quot;random_string&quot;, 10))</code></pre>
<pre><code>##  [1]  9 10 12 13 14 15 16 17 18 19 20</code></pre>
<ol start="4" style="list-style-type: decimal">
<li>Функція columnmean(x, removeNA), яка розраховує середнє значення
(mean) по кожному стовпцю матриці, або data frame. Логічний параметр
removeNA вказує, чи видаляти NA значення. По замовчуванню він дорівнює
TRUE.</li>
</ol>
<pre class="r"><code>columnmean_v1 &lt;- function(x,removeNA = TRUE){
  for(i in seq_len(ncol(x))){
    print(mean(x[,i],trim=0,na.rm=removeNA))
  }
}

columnmean_v2 &lt;- function(x,removeNA = TRUE){
  apply(x, 2, mean, na.rm = removeNA)
}

dataframe_of_students &lt;- data.frame (
  Numeric_value = c(12, NA, NA),
  Age = c(22, 22, 23),
  HasCar = c(FALSE, TRUE, FALSE)
)

vector_for_matrix &lt;- list(0.5, 1.3, 3.5, 3.9, 131, 2.8, 0, 2.2, 4.6, 2, 7, 5.1)
new_matrix &lt;- matrix(c(0.5, 1.3, 3.5, 3.9, 131, 2.8, 0, 2.2, 4.6, 2, 7, 5.1))

columnmean_v1(dataframe_of_students)</code></pre>
<pre><code>## [1] 12
## [1] 22.33333
## [1] 0.3333333</code></pre>
<pre class="r"><code>columnmean_v1(new_matrix)</code></pre>
<pre><code>## [1] 13.65833</code></pre>
<pre class="r"><code>columnmean_v2(dataframe_of_students)</code></pre>
<pre><code>## Numeric_value           Age        HasCar 
##    12.0000000    22.3333333     0.3333333</code></pre>
<pre class="r"><code>columnmean_v2(new_matrix)</code></pre>
<pre><code>## [1] 13.65833</code></pre>




</div>

</body>
</html>
