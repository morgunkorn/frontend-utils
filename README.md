# Frontend-Utils
A collection of snippets to make the life of a Frontender easier

#### LESS

* Responsive font-size: [fluid-font](#fluid-font)
* Beautiful transparent CSS gradients: [scrim-gradient](#scrim-gradient)

## LESS Mixins

### Fluid Font

This LESS mixin defines a minimal and maximal font-size between 2 or more viewport widths (breakpoints).

When used with 2 breakpoints, the minimal font size is defined under the first breakpoint, and the maximal font-size above the second breakpoint. Between the two breakpoints, the font-size will proportionally increase (or decrease), from the minimum to the maximum.

When used with 3 or more breakpoints, the font-size is reset to the minimal at every breakpoint (except the last) and grows up to the maximal font-size right before the next breakpoint.

You can use `px`, `em` or `rem` in the parameters.

* If you use `px`, the breakpoint values will also have to be in `px`. 
* If you use `em` or `rem`, you can mix those units. 

Source: [fluid-font.less](css/fluid-font.less)

#### .fluid-font examples

**Example A:** 2 breakpoints, uniform rate of growth

```less
/* Input */
.selector {
  .fluid-font(1em, 2em, 30em, 60em);
}

/* Output */
.selector {
  font-size: 1em;
}
@media (min-width: 30em) and (max-width: 59.999em) {
  .selector {
    font-size: 3.333vw;
  }
}
@media (min-width: 60em) {
  .selector {
    font-size: 2em;
  }
}
```

**Example B:** 3 breakpoints, variable rate of growth

```less
/* Input */
.selector {
    .fluid-font(1em, 1.5em, 20em, 48em, 64em);
}

/* Output */
.selector {
  font-size: 1em;
}
@media (min-width: 20em) and (max-width: 47.999em) {
  .selector {
    font-size: calc(0.643em + 1.786vw);
  }
}
@media (min-width: 48em) and (max-width: 63.999em) {
  .selector {
    font-size: calc(-0.5em + 3.125vw);
  }
}
@media (min-width: 64em) {
  .selector {
    font-size: 1.5em;
  }
}
```

* * *

### Scrim Gradient

The standard css `linear-gradient()` function generates a gradient with hard edges, which can potentially look bad when compared to the original design.

This LESS mixin creates a CSS Gradient from any color (also partially transparent) to full transparency that looks more natural, similar to what you obtain in Photoshop, for example.

Source: [scrim-gradient.less](css/scrim-gradient.less)

#### .scrim-gradient examples

**Example A:** call with standard values, from top to bottom, black 70% opacity to 0% opacity.

```less
/* Input */
.selector {
    .scrim-gradient();
}

/* Output */
.selector{
  background: linear-gradient( 
    to bottom, 
    rgba(0, 0, 0, 0.5) 1%, 
    rgba(0, 0, 0, 0.369) 19%, 
    rgba(0, 0, 0, 0.2705) 34%, 
    rgba(0, 0, 0, 0.191) 47%, 
    rgba(0, 0, 0, 0.139) 56.5%, 
    rgba(0, 0, 0, 0.097) 65%, 
    rgba(0, 0, 0, 0.063) 73%, 
    rgba(0, 0, 0, 0.0375) 80.2%, 
    rgba(0, 0, 0, 0.021) 86.1%, 
    rgba(0, 0, 0, 0.0105) 91%, 
    rgba(0, 0, 0, 0.004) 95.2%, 
    rgba(0, 0, 0, 0.001) 98.2%, 
    rgba(0, 0, 0, 0)  100% 
  );
}
```

**Example B:** sideways gradient from half transparent red to transparent.

```less
/* Input */
.selector{
  .scrim-gradient( to left, fade(red, 50%) );
}

/* Output */
.selector{
  background: linear-gradient( 
    to left, 
    rgba(255, 0, 0, 0.5) 1%, 
    rgba(255, 0, 0, 0.369) 19%, 
    rgba(255, 0, 0, 0.2705) 34%, 
    rgba(255, 0, 0, 0.191) 47%, 
    rgba(255, 0, 0, 0.139) 56.5%, 
    rgba(255, 0, 0, 0.097) 65%, 
    rgba(255, 0, 0, 0.063) 73%, 
    rgba(255, 0, 0, 0.0375) 80.2%, 
    rgba(255, 0, 0, 0.021) 86.1%, 
    rgba(255, 0, 0, 0.0105) 91%, 
    rgba(255, 0, 0, 0.004) 95.2%, 
    rgba(255, 0, 0, 0.001) 98.2%, 
    rgba(255, 0, 0, 0)  100% 
  );
}
```