Shoelace makes extensive use of CSS Custom Properties, or "CSS variables." As a result, you can load the entire library via CDN and customize it by overriding the necessary variables in your own stylesheet. **You don't need to build Shoelace from source, nor do you need to use a preprocessor to customize it.**

Each theme defines the core **theme variables**. Theme variables aren't component-specific; rather they define a set of design tokens that each component uses as a basis for its own styles.

For example, `--sl-form-control-font-family` is a base variable that is used by a number of form controls, including `<sl-button>` and `<sl-input>`. Therefore, you can override `--sl-form-control-font-family` to adjust the font for all buttons, inputs, et al.

```css
:root {
  --sl-form-control-font-family: 'Open Sans', sans-serif;
  --sl-form-control-color: black;
}
```

Alternatively, you can override the button's `--sl-font-family` variable to adjust the font only for buttons.

```css
sl-button {
  --sl-font-family: '', sans-serif;
  --color: white;
}
```

Astute readers might be wondering why the button variables aren't located in the same `:root` selector as the theme variables — or why they don't use any sort of prefix. This is because theme variables are defined at the `:root` level, whereas component variables are defined at the `:host` level (e.g. `<sl-button>`). This design decision provides us with a few helpful benefits:

- It's impossible to reuse component variables in other components. This is a good thing, as it prevents changes in one component's styles from inadvertently affecting another. (As a rule of thumb, if a style _really_ needs to be shared between components, it should be promoted to a theme variable.)

- It's easier to document and manage component-specific variables when they live with their components, and customizing the library becomes easier as you don't have to sift through an exhaustive list of variables to find the ones you need (i.e. variable hell).

- Component-specific overrides are very explicit in your stylesheet. There's no question as to which overrides affect which components.

- Theme files remain small since they consist only of theme variables (and potentially a handful of component-specific overrides depending on the designer's intent).

## Shadow DOM

Most Shoelace components use a Shadow DOM with the exception of form controls. This is for your convenience, since form controls inside a shadow DOM aren't submitted with standard HTML forms. In the future, when StencilJS and browsers add support for [Form-associated Custom Elements](https://html.spec.whatwg.org/multipage/custom-elements.html#custom-elements-face-example), it would be nice if all components can use a Shadow DOM.