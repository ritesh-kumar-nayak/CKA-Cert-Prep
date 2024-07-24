FROM node:18-alpine AS Installer
WORKDIR /app
COPY package*.json ./

RUN npm install
# With this COPY instruction below, we are copying the output artifacts of "npm install" to 'this layer' only not to the container.
COPY . .
RUN npm run build

FROM nginx:latest AS Deployer
COPY --from=Installer /app/build /usr/share/nginx/html


