# Changes made by @lucho870601:

## Image dimention mixin

Added `sized-hidpi` mixin to supply the original image width and height as CSS properties. This is useful when you have background image on an empty element with no size `width:0; height:0`.

```scss
.icon_foo {
    @include sized-hidpi(icon_foo);
}
```


## Sized image definition

```scss
@include sized-hidpi-image(icon_foo);
```


## Easier building of retina sprites

Added support for easier building of retina sprites based on [Gist: Magically retinafy your sprites with Compass and HiDPI](https://gist.github.com/4160546).

```scss
@import "icons/*.png";
@import "icons_x2/*.png";
@include retina-sprites-support($icons-sprites, $icons_x2-sprites);
@include all-icons-sprites(true);
```

# Retinafy your website with Sass & Compass

`hidpi()` is a [Sass](http://sass-lang.com/ "Sass - Syntactically Awesome Stylesheets") mixin that seamlessly serves high resolution
background images to high density (Retina-like) displays. It comes with a
debug mode to test Retina graphics on a regular display.

**[Demonstration](http://www.kaelig.fr/hidpi/examples/ "HiDPI Examples")**

## How to Use It

[Download _hidpi.scss](https://raw.github.com/kaelig/hidpi/master/_hidpi.scss)
to your Sass project (preferably with [Compass](http://compass-style.org/ "Compass Home | Compass Documentation") enabled).

Import the partial in your Sass files:

```scss
@import 'hidpi';
```

Perfect, you can now use the mixin in your selectors.

### Passing Content to the Mixin

You can virtually pass anything to the mixin and it will be displayed on high
density displays.

In this example, the border color of the `#logo` element is:

- **red** on regular displays
- **blue** on HiDPI (Retina-like) displays

```scss
#logo {
  background: url('../images/logo.png') no-repeat;
  border: 1px solid blue;

  @include hidpi {
    background-image: url('../images/logo_x2.png');
    background-size: 250px 188px;
    border-color: red;
  }
}
```

Compiles to:

```css
#logo {
  background: url("../images/logo.png") no-repeat;
  border: 1px solid blue;
}
@media (-webkit-min-device-pixel-ratio: 1.3),
       (-o-min-device-pixel-ratio: 2.6/2),
       (min--moz-device-pixel-ratio: 1.3),
       (min-device-pixel-ratio: 1.3),
       (min-resolution: 1.3dppx) {
  #logo {
    background-image: url("../images/logo_x2.png");
    background-size: 250px 188px;
    border-color: red;
  }
}
```

### Image Only

When passing the name of an image as an argument, `hidpi()` serves the
equivalent high-resolution image on high-definition displays.

Image files should be named as follows, placed in the `images` folder
of your Compass project:

- `image.png`: default image
- `image_x2.png`: high-resolution image

```scss
#logo-auto {
  @include hidpi(logo);
}
```

Compiles to:

```css
#logo-auto {
  background-image: url('../images/logo.png');
}
@media (-webkit-min-device-pixel-ratio: 1.3),
       (-o-min-device-pixel-ratio: 2.6/2),
       (min--moz-device-pixel-ratio: 1.3),
       (min-device-pixel-ratio: 1.3),
       (min-resolution: 1.3dppx) {
  #logo-auto {
    background-image: url('../images/logo_x2.png');
    -webkit-background-size: 250px 188px;
    -moz-background-size: 250px 188px;
    -o-background-size: 250px 188px;
    background-size: 250px 188px;
  }
}
```

Note: this usage requires [Compass](http://compass-style.org/ "Compass Home | Compass Documentation").

### Debug Mode

You can force `hidpi()` to always serve high-resolution graphics and test
the rendering on a standard, non-Retina display.

Set the `$hidpi-debug` variable to `true`:

```scss
#logo-auto-debug {
  $hidpi-debug: true; // Force high-resolution graphics on standard displays
  @include hidpi(logo);
}
```

Compiles to:

```css
#logo-auto-debug {
  background-image: url('../images/logo_x2.png');
  -webkit-background-size: 250px 188px;
  -moz-background-size: 250px 188px;
  -o-background-size: 250px 188px;
  background-size: 250px 188px;
}
```

It loads `logo_x2.png` by default (no `@media` queries).

#### Non-PNG images

`hidpi(image)` is looking by default for `images/image.png`.

If your image is a JPEG, for example `image.jpg`, you should specify it as
a second argument:

```scss
#image-jpeg {
  @include hidpi(image, jpg);
}
```

Same story with a GIF:

```scss
#image-gif {
  @include hidpi(image, gif);
}
```

## Requirements

- Sass ~> 3.2 (for manual `@include hidpi {}`)
- Compass ~> 0.12.2 (for auto `@include hidpi(image);`)

Note: Compass is only needed when passing arguments to `hidpi()` instead of
a content-block.

## Also Read

- [Easy retina-ready images using SCSS by Jason Z. of 37signals](http://37signals.com/svn/posts/3271-easy-retina-ready-images-using-scss)
- [Retinafy your web sites and apps — ebook by Thomas Fuchs](http://retinafy.me/)

## More HiDPI examples and resources

- [Gist: Magically retinafy your sprites with Compass and HiDPI](https://gist.github.com/4160546)
- [Gist: Using Compass to generate normal and retina sprite maps](https://gist.github.com/2140082)
- [Compass mixins for dealing with HDPI (a.k.a. Retina) sprites and images in your CSS by @pierreburel](https://github.com/pierreburel/compass-hdpi)
- [A mixin for creating retina sprites with hover & active states by @AdamBrodzinski](https://github.com/AdamBrodzinski/Retina-Sprites-for-Compass)
- [Retina Sprites with Compass](https://github.com/Gaya/Retina-Sprites-for-Compass) — [Blog post](http://www.gayadesign.com/diy/retina-sprites-for-compass/)
