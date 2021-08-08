# Шпаргалка по CSS Flexbox

<span style="color:red">   

## 1. display: flex

</span>

<p>Есть страница:</p>
<img src="https://tproger.ru/s3/uploads/2017/02/600x266_flex_1.gif">

На ней размещено 4 `div` разных размеров, которые находятся внутри серого `div`. У каждого `div` есть свойство `display: block`. Поэтому каждый блок занимает всю ширину строки. Чтобы начать работать с CSS Flexbox, нужно сделать контейнер flex-контейнером. Делается это так:

```
#container {
  display: flex;
}
```
<img src="https://tproger.ru/s3/uploads/2017/02/600x258_flex_2.gif">

Так у блоков появилось свойство flex-контекст, которое в дальнейшем позволит ими управлять гораздо проще, чем с использованием стандартного CSS.

<span style="color:red">   

## 2. flex-direction

</span>
<p>У flex-контейнера есть две оси: главная и перпендикулярная ей.</p>

<img src="https://tproger.ru/s3/uploads/2017/02/axes.png">

По умолчанию все предметы располагаются вдоль главной оси — слева направо. Именно поэтому блоки в предыдущем примере выстроились в линию, когда мы применили `display: flex`. А вот `flex-direction` позволяет вращать главную ось.

```
#container {
  display: flex;
  flex-direction: column;
}
```

<img src="https://tproger.ru/s3/uploads/2017/02/600x258_flex_3.gif">

Обратите внимание, что `flex-direction`: column не выравнивает блоки по оси, перпендикулярной главной. Главная ось сама меняет своё расположение, и теперь направлена сверху вниз.

Есть ещё парочка свойств для `flex-direction: row-reverse` и `column-reverse`.

<img src="https://tproger.ru/s3/uploads/2017/02/600x258_flex_4.gif">

<span style="color:red">   

## 3. justify-content

</span>

Отвечает за выравнивание элементов по главной оси:
```
#container {
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
}
```
Justify-content может принимать 5 значений:
```
    flex-start
    flex-end
    center
    space-between
    space-around
```
<img src="https://tproger.ru/s3/uploads/2017/02/600x134_flex_5.gif">

`Space-between` задаёт одинаковое расстояние между блоками, но не между контейнером и блоками. `Space-around` также задаёт одинаковое расстояние между блоками, но теперь расстояние между контейнером и блоками равно половине расстояния между блоками.

<span style="color:red">   

## 4. align-items

</span>

Если `justify-content` работает с главной осью, то `align-items` работает с осью, перпендикулярной главной оси. Вернёмся к `flex-direction: row` и пройдёмся по командам `align-items`:
```
    flex-start
    flex-end
    center
    stretch
    baseline
```
<img src="https://tproger.ru/s3/uploads/2017/02/600x210_flex_6.gif">

Стоит заметить, что для `align-items: stretch` высота блоков должна быть равна auto. Для `align-items: baseline` теги параграфа убирать не нужно, иначе получится так:

<img src="https://tproger.ru/s3/uploads/2017/02/flex_7.png">

Чтобы получше разобраться в том, как работают оси, объединим `justify-content` с `align-items` и посмотрим, как работает выравнивание по центру для двух свойств `flex-direction`:

<img src="https://tproger.ru/s3/uploads/2017/02/600x313_flex_8.gif">

<span style="color:red">  

## 5. align-self

</span>

Позволяет выравнивать элементы по отдельности:
```
#container {
  align-items: flex-start;
}
.square#one {
  align-self: center;
}
// Only this square will be centered.
```
Для двух блоков применим `align-self`, а для остальных — `align-items: center` и `flex-direction: row`.

<img src="https://tproger.ru/s3/uploads/2017/02/600x188_flex_9.gif">

<span style="color:red">  

## 6. flex-basis

</span>

Отвечает за изначальный размер элементов до того, как они будут изменены другими свойствами CSS Flexbox:

