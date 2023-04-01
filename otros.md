
# OTROS

## Herramientas

### Node: 

Permite correr javascript del lado del servidor, tambien 
permite desarrollar localmente.  
Existen paquetes dentro de node que permiten muchas funcionalidades,
por ej, paquetes para trabajar con archivos en un servidor, conectarse
a bases de datos, etc.  
Babel es uno de los paquetes que esta disponible en node.  
Puedo poner node en la terminal para entrar en modo de ejecucion
y poner cualquier codigo de Javascript.  
Normalmente los modulos de node se dejan por fuera del git porque 
se pueden constriur facilmente en base al package.json


### NPM: 

Gestor de paquetes de node  
- **npm init** => crea el package.json  
  **npm init -y** => para indicar que si aceptas el contenido por defecto
- **npm install** => para instalar los modulos de node y los paquetes que
  estan en el package.json  
- **npm start** => para lanzar el servidor local
- **npm install -g** => para instalar de manera global
- **npm install** => para instalar como dependencia de produccion
- **npm install --save-dev** => para instalar como dependecia de desarrollo  
  **npm install -D**  
- **npm install --save** => para instalar de forma local en el proyecto  
  **npm install -s**
- **npm i nombrePaquete@version** => para instalar una version en especifico de 
  un paquete
- **npm i nombrePaquete@latest** => para instalar la ultima version de un paquete
- **-E** es para que instale la version exacta.  

**npx** es lo mismo que ejecutar ./node_modules/.bin/  
Permite ejecutar el comando de una libreria que no ha sido instalada.
Permite ejecutar comandos arbitrarios que estan en el npm package.  
Permite instalar paquetes de forma global en una carpeta temporal
y ejecutar el binario al vuelo  
ej, ./node_modules/.bin/eslint --init seria lo mismo que ejecutar  
npx eslint --init  

Instalar las dependencias siempre de manera local y no global. De manera global solo se 
puede usar una versión de un dependencia y si se tienen varios proyectos con distintas 
versiones de las dependencias, se puede tener problemas.  

Se puede crear un archivo `.npmrc` para configurar npm de manera local, esto sobreescribe
la configuracion global.  


### NVM: 

Node version manager, manejar la instalacion de versiones de node.  
Puedo instalar una version de node en concreto con:  
`nvm install version`  
Puedo usar una version de node en concreto con:  
`nvm use version`  
- **nvm -v** => version de NVM
- **nvm install versionNode** => instalar una version de node  
  **nvm install lts** => para instalar la ultima version lts de node
- **nvm use versionNode** => usar una version de node
- **nvm current** => ver la version actual de node
- **nvm ls** => listar las versiones de node disponibles
- **nvm uninstall versionNode** => desinstalar una version de node


### package.json: 

Le dice a node y a nosotros como funciona la 
aplicacion, que dependencias son necesarias para pasar a 
produccion, que puedo descartar para pasar a produccion, etc.
devDependencies del package.json son dependencias de desarrollo y
estas no llegan a la version de produccion.  

Dentro del package.json y las dependencias:
- ^ aceptara versiones dentro del rango de versiones menores, ej:  
 	^3.4.4 acepta 3.x.x
- ~ aceptara versiones dentro del rango de versiones de parche, ej:  
 	~3.4.4 acepta 3.4.x
- si no tiene nungun simbolo antes, solo acepta esa version exacta, ej:  
 	3.4.4

Dentro de los scripts puedo poner el comando:  
`"phoenix": "rm -f package-lock.json && rm -rf ./node_modules && npm install --no-fund --no-audit"`  
Lo que hace es eliminar el *package-lock.json* y el *node_modules* para
reinstalar los paquetes, normalmente se usa cuando se actualizan los
paquetes.  
El *--no-fund* es para que no muestre los mensajes de paquetes
que piden donaciones y el *--no-audit* es para que no muestre los mensajes 
de paquetes que piden auditar, ambos se usan para hacer una pequeña
optimizacion que puede ahorrar unos segundos en las instalaciones.

En los scripts puedo poner un comando para pasar el linter por todos los archivos, 
`"lint": "eslint . --fix"`

**peerDependencies** significa que no lo vamos a instalar nosotros, sino que vamos 
a depender de que el proyecto donde lo vamos a utilizar ya tenga instalada esa utilidad.  
El paquete necesita una dependencia de produccion que debe ser instalada por el usuario.  



