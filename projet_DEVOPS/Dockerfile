FROM alpine:3.18
ENV NODE_VERSION 21.6.2

CMD ["node",  "-v"]
# Installing libvips-dev for sharp Compatibility
RUN apk update && apk add --no-cache build-base gcc autoconf automake zlib-dev libpng-dev nasm bash vips-dev git
# ARG NODE_ENV=development
# ENV NODE_ENV=${NODE_ENV}

WORKDIR /opt/
COPY package.json package-lock.json ./
RUN npm cache clean --force
RUN npm install --ignore-scripts=false --foreground-scripts --verbose sharp
RUN npm install -g node-gyp
# RUN npm install sharp 
RUN npm config set fetch-retry-maxtimeout 600000 -g && npm install
#RUN npm install --platform=linuxmusl --arch=x64 sharp
ENV PATH /opt/node_modules/.bin:$PATH
# RUN npm rebuild --verbose sharp
WORKDIR /opt/app
COPY . .
RUN chown -R node:node /opt/app
USER node
RUN npm ci
RUN ["npm", "run", "build"]
EXPOSE 1337
CMD ["npm", "run", "develop"]
