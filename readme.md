# Guida per il package.json in SASS

Vedi la guida [qui](https://thinkdobecreate.com/articles/minimum-static-site-sass-setup/) per avere tutte le dipendenze. Cambia le `dependencies` in `devDependencies`.

Attenzione, nello script di watch:html vai a cambiare le single-quote con i doppi apici per farlo funzionare con Windows. Ho notato che con la shell linux in windows ho problemi, mentre con bash funziona.

Aggiungi la copia e il watch degli assets: `"copy:assets": "copyfiles -u 1 ./src/assets/**/* public",` `"watch:assets": "onchange \"src/assets/**/*\" -- npm run copy:assets",`

Infine inserisci una licenza: `"license": "MIT",`

```json
{
  "name": "ambiente",
  "version": "0.1.0",
  "description": "SASS compile|autoprefix|minimize and live-reload dev server using Browsersync for static HTML",
  "main": "public/index.html",
  "author": "Lorenzo",
  "license": "MIT",
  "scripts": {
    "build:sass": "sass  --no-source-map src/sass:public/css",
    "copy:assets": "copyfiles -u 1 ./src/assets/**/* public",
    "copy:html": "copyfiles -u 1 ./src/*.html public",
    "copy": "npm-run-all --parallel copy:*",
    "watch:assets": "onchange 'src/assets/**/*' -- yarn copy:assets",
    "watch:html": "onchange \"src/*.html\" -- yarn copy:html",
    "watch:sass": "sass  --no-source-map --watch src/sass:public/css",
    "watch": "npm-run-all --parallel watch:*",
    "serve": "browser-sync start --server public --files public",
    "start": "npm-run-all copy --parallel watch serve",
    "build": "npm-run-all copy:html build:*",
    "postbuild": "postcss public/css/*.css -u autoprefixer cssnano -r --no-map"
  },
  "devDependencies": {
    "autoprefixer": "^10.4.2",
    "browser-sync": "^2.27.7",
    "copyfiles": "^2.4.1",
    "cssnano": "^5.0.17",
    "npm-run-all": "^4.1.5",
    "onchange": "^7.1.0",
    "postcss-cli": "^9.1.0",
    "sass": "^1.49.8"
  }
}
```

# Yarn

Per questo ambiente ho usato yarn. Quando installi le dipendenze ignora i warning, tanto userai questi tool in ambiente locale per fare la build del tuo sito web.

# Alternativa 1: Node Sass

A volte troverai progetti con node sass:

```
npm i -g node-sass
node-sass -o css sass/main.scss
```

questi comandi installano Node-Sass e compila il mio file in sass/main.scss nel target css dove creerà il file main.css.

Posso creare un comando in package.json per il watch:

```json
"watch": "node-sass -o css sass/main.scss -w'
```

e avvio con `npm run watch` o con yarn se uso questo package manager.

# Alternativa 2: Live Sass Compiler per VSCode

Installa l'estensione `Live Sass Compiler` di Ritwick Dey e apri i settaggi cercando live sass compiler e apriamo il file settings.json, a questo punto troviamo le impostazioni `liveSassCompile.settings.formats`. Qui impostiamo il save path come preferiamo.

# GitIgnore

Crea un file `.gitignore`:

```
node_modules/
public/
dist/
.env
.git
```

# Organizzazione file

Avrai un file `style.scss` o `main.scss` che importa i vari fogli di stile sass con `@use`:

```scss
@use 'abstract';
@use 'base';
@use 'utilities';
@use 'components';
@use 'layouts';
```

In `base` avrò il file di reset, font-face, typography e altre impostazioni di base
Nei `components` ci vado ad inserire i fogli di stile per i buttons, label, nav, article, ecc...
In `layout` ci inserisco le mie pagine come home, index, about, contact, courses, ecc...
I file `scss` all'interno di queste folder cominceranno sempre con un `_`: `_buttons.scss`.


# Video

https://www.youtube.com/watch?v=o4cECvhrBo8
https://www.youtube.com/watch?v=BEdCOvJ5RY4
https://www.youtube.com/watch?v=cM6UQxF9PSA

https://www.youtube.com/kepowob/videos