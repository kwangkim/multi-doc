# Moconti

## About
* Lightweight Sleep Script Web Application Server based on Sleep Script
 * based on NanoHTTPD (with a lot of modifications)
* Developer: Raphael Mudge
* Download: [here](http://sleep.dashnine.org/download/moconti.tgz)
* Architecture:
 * templates: templates (think PHP with Sleep)
 * app file: can hook into different URLs
 * static files
 * Session isolation: The server gives each client a  cookie and calls functions within their app environment. This means each user session looks like its own isolated thing.
 * These environments persist in memory but the server is smart enough to expire them or start dumping them really fast when memory gets low.
* details: docs/readme.txt