<img src="https://tproger.ru/s3/uploads/2017/02/flex_10.gif">

`flex-basis` влияет на размер элементов вдоль главной оси. Давайте посмотрим, что случится, если мы изменим направление главной оси:

<img src="https://tproger.ru/s3/uploads/2017/02/770x284_flex-11.gif">

Заметьте, что нам пришлось изменить и высоту элементов: `flex-basis` может определять как высоту элементов, так и их ширину в зависимости от направления оси.

<span style="color:red">  

## 7. flex-grow

</span>

Это свойство немного сложнее. Для начала зададим блокам одинаковую ширину в 120px:

<img src="https://tproger.ru/s3/uploads/2017/02/flex_pic_1.png">

По умолчанию значение `flex-grow` равно 0. Это значит, что блокам запрещено увеличиваться в размерах. Зададим `flex-grow` равным 1 для каждого блока:

<img src="https://tproger.ru/s3/uploads/2017/02/flex_pic_2.png">

Теперь блоки заняли оставшееся место в контейнере. Но что значит `flex-grow: 1`? Попробуем сделать `flex-grow` равным 999:

<img src="https://tproger.ru/s3/uploads/2017/02/flex_pic_3.png">

И… ничего не произошло. Так получилось из-за того, что `flex-grow` принимает не абсолютные значения, а относительные. Это значит, что не важно, какое значение у `flex-grow`, важно, какое оно по отношению к другим блокам:

<img src="https://tproger.ru/s3/uploads/2017/02/770x179_flex_12.gif">

Вначале `flex-grow` каждого блока равен 1, в сумме получится 6. Значит, наш контейнер разделён на 6 частей. Каждый блок будет занимать 1/6 часть доступного пространства в контейнере. Когда `flex-grow` третьего блока становится равным 2, контейнер делится на 7 частей: 1 + 1 + 2 + 1 + 1 + 1. Теперь третий блок занимает 2/7 пространства, остальные — по 1/7. И так далее.

`flex-grow` работает только для главной оси, пока мы не изменим её направление.

<span style="color:red">  

## 8. flex-shrink

</span>

Прямая противоположность `flex-grow`. Определяет, насколько блоку можно уменьшиться в размере. `flex-shrink` используется, когда элементы не вмещаются в контейнер. Вы определяете, какие элементы должны уменьшиться в размерах, а какие — нет. По умолчанию значение `flex-shrink` для каждого блока равно 1. Это значит, что блоки будут сжиматься, когда контейнер будет уменьшаться.

Зададим `flex-grow` и `flex-shrink` равными 1:

<img src="https://tproger.ru/s3/uploads/2017/02/600x134_flex_13.gif">

Теперь поменяем значение `flex-shrink` для третьего блока на 0. Ему запретили сжиматься, поэтому его ширина останется равной 120px:

<img src="https://tproger.ru/s3/uploads/2017/02/600x134_flex_14.gif">

`flex-shrink` основывается на пропорциях. То есть, если у первого блока `flex-shrink` равен 6, а у остальных он равен 2, то, это значит, что первый блок будет сжиматься в три раза быстрее, чем остальные.

<span style="color:red">  

## 9. flex

</span>

Заменяет `flex-grow`, `flex-shrink` и `flex-basis`. Значения по умолчанию: `0 (grow) 1 (shrink) auto (basis)`.

Создадим два блока:
```
.square#one {
  flex: 2 1 300px;
}
.square#two {
  flex: 1 2 300px;
}
```

У обоих одинаковый `flex-basis`. Это значит, что оба будут шириной в 300px (ширина контейнера: 600px плюс `margin` и `padding`). Но когда контейнер начнет увеличиваться в размерах, первый блок (с большим `flex-grow`) будет увеличиваться в два раза быстрее, а второй блок (с наибольшим `flex-shrink`) будет сжиматься в два раза быстрее:

<img src="https://tproger.ru/s3/uploads/2017/02/flex_15.gif">

[На главную](../mainPage.md)