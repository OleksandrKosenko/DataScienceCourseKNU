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



<h1 class="title toc-ignore">Lab5</h1>
<h4 class="author">Kosenko Oleksandr</h4>
<h4 class="date">2022-10-14</h4>

</div>


<ol style="list-style-type: decimal">
<li><p>Написати функцію pmean, яка обчислює середнє значення (mean)
забруднення сульфатами або нітратами серед заданого переліка моніторів.
Ця функція приймає три аргументи: «directory», «pollutant», «id».
Directory – папка, в якій розміщені дані, pollutant – вид забруднення,
id – перелік моніторів. Аргумент id має значення за замовчуванням 1:332.
Функція повинна ігнорувати NA значення. Приклад роботи функції:</p>
<p>pmean(“specdata”, “sulfate”, 1:10)</p>
<p>## [1] 4.064128</p>
<p>pmean(“specdata”, “sulfate”, 55)</p>
<p>## [1] 3.587319</p>
<p>pmean(“specdata”, “nitrate”)</p>
<p>## [1] 1.702932</p></li>
</ol>
<pre class="r"><code>library(&quot;data.table&quot;)

my_directory &lt;- file.path(&quot;C:&quot;, &quot;Users&quot;, &quot;Alex&quot;, &quot;Desktop&quot;, &quot;specdata&quot;)

pmean_v1 &lt;- function(directory, pollutant, id = 1:332) {
  
  pollutants = c()

  filenames = list.files(directory)
  
  for(i in id) {
    
    filepath = paste(directory,&quot;/&quot; ,filenames[i], sep = &quot;&quot;)
    
    specdata = read.csv(filepath, header = TRUE)
    
    pollutants = c(pollutants, specdata[,pollutant])
    
  }
  
  pollutants_mean = mean(pollutants, na.rm = TRUE)
  pollutants_mean
  
}