### Babel: 

Libreria que convierte el codigo y lo hace compatible con
navegadores mas antiguos. pagina babeljs.io  
para instalarlo en nuestro proyecto:  
`npm install --save-dev babel-loader @babel/core`  
babel playground: para ver como queda transpilado el codigo


### Webpack:  

Empaquetador de modulos, automatiza muchas tareas, 
permite gestionar las dependencias de nuestra aplicacion, montar 
servidores de desarrollo y pruebas, cargar modulos, convertir a 
diferentes formatos, minimizar codigo, compilar SASS a CSS, 
compilar TS a JS, nos permite trabajar con Javascript moderno 
pues se encarga de la compatibilidad  

webpack.js.org: sitio oficial de webpack  

Estos serian los comandos para iniciar el webpack:  
crear el directorio:  
`mkdir webpack-demo`  
acceder al directorio:  
`cd webpack-demo`  
crear el package.json:  
`npm init -y`  
instalar webpack o reconstruir los modulos de node si ya 
esta instalado:  
`npm install webpack webpack-cli --save-dev`  
--save-dev indica que es una dependencia de desarrollo

Dentro del package.json, la parte de "scripts" son los comandos
que podemos ejecutar bajo la instruccion  
`npm run nombreComando`

Dentro del package.json en la parte de "scripts" la linea "build" 
sirve para construir la version de produccion de mi aplicacion
`npm run build` en la terminal para ejecutarla

la dependencia **"html-loader"** ayuda a cargar el html.  
la dependencia **"html-webpack-plugin"** ayuda a inyectar el modo final
de nuestro archivo JS al index.html.   
la dependencia **"webpack-dev-server"** ayuda a montar un servidor local
para las pruebas, se ejecuta en el terminal con la instruccion
`npm run start` ó npm start.  
las dependencias **"css-loader" y "style-loader"** ayudan a cargar 
el CSS y los estilos.  
la dependencia **"mini-css-extract-plugin"** para inyectar archivos css.  
la dependencia **"file-loader"** ayuda a cargar imagenes y demas recursos.  
la dependencia **"copy-webpack-plugin"** ayuda a cargar los resursos estaticos  
las dependencias **"css-minimizer-webpack-plugin" y "terser-webpack-plugin"** 
para minimizar el css.  
la dependencia **"@babel/core"** ayuda a convertir el codigo de js  
la dependencia **"babel-loader"** ayuda a cargar el babel 


### Axios: 

Es un paquete que permite trabajar con peticiones http, para instalar:  
`npm i axios`

### RXJS: 

Libreria de Javascript que permite implementar
programacion reactiva en Angular. Se trabaja a traves de eventos
y suscribirse a ellos, para escuchar cuando se emitan los datos
y ejecutar algo

### Redux: 

Manejador de estados globales

### Jest: 

Test  
instalar como devDependency:  
`npm install jest -D`  
Instalar los tipos de jest:  
`npm install @types/jest -D`  
instalar STANDARD como devDependency, para poder exportar entre archivos:  
`npm install standard -D`  
en el package.json dentro de scripts poner "test": "jest" y ejecutar con:  
`npm run test`  
Tambien puedo agregar el comando: `"test:watch": "jest --watchAll"` para   
que este escuchando los cambios, lo ejecuto con: `npm run test:watch`.  
igualmente ver en jestjs.io y en **03-Javascript/04-JavascriptEjercicios**

### FNM:

Alternativa a NVM para manejar multiples versiones de NodeJS

### Astro: 

Framework para crear sitios web estaticos

### Electron: 

Es un framework que permite crear aplicaciones de escritorio
utilizando tecnologias web (HTML, CSS , JavaScript)  
Pagina: electronjs.org

### GraphQL:  

Es un lenguaje para hacer consultas

### Deno: 

Alternativa a node

### Bun: 

Es un post-css, babel, node, webpack todo en uno.  
tiene un entorno de ejecucion como lo son Node y Deno, tiene un manejador
de paquetes como es npm, es un empaquetador como lo es webpack.

### json-server: 

