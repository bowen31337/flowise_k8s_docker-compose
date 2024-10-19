#### Nginx Proxy Automation

For the Nginx reverse proxy, we're using the [nginx-proxy-automation](https://github.com/evertramos/nginx-proxy-automation) project. This provides an automated Docker Nginx proxy integrated with Let's Encrypt for SSL certificates.

Setting up the Nginx Proxy:

1. Clone the repository with submodules:
   ```
   git clone --recurse-submodules https://github.com/evertramos/nginx-proxy-automation.git proxy
   ```

2. Run the fresh start script:
   ```
   cd proxy/bin && ./fresh-start.sh --yes --skip-docker-image-check -e your_email@domain.com
   ```
   Replace `your_email@domain.com` with your actual email address.

3. Test the proxy:
   ```
   docker run -dit -e VIRTUAL_HOST=your.domain.com --network=proxy --name test-web httpd:alpine
   ```
   Or use the provided test script:
   ```
   ./test.sh your.domain.com
   ```