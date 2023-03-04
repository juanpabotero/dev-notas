
# CSS

## Propiedades

- Es recomendable hacer un reset de los estilos por defecto, usar:
  ```css
  *, *::before, *::after {
  	box-sizing: border-box;
		font: inherit;
  	margin: 0;
  	padding: 0;
  }
	html, body {
		min-height: 100%;
	}
	img, picture, svg, video {
		display: block;
		max-width: 100%;
	}
  ```

- Es recomendable poner los estilos a traves de clases, donde unas controlen  
  el layout y otras los estilos de los elementos.


- la etiqueta "p" sirve para agregar literalmente un parrafo, si tengo 2
  parrafos seguidos, creo 2 etiquetas "p"


- A los elementos in-line no se les puede aplicar las propiedades de 
  width y height


- `margin-block` y `margin-inline` son logical properties.   
  `margin-block` maneja el top y bottom margin.  
	`margin-inline` maneja left y right margin.


- En vez de poner un `width: 100%` y `max-width: 1280px`, puedo usar  
  `width: min(100%, 1280px)`


- se puede usar los pseudoelementos ::after y ::before para estilar en vez
  crear nuevos elementos HTML.  
  Dentro de los pseudoelementos ::after y ::before, se puede activar el
  atributo attr para cambiar el contenido desde el html, ej:  
	en el html:  
	`<button data-count="8"></button>`  
	en el css:  
	```css
	button::after {
		content: attr(data-count);
	}
	```


- :has() para buscar elementos que contengan un elemento especifico,
	selecciona el elemento padre:  
	```css
	.container:has(.item) {
		background: red;
	}
	```
	selecciona los container que contengan el elemento item


- :is() permite agrupar selectores:  
  en vez de escribir:  
	`header a, header p {}`  
  puedo escribir:  
	`header:is(a, p) {}`  
  otras formas:  
	`header:is(p, .greenButton) {}`  
	`:is(header, footer, section) a:hover {}`  
  hay que tener cuidado usandolo porq la especificidad la da el selector
  mas especifico que esté dentro del parentesis.


- :where() tambien permite agrupar selectores al igual que is() pero
  tiene una especificidad constante


- para redondear los bordes, puedo usar:  
	`border-radius: 100vmax;`


- `transform: scale()` y `outline` no modifican el DOM, solo es estetico 


- las animaciones se deberian hacer con:  
  `transform: translate3d(10px, 10px, 0)`  
  porque el 3d utiliza la GPU y no la CPU y el movimiento queda mas fluido


- `color: currentColor;`  
	Quiere decir que el elemento hereda el color de su padre. Se puede usar 
  por ejemplo para poner el color a un texto del menu con su icono, tanto 
  el texto como el icono se ponen con el currentColor y la etiqueta "a" 
  que los envuelve a los 2, es decir, el padre, es quien va a tener el color


- Cuando se utilice border-radius, no usar el mismo para el elemento externo
  y el interno, poner un poco mas pronunciado el redondeo del externo


- Poner una animacion al input cuando sea invalido:  
  ```css
  input:invalid{
    animation: invalidInput .3s
  }
	```

- Esconder texto muy largo:  
  ```css
  p{
    overflow: hidden;
    text-overflow: ellipsis;
  }
	```

- Remover outline cuando se hace click en los controles pero no para usuarios  
  que usan el teclado:
	```css
	button:focus:not(:focus-visible) {
		outline: none;
	}
	button:focus-visible {
		outline: 2px solid blue;
	}
	```  


---

## Responsive

- es recomendable usar un max-width y no width, porque permite flexibilidad
  del elemento, con width el tamaño es fijo.

- es recomendable usar un min-height y no height, porque permite flexibilidad
  del elemento, con height el tamaño es fijo.


- para los textos puedo poner un max-width en caracteres, por ej 70ch


- Usar media queries para agregar complejidad, es recomendable hacer mobile
	first, es decir, hacer el diseño para mobile y luego agregarle complejidad
	para desktop, ya que normalmente en mobile los elementos van unos debajo de otros,
	que es el comportamiento por defecto, y para desktop se agrega la complejidad.  
	(ver youtube, lista css, video 
	**5 simple tips to making responsive layouts the easy way**)
	

- Un `width` recomendado para usar en los media queries es 40rem (640px).


- El comportamiento por defecto de `flex` es crear una fila, por lo que sus hijos  
  seran columnas.  
	El comportamiento por defecto de `grid` es crear una columna, por lo que sus  
	hijos seran filas. Para crear columnas, puedo usar la propiedad  
	`grid-auto-flow: column;`.


- `flex` es el diminutivo de las propiedades `flex-grow, flex-shrink y flex-basis` y sus  
  valores por defecto son 0 1 auto, respectivamente.
	Cuando se usa `flex: 1` los valores son 1 1 0%, lo que hace que el elemento ponga su  
	`width: min-content` pero despues se expande hasta ocupar todo el espacio disponible.  
	`flex-basis: 100%` hace que el elemento tenga el tamaño de su content width, pero  
	se expande hasta ocupar todo el espacio disponible.  
	`flex-flow` es el diminutivo de las propiedades `flex-direction y flex-wrap` y sus 
	valores por defecto son row nowrap, respectivamente.


- Una vez `flex-wrap: wrap` se activa (por defecto es nowrap), align-content funciona.


