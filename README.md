# vanilla-framework-svelte

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

```js
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
