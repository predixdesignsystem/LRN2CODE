# Things to watch out for in the Polymer 2 upgrade

## Sass
Nesting will not work with the `:host` or `:slotted` pseudo-classes.

This won't work:
```
:host {
  &[full-bleed] .content {
    padding: 0;
  }
}
```
Do this instead:
```
:host([full-bleed]) .content {
  padding: 0;
}
```

## Import Paths
If you see 404s when loading local assets in Polymer 2.x:

`<img src="[[importPath]]monogram-wdmk.png"`
[see Polymer docs](https://www.polymer-project.org/2.0/docs/devguide/dom-template#urls-in-templates)

# Other stuff

## Flex in ie11

In most browsers, a item with `display: block` inside a flex container will automatically calculate its max width based on the size of its parent. However, in ie11, you need to explicitly set `width: 100%` so the item does not stretch beyond its parent container.

See [CodePen example](https://codepen.io/talimarcus/pen/zpKXpN). (Note: view the example in ie in order to see it not working.)

## dom-if and dom-repeat

You DO NOT need `<dom-if>` or `<dom-repeat>` wrappers inside a component template. You only need them if they're in the root of an HTML document, not managed by a Polymer template. If you're in a template the same old `<template is="dom-if">` etc. still work.

## Custom styles

Do NOT put `<custom style>` tags anywhere inside a web component. It breaks IE and will cause IE to dump all the theme styles (yay). `<custom-style>` tags are only ever needed outside a component (top level of a page etc.), never inside a component.
Same goes for `is="custom-style"`. Never needed inside a component template.

```<dom-module id="px-tile-demo">
  <template>
    <custom-style>
      <style is="custom-style">
```
^^ bad
```<dom-module id="px-tile-demo">
  <template>
    <custom-style>
      <style>
```
^^ also bad
```<dom-module id="px-tile-demo">
  <template>
      <style>
```
^^ good

## Async/await in a nutshell

```<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>

  </head>
  <body>
    <script>

      let moo = () => {
        return new Promise( (resolve) => {

          return setTimeout((res) => {
            console.log('here');
            return resolve('resolved');
          }, 2000);
        });
      }

      let baa = async () => {
        await moo();
        await moo();
        console.log('done');
      }

      baa();
    </script>
  </body>
</html>
```
will log:
``` 
here
here
done
```
without the `await` will long
```
done
here
here
```

(Note: does not work in IE)

# Compoennts

## Naming things

* `key` is a property used in React, so for easier integration, avoid just `key` as a Polymer property
* `title` attributes causes a browser tooltip in some browsers/OS
* `inert` is a new HTML spec attribute
