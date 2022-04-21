## Colori

Definisci il tuo set di colori in `abstracts/_colors.scss`.

```scss
$colors: (
  primary: (
    400: #5683f0
  ),
  secondary: (
    400: #e600bb,
    500: #b311ff
  ),
  neutral: (
    100: #fff,
    400: #737a82,
    800: #282b2f,
    900: #1a1c1d
  )
);
```

che userai con:

```scss
.text-primary {
  color: var(--clr-primary-100);
}
```

o con un `@each` che definisce le classi di text e background con i colori presenti in `_colors.scss`.

In maniera più "easy" puoi definire delle costanti:

```scss
$primary: rgba(4, 140, 168, 1);
$secondary: rgba(22, 219, 147, 1);
$accent: rgba(211, 24, 105, 1);

$white: rgb(255, 255, 255);

$text-primary: $primary
$text-inverse: $white
$text-accent: $accent
$text-secondary: $secondary
```

## Font

Definisci un set di fonts compreso eventuali import di font esterni (es. Roboto, Lato, Nunito, Inconsolata, ecc...)

```scss
$font-stack: 'Roboto', sans-serif;
$font-sign: 'Square Peg', cursive;

$font-light: 100;
$font-normal: 400;
$font-bold: 700;
$font-black: 900;

@mixin font($weight, $font-family) {
  font-family: $font-family;
  font-weight: $weight;
}
```

Il mixin mi è utile per definire una funzione che dato un weight e un set di font family mi imposta le regole.
Esempio di uso:

```scss
html {
  @include font($font-light, $font-stack);
}
```