FROM node:alpine as builder
WORKDIR '/app'
# Install dependencies
COPY ./package.json ./
RUN npm install
# Copy all files from current directory into container
COPY . .
# Build
RUN npm run build

# Run Phase
FROM nginx
EXPOSE 3000
# Copy nginx defualt.conf file and overwerite existing default.conf file
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
# copy production build assets from builder phase
COPY --from=builder /app/build /usr/share/nginx/html