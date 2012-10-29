# HiDPI for Sass & Compass

`hidpi()` is a Sass mixin that seamlessly serves high resolution
background images to high density (Retina-like) displays.

**[View examples](http://www.kaelig.fr/hidpi/examples/ "HiDPI Examples")**

## How to Use It

[Download _hidpi.scss](https://raw.github.com/kaelig/hidpi/master/_hidpi.scss)
to your Sass or Compass project.

Import the partial in your Sass files:

```scss
@import 'hidpi';
```

Perfect, you can now use the mixin in your selectors:

```scss
#logo {
  background: url('../images/logo.png') no-repeat;

  // Manually include high resolution graphics and background-size
  @include hidpi {
    background-image: url('../images/logo_x2.png');
    background-size: 250px 188px;
  }
}

#logo-auto {
  // Or let Compass do the magic
  @include hidpi(logo);
}
```

Will output:

```css
#logo {
  background: url("../images/logo.png") no-repeat;
}
@media (-webkit-min-device-pixel-ratio: 1.3),
       (-o-min-device-pixel-ratio: 2.6/2),
       (min--moz-device-pixel-ratio: 1.3),
       (min-device-pixel-ratio: 1.3),
       (min-resolution: 1.3dppx) {
  #logo {
    background-image: url("../images/logo_x2.png");
    background-size: 250px 188px;
  }
}

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

### Debug Mode

You can force `hidpi()` to always serve high-definition graphics and test
the rendering on a regular display.

Set the `$hidpi-debug` variable to `true`:

```scss
#logo-auto-debug {
  $hidpi-debug: true; // Force high-res mode
  @include hidpi(logo);
}
```

It will then load `logo_x2.png` by default (no `@media` queries):

```css
#logo-auto-debug {
  background-image: url('../images/logo_x2.png');
  -webkit-background-size: 250px 188px;
  -moz-background-size: 250px 188px;
  -o-background-size: 250px 188px;
  background-size: 250px 188px;
}
```

### Non-PNG images

`hidpi(image)` is looking by default for `images/image.png`.

If your image is a JPEG, for example `image.jpg`, you should specify it as
a second argument:

```scss
#image-jpeg {
  @include(image, jpg);
}
```

Same story with a GIF:

```scss
#image-gif {
  @include(image, gif);
}
```

## Requirements

To use Sass HiDPI, you need:

- Sass ~> 3.2 (for manual `@include`)
- Compass ~> 0.12.2 (for auto `@include(image);`)

Image files should follow these naming conventions:

- `image.png # default`
- `image_x2.png # High DPI`

## Also Read

- [Easy retina-ready images using SCSS by Jason Z. of 37signals](http://37signals.com/svn/posts/3271-easy-retina-ready-images-using-scss)
- [Retinafy your web sites and apps — ebook by Thomas Fuchs](http://retinafy.me/)