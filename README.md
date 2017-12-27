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
