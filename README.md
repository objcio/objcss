# objcss
Shared CSS for objc.io sites

This documentation is a work-in-progress.

# CSS

## Utilities

### Spacing

Basic directional spacing is in the form of `[rule][direction][multiplier]`.

`[rule]`:
* `m`: margin
* `p`: padding

`[direction]`:
* _(blank)_: all directions
* `t`: top
* `r`: right
* `b`: bottom
* `l`: left
* `h` (horizontal): left & right
* `v` (vertical): top & bottom

`[variant]`:
* _(blank)_: 1em
* `+`: 1.5em
* `++`: 2.5em
* `-`: 0.5em
* `--`: 0.25em
* `---`: 0.15em
* `0`: 0em

_These are current-as-of-writing values, but can be changed in `_settings.scss`_

#### Examples:

```
mt
m+
pv-
ph++
mb0
```

### Negative Spacing

Basic negative directional **margin** is in the form of `n-m[direction][multiplier]`.  
These work as positive spacing, but only for margin and a subset of directions and multipliers, as such:

`[direction]`:
* `t`: top
* `r`: right
* `b`: bottom
* `l`: left

`[variant]`:
* _(blank)_: 1em
* `+`: 1.5em
* `++`: 2.5em

#### Examples:

```
n-mt
n-mb+
n-ml--
```

### Stack

The `stack` utility is applied to an element to **vertically space its children** from one another.  This is useful to space a sequence of list of similar elements, like lists of episodes, books, comments, etc.

The utility is in the form of `stack[variant]`, using the site-wide spacing variants as defined in `_settings.scss`, and works but applying top margin to each each children in the stack except the first. It is defined as simply as:

```scss
.stack{$variant} > + * + {
  margin-top: $variant-value;
}
```

#### Example:
```html
<ul class="stack+">
  <li>...</li>
  <li>...</li>
  ...
</ul>
```
