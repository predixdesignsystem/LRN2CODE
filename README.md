# Things to watch out for in the Polymer 2 upgrade

## WCT
If you see an error thrown by Firefox outside of the test function `document.getElementById(...).create is not a function`, try changing your test-fixture `id` from dash-case to camelCase (no idea why this works ¯\\_(ツ)_/¯ ).

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