Servidor que permite hacer peticiones HTTP.  
Pagina y documentacion: npmjs.com/package/json-server.  
Para instalar de manera global se abre la terminal como 
administrador y ejecutar:  
`npm install -g json-server`  
Crear un archivo de texto con la informacion y llamarlo db.json.  
Para levantar el servidor de Json-server, en la terminal, 
estando en la carpeta donde esta el archivo db.json:  
`json-server --watch db.json`  
Debo dejar corriendo la terminal donde ejecute el comando.  
Normalmente levanta el servidor en **localhost:3000**

### Firebase: 

Es un servicio en la nube que nos permite tener nuestra base
de datos no relacional (NoSQL) y tambien nos da la posibilidad de
crear nuestro propio backend en sus servicios.  

**Cloud functions**: funciones que se ejecutan en la nube. podria crear
un servicio rest personalizado


### JQuery: 

libreria Javascript  
**JQuery UI**: para crear interfaces de usuario


### Sonarqube: 

Herramienta de revision de codigo automatica para detectar bugs
vulnerabilidades, code smells. Se puede integrar con el flujo de trabajo
actual para permitir la inspeccion continua de codigo en las ramas del 
proyecto.  

Inicar SonarQube, abrir el CMD y ejecutar:  
- cd C:\Users\juanp\Instaladores\sonarqube-8.9.9.56886\bin\windows-x86-64
- StartSonar.bat
- cuando diga SonarQube is up puedo ir al localHost:9000 y ver la pagina
  de inicio de SonarQube.

Para correr el scanner en un proyecto, en la terminal, estando en la 
carpeta donde esta el proyecto, ejecuto:  
`sonar-scanner.bat -D"sonar.projectKey=test-angular-material" -D"sonar.sources=." -D"sonar.host.url=http://localhost:9000" -D"sonar.login=e95d357b8fd390666dff709c1f4756816dc5bfc6"`  
cuando aparezca EXECUTION SUCCESS puedo ver el proyecto que se ha analizado
en el localHost:9000.


### Github actions: 

Para hacer continous integration


### Eslint:  

Declarar reglas de uso del codigo.  
Una configuracion rapida en algun proyecto puedo instalar
standard o semistandard (el mismo standard pero con semicolons),
funciona para archivos .js, .jsx:  
En la teminal `npm install standard -D`  
Dentro del **package.json** pongo:  
```json
"eslintConfig": {
	"extends": "standard"
}
```  
Para un proyecto en el que use React debo poner, no lo de arriba, 
si no esto:  
```json
"eslintConfig": {
	"extends": "./node_modules/standard/eslintrc.json"
}
```  

Para instalar eslint en un proyecto que use TypeScript seria mejor 
hacerlo asi:  
`npx eslint --init`  

1. Seleccionar, To check syntax, find problems, and enforce code style
2. Seleccionar, JavaScript modules (import/export)
3. Seleccionar, React
4. Seleccionar, Yes
5. Seleccionar, Browser
6. Seleccionar, Use a popular style guide
7. Seleccionar, Standard
8. Seleccionar, JavaScript
9. Seleccionar, Yes
10. Seleccionar, npm

El resumen de las preguntas que se hacen quedaria asi:  
How would you like to use ESLint? · style
What type of modules does your project use? · esm
Which framework does your project use? · react
Does your project use TypeScript? » Yes
Where does your code run? · browser
How would you like to define a style for your project? · popular guide
Which style guide do you want to follow? · standard-with-typescript
What format do you want your config file to be in? · JavaScript
Would you like to install them now? · Yes
Which package manager do you want to use? · npm

En el archivo `.eslintrc.cjs`, en `"parserOptions"`, agregar: `"project": "./tsconfig.json"` 
para que vea el archivo que tiene la configuracion de TypeScript.  

Si deseo desactivar alguna regla de Eslint, en el archivo `.eslintrc.cjs`, 
en `"rules"` (es un objeto), agregar la regla que quiero desactivar, por ejemplo: 
`"@typescript-eslint/explicit-function-return-type": "off"`.  

Como tip es que si quiero desactivar alguna regla, en el editor puedo pararme 
encima del error y darle la opción de desactivar la regla, copio el texto que 
está despues de *eslint-disable-next-line* y lo pego en el archivo `.eslintrc.cjs`, 
en `"rules"` y le agregó el valor `"off"`.  

### Prettier:  

