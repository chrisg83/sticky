# Sticky-icky

Sticky-icky is a jQuery plugin that gives you the ability to make any element on your page always stay visible to the user.

## Sticky-icky in brief was based a the 'Sticky JS' Concept  

The Sticky Js I used can be found here: http://stickyjs.com
The 'Icky' Update just expands on the orignal concept of one sticky element and allows you to have multiple.

This is how it works:

- When the target element is about to be hidden, the plugin will add the class `className` to it (and to a wrapper added as its parent), set the element to `position: fixed` and calculate its new `top`,this is the distance to the top of the page, it is also based on the element's height and the `topSpacing` and `bottomSpacing` options.
- That's it. 
In some cases you might need to set a fixed width to your element when it is "sticked".
But by default (`widthFromWrapper == true`) sticky updates elements's width to the wrapper's width.
Check the `example-*.html` files for some examples.

## Usage

- Include jQuery & Sticky.
- Call Sticky.

```html
<script src="jquery.js"></script>
<script src="jquery.sticky.js"></script>
<script>
  $(document).ready(function(){
    $("#sticker").sticky({topSpacing:0});
  });
</script>
```

## Add To Head
```html
<script src="http://YOUR-DOMAIN-HERE/wp-content/themes/YOUR-THEME-FOLDER-NAME-HERE/js/jquery.sticky.js"></script> <script>   jQuery(document).ready(function(){ jQuery("#sticker").sticky({topSpacing:200});
   });
</script>
```
Aside from getting the src link correct, the other important line of code in the snippet above is this one.
```html
jQuery("#sticker").sticky({topSpacing:0});
```
What this line of code means is that any element you give the css class “sticky” to or the css id “sticker” to will become a sticky element. I recommend you use the “sticker” css id so that the same snippet can be used for many elements with custom css styles for each.
If you want more than one element to be sticky all you need to do is add another line directly below the original with a different css id.
```html
jQuery("#sticker2").sticky({topSpacing:0});
```
With a few sticky elements added it will look like this.
```html
<script src="http://YOUR-DOMAIN-HERE/wp-content/themes/YOUR-THEME-FOLDER-NAME-HERE/js/jquery.sticky.js"></script>
<script>
(function($) {
    $(document).ready(function() {
        function becomeSticky(el, padding) {
            if (el.length) {
                el.sticky({
                    topSpacing: padding
                });
            }
        }
        becomeSticky($("#sticker2"), 150);
        becomeSticky($("#sticker3"), 100);
    });
})(jQuery);
</script>
```
You can also change the “topSpacing” value to be whatever you want. For instance, I found that “150” was ideal for my sidebar module. You can play with it to get the value that works best for you.

Next, assign the “sticker” css id (or “sticker2”, “sticker3”, etc.) to whatever module(s) or page element(s) you want to be sticky. And of course you are free to change “sticker”, “sticker2”, and “sticker3” to whatever words you want your css id’s to be. Such as “#left-sidebar” or “#right-sidebar” or “#sticky-optin” etc. Just so long as it’s the same in the snippet and your module/page element.

If you have more then 
- Edit your css to position the elements (check the examples in `example-*.html`).

## Unstick 
- To unstick an object

```html
<script>
  $("#sticker").unstick();
</script>
```

## Options

- `topSpacing`: (default: `0`) Pixels between the page top and the element's top.
- `bottomSpacing`: (default: `0`) Pixels between the page bottom and the element's bottom.
- `className`: (default: `'is-sticky'`) CSS class added to the element's wrapper when "sticked".
- `wrapperClassName`: (default: `'sticky-wrapper'`) CSS class added to the wrapper.
- `center`: (default: `false`) Boolean determining whether the sticky element should be horizontally centered in the page.
- `getWidthFrom`: (default: `''`) Selector of element referenced to set fixed width of "sticky" element.
- `widthFromWrapper`: (default: `true`) Boolean determining whether width of the "sticky" element should be updated to match the wrapper's width. Wrapper is a placeholder for "sticky" element while it is fixed (out of static elements flow), and its width depends on the context and CSS rules. Works only as long `getWidthForm` isn't set.
- `responsiveWidth`: (default: `false`) Boolean determining whether widths will be recalculated on window resize (using getWidthfrom).
- `zIndex`: (default: `inherit`) controls z-index of the sticked element.

## Methods

- `sticky(options)`: Initializer. `options` is optional.
- `sticky('update')`: Recalculates the element's position.

## Events

- `sticky-start`: When the element becomes sticky.
- `sticky-end`: When the element returns to its original location
- `sticky-update`: When the element is sticked but position must be updated for constraints reasons
- `sticky-bottom-reached`: When the element reached the bottom space limit
- `sticky-bottom-unreached`: When the element unreached the bottom space limit

To subscribe to events use jquery:

```html
<script>
  $('#sticker').on('sticky-start', function() { console.log("Started"); });
  $('#sticker').on('sticky-end', function() { console.log("Ended"); });
  $('#sticker').on('sticky-update', function() { console.log("Update"); });
  $('#sticker').on('sticky-bottom-reached', function() { console.log("Bottom reached"); });
  $('#sticker').on('sticky-bottom-unreached', function() { console.log("Bottom unreached"); });
</script>
```
