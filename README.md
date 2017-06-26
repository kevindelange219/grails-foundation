# Grails foundation-sites plugin
Foundation for Sites for Grails projects

Include [ZURB Foundation for Sites](http://foundation.zurb.com/) and [Motion UI](http://zurb.com/playground/motion-ui) in a Grails 2.x project, directly usable with the ```sass-asset-pipeline``` plugin.

## Prerequisites

The asset-pipeline must be configured with the [sass-asset-pipeline](https://github.com/bertramdev/asset-pipeline/tree/master/sass-asset-pipeline) plugin to compile the Foundation SCSS.
Foundation 6 supports the latest ```sass-asset-pipeline``` based on jsass, but in this case Java 8 is required. Older ```JRuby``` based plugins should also work.

## Installation

Install by adding the plugin to ```BuildConfig.groovy```:

```groovy
plugins {
  // plugins for the compile step
  /* other plugins */
  compile ":foundation-sites:6.3.1.1"
}
```

To support compilation of ES6 used in Foundation, for partial includes, you must add the following to ```Config.groovy```:

```groovy
grails {
    assets {
        minifyOptions = [languageMode: 'ES6', targetLanguage: 'ES5']
    }
}
```

## Usage

### Foundation template
The plugin includes a ```foundation``` template which includes all dependencies on Foundation.

```html
<meta name="layout" content="foundation">
```

If you want to use the default Foundation styling, this is all you need. By default all components are included.
For Motion UI the [default CSS](https://github.com/zurb/motion-ui/blob/master/docs/classes.md) and JavaScript is included.

### Manual include

If you do not wish to include everything, you can include parts of the plugin manually:

```
<asset:stylesheet src="vendor/foundation-sites/assets/foundation.css"/>
<asset:javascript src="vendor/jquery/dist/jquery.min.js"/>
<asset:javascript src="vendor/what-input/dist/what-input.min.js"/>
<asset:javascript src="vendor/foundation-sites/dist/js/foundation.min.js"/>
<asset:stylesheet src="vendor/motion-ui/dist/motion-ui.min.css"/>
<asset:javascript src="vendor/motion-ui/dist/motion-ui.min.js"/>
```

Instead of including ```<asset:javascript src="vendor/foundation-sites/dist/js/foundation.min.js"/>``` you can also just import the components you need:
```
<asset:javascript src="foundation.abide.js"/>
<asset:javascript src="foundation.core.js"/>
```

Full list:
```
<asset:javascript src="foundation.abide.js"/>
<asset:javascript src="foundation.accordion.js"/>
<asset:javascript src="foundation.accordionMenu.js"/>
<asset:javascript src="foundation.core.js"/>
<asset:javascript src="foundation.drilldown.js"/>
<asset:javascript src="foundation.dropdown.js"/>
<asset:javascript src="foundation.dropdownMenu.js"/>
<asset:javascript src="foundation.equalizer.js"/>
<asset:javascript src="foundation.interchange.js"/>
<asset:javascript src="foundation.foundation.magellan.js"/>
<asset:javascript src="foundation.foundation.offcanvas.js"/>
<asset:javascript src="foundation.foundation.orbit.js"/>
<asset:javascript src="foundation.foundation.responsiveMenu.js"/>
<asset:javascript src="foundation.foundation.responsiveToggle.js"/>
<asset:javascript src="foundation.foundation.reveal.js"/>
<asset:javascript src="foundation.foundation.slider.js"/>
<asset:javascript src="foundation.foundation.sticky.js"/>
<asset:javascript src="foundation.foundation.tabs.js"/>
<asset:javascript src="foundation.foundation.toggler.js"/>
<asset:javascript src="foundation.foundation.tooltip.js"/>
<asset:javascript src="foundation.foundation.util.box.js"/>
<asset:javascript src="foundation.foundation.util.keyboard.js"/>
<asset:javascript src="foundation.foundation.util.mediaQuery.js"/>
<asset:javascript src="foundation.foundation.util.motion.js"/>
<asset:javascript src="foundation.foundation.util.nest.js"/>
<asset:javascript src="foundation.foundation.util.timerAndImageLoader.js"/>
<asset:javascript src="foundation.foundation.util.touch.js"/>
<asset:javascript src="foundation.foundation.util.triggers.js"/>
<asset:javascript src="foundation.foundation.zf.responsiveAccordionTabs.js"/>
```


If you use the JavaScript components, then ```jQuery``` is required. The dependency ```what-input``` is optional, but recommended for better accessibility.
You also should initialize the components just before closing the body:

```
<script>
    $(document).foundation();
</script>
```

Additionally, you can also turn off components in the scss files by customizing some of the scss files

To install these files in your local project, run the script:

```
grails foundation-configurable
```

The files will be copied to:

```
grails-app/assets/stylesheets/vendor/foundation-sites/assets/foundation.scss
grails-app/assets/stylesheets/vendor/foundation-sites/scss/foundation.scss
grails-app/assets/stylesheets/vendor/foundation-sites/scss/settings/_settings.scss
```

** In foundation-sites/assets/foundation.scss **
Here is the mixin executed which loads foundation components. If you run this mixin with a true parameter, foundation will make use of the flexbox grid. like: ```@include foundation-everything(true);``` instead of ```@include foundation-everything;```

** In  stylesheets/vendor/foundation-sites/scss/foundation.scss **
Here you can set which component needs to be included in the mixin.

** In  stylesheets/vendor/foundation-sites/scss/settings/_settings.scss **
Here you can adjust foundation settings, by setting a primary and secondary color for instance.

Modify these files in your local project to customize any settings.

For more information, see the [Foundation for Sites documentation](http://foundation.zurb.com/sites/docs/javascript.html).

## Versioning

The plugin follows the same versioning as Foundation, but may append a "patch" version for patches to the plugin unrelated to Foundation upgrades.

## Release history

|version|date|notes|
|---|---|---|
|6.3.1.1|2017-06-23|Fixed release, include assets.|
|6.3.1|2017-05-02|Broken initial release. Missing assets.|
