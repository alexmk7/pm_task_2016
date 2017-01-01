# Общие условия

Чтобы получить пароль к тестовому серверу, нужно пройти по [ссылке](http://52.200.49.43/2016it/register) и вбить туда свою фамилию, имя и отчество (если было указано в списке группы) + номер группы. Запросить пароль на своё имя можно один раз (так что лучше его записать), если кто-то успел это сделать до вас, то претензии принимаются до 20/12/2016 .

Задачи проверяются автоматически, для этого нужно зайти на соответствующий тестовый сервер, ввести пароль, комментарий и загрузить файл. На каждое задание дается 10 попыток.

В комментарий нужно ввести краткое описание своего алгоритма, если описание слишком большое, то можно оставить ссылку на сервис вроде http://pastebin.com .

Кроме того, во избежание спорных моментов на экзамене, настоятельно рекомендуется зарегистрироваться на [GitHub](http://github.com) или [BitBucket](http://bitbucket.org), и оставить в комментарии ссылку на код (ревизию), который воспроизводит решение. 


# Задание 1

Задача: с некоторых новостных сайтов были загружены тексты новостей за период  несколько лет, причем каждая новость принаделжит к какой-то рубрике (*science*, *style*, *culture*, *life*, *economics*, *business*, *travel*, *forces*, *media*, *sport*). Нужно написать программу, которая автоматически определяет к какой рубрике можно отнести новость. Данные расположены в архиве, который можно загрузить  [здесь](https://raw.githubusercontent.com/alexmk7/pm_task_2016/master/news_data.zip), тестовый сервер здесь: http://52.200.49.43/2016it/news . В файле **news_train.txt** 60,000 строк, в каждой строке содержится метка рубрики, заголовок новостной статьи и сам текст статьи, например:

>    **sport**&nbsp;&lt;tab&gt;&nbsp;**Сборная Канады по хоккею разгромила чехов**&nbsp;&lt;tab&gt;&nbsp;**Сборная Канады по хоккею крупно об...**

где &lt;tab&gt; символ табуляции. В файле **news_test.txt** 15,000 строк, на каждой строке заголовок и новость без метки. Задача -- предсказать категорию всех новостей из тестового файла. 

В качестве решения принимается файл из 15,000 строк, на каждой строке которого стоит метка, соответствующая одной из 10 категорий, пример такого файла в **news_output_example.txt** . Все файлы имеют кодировку *utf-8*.

####Оценка результатов
Оценивается точность, то есть доля правильно угаданных меток, для зачета необходимо получить результат больше 0.7 .


# Задание 2

Данные для задачи расположены в [архиве](https://raw.githubusercontent.com/alexmk7/pm_task_2016/master/transport_data.zip), тестовый сервер по ссылке http://52.200.49.43/2016it/transport . В некотором *городе N* на каждом автобусе/троллейбусе/трамвае установлены GPS (или даже ГЛОНАСС) трекеры, которые с некоторым промежутком времени передают информацию о своем местоположении на специальный сервер. 

Допустим, что данные для всех транспортных средства одного маршрута непрерывно записывались на протяжении недели, потом GPS координаты (широта и долгота) были спроецированы на плоскость с использованием [проекции Меркатора](https://ru.wikipedia.org/wiki/%D0%9F%D1%80%D0%BE%D0%B5%D0%BA%D1%86%D0%B8%D1%8F_%D0%9C%D0%B5%D1%80%D0%BA%D0%B0%D1%82%D0%BE%D1%80%D0%B0) и некоторого линейного преобразования. Эти данные записаны в файле **train.txt** в виде:
s
>    **1447037729**&nbsp;&nbsp;&lt;tab&gt;&nbsp;&nbsp;**3054.619968**&nbsp;&nbsp;&lt;tab&gt;&nbsp;&nbsp;**2409.828279**&nbsp;&nbsp;&lt;tab&gt;&nbsp;&nbsp;**570d8**

поля разделены табуляцией. Здесь:
- **1447037729** - [UNIX-время](https://ru.wikipedia.org/wiki/UNIX-%D0%B2%D1%80%D0%B5%D0%BC%D1%8F), которое без труда можно преобразовать во что-то разумное с помощью стандартной библиотеки  любимого языка программирования ([Java](https://docs.oracle.com/javase/8/docs/api/java/time/Instant.html#ofEpochSecond-long-), [C#](http://stackoverflow.com/questions/249760/how-to-convert-a-unix-timestamp-to-datetime-and-vice-versa), [Python](https://docs.python.org/2/library/datetime.html#datetime.date.fromtimestamp), [Go](https://golang.org/pkg/time/#Unix)).
- **3054.619968** - координата "x"
- **2409.828279** - координата "y"
- **570d8** - уникальный идентификатор транспортного средства, от которого получен сигнал. 

Задача состоит в определении координат остановок в одном направлении. Известно, что в этом направлении всего 39 остановок, первая имеет координаты:

>   **(11038.08464497, 8253.17542416)**

последняя:

>   **(283.08479678,  163.45489494)**

кроме того известно, что есть остановка с координатами:

>   **(3425.67079005, 3469.94198377)**

В тестовом файле должны быть координаты **37** промежуточных остановок (все, что между первой и последней), остановки должны быть упорядочены. Координаты задаются двумя вещественными числами, соответственно "x" и "y". Числа разделены табуляцией или пробелом, пример тестового файла в **output_example.txt** .

####Оценка результатов

За каждую неправильно определенную остановку засчитывается штраф, потом штрафы усредняется по всем остановкам - это и есть результат . 

Формально, пусть известны точные координаты остановочных павильонов:

![$$S = \{(x_i, y_i)\}_{i=1}^{37}$$](http://www.sciweavers.org/upload/Tex2Img_1482005818/render.png)

пусть предсказаны следующие координаты остановок:

![$$\hat{S} = \{(\hat{x_i}, \hat{y_i}\}_{i=1}^{37}$$](http://www.sciweavers.org/upload/Tex2Img_1482005760/render.png)

тогда штраф считается по формуле:

![$$\frac{1}{37}\sum_{i}^{37}f\big(\sqrt{(x_i - \hat{x_i}))^2 + (y_i - \hat{y_i})^2}\big)$$](http://www.sciweavers.org/upload/Tex2Img_1482005840/render.png)

где

![$$f(x) = \begin{cases} 0 &\mbox{if } x \le 20 \\ (x - 20)^2 & \mbox{if } x \gt 20 \end{cases} $$](http://www.sciweavers.org/upload/Tex2Img_1482005880/render.png)

То есть если оценка попадает в круг радиуса *20* от известных координат, то остановка считается угаданной верно. В противном случае начисляется штраф, равный квадрату расстояния от круга. 