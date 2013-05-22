# Changelog

## 2.0.0 (2013-05-08)

- Postfix (`_x2` at the end of filenames) is configurable (thanks to @sxtxixtxcxh) - #3
- Device pixel ratio is configurable (default: `1.3`)
- Better inline documentation directly in `_hidpi.scss`
- Lighter output:
    - `@media` query updated, inspired by @bjankord's [research on the matter](http://www.brettjankord.com/2012/11/28/cross-browser-retinahigh-resolution-media-queries/ "Brett Jankord  &#8211; Cross Browser Retina/High Resolution Media Queries").
    - Use `background-size` standard notation since all targeted devices [support it](http://caniuse.com/background-img-opts "Can I use CSS3 Background-image options").
- Ready to be installable as a [Bower](http://bower.io/ "BOWER: A package manager for the web") package: `bower install sass-hidpi`
- License mentions contributors

## 1.0.0 (2012-10-26)

- Initial release
