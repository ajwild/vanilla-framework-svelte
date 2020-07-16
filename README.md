# vanilla-framework-svelte

A quick test to see if the Vanilla CSS framework will play nicely with Svelte in a modular way.

## Size

The table below shows the (minified and gzipped) size of a completely empty app, versus an app which
only contains the contextual menu from the example. Realistically, the JS would be a similar size if
you were to write the component yourself in Svelte. The main difference is the additional CSS. The
first component added includes the base styles of vanilla-framework, including normalize,
typography, buttons etc. Adding additional components will not duplicate this, so the CSS size
should not grow too quickly.

|                            | **JS**       | **CSS**      |
|----------------------------|-------------:|-------------:|
| **App w/ no content**      |  1,135 bytes |     70 bytes |
| **App w/ contextual menu** |  3,204 bytes |  7,793 bytes |
|                            |              |              |
| **Change**                 | +2,069 bytes | +7,723 bytes |

Note: This will also include the Ubuntu font - hopefully this can be remove with SASS/CSS variables.

## Viewing the example

See [./example/README.md](./example/README.md).

## Adding to an existing project

### Install package

```bash
npm install --save-dev git://github.com/ajwild/vanilla-framework-svelte.git#master
```

### Install postcss

```bash
npm install --save-dev node-sass rollup-plugin-postcss
```

### Update rollup.config.js

```js
 import livereload from 'rollup-plugin-livereload';
 import { terser } from 'rollup-plugin-terser';
+import postcss from 'rollup-plugin-postcss';
 
 const production = !process.env.ROLLUP_WATCH;
```

```js
     commonjs(),
 
+    postcss({
+      extract: true,
+      minimize: true,
+      use: [
+        [
+          'sass',
+          {
+            includePaths: ['./node_modules'],
+          },
+        ],
+      ],
+    }),
+
     // In dev mode, call `npm run start` once
     // the bundle has been generated
     !production && serve(),
```

### Use component

```html
<script>
  import {
    ContextualMenu,
    ContextualMenuContent,
    ContextualMenuGroup,
    ContextualMenuItem,
    ContextualMenuTrigger
  } from "vanilla-framework-svelte";
</script>

<ContextualMenu let:active>
  <ContextualMenuTrigger {active} />
  <ContextualMenuContent {active}>
    <ContextualMenuGroup>
      <ContextualMenuItem>Item one</ContextualMenuItem>
      <ContextualMenuItem>Item two</ContextualMenuItem>
      <ContextualMenuItem>Item three</ContextualMenuItem>
    </ContextualMenuGroup>
    <ContextualMenuGroup>
      <ContextualMenuItem>Another item</ContextualMenuItem>
    </ContextualMenuGroup>
  </ContextualMenuContent>
</ContextualMenu>
```