Puedo instalar Prettier en cualquier proyecto, para usar una configuracion  
especifica en ese proyecto y estandarizar cuando se quiere trabajar en equipo.  
Ejecuto `npm install prettier -D`  
Creo el archivo `.prettierrc.json`  
Agrego la configuracion que quiero en formato json, ej:
```json
{
	"semi": true,
	"singleQuote": true,
	"trailingComma": "none"
}
```
Si hay algun conflicto entre el formeteo de prettier y EsLint, puedo  
desactivar esa regla en la configuración del EsLint:  
```json
"eslintConfig": {
	"extends": "standard",
	"rules": {
		"space-before-function-paren": "off"
	}
}
```  


### Playwright: 

Para hacer test E2E.  
- Para instalarlo en el proyecto: `npm init playwright@latest`  
- Una vez configurados los test, los ejecuto con: `npx playwright test`  
- Si me sale el error *ReferenceError: require is not defined in ES module scope*  
	debo cambiar el archivo playwright.config.js a playwright.config.cjs  
(ver react/midudev/projects/04-react-prueba-tecnica)  


### wc-toast 

wc-toast de npm packages para crear un toast (una alerta)


### TDD (Test Driven Development)

Desarrollo guiado por test, primero se escriben los test y despues el
codigo.  
Se escribe un test que no pase, se hace el código para que pase y despues 
se resfactoriza con la seguridad de que ya tengo un test que me cubre.  
Si escribo un test y pasa inmediatemente, puedo evaluarlo y ver si me está 
aportando o si ya hay otro test que lo cubre.  
Puedo ir quitando los test redundantes.


---

## Conceptos


### Polyfill: 

Es un codigo que provee el funcionamiento de una nueva 
caracteristica de Javascript (ES6), en versiones viejas como ES5.  
Parchea el objeto global para añadir soporte de una funcionalidad que 
ese navegador todavía no soporta.

### Ponyfill:  

Una implementación de una funcionalidad que debería existir en el navegador, 
pero no existe. No parchea el objeto global, sólo exporta la funcionaidad para 
que la puedas usar.  


### SPA: 

Single Page Application


### SSR (Server Side Rendering): 

Se ejecuta en el servidor, y se renderiza la pagina en el cliente.


### Serializar 

Serializar la informacion es transformar la informacion en un string para
que pueda viajar desde el servidor al cliente porque si se envian objetos
complejos se perderia informacion, por eso se transforma a un string


### Expresiones regulares (regex):

- /expresion/: expresion regular
- /expresion/g: expresion regular global
- /expresion/i: expresion regular insensible a mayusculas y minusculas
- /expresion/m: expresion regular multilinea
- \: es el simbolo de escape, para quitar la relacion y buscar el simbolo 
  como tal. Dentro del conjunto de caracteres no es necesario escapar
  los simbolos.

- coincidencias basicas:
	- .: cualquier caracter, excepto el salto de linea
	- \d: digito (0-9)
	- \D: no es digito (0-9)
	- \w: caracter alfanumerico (a-zA-Z0-9_)
	- \W: no es caracter alfanumerico (a-zA-Z0-9_)
	- \s: espacio de cualquier tipo (tab, espacio, salto de linea)
	- \S: no es espacio de cualquier tipo (tab, espacio, salto de linea)
- limites:
	- \b: limite de palabra
	- \B: no es limite de palabra
	- ^: inicio de cadena de texto
	- $: fin de cadena de texto
- cuantificadores:
	- *: 0 o más veces
	- +: 1 o más veces
	- ?: 0 o 1 vez
	- {n}: numero exacto de veces
	- {n,m}: rango (minimo, maximo)
- conjunto de caracteres:
	- [abc]: cualquier caracter de la lista
	- [^abc]: cualquier caracter que no esta en la lista
- grupos:
	- (expresion): grupo de expresiones
	- (expresion)?: grupo de expresiones opcionales
	- |: uno u otro

	- regexr.com: distintas expresiones regulares para validaciones


### Depurar (debugging): 

Identificar y corregir errores.  
Para hacerlo con VSCode y chrome, debe estar corriendo la
aplicacion, doy F5 en VS, selecciono chrome, en el archivo 
launch.json pongo el puerto que estoy usando y en webroot 
la carpeta del proyecto y guardo los cambios. Doy F5 para 
correr el debuger y esto me abre una nueva ventana de chrome. 
Pongo el breakpoint en VS donde quiero revisar el funcionamiento.  

