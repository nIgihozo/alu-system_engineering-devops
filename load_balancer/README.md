# Load balancer Project!!
# HAProxy Load Balancer with Custom HTTP Header

This project sets up a load balancer (`lb-01`) using HAProxy to distribute HTTP traffic between two web servers (`web-01` and `web-02`) in round-robin. Each server is configured to respond with a custom HTTP header `X-Served-By` to identify which server handled the request.

## Key Features

- HAProxy forwards traffic using round-robin
- Nginx adds `X-Served-By: <hostname>` to all responses
- Header used to verify backend server identity
- Handle custom http header

## Configuration Summary

### HAProxy (`lb-01`)
- Enable HAProxy: set `ENABLED=1` in `/etc/default/haproxy`
- Configure `/etc/haproxy/haproxy.cfg`:
  ```haproxy
  frontend http_front
      bind *:80
      http-request set-path /
      default_backend http_back

  backend http_back
      balance roundrobin
      server web-01 <WEB_01_IP>:80 check
      server web-02 <WEB_02_IP>:80 check
Nginx (web-01, web-02)
In /etc/nginx/sites-available/default, inside location / block:

nginx
add_header X-Served-By "$hostname" always;
Automation Script (0-custom_http_response_header)
Remotely updates Nginx config on web-01:


## Testing
Run multiple times to verify round-robin and header:

## bash
curl -sI http://<LB_IP> | grep X-Served-By
## Expected alternating output:
- X-Served-By:  Then your user name of your server
- X-Served-By:
# Code
- X-Served-By: Your server name
- X-Served-By:  Your server name
## Author
Nyiramanzi Igihozo
