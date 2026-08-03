FROM node:16 AS web-build
WORKDIR /usr/src/app
COPY ./ ./client

ENV NODE_OPTIONS=--max_old_space_size=4096

RUN cd client && npm install

RUN cd client && npm run build --prod

# Use official nginx image as the base image
FROM nginx:latest

# Copy the build output to replace the default nginx contents.
COPY --from=web-build /usr/src/app/client/dist/client/ /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose port 4200
EXPOSE 4200