otra forma es poniendo la palabra debugger en el codigo donde
quiero que se detenga la aplicacion una vez este corriendo, 
esto lo veriamos en chrome.  

para usar la depuracion y los breakpoint del navegador, abro el devTool
del navegador, entro al archivo que quiero depurar, poner los breakpoint
dando click sobre el numero de la linea que quiero y controlo el avance
de la depuracion con las opciones disponibles (las flechas)  


### Microfrontend: 

Son componentes de la ui que se pueden desplegar de forma separada


### Monorepo: 

Es un unico repositorio que contiene multiples proyectos distintos con relaciones bien definidas entre si


### Storybook: 

Sirve para tener un catalogo de componentes y poder verlas en una pagina web.


### Docker: 

Es un set de herramientas usado para crear y correr contenedores

### Contexto

Engloba toda la aplicacion para que todos los componentes puedan tener disponible 
la informacion de manera global.

### Hidratación

Es darle vida al componente, agregarle intaractividad, eventos, un estado, etc.  
Cuando se trae la información al cliente desde el servidor solo se trae HTML, si  
no se hidrata (si no se ejecuta el Javascript) no se tiene interactividad.

### Web Components

Son una serie de tecnologías que se complementan entre si, que nos permiten crear  
componentes reutilizables sin ninguna dependencia.  
Una de las tecnologías son los **Custom Elements**, que permiten crear elementos HTML  
personalizados. ej:  
`<tool-tip></tool-tip>`  
Se diferencian de las demas etiquetas HTML porque siempre deben tener 2 palabras  
separadas por un guion. Se podria estilar y usar como cualquier otro elemento HTML.  
Por defecto se comportan como elementos in-line.  

### Otros conceptos:

- el archivo .gitignore le dice a git que archivos quiero ignorar


- transpilar: traducir de un lenguaje a otro
- compilar: traducir de un lenguaje a lenguaje de maquina


- Patron modulo: patron de diseño mas comun en JS


- para los nombres de archivos, escribirlos en minuscula y separados
  por un guion, ej: pais-tabla.js


- nombrearchivo-min.js: es el archivo minificado, este seria el archivo
  de produccion. igualmente se recomienda tener el archivo de desarrollo
  en el cual vamos a programar y desde el cual vamos a minificar


- assets es la carpeta de recursos estaticos de la pagina web, 
  es buena practica poner allí los recursos como css, js, imagenes y demas


- pensar primero y diagramar la solucion del problema (UML)


- un token es usado para mantener de forma pasiva el estado del usuario 
  en nuestra aplicacion


- expresion devuelve un valor  
  declaracion no devuelve un valor


- CI: continous integration  
  CD: continuous deployment


- JIT (Just In Time): Una compilacion que ocurre durante el runtime
  de la aplicacion. Tiene menos performace que la compilacion
- AOT (Ahead Of Time): Una compilacion que ocurre antes del runtime
  de la aplicacion. Tiene mejor performace.


- los frameworks actuales hacen los siguientes pasos para cargar una web:
	- SSR del HTML lo envia desed el servidor y lo renderiza el navegador
	- El navegador descarga el javascript de la aplixcacion
	- El navegador ejecuta el javascript de la aplicaciony empieza el 
	  proceso de reconciliacion.
	- El framework pide los componentes lazy load porq estan visibles
	- El framework completa la rehidratacion de la aplicacion  


- Estilos de escritura:  
  - PascalCase  
  - camelCase  
  - kebab-case  
  - snake_case


---

## Web Performance

- **TTFB (time to first byte)**: mide el tiempo desde que el navegador
	hace la peticion de la pagina hasta que el primer byte es recibido.  
	<600ms

- **FCP (First Contentful Paint)**: Señala el tiempo que ha tardado en renderizar 
  cualquier texto o imagen (incluido fondos). Le dice al usuario si realmente la 
	web funciona y pueda empezar a consumir la web.  
	<1.8s

- **LCP (Largest Contenful Paint)**: El tiempo que tarda en renderizarse la pieza 
  de contenido mas grande que esta en el viewport. Es una de las tres Web Vitals 
	de Google, visualmente impacta mucho al usuario.  
	<2.5s  

