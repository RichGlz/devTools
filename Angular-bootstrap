# Agregar Bootstrap a un proyecto de Angular

## 1. Instalar Bootstrap

El nuevo comando de *Angular CLI* para agregar estos paquetes.

``` shell
npm i jquery bootstrap @popperjs/core --save
```

## 2. Instalar **Boostrap** `angular.json`

**Antes:**

``` ts
...
  "styles": [
  "src/styles.scss"
  ],
  "scripts": []
...
```

**Después:**

``` ts
...
  "styles": [
  "src/styles.scss",
  "./node_modules/bootstrap/dist/css/bootstrap.min.css"
  ],
  "scripts": [
    "./node_modules/jquery/dist/jquery.slim.min.js",
    "./node_modules/bootstrap/dist/js/bootstrap.min.js",
    "./node_modules/@popperjs/core/dist/umd/popper.min.js"
  ]
...
```

## 3. Ejecutar el servidor

``` shell
ng serve -o
```
