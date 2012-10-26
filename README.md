# Sass HiDPI

Sass HiDPI is a Sass mixin that helps you seamlessly serve high resolution 
graphics for high density displays.

## How to use it

[Download _hidpi.scss](https://raw.github.com/Kaelig/sass-hidpi/master/_hidpi.scss)
and put it in your compass project.

Import the partial in your Sass files:

```scss
@import 'hidpi';
```

Perfect, you can now use the mixin in your selectors:

```scss
/* Example: Logo */
#logo {
  background: url('../images/logo.png') no-repeat;

  // Manually include graphics and background-size
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

### Debug mode

You can force the high resolution mode:

```scss
#logo-auto-debug {
  $hidpi-debug: true; // Force high-res mode
  @include hidpi(logo);
}
```

Will output:

```css
#logo-auto-debug {
  background-image: url('../images/logo_x2.png');
  -webkit-background-size: 250px 188px;
  -moz-background-size: 250px 188px;
  -o-background-size: 250px 188px;
  background-size: 250px 188px;
}
```

It's particularly handy when debugging on a regular monitor.

## Requirements

To use Sass HiDPI, you need:

- Sass 3.2+
- Compass

Images should follow these naming conventions:

- `image.png # default`
- `image_x2.png # High DPI`

## Also read

- [Easy retina-ready images using SCSS by Jason Z. of 37signals](http://37signals.com/svn/posts/3271-easy-retina-ready-images-using-scss)
- [Retinafy your web sites and apps — ebook by Thomas Fuchs](http://retinafy.me/)