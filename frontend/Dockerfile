FROM node:10 AS NPM_TOOL_CHAIN
RUN mkdir -p /home/node/app/node_modules && chown -R node:node /home/node/app
WORKDIR /home/node/app
COPY ./ /home/node/app
RUN rm -rf dist && npm install && npm run build --prod

FROM nginx:1.13.3-alpine
COPY /nginx/default.conf /etc/nginx/conf.d/
RUN rm -rf /usr/share/nginx/html/*
COPY --from=NPM_TOOL_CHAIN /home/node/app/dist/shop /usr/share/nginx/html