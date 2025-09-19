FROM nginx:alpine
# Use the official Nginx image as a base
COPY . /usr/share/nginx/html
# Copy the website files to the Nginx HTML directory
EXPOSE 80
# Expose port 80
CMD ["nginx", "-g", "daemon off;"]
# Start Nginx in the foreground 
# to keep the container running