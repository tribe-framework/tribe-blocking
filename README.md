# tribe-blocking
Prerendering engine / middleware for Ember based front-end apps within projects built on the Tribe framework.

## Why the name "blocking"?
https://en.wikipedia.org/wiki/Blocking_(stage)

## Initial concept note
Every front-end app can have a blocking engine.
The blocking engine can do things like:
- generate metatags for opengraph, twitter and SEO
- generate JSON-LD
- noindex, nofollow instructions
- handle sitemap.xml
- show the loading spinner
- preload analytics javascript code
- generate screenshots
- show content before the front-end app has loaded

## Architecture
1. In Ember's public folder, following 6 php hook files will be placed - _metatags.php, _header.php, _analytics.php, _loading.php, _screenshots.php and _footer.php
3. Ember's index.html will be replaced by index.php (which will have the 6 hooks), via NGINX configuration
4. NGINX will be configured to handle sitemap.xml via public/php/sitemap.php
5. The blocking engine is completely JSON based, does not require database queries.
6. Junction will be used to create, update and delete JSON files in uploads folder. Saving a public object will automatically render a JSON and PNG. Making a post private or draft or deleting it in Junction will delete the JSON and PNG.
7. Rendered files will be located at uploads/blocking/<type>/<slug>.json and .png
