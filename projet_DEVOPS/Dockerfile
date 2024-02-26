FROM node:18-alpine
# Installing libvips-dev for sharp Compatability
RUN apk update && apk add  build-base gcc autoconf automake zlib-dev libpng-dev nasm bash vips-dev
ARG NODE_ENV=development
ENV NODE_ENV=${NODE_ENV}
WORKDIR /opt/app
COPY ./package.json ./yarn.lock ./
# ENV PATH /opt/node_modules/.bin:$PATH
RUN yarn config set network-timeout 600000 -g && yarn install
RUN yarn add --verbose --platform=linuxmusl --arch=x64 sharp
# WORKDIR /opt/app
COPY ./ .
RUN yarn build
EXPOSE 1337
CMD ["yarn", "develop"]


# RN EBADENGINE Unsupported engine {                                                                                     
#  => => # npm WARN EBADENGINE   package: '@strapi/utils@4.20.1',                                                                       
#  => => # npm WARN EBADENGINE   required: { node: '>=18.0.0 <=20.x.x', npm: '>=6.0.0' },                                               
#  => => # npm WARN EBADENGINE   current: { node: 'v21.6.2', npm: '10.2.4' }                                                            
#  => => # npm WARN EBADENGINE }            