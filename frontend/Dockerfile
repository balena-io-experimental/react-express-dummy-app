FROM balenalib/raspberrypi3-alpine-node
WORKDIR /usr/src/app

# install nginx
RUN apk --no-cache add nginx

# install node dependencies
COPY package.json package-lock.json ./
RUN npm i

# build app
COPY ./src ./src
COPY ./public ./public
RUN npm run build

# copy built app to public html path
RUN mv /usr/src/app/build /usr/share/nginx/html
COPY conf/nginx.conf /etc/nginx/http.d/default.conf

# run nginx
CMD ["/bin/sh", "-c", "nginx -g \"daemon off;\""]
