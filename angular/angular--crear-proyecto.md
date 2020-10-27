# Crear un proyecto con **Angular CLI**

## 1. Crear un nuevo proyecto:

  **En Windows:**

  1. Vaya a la carpeta donde creará el proyecto.
  2. Presione `shift + clic derecho`
  3. Seleccione ` Abrir la ventana de PowerShell aquí `

## 2. En el PowerShell

``` shell
npm install -g @angular/cli
ng new <nombre-del-proyecto>
cd <nombre del proyecto>
```

> En cuanto a **estilos** prefiero utilizar *SCSS*; es similar a *CSS* pero con más opciones. 👌🏻

## 2. Ejecutar el servidor

``` shell
ng serve -o
```

> `-o` es de `open`. Para que una vez finalizado, abra una ventana del navegador en el *localhost:4200*.
