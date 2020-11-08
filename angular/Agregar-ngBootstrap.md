# Agregar Bootstrap a un proyecto de Angular

## 1. Instalar Bootstrap

El nuevo comando de *Angular CLI* para agregar estos paquetes.

``` shell
ng add @ng-bootstrap/ng-bootstrap
```

> Esto instalará ng-bootstrap como aplicación predeterminada en tu `angular.json`. Si tienes múltiples proyectos y se quiere agregar una aplicación determinada, podrás especificarlo con la opción `--project`:

Por ejemplo: 
``` shell
ng add @ng-bootstrap/ng-bootstrap --project miProyecto
```

## 3. Ejecutar el servidor (opcional)
``` shell
ng serve -o
```

##### Fuente: [Documentación oficial de ng-bootstrap](https://ng-bootstrap.github.io/#/getting-started).