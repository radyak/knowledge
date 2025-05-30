### Frontend Build
FROM node:lts-alpine AS frontend-build

WORKDIR /app

COPY installation/package*.json ./
RUN npm install
COPY installation ./

EXPOSE 8000

CMD ["npm", "start", "--", "--host", "0.0.0.0"]