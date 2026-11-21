FROM node:22-alpine
WORKDIR /app
COPY package*.json .
RUN npm ci --omit=dev
COPY . .
RUN mkdir -p src/uploads && chown -R node:node src/uploads
USER node
EXPOSE 5000
CMD ["npm", "run" ,"start"]