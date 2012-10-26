# Sass HiDPI

`hidpi()` is a Sass mixin that seamlessly serves high resolution
background images to high density (Retina-like) displays.

## How to Use It

[Download _hidpi.scss](https://raw.github.com/Kaelig/sass-hidpi/master/_hidpi.scss)
to your Compass project.

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
    background-size: 100px 30px;
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
@media (-webkit-min-device-pixel-ratio: 1.3), (-o-min-device-pixel-ratio: 2.6 / 2), (min--moz-device-pixel-ratio: 1.3), (min-device-pixel-ratio: 1.3) {
  #logo {
    background-image: url("../images/logo_x2.png");
    background-size: 100px 30px;
  }
}

@media (-webkit-min-device-pixel-ratio: 1.3), (-o-min-device-pixel-ratio: 2.6 / 2), (min--moz-device-pixel-ratio: 1.3), (min-device-pixel-ratio: 1.3) {
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

You can force `hidpi()` to output high resolution graphics to always serve
high-definition images and test rendering on a regular display.

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

## Requirements

To use Sass HiDPI, you need:

- Sass ~> 3.2
- Compass ~> 0.12.2

Image files should follow these naming conventions:

- `image.png # default`
- `image_x2.png # High DPI`

## Also Read

- [Easy retina-ready images using SCSS by Jason Z. of 37signals](http://37signals.com/svn/posts/3271-easy-retina-ready-images-using-scss)
- [Retinafy your web sites and apps — ebook by Thomas Fuchs](http://retinafy.me/)