```apacheconf
<IfModule mod_php7.c>
  php_flag display_errors Off
</IfModule>

# Don't list directories
<IfModule mod_autoindex.c>
  Options -Indexes
</IfModule>

Options -Indexes

<IfModule mod_deflate.c>
  AddOutputFilterByType DEFLATE text/html text/xml text/css text/plain text/x-component text/x-js text/richtext text/xsd text/xsl image/svg+xml application/xhtml+xml application/xml image/x-icon application/rdf+xml application/xml+rdf application/rss+xml application/xml+rss application/atom+xml application/xml+atom text/javascript application/javascript application/x-javascript application/json application/x-font-ttf application/x-font-otf font/truetype font/opentype

  <IfModule mod_headers.c>
    Header append Vary User-Agent env=!dont-vary
  </IfModule>

  <IfModule mod_mime.c>
    AddOutputFilter DEFLATE js css htm html xml
  </IfModule>
</IfModule>

<IfModule mod_expires.c>
  ExpiresActive On
  ExpiresDefault "access plus 31536000 seconds"
  ExpiresByType text/cache-manifest "access plus 0 seconds"

  ExpiresByType text/xml "access plus 60 minutes"
  ExpiresByType application/xml "access plus 60 minutes"
  ExpiresByType text/json "access plus 0 seconds"
  ExpiresByType application/json "access plus 0 seconds"

  ExpiresByType application/rss+xml "access plus 3600 seconds"
  ExpiresByType application/atom+xml "access plus 3600 seconds"

  ExpiresByType image/x-icon "access plus 31536000 seconds"

  ExpiresByType image/gif "access plus 31536000 seconds"
  ExpiresByType image/png "access plus 31536000 seconds"
  ExpiresByType image/jpeg "access plus 31536000 seconds"
  ExpiresByType image/jpg "access plus 31536000 seconds"
  ExpiresByType video/ogg "access plus 31536000 seconds"
  ExpiresByType audio/ogg "access plus 31536000 seconds"
  ExpiresByType video/mp4 "access plus 31536000 seconds"
  ExpiresByType video/webm "access plus 31536000 seconds"

  ExpiresByType text/x-component "access plus 31536000 seconds"

  ExpiresByType application/x-font-ttf "access plus 31536000 seconds"
  ExpiresByType font/opentype "access plus 31536000 seconds"
  ExpiresByType font/woff2 "access plus 31536000 seconds"
  ExpiresByType application/x-font-woff "access plus 31536000 seconds"
  ExpiresByType image/svg+xml "access plus 31536000 seconds"
  ExpiresByType application/vnd.ms-fontobject "access plus 31536000 seconds"

  ExpiresByType text/css "access plus 31536000 seconds"
  ExpiresByType application/javascript "access plus 31536000 seconds"
  ExpiresByType text/javascript "access plus 31536000 seconds"
  ExpiresByType application/javascript "access plus 31536000 seconds"
  ExpiresByType application/x-javascript "access plus 31536000 seconds"

  ExpiresByType application/x-shockwave-flash "access plus 31536000 seconds"
  ExpiresByType application/octet-stream "access plus 31536000 seconds"
</IfModule>

<IfModule mod_headers.c>
  <filesMatch "\.(ico|jpe?g|png|gif|swf)$">
    Header set Cache-Control "public, max-age=31536000, s-maxage=31536000"
    Header set Pragma "public"
  </filesMatch>

  <filesMatch "\.(css|js|ttf|ttc|otf|eot|woff|woff2|font.css|css)$">
    Header set Cache-Control "public, max-age=31536000, s-maxage=31536000"
    Header set Pragma "public"
  </filesMatch>

  <filesMatch "\.(ttf|ttc|otf|eot|woff|woff2|font.css|css|xml)$">
    Header set Access-Control-Allow-Origin "*"
  </filesMatch>

  # Canoncial link config
  <FilesMatch "\.(jpg|jpeg|gif|png|ico|svg|bmp|pict|tif|tiff|webp|eps|svgz|css|js|ejs|ttf|woff2|woff|eot|otf|wav|ogg|mp3|wma|mid|midi|rm|ram|aac|m4a|pls|mpg|mpeg|avi|wmv|mov|webm|mp4|m4v|ogv|flv|swf|pdf|csv|doc|ppt|docx|xlsx|xls|pptx|ps|class|jar)(\.gz)?(\?.*)?$">
    Header set Link "<%{CANONICAL}e>; rel=\"canonical\""
  </FilesMatch>

  # Header cache control
  <filesMatch "\.(ico|jpe?g|png|gif|swf)$">
    Header set Cache-Control "public"
  </filesMatch>

  <filesMatch "\.(css)$">
    Header set Cache-Control "public"
  </filesMatch>

  <filesMatch "\.(js)$">
    Header set Cache-Control "private"
  </filesMatch>

  <filesMatch "\.(x?html?|php)$">
    Header set Cache-Control "private, must-revalidate"
  </filesMatch>
</IfModule>

<IfModule mod_rewrite.c>
  RewriteEngine On
  RewriteBase /
  AddDefaultCharset UTF-8

  RewriteCond %{REQUEST_URI} !^.*//.*$
  RewriteCond %{QUERY_STRING} !^.*(s\=|submit\=|wp\-admin|wp\-content|wp\-includes|\.php|/cart/|/my\-account/|/checkout/|/addons/|add\-to\-cart\=).*$
  RewriteCond %{REQUEST_URI} !^.*(s\=|submit\=|wp\-admin|wp\-content|wp\-includes|\.php|/cart/|/my\-account/|/checkout/|/addons/|add\-to\-cart\=).*$
  RewriteCond %{REQUEST_METHOD} GET
  RewriteCond %{QUERY_STRING} !.*=.*
  RewriteCond %{HTTP:Cookie} !^.*(comment_author|wp\-postpass|wptouch_switch_toggle|wordpress_logged_in|woocommerce_cart_).*$
  RewriteCond %{HTTPS} !on
  RewriteCond %{DOCUMENT_ROOT}/wp-content/pep-vn/cache/request-uri/data/%{SERVER_NAME}/$1/index-sw_.html -f
  RewriteRule ^(.*) "/wp-content/pep-vn/cache/request-uri/data/%{SERVER_NAME}/$1/index-sw_.html" [L]

  RewriteCond %{REQUEST_URI} !^.*//.*$
  RewriteCond %{QUERY_STRING} !^.*(s\=|submit\=|wp\-admin|wp\-content|wp\-includes|\.php|/cart/|/my\-account/|/checkout/|/addons/|add\-to\-cart\=).*$
  RewriteCond %{REQUEST_URI} !^.*(s\=|submit\=|wp\-admin|wp\-content|wp\-includes|\.php|/cart/|/my\-account/|/checkout/|/addons/|add\-to\-cart\=).*$
  RewriteCond %{REQUEST_METHOD} GET
  RewriteCond %{QUERY_STRING} !.*=.*
  RewriteCond %{HTTP:Cookie} !^.*(comment_author|wp\-postpass|wptouch_switch_toggle|wordpress_logged_in|woocommerce_cart_).*$
  RewriteCond %{HTTPS} on
  RewriteCond %{DOCUMENT_ROOT}/wp-content/pep-vn/cache/request-uri/data/%{SERVER_NAME}/$1/index-https-sw_.html -f
  RewriteRule ^(.*) "/wp-content/pep-vn/cache/request-uri/data/%{SERVER_NAME}/$1/index-https-sw_.html" [L]

  RewriteCond %{REQUEST_URI} !^.*//.*$
  RewriteCond %{QUERY_STRING} !^.*(s\=|submit\=|wp\-admin|wp\-content|wp\-includes|\.php|/cart/|/my\-account/|/checkout/|/addons/|add\-to\-cart\=).*$
  RewriteCond %{REQUEST_URI} !^.*(s\=|submit\=|wp\-admin|wp\-content|wp\-includes|\.php|/cart/|/my\-account/|/checkout/|/addons/|add\-to\-cart\=).*$
  RewriteCond %{REQUEST_URI} !^.*(wp-includes|wp-content|wp-admin|\.php).*$
  RewriteCond %{REQUEST_METHOD} GET
  RewriteCond %{QUERY_STRING} !.*=.*
  RewriteCond %{HTTP:Cookie} !^.*(comment_author|wp\-postpass|wptouch_switch_toggle|wordpress_logged_in|woocommerce_cart_).*$
  RewriteCond %{HTTPS} !on
  RewriteCond %{DOCUMENT_ROOT}/wp-content/pep-vn/cache/request-uri/data/%{SERVER_NAME}/$1/index.xml -f
  RewriteRule ^(.*) "/wp-content/pep-vn/cache/request-uri/data/%{SERVER_NAME}/$1/index.xml" [L]

  RewriteCond %{REQUEST_URI} !^.*//.*$
  RewriteCond %{QUERY_STRING} !^.*(s\=|submit\=|wp\-admin|wp\-content|wp\-includes|\.php|/cart/|/my\-account/|/checkout/|/addons/|add\-to\-cart\=).*$
  RewriteCond %{REQUEST_URI} !^.*(s\=|submit\=|wp\-admin|wp\-content|wp\-includes|\.php|/cart/|/my\-account/|/checkout/|/addons/|add\-to\-cart\=).*$
  RewriteCond %{REQUEST_URI} !^.*(wp-includes|wp-content|wp-admin|\.php).*$
  RewriteCond %{REQUEST_METHOD} GET
  RewriteCond %{QUERY_STRING} !.*=.*
  RewriteCond %{HTTP:Cookie} !^.*(comment_author|wp\-postpass|wptouch_switch_toggle|wordpress_logged_in|woocommerce_cart_).*$
  RewriteCond %{HTTP:Accept-Encoding} gzip
  RewriteCond %{HTTPS} on
  RewriteCond %{DOCUMENT_ROOT}/wp-content/pep-vn/cache/request-uri/data/%{SERVER_NAME}/$1/index-https.xml -f
  RewriteRule ^(.*) "/wp-content/pep-vn/cache/request-uri/data/%{SERVER_NAME}/$1/index-https.xml" [L]

  RewriteRule ^index\.php$ - [L]
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteRule . /index.php [L]
</IfModule>

Header unset ETag
FileETag None
```