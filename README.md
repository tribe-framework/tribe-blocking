# tribe-blocking
Prerendering engine / middleware for Ember based front-end apps within projects built on the Tribe framework.

## Why the name "blocking"?
https://en.wikipedia.org/wiki/Blocking_(stage)

## Initial concept note
Every front-end app can have a "blocking engine".
The blocking engine can do things like:
- generate metatags for opengraph, twitter and SEO
- generate JSON-LD
- noindex, nofollow instructions
- handle sitemap.xml
- show the loading spinner
- preload analytics javascript code
- generate screenshots
- show text content before the front-end app has loaded

## Architecture
1. Ember apps will be rendered on the same machine as where their backend tribe is saved.
2. After we "ember build" and generate the dist folder, the blocking code will reconfigure Ember's dist folder. It will replace index.html with index.php and inject sitemap.php using - [app-deploy.sh](https://github.com/tribe-framework/tribe/blob/master/install/app-deploy.sh)
3. The domain name setup, certbot installation and NGINX configuration for the index.php and sitemap.xml (alias for sitemap.php) will be handled by [app-config.sh](https://github.com/tribe-framework/tribe/blob/master/install/app-config.sh)
4. The index.php file will have six hook files - _metatags.php, _jsonld.php, _analytics.php, _loading.php, _content.php and _screenshots.php
5. The blocking engine will be completely JSON based, will not require database queries.
6. Junction will be used to create, update and delete JSON files in uploads folder. Saving a public object will automatically render a JSON and PNG. Making a post private or draft or deleting it in Junction will delete the JSON and PNG.
7. Rendered object-wise JSON will be located at uploads/blocking/type-slug/object-slug.json and uploads/blocking/type-slug/object-slug.png
8. The metatags and JSON-LD info for the homepage and archive pages will be generated using types.json
