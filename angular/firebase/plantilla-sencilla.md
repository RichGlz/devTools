# Plantilla1

## Dentro de `src/app/app.component.html`:

> O bien dentro de tu componente de HTML

``` html
<div class="container py-5">

<div class="d-flex text-white text-center justify-content-center">
  <h1 class="display-3 text-center"> {{title}} </h1>
  <span class="h2"> {{ version }} </span>
</div>

  <ul class="list-group py-5 col-4 mx-auto">
    <li
      *ngFor="let item of items"
      class="list-group-item my-2 rounded text-center">

      <!-- Descomenta "<code>" si estás leyendo  IDs -->
      <!-- <code class="d-flex small text-muted">
        {{ item.id }}
      </code> -->

      {{ item.name }}
    </li>
  </ul>

</div>
```

## Dentro de `src/styles.scss` o `src/styles.css`

``` css

body {
  background: #0F2027;  /* fallback for old browsers */
  background: -webkit-linear-gradient(to top, #2C5364, #203A43, #0F2027);  /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(to top, #2C5364, #203A43, #0F2027); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  
  /*Este siempre va al final*/
  background-attachment: fixed;
}
```

> Puedes encontrar más combinaciones de colores en [UIgradients](https://uigradients.com/), sólo recuerda escribir `background-attachment: fixed;` **al final** del todo.
