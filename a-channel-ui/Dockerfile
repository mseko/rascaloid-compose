FROM node:9.9.0-alpine AS build
RUN apk update
RUN apk add git 
WORKDIR /YuyaHirooka
RUN git clone https://github.com/YuyaHirooka/rascaloid-backlog-a-channel.git
WORKDIR rascaloid-backlog-a-channel
RUN npm install && npm run build

FROM node:9.9.0-alpine
EXPOSE 5000
RUN npm install -g serve
COPY --from=build /YuyaHirooka/rascaloid-backlog-a-channel/build/ /rascaloid-backlog-a-channel
WORKDIR /rascaloid-backlog-a-channel
ENTRYPOINT ["serve","-s","."]