- **SI (Speed Index)**: Calcula como de rapido el contenido visual, se ha 
  renderizado progresivamente en el viewport. No es lo mismo que una pagina este 
	en blanco 3 segundos y se muestre todo de golpe, a hacerlo progresivamente. 
	Se percibe distinto.  
	<2.5s  

- **FID (First Input Delay)**: Mide el tiempo que tarde en responder la interfaz 
  a la primera interaccion del usuario. Es la Web Vitals de interactividad.  
	<100ms  

- **TBT (Total Blocking Time)**: Suma la duracion de la tareas largas (mas de 50ms)
  de JS que han bloqueado el hilo principal despues del FCP. Cuanto mas tiempo esta
	bloqueado el hilo, menos usable es la pagina.  
	<200ms

- **mFID (Max Potential First Input Delay)**: Mide el maximo FID posible teniendo
  en cuenta el tiempo que el hilo principal esta bloqueado. Interesante para detectar
	en pruebas posibles valores del FID.  
	<130ms

- **CLS (Cumulative Layout Shift)**: Mide los saltos que ha dado el layout de tu pagina 
  mientras cargaba. La Web Vital de estabilidad visual. Suele pasar con imagenes 
	y banners de publicidad.  
	<0.1s

- **TTI (Time to Interactive)**: El tiempo que tarde la pagina en haber mostrado todo
  el contenido util, los eventos de los elementos mas visibles han sido registrados y 
	la pagina responde a interacciones en 50ms. Inestable, mejor mirar el TBT.   
	<3.8s  

### Ver rendimiento de una página

En las devTools del navegador, en cobertura, miro el código que no se usa y reviso en los  
archivos que es lo que no se usa.  
En red, filtro por imágenes y veo si no hay imágenes optimizadas, también puedo ver otros
recursos como el JS o el CSS.  
En performance insight, veo como cargan los recursos.  


---

## Estructuras de datos

Son una forma de almacenar y organizar datos, nos permiten acceder a los datos de una  
forma rápida y sencilla.  

- **List**: Guarda elementos en memoria en celdas contiguas, es decir, los elementos  
  quedan continuo.  
- **Linked list (Lista enlazada)**: Los elementos se guardan como nodos en diferentes  
	partes de la memoria, cada elemento de la lista contiene un enlace al elemento siguiente.  
- **Double Linked list**: Cada elemento enlaza con el elemento anterior y el siguiente.  
- **Stack (pila)**: El ultimo elemento que se añade a la pila, es el primero que sale  
  (lifo: last in, first out).  
- **Queue (cola)**: El primer elemento que se añade a la pila, es el primero que sale  
  (fifo: first in, first out).  
- **Hash Table (Tabla Hash)**: Utiliza una función de hash para almacenar y recuperar valores.  
  Su omonimo en JavaScipt, es un objeto.  
- **Tree (Arbol)**: Cada elemento es un nodo, donde cada nodo puede tener uno o más hijos.  
- **Binary Tree (Arbol binario)**: Cada elemento es un nodo, donde cada nodo puede tener  
  como máximo 2 hijos.  
- **Graphs (Grafos)**: Cada elemento es un nodo que estan conectados por enlaces.  


---

## Otros

- Redimensionar, comprimir y pasar a formato WebP o AVIF
  las imagenes antes de subirlas en la pagina web.  
	Usar jpg, webP cuando es una imagen grande con muchos colores.
	Usar png cuando se necesita transparencia o una imagen de maximo
	32 colores, para iconos normalmente se usa svg.


- Mantener las paginas por debajo de 3Mb  
  Un buen tiempo de carga de una pagina es por debajo de 3sg


- no usar mas preprocesadores, sobretodo stylus y Less, SASS podria 
  usarse de ser necesario. Mejor usar postprocesadores como postcss


- lightning-css: es el nuevo nombre de parcel-css, empaqueta y minifica el css, 
  una alternativa a postcss


- No usar Snowpack, usar Vite, EsBuild o Parcel


- node 18 ya permite hacer test  
  (ver en twitch midu, el video de NODE 18, min 31:00)


- articulo sobre como evitar los cambios de diseño causados ​​por las fuentes web, 
  [ver...](https://simonhearne.com/2021/layout-shifts-webfonts/)  

