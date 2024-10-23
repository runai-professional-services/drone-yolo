# Use an official Alpine base image
FROM alpine:latest

# Install necessary dependencies
RUN apk add --no-cache bash curl gcc libc-dev make openssl-dev pcre-dev zlib-dev git

# Create a directory for the Nginx source and RTMP module
RUN mkdir -p /usr/src && \
    cd /usr/src && \
    curl -LO http://nginx.org/download/nginx-1.21.6.tar.gz && \
    tar -zxvf nginx-1.21.6.tar.gz

# Clone the Nginx RTMP module into the src directory
RUN cd /usr/src && \
    git clone https://github.com/arut/nginx-rtmp-module.git

# Configure and build Nginx with the RTMP module
RUN cd /usr/src/nginx-1.21.6 && \
    ./configure --add-module=/usr/src/nginx-rtmp-module --with-http_ssl_module && \
    make && \
    make install

# Clean up unnecessary files after installation to reduce image size
RUN rm -rf /usr/src/nginx-1.21.6 /usr/src/nginx-rtmp-module

# Copy custom nginx.conf file that includes RTMP configuration
COPY nginx.conf /etc/nginx/nginx.conf

# Expose RTMP and HTTP ports
EXPOSE 1935 8080

# Ensure that Nginx is in the PATH
ENV PATH="/usr/local/nginx/sbin:$PATH"

# Run Nginx in the foreground
CMD ["nginx", "-g", "daemon off;"]
