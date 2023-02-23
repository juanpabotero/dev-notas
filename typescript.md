
# TypeScript

- Typescript transpila el codigo a Javascript para ser leido por el 
  navegador


- Instalar Typescript de manera global, abro la terminal como 
  administrador y ejecuto:  
    `npm install -g typescript`


- Crear el fichero de configuracion para typescript, tsconfig.json.  
  En la terminal, estando en la carpeta del proyecto, doy:  
	`tsc -init`  ó  `tsc --init`


- Si escribo un archivo en typescript, debo transpilarlo para que se 
  pase a Javascipt y el navegador pueda leerlo.  
  En la terminal bash, estando en la carpeta del proyecto, debo darle:    
  `tsc -w`  ó  `tsc -w *.ts`  
  Para que este viendo y transpilando todos los archivos .ts del proyecto.  
  En el index HTML debo cargar los archivos Javascript (.js) que se crean
  despues de la transpilacion y no los archivos Typescript (.ts)


- En el **tsconfig.json**, descomento la propiedad **"rootDir"** y pongo la 
  nueva ruta, para configurar la ruta desde la cual se va a cargar 
  los ficheros de Typescript


- En el **tsconfig.json**, descomento la propiedad **"outDir"** y pongo la 
  nueva ruta, para configurar la ruta de salida para los archivos 
  transpilados de Javasript


- En el **tsconfig.json** y en **"target"** cambio la version, para cambiar 
  la version de Javascript a la cual se va a transpilar


- En el **tsconfig.json**, si descomento **"sourceMap"**, este me creara unos
  nuevos archivos pero me permitira que en la ejecucion en el navegador
  se relacione con el archivo Typescript y no con el Javascript


- En el **tsconfig.json**, descomento **"outFile"** y pongo el nombre del 
  archivo que va a ser la salida de todos nuestros archivos Typescript.  
  Es normal y recomendable que nuestro archivos Typescript se transpilen
  a un solo archivo Javascript, ej:  
  `"outFile": "./main.js"`  
  Igualmente desde el navegador y gracias a los maps, puedo saber que 
  archivo creó que codigo, se encuentra la referencia a los archivos 
  de Typescript. Esto es mas rapido porque solo se lee un archivo y centraliza 
  el archivo de salida


- En el **tsconfig.json**, descomento **"removeComments"**, para remover los
  comentarios de los archivos Javascript, pero se mantienen en los 
  archivos Typescript


- En el **tsconfig.json**, para incluir o excluir archivos o carpetas 
  que se quieran o no transpilar, voy al final del tsconfig e incluyo:  
  
		"exclude": [
				"nombre carpeta o archivo"
		],
		"include": [
				"nombre carpeta o archivo"
		]


- En el **tsconfig.json** puedo configurar las rutas para hacer las  
  importaciones más cortas:  
  ```typescript
  "compilerOptions": {
    "paths": {
      "@components/*": ["src/components/*"],
      "@layouts/*": ["src/layouts/*"],
      "@services/*": ["src/services/*"],
    }
  }
  ```  


- Los modulos de node estan excluidos de manera automatica para 
  la transpilacion


