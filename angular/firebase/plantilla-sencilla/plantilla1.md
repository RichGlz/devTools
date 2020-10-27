# Plantilla1

## Dentro de `src/app/app.component.html`:

> O bien dentro de tu componente de HTML

``` html
<div class="container py-5">

  <h1 class="display-3 text-white text-center"> {{title}} </h1>

  <ul class="list-group py-5">
    <li class="list-group-item my-2 rounded" *ngFor="let item of items | async" >
      {{ item.name }}
    </li>
  </ul>

</div>
```

## Dentro de `src/styles.scss` o `src/styles.css`:
``` css

body {
  background: #0F2027;  /* fallback for old browsers */
  background: -webkit-linear-gradient(to top, #2C5364, #203A43, #0F2027);  /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(to top, #2C5364, #203A43, #0F2027); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  
  /*Este siempre va al final.*/
  background-attachment: fixed;
}
```

> Puedes encontrar más combinaciones de colores en [UIgradients](https://uigradients.com/), sólo recuerda escribir `background-attachment: fixed;` al final de los colores.
