# FROM node:alpine

# WORKDIR /usr/src/app

# COPY . /usr/src/app

# RUN npm install -g @angular/cli

# RUN npm install --legacy-peer-deps

# CMD ["ng", "serve", "--host", "0.0.0.0","--disable-host-check"]

# Stage 1: Build the Angular application
FROM node:alpine AS build

WORKDIR /app

COPY package.json package-lock.json ./
RUN npm install --legacy-peer-deps

COPY . .
RUN npm run build --prod

# Stage 2: Serve the built application with Nginx
FROM nginx:alpine

# Copy custom Nginx configuration
# COPY nginx.conf /etc/nginx/nginx.conf


# Copy the built Angular application from the build stage
COPY --from=build /app/dist/aig-api-documentation /usr/share/nginx/html/

EXPOSE 4400

CMD ["nginx", "-g", "daemon off;"]