pmean_v2 &lt;- function(directory, pollutant, id = 1:332) {
  
  fileNames &lt;- paste0(directory, &#39;/&#39;, formatC(id, width=3, flag=&quot;0&quot;), &quot;.csv&quot; )
  
  list &lt;- lapply(fileNames, data.table::fread)
  specdata &lt;- rbindlist(list)
  
  if (c(pollutant) %in% names(specdata)){
    return(specdata[, lapply(.SD, mean, na.rm = TRUE), .SDcols = pollutant][[1]])
    
  } 
  
}



pmean_v1(my_directory, &quot;sulfate&quot;, 1:10)</code></pre>
<pre><code>## [1] 4.064128</code></pre>
<pre class="r"><code>pmean_v1(my_directory, &quot;sulfate&quot;, 55)</code></pre>
<pre><code>## [1] 3.587319</code></pre>
<pre class="r"><code>pmean_v1(my_directory, &quot;nitrate&quot;)</code></pre>
<pre><code>## [1] 1.702932</code></pre>
<pre class="r"><code>pmean_v2(my_directory, &quot;sulfate&quot;, 1:10)</code></pre>
<pre><code>## [1] 4.064128</code></pre>
<pre class="r"><code>pmean_v2(my_directory, &quot;sulfate&quot;, 55)</code></pre>
<pre><code>## [1] 3.587319</code></pre>
<pre class="r"><code>pmean_v2(my_directory, &quot;nitrate&quot;)</code></pre>
<pre><code>## [1] 1.702932</code></pre>
<ol start="2" style="list-style-type: decimal">
<li>Написати функцію complete, яка виводить кількість повних
спостережень (the number of completely observed cases) для кожного
файлу. Функціяприймає два аргументи: «Directory» та «id» та повертає
data frame, в якому перший стовпчик – ім&#39;я файлу, а другий – кількість
повних спостережень. Приклад роботи функції: complete(“specdata”, 1) ##
id nobs ## 1 1 117 complete(“specdata”, c(2, 4, 8, 10, 12)) ## id nobs
## 1 2 1041 ## 2 4 474 ## 3 8 192 ## 4 10 148 ## 5 12 96
complete(“specdata”, 50:60) ## id nobs ## 1 50 459 ## 2 51 193 ## 3 52
812 ## 4 53 342 ## 5 54 219 ## 6 55 372 ## 7 56 642 ## 8 57 452 ## 9 58
391 ## 10 59 445 ## 11 60 448</li>
</ol>
<pre class="r"><code>complete &lt;- function(directory, id= 1:332){
  
  ids = c()
  
  nobss = c()
  
  filenames = list.files(directory)
  
  for(i in id) {
    
    filepath = paste(directory,&quot;/&quot; ,filenames[i], sep = &quot;&quot;)
    
    data = read.csv(filepath, header = TRUE)
    
    completeCases = data[complete.cases(data), ]
    
    ids =  c(ids, i)
    nobss = c(nobss, nrow(completeCases))
   
  }
  
  data.frame(id=ids, nobs=nobss)
  
}



complete(my_directory, 1)</code></pre>
<pre><code>##   id nobs
## 1  1  117</code></pre>
<pre class="r"><code>complete(my_directory, c(2, 4, 8, 10, 12))</code></pre>
<pre><code>##   id nobs
## 1  2 1041
## 2  4  474
## 3  8  192
## 4 10  148
## 5 12   96</code></pre>
<pre class="r"><code>complete(my_directory, 50:60)</code></pre>
<pre><code>##    id nobs
## 1  50  459
## 2  51  193
## 3  52  812
## 4  53  342
## 5  54  219
## 6  55  372
## 7  56  642
## 8  57  452
## 9  58  391
## 10 59  445
## 11 60  448</code></pre>
<ol start="3" style="list-style-type: decimal">
<li>Написати функцію corr, яка приймає два аргументи: directory (папка,
де знаходяться файли спостережень) та threshold (порогове значення, за
замовчуванням дорівнює 0) та обчислює кореляцію між сульфатами та
нітратами для моніторів, кількість повних спостережень для яких більше
порогового значення. Функція повинна повернути вектор значень кореляцій.
Якщо ні один монітор не перевищує порогового значення, функція повинна
повернути numeric вектор довжиною 0. Для обчислення кореляції між
сульфатами та нітратами використовуйте вбудовану функцію «cor» з
параметрами за замовчуванням. Приклад роботи функції: cr &lt;-
corr(“specdata”, 150) head(cr); summary(cr) ## [1] -0.01895754
-0.14051254 -0.04389737 -0.06815956 -0.12350667 - 0.07588814 ## Min. 1st
Qu. Median Mean 3rd Qu. Max. ## -0.21060 -0.04999 0.09463 0.12530
0.26840 0.76310 cr &lt;- corr(“specdata”, 400) head(cr); summary(cr) ##
[1] -0.01895754 -0.04389737 -0.06815956 -0.07588814 0.76312884 -
0.15782860 ## Min. 1st Qu. Median Mean 3rd Qu. Max. ## -0.17620 -0.03109
0.10020 0.13970 0.26850 0.76310 cr &lt;- corr(“specdata”, 5000)
head(cr); summary(cr) ; length(cr) ## numeric(0) ## Min. 1st Qu. Median
Mean 3rd Qu. Max. ## [1] 0</li>
</ol>
<pre class="r"><code>corr &lt;- function(directory, threshold = 0) {

  list &lt;- lapply(file.path(directory, list.files(path = directory, pattern=&quot;*.csv&quot;)), data.table::fread)
  
  specdata &lt;- rbindlist(list)
  
  specdata &lt;- specdata[complete.cases(specdata),]
  
  specdata &lt;- specdata[, .(nobs = .N, corr = cor(x = sulfate, y = nitrate)), by = ID][nobs &gt; threshold]
  
  specdata[, corr]
  
}

cr &lt;- corr(my_directory, 150)
head(cr); summary(cr)</code></pre>
<pre><code>## [1] -0.01895754 -0.14051254 -0.04389737 -0.06815956 -0.12350667 -0.07588814</code></pre>
<pre><code>##     Min.  1st Qu.   Median     Mean  3rd Qu.     Max. 
## -0.21057 -0.04999  0.09463  0.12525  0.26844  0.76313</code></pre>
<pre class="r"><code>cr &lt;- corr(my_directory, 400)
head(cr); summary(cr)</code></pre>
<pre><code>## [1] -0.01895754 -0.04389737 -0.06815956 -0.07588814  0.76312884 -0.15782860</code></pre>
<pre><code>##     Min.  1st Qu.   Median     Mean  3rd Qu.     Max. 
## -0.17623 -0.03109  0.10021  0.13969  0.26849  0.76313</code></pre>
<pre class="r"><code>cr &lt;- corr(my_directory, 5000)
head(cr); summary(cr); length(cr)</code></pre>
<pre><code>## numeric(0)</code></pre>
<pre><code>##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
## </code></pre>
<pre><code>## [1] 0</code></pre>




</div>


</body>
</html>
