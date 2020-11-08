# Decoradores `Inputs` y `Outputs`

## Input

Para comunicar de un componente padre a un componente hijo usamos Input

``` ts
export class ProductComponent {

  // Equivalente a prop, dónde le vamos a pasar la data al componente 
  @Input() product: Product;
}
```

Para pasar argumentos, desde el template padre podemos utilizar los corchetes cuadrados con el Input para pasar el argumento

``` html
<app-product [product]="products[0]"></app-product>
```

``` html
<div *ngFor="let product of products">
  <app-product [product]="product"></app-product>
</div>
```

## Output

> Para comunicar de un componente hijo a un componente padre usamos `Output`.

> Los `Output` son eventos que podemos cachar desde nuestro componente hijo por parte del padre.

> Para declararlos en nuestro componente tenemos que usar el decorador `@Output` sobre un `EventEmitter`

``` ts
export class ProductComponent {
  @Output() clickAddToCart = new EventEmitter<any>();
  // (clickAddToCart)= eventHandler($event):function
  ...
}
```

Los `EventEmmiter's` pueden emitir un evento con un argumento que será recibido por el padre.

``` ts
export class ProductComponent {
  @Output() clickAddToCart = new EventEmitter<any>();
  // (clickAddToCart)= eventHandler($event):function

  addToCart(){
    this.clickAddToCart.emit(this.product.id)
  }
}
```

> Para hacer uso del output podemos llamar el evento desde paréntesis y asignarle un evento `(clickAddToCart)="handler($event)"`:

### Componente padre

``` ts
// TypeScript
export class AppComponent {
 ...
  handleProductAddToCart(id: number) {
    console.log('product -> id', id);
  }
}
```

``` html
<!-- HTML -->
<app-product
  (clickAddToCart)="handleProductAddToCart($event)">
</app-product>
```

El event es recibido desde el emit del EventEmmiter es:

``` ts
this.clickAddToCart.emit(this.product.id)
```
