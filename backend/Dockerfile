FROM node:18-alpine

WORKDIR /app

COPY package*.json ./

ENV HUSKY=0

RUN npm install

COPY . .

EXPOSE 5007

CMD ["npm", "start"]