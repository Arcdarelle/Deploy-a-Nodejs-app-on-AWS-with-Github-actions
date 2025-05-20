# --- Build Stage ---
    FROM node:16.20-buster-slim AS builder

    WORKDIR /app
    COPY package*.json ./
    RUN npm install
    COPY . .
    ARG REACT_APP_API_URL
    ENV REACT_APP_API_URL=$REACT_APP_API_URL
    RUN npm run build
    
    # --- Serve Stage ---
    FROM nginx:alpine
    COPY --from=builder /app/build /usr/share/nginx/html
    
    # Optional: Custom nginx config for SPA routing
    # COPY nginx.conf /etc/nginx/nginx.conf
    
    EXPOSE 80
    CMD ["nginx", "-g", "daemon off;"]
    