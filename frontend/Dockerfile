# build environment
FROM node:12.16.1-alpine as builder

# set working directory
WORKDIR /usr/frontend/app

# for yarn cache
COPY package.json package-lock.json /usr/frontend/app/

RUN npm install

# copy contets of the project
COPY . .

# production build
RUN npm run-script build

# runtime environment
FROM node:12.16.1-alpine

RUN apk add --no-cache bash \
    && npm config set unsafe-perm true \
    && npm install --global serve

WORKDIR /app

COPY --from=builder /usr/frontend/app/startup.sh /
COPY --from=builder /usr/frontend/app/build build/

CMD /startup.sh
