
# HTML

## Conceptos

- Node vs Element:
  Node y NodeList representan cualquier "cosa" del DOM, un elemento html, 
  texto, un comentario. Puede usarse forEach con NodeList.
  Element y HTMLCollection representa un elemento html. No puede usarse 
  ningun metodo de array con HTMLCollection


- Solo debe haber un h1 por pagina


- hr se deberia usar mas semanticamente que para estilar, éste separa 
  dos elementos


- Se puede tener mas de una etiqueta header y footer por pagina, 
  siempre que tenga sentido


- Si quiero poner la forma en que se cargan las imagenes en el HTML, pongo la
  propiedad `loading="eager"` para las imagenes que ya estan en la vista del
  usuario, y la propiedad `loading="lazy"` para las imagenes que no estan en la vista del usuario.


- Las navegaciones de las paginas se hacen con etiquetas a, no con botones, 
  un boton es para hacer una accion, un anchor es para la navegacion, se pueden
  estilar los anchor para que parezcan botones.  
  Ademas, nunca se debe poner etiquetas a dentro de botones o viceversa.


- div es el contenedor para elementos en bloque y span es el contenedor 
  para elementos en linea


- Atributo `title` dentro de la etiqueta p para que se vea como tooltip


- `data-*` como atributo de un elemento, normalmente se usa como identificador  
  para después usar ese elemento en el JS, ej:
  ```html
  `<button data-id="button-1"></button>`  
  ```
  En el JS:  
  ```js
  const button = document.querySelector('[data-id="button-1"]');
  ```  

- El atributo `aria` se usa para darle mas informacion a los lectores de 
  pantalla, por ejemplo, si quiero que un elemento sea leido como un boton, 
  puedo ponerle el atributo `role="button"`


- Poner el atributo `fetchpriority="high"` a un elmento le dice al navegador 
  que tiene alta prioridad para que se haga su carga, esto se puede usar por ej 
  en el LCP (Largest Contentful Paint) para que se cargue lo mas rapido posible.  


- Poner alto y ancho a las imágenes como atributos de la etiqueta img, 
  ayuda a que el navegador sepa el tamaño de la imagen antes de cargarla, 
  y asi no se vea el efecto de carga de la imagen y no haya movimiento del  
  layout. Despues se puede usar CSS para formatear mejor la imagen.  


---


## Utilidades

- Para cargar diferentes tamaños de imagenes:  
  ```html
  <img  src="perro-800w.jpg" 
        srcset="perro-480w.jpg 480w, 
                perro-800w.jpg 800w"
        sizes="(max-width: 600px) 480px, 800px"
        alt="perro">
  ```
  	otra forma:  
  ```html
  <picture>
  	<source media="(max-width: 799px)" srcset="perro-480w.jpg">
  	<source media="(min-width: 800px)" srcset="perro-800w.jpg">
  	<img src="perro-800w.jpg" alt="perro">
  </picture>
  ```


- Cargar diferentes formatos de imagenes, etiqueta picture, dentro poner el source
  con el formato webp y como fallback poner la etiqueta img con la imagen en jpg
  ```html
  <picture>
  	<source srcset="perro.webp" type="image/webp">
  	<img src="perro.jpg" alt="perro">
  </picture>
  ```


- Crear un autocomplete:  
  ```html
  <label>
  	Elige el mejor framework:
  	<input list="frameworks"/>
  </label>
  <datalist id="frameworks">
  	<option value="Angular"></option>
  	<option value="React"></option>
  	<option value="Vue"></option>
  	<option value="Svelte"></option>
  </datalist>
  ```


- Crear una lista para seleccionar:  
  ```html
  <select>
  	<option value="Angular">Angular</option>
  	<option value="React">React</option>
  	<option value="Vue">Vue</option>
  	<option value="Svelte">Svelte</option>
  </select>
  ```


- Puedo cargar un gif de la siguiente manera para ahorrar el peso del gif,
  se pone el **autoplay** con el **muted** (los navegadores no permiten autoplay sino se tiene muted) y **loop** para que se repita infinitamente:  
	`<video muted autoplay loop src="rutaVideo" />`


- Cargar un archivo abriendo la camara trasera o delantera del celular:  
  `capture` me dice si abre la camara delantera o trasera y `accept` me dice
  si acepta un video o una foto  
  ```html
  <label>
    Video trasero
    <input type="file"  capture="environment"  accept="video/*">
  </label>

  <label>
    Foto delantera
    <input type="file"  capture="user"  accept="image/*">
  </label>
  ```


- Crear una galeria de imagenes:  
  ```html
  <section>
  	<img src="perro-1.jpg" alt="perro">
  	<img src="perro-2.jpg" alt="perro">
  	<img src="perro-3.jpg" alt="perro">
  	<img src="perro-4.jpg" alt="perro">
  </section>
  ```
  ```css	
  section {
  	display: flex;
  	width: 600px;
    height: 400px;
  }
  section img {
  	width: 0;
    flex-grow: 1;
  	object-fit: cover;
    opacity: 0.8;
    transition: 0.5s ease;
  }
  section img:hover {
    widht: 300px;
  	opacity: 1;
    filter: contrast(120%);
  }
  ```  


- Crear una modal  
  ```html
  <dialog>
    <h1>Esta es una modal</h1>
    <p>El párrafo de la modal</p>
    <button id="cancel">Salir</button>
  </dialog>
  <button id="show">Abrir modal</button>
  ```
  ```js
  const dialog = document.querySelector('dialog');
  const show = document.querySelector('#show');
  const cancel = document.querySelector('#cancel');
  show.addEventListener('click', () => dialog.showModal());
  cancel.addEventListener('click', () => dialog.close());
  ```
  ```css
  dialog::backdrop {
    background-color: rgba(0, 0, 0, 0.5);
    backdrop-filter: blur(5px);
  }
  ```