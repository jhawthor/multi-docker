# Two Step build process
FROM node:alpine as builder 
WORKDIR '/app'
COPY ./package.json ./
# install dependencies
RUN npm install
COPY . .
# build the react app
RUN npm run build

# build the prod container with the output from "npm run build"
FROM nginx
EXPOSE 3000
# copy the nginx conf file
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
# copy the compiled code for the app from the bild folder
# so that nginx can serve it
COPY --from=builder /app/build /usr/share/nginx/html

