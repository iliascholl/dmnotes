FROM node:14.15.3-alpine3.11 as build
WORKDIR /app
ENV PATH /app/node_modules/.bin:$PATH
COPY package.json yarn.lock .yarnrc.yml ./
COPY .yarn ./.yarn
RUN yarn install --immutable
COPY . ./
RUN yarn build 

FROM nginx:stable-alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
