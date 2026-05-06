# ---- Build stage ----
FROM node:24.9.0-alpine AS build

WORKDIR /app

# Install deps first (better caching)
COPY package*.json ./
RUN npm ci

# Copy source and build
COPY . .
RUN npm run build

# ---- Production stage ----
FROM nginx:alpine AS prod

# Vite default build output is "dist"
# Copy build artifacts to nginx html directory
COPY --from=build /app/dist /usr/share/nginx/html

# (Optional) If you have a custom nginx config, uncomment:
# COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]