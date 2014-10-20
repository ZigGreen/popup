popup
=====
Всплывающие окно. Способы реализации.
-----
Задача реализации сводится к поиску решания, позволяющего центрировать блок по видимой области экрана.

##Чистый CSS

Есть некоторое количество возможностей позиционировать блок, предустановив размеры контейнера; 
а в случае отсутствия информации или недопустимости жёсткого задания размеров задача усложняется.

В первом случае: 
1. **Отрицательные отступы**:  
   позиционируем абсолютно, задаём отступы слева и сверху, равные половине ширины и высоты блока соответственно;   
   *Почему плохо?* Фиксированные размеры, необходимость предка спозиционированного абсолютно к левому верхнему углу.  
   [Demo](http://jsfiddle.net/ZigGreen/nyzrhkwr/2/)
   
2. **Автоотступы**  
   Задаём `left`, `right`, `top`, `bottom` на 0 и выставляем ``margin: auto``  
   *Почему плохо?* Фиксированные размеры.  
   [Demo](http://jsfiddle.net/ZigGreen/nyzrhkwr/4/)
   
Во втором случае:

1. **Эмуляция таблицы**  
   Нужен: 
    - предка спозиционированный абсолютно к левому верхнему углу
    - в нём элеменнт с `display: table`
    - в нём элеменнт `display: table-cell`, эмулирующий ячейку, к которому пременяется 
    ```
    text-align: center;
    vertical-align: middle;
    ```
    - И уже только потом наш блок, обязательно с `display: inline-block`
    
   *Почему плохо?* Целая канонада вспомогательных элементов, несемантичность.  
   [Demo](http://jsfiddle.net/ZigGreen/nyzrhkwr/5/)
   
2. **Псевдоэлемент**  
   Предку *контейнеру* спозиционированному абсолютно к левому верхнему
   углу задаём псевдоэлемент *before* c 100% высотой.  ...  
   *Почему плохо?* Лучший вариант, на мой взгляд. Возможны проблемы связанные 
   с плохой реализацией `::before` в устаревших браузерах.  
   [Demo](http://jsfiddle.net/ZigGreen/nyzrhkwr/6/)
   
[Ссылка на источник.](http://habrahabr.ru/post/238449/)


##С помошью JS

###Отрицательные отступы 
http://moikrug.ru

```css
/* генерируются js */
element.style {
   width: 450px;
   height: 254px;
   margin-top: -128px; 
   margin-left: -226px;
}
```
```css
#mk-popup-window {
   background: #FFF;
   height: 150px; /* перекрывается в element.style */
   width: 150px; /* перекрывается в element.style */
   margin: -75px 0 0 -75px; /* перекрывается в element.style */
   z-index: 99;
   position: fixed;
   top: 50%;
   left: 50%;
   border: 1px solid #AAA;
   border-radius: 5px;
   -moz-border-radius: 5px;
   -webkit-border-radius: 5px;
   overflow: hidden;
}
```
![Yandex popup](https://contact-janet.codio.io/img/box.png "")

###Вычисление отступов
https://github.com/

```css
element.style {
   top: 587.1px;
   left: 120px;
}
```
```css
.facebox {
   position: absolute;
   top: 0; /* перекрывается в element.style */
   left: 0; /* перекрывается в element.style */
   z-index: 100;
   padding-bottom: 40px;
}
```
![Yandex popup](https://contact-janet.codio.io/img/box_gh.png "")

##Заглушка
 