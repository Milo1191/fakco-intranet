FROM ubuntu:18.04
LABEL maintainer="erickidder11@gmail.com"

# Install Nginx
RUN apt-get update && apt-get install -y nginx \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Remove default Nginx site to avoid conflicts
RUN rm -f /etc/nginx/sites-enabled/default \
    && rm -f /usr/share/nginx/html/index.nginx-debian.html

# Copy custom Nginx config
COPY files/default /etc/nginx/sites-available/default
RUN ln -sf /etc/nginx/sites-available/default /etc/nginx/sites-enabled/default

# Copy all HTML files into the Nginx web root
COPY files/*.html /usr/share/nginx/html/

# Ensure proper permissions
RUN chmod -R 644 /usr/share/nginx/html/*.html \
    && chown -R www-data:www-data /usr/share/nginx/html

# Expose HTTP port
EXPOSE 80

# Start Nginx in the foreground
CMD ["/usr/sbin/nginx", "-g", "daemon off;"]
