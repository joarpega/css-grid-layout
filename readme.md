# css-grid-layout
## Ejemplos para usar CSS Grid Layout

~~~
<div class="container">
	<div class="item"></div>
	<div class="item">
		<p class="sub-item"> </p>  /*Este no es un grid item */
	</div>
	<div class="item"></div>
</div>
~~~

Grid Container: Va a ser nuestro elemento padre el cual va a llevar nuestro nuevo display llamado grid.


Grid Item: Los grid item son los hijos directos de un grid container.


Grid Line: Lineas divisorias horizontales, verticales y el contorno del grid.
![Grid track](/img-doc/1_diagram_numbered_grid_lines.png)


Grid Track: Espacio entre dos lineas adyacentes, filas y columnas.
![Grid track](/img-doc/1_Grid_Track.png)


Grid Cell: Espacio en dos filas adyacentes y dos columnas adyacentes.
![Grid track](/img-doc/1_Grid_Cell.png)


Grid Area: Espacio rodeado por cuatro grid lines (puede ser mayor tamaño).
![Grid track](/img-doc/1_Grid_Area.png)


Para inicializar un contenedor con grid debemos colocar  [ display: grid; ], con grid-template-columns se especifica el tamaño de las columnas y la cantidad de columnas.
~~~
.container {
    display: grid;
    grid-template-columns: 25% 50% 25%;
}
~~~

Con [ grid-template-rows ] se especifica el tamaño de las filas y la cantidad de filas.
~~~
.container {
    display: grid;
    grid-template-rows: 25% 50% 25%;
}
~~~
Con [ grid-template: filas / columnas; ] podemos configurar las dos anterionres
~~~
.container {
    display: grid;
    grid-template: 300px 100px 100px / 50% 200px 400px; 
}
~~~
Al colocar el [ display: grid ] y [ grid-template: filas / columnas; ] en el hijo 
directo creamos un "Subgrid"

Nota: nth-of-type(4) nos permite seleccionar el 4to hijo que tenga la clase 
especificada
~~~
.container {
    display: grid;
    grid-template: 300px 100px 100px / 50% 200px 400px; 
}
.item {
    background: rgb(174, 221, 236);
    padding: 10px;
    border: solid 2px red;
}

.item:nth-of-type(4) {
    background: blue;
    overflow: auto;
    display: grid;
    grid-template: 50px 50px 50px / 100px 100px 100px;
}

.item .item {
    background: yellow;
}
~~~
         
Al usar [ grid-column-gap: 30px; ] nos permite colocar un margen a las columnas.

Al usar [ grid-row-gap: 30px; ] nos permite colocar un margen a las filas.

Al usar [ grid-gap: filas columnas; ] nos permite colocar un margen a las filas y columnas
~~~
.container {
    display: grid;
    grid-template: 300px 100px 100px / 50% 200px 25%;
    grid-gap: 10px 100px;
}
~~~

Nueva unidad de medida para los grids [ fr = fracciones ], distribuye el espacio entre columnas de una manera homogenea

Funcion: [ repeat(cantidad, tamaño) ] nos permite repetir la cantidad de columnas o filas  especificada.
Funcion: [ minmax(tam-minimo, tam maximo) ] permite especificar el tamaño minimo y maximo de una columna.
~~~
.container {
    display: grid;
    grid-template: 300px 100px 100px / repeat(4, minmax(200px, 1fr));
    grid-gap: 10px;
}
~~~

Al usar [ grid-template-areas ] se debe especificar en el contenedor padre, lo cual nos permitira indicar cuantas areas contendra una fila.
[ grid-area ] Propiedad aplicada a los hijos de un Grid-Container, nos permite especificar el area que ocupara una celda, esta clase se debe colocar en el item hijo. 
~~~
<section class="container">
    <div class="item header">contenido #1</div>
    <div class="item left">contenido #2</div>
    <div class="item contenido">contenido #3</div>
    <div class="item footer">contenido #5</div>