- Poner espaciado entre elementos de un container flex:  
	```css
	.container{
		display: flex;
	}
	.container:first-child{
		margin-right: auto;
	}
	.container:last-child{
		margin-left: auto;
	}
	```


- para hacer una layout responsive:  
	```css
	.container{
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(min(200px, 100%), 1fr));
	}
	```
  otra opcion:  
	```css
	@media (min-width: 40em) {
		.container{
			display: grid;
			grid-auto-flow: column;
			grid-auto-columns: 1fr;
		}
	}
	```

- para poner un texto centrado y una imagen de fondo:  
	```css
	.container{
		display: grid;
		place-items: center;
	}
	.container > *{
		grid-column: 1 / 2;
		grid-row: 1 / 2;
	}
	.container > img{
		aspect-ratio: 16/9;
		object-fit: cover;
		z-index: -1;
	}
	```

- tipografia para una layout responsive:  
  usando clamp():  
  se suma el valor en rem para que la fuente se modifique cuando el
  usuario hace zoom, la medida en vw no se modifica con el zoom.  
	`font-size: clamp(2rem, 10vw + 1 rem, 10rem);`  
  usando custom properties:  
	```css
	:root{
		--fs-600: 2rem;
		--fs-400: 1rem;
	}
	@media (min-width: 40em) {
		:root{
			--fs-600: 3rem;
			--fs-400: 1.25rem;
		}
	}
	```

- padding o margin en una layout responsive:  
  ```css
	padding: clamp(2rem, 20vh, 10rem) 0;
	padding: min(20vh, 10rem) 0;
	```
	es una logical property, solo maneja el top and bottom padding:  
	`padding-block: min(20vh, 10rem);`  


- Crear un menu responsive:  
  Ver curso-react-midudev/06-shopping-cart/components/Cart.css y Cart.jsx  

---

## Colores

- rgb, a parte de escribirlo de 0 a 255, lo puedo esrcibir en porcentajes:  
	`rgb(100%, 50%, 100%);`

---

## Imágenes  

- Poner las imagenes de una mejor manera:  
  ```css
	img{
		width: 100%;
		aspect-ratio: 16/9;
		object-fit: cover;
	}
	```

- Poner imagenes o logos de la misma altura:
  ```css
	img {
		width: 50px;
		aspect-ratio: 3/2;
		object-fit: contain;
		mix-blend-mode: color-burn;
	}
	```

---

## Metodología BEM  

BEM significa Bloque, Elemento, Modificador.  

Un bloque es un contenedor donde se encontrarán los diferentes elementos. El bloque 
corresponde a la raíz de la clase y deberá ir siempre primero. Cuando ya está definido 
es posible nombrar los elementos que compondrán la estructura final y su contenido.  
Algunas restricciones a la hora de nombrar un bloque:  
No puedes usar mayúsculas. No puedes usar dos guiones bajos seguidos, porque está 
reservado para los elementos. Y tampoco puedes usar dos guiones seguidos, porque 
está reservado para los modificadores.  

Un elemento es una de las piezas que compondrán la estructura de un bloque.  

Un modificador sirve para modificar algunas propiedades de un bloque o elemento.  

Para atacar los estilos del bloque en CSS, tienes que utilizar solo el selector de 
clase con el nombre del bloque.

Ejemplo:  

```html
<!-- EJEMPLO 1 -->
<div class="block">
    <div class="block__element">Elem 1</div>
    <div class="block__element">Elem 2</div>
    <div class="block__element block__element--modifier">Elem 3</div>
</div>
<!-- EJEMPLO 2 -->
<div class="item item--modifier">
    <div class="item__element">Elem 1</div>
    <div class="item__element">
        <div class="item__another-element">Elem 2</div>
        <div class="item__another-element">Elem 3</div>
    </div>
    <div class="item__element item__element--modifier">Elem 4</div>
</div>
```  
Los estilos usando un preprocesador de css:  
```css
// EJEMPLO 1
.block{ 
    color: inherit;
    &__element{
        color: inherit;
        &--modifier{ 
            color: inherit;
        }
    }
}
// EJEMPLO 2
.item{ 
    color: inherit;
    &--modifier{
        color: inherit;
    }
    &__element{
        color: inherit;
        &--modifier{
            color: inherit;
        }
    }
    &__another-element{
        color: inherit;
    }
}
```  


---

## Otros

- Medidas
	- **rem**: es una medida relativa, relativa al root o el html, 
	  normalmente **1rem = 16px**.   
	  Es preferible que trabajar con pixeles porq respeta la configuracion 
	  de otros navegadores o del usuario, pero si quiero consistencia por
	  ejemplo usando media-queries, puedo usar pixeles o em.  
	  Es preferible que trabajar con em porq solo hace referencia a un
	  elemento, el root, y no a distintos elementos, aunque puede haber 
	  situaciones donde se pueda usar.  
	- **em**: es una medida relativa, relativa al elemento que lo contiene,
	  normalmente **1em = 16px**


- no es necesario usar metodologia BEM cuando se trabaja a traves de
  modulos porq normalmente el framework le pone hash a las clases


- El css de una pagina es critico porque bloquea la carga de la pagina, 
  es mejor cargar el critical css (el css minimo para que la pagina se
  vea bien) en line, es decir, en el HTML para que la pagina cargue mas
  rapido porque la descarga del css bloquea mucho, entonces es mejor dejar 
  el resto del css para descargar despues.  
	