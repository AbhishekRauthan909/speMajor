FROM node:16-alpine
WORKDIR /SPE_FRONTEND
COPY ./package*.json ./
RUN npm install
COPY . .
CMD [ "npm", "run", "dev" ]