</section>

.container {
    display: grid;
    grid-template: 100px 1fr 130px / 300px 1fr;
    grid-gap: 10px;
    height: 100vh;
    grid-template-areas:    "header header"
                            "left contenido"
                            "footer footer";
}

.header {
    grid-area: header;
}

.left {
    grid-area: left;
}

.contenido {
    grid-area: contenido;
}

.footer {
    grid-area: footer;
}

.item {
    background: rgb(174, 221, 236);
    padding: 10px;
    border: solid 2px red;
}
~~~

[ grid-column-start: inicio ] El inicio esta definido por la linea donde debe empezar.

[ grid-column-end: fin ] El fin esta definido por la linea donde debe terminar.

[ grid-column: inicio / areas_abarca ] Con esta instruccion podemos indicar en que columna inicia y en cual termina, tambien soporta span y valores negativos. 
~~~
.container {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: repeat(4, 1fr);
    grid-gap: 10px;
    height: 100vh;
}

.item {
    background: rgb(174, 221, 236);
    padding: 10px;
    border: solid 2px red;
}

.item:nth-of-type(1) {
    background: blue;
    grid-column-start: 1;
    grid-column-end: 3;
}

.item:nth-of-type(8) {
    background: blue;
    /* grid-column: 2 / span 2; */
    grid-column: 1 / -1;
}

.item:nth-of-type(7) {
    background: blue;
    grid-column: 2 / 4;
}
~~~

Ejemplo para nombrar lineas y su uso.
~~~
.container {
    display: grid;
    grid-template-columns:  [inicio] 1fr 
                            [linea2] 1fr 
                            [linea3] 1fr 
                            [destacado-end] 1fr 
                            [linea5] 1fr 
                            [destacado2-end] 1fr 
                            [linea7] 1fr 
                            [Final];
    grid-template-rows: [inicio] 200px 
                        [inicio2] 200px 
                        [final];
    grid-gap: 5px;
}

.item {
    background: rgb(174, 221, 236);
    padding: 10px;
    border: solid 2px black;
}

.item:nth-of-type(1) {
    grid-column: inicio / destacado-end;
    grid-row: inicio / final;
}
~~~

[ grid-auto-flow: row; ] Especifica el flujo que debe seguir el grid implicito, puede ser en colunas o en filas. El valor por defecto es en filas "row".

~~~

.container {
    display: grid;
    grid-template-columns:  [inicio] 1fr 
                            [linea2] 1fr 
                            [linea3] 1fr 
                            [destacado-end] 1fr 
                            [linea5] 1fr 
                            [destacado2-end] 1fr 
                            [linea7] 1fr 
                            [Final];
    grid-template-rows: [inicio] 200px 
                        [inicio2] 200px 
                        [final];
    grid-gap: 5px;
    /* grid-auto-flow: column; */
    /* grid-auto-columns: 50px 100px; */
    grid-auto-rows: 50px 100px;
}
~~~


### Alineando items

[ justify-items ] Valores posibles: start end center stretch;

[ align-items ] Valores posibles: start end center stretch;
~~~
.container {
    display: grid;
    grid-gap: 5px;
    height: 100vh;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(4, 1fr);
    justify-items: center;
    align-items: center;
}

.item {
    background: rgb(174, 221, 236);
    padding: 10px;
    border: solid 2px black;
}

.item:nth-of-type(5) {
    align-self: start;
    justify-self: start;
}
~~~

### Alineando contenido

[ justify-content ] Valores posibles: start end center stretch space-around space-between space-evenly

[ align-content ] Valores posibles: start end center stretch space-around space-between space-evenly
~~~
.container {
    display: grid;
    grid-gap: 5px;
    height: 100vh;
    grid-template-columns: repeat(3, 200px);
    grid-template-rows: repeat(4, 100px);
    justify-content: center;
    align-content: center;
}

.item {
    background: rgb(174, 221, 236);
    padding: 10px;
    border: solid 2px black;
}
~~~