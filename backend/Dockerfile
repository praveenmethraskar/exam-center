FROM node:20 AS build
WORKDIR /usr/src/app
COPY backend/package*.json ./
RUN npm install
COPY backend/ .

FROM node:20-slim
WORKDIR /usr/src/app
COPY --from=build /usr/src/app .
EXPOSE 3001
CMD ["npm", "start"]
