Explanation:


•	In the code Main server block listens on port 80 and defines domain name, Sets up access logging to custom log format  
•	  location ~* \.(css|jpg|jpeg|js|json|png|mp4|pdf)$ {
        return 404;

Uses a location block with a regular expression (~* .()) to match requests that end with css, jpg, jpeg, js, json, png, mp4, or pdf. For any matching request, it will immediately return a 404 Not Found response.

•	Used Location/block proxies requests to an upstream backend and added security headers

X-Content-Type-Options: nosniff: Prevents browsers from MIME-sniffing response content and forces them to use the returned Content-Type header. Protects against certain types of attacks.
X-Frame-Options: SAMEORIGIN: Restricts who can put the site in a frame/iframe to only same origin domains. Prevents clickjacking attacks.
X-XSS-Protection: 1; mode=block: Enables browser built-in XSS protection and tells it to block the page if an attack is detected, rather than sanitize.
Referrer-Policy: no-referrer-when-downgrade: Strips the referrer header when downgrading from HTTPS to HTTP to avoid leaking secure URLs.
The always parameter ensures the headers get set even for non-200 responses from the upstream.

•	Defined a custom log format specifically for the location ~* block that logs following


-time_local - local time of request
-nginx_version - nginx version handling request
-remote_addr - client IP
-request_id - unique ID for request
-status - response status code
-body_bytes_sent - bytes sent to client
-http_user_agent - client user agent
-proxy_protocol_addr - client IP from proxy protocol
-server_name - name of server handling request
-upstream_addr - upstream server IP
-request_time - time to process request
-upstream_* times - connect, header, response times
-request_uri - original request URI
-upstream_status - upstream status
-ssl_* - SSL session details
-http_x_forwarded_for - original client IP if behind proxy

