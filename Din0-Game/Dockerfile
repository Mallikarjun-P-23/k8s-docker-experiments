FROM nginx:alpine

# Copy the Handlebars file and rename it to index.html
COPY index.hbs /usr/share/nginx/html/index.html

# Copy custom nginx configuration
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80