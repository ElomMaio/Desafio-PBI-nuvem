version: '3.8'

services:
  db:
    image: postgres:latest
    environment:
      POSTGRES_USER: elom
      POSTGRES_PASSWORD: 123456
      POSTGRES_DB: azure_company
    volumes:
      - ./initdb:/docker-entrypoint-initdb.d
    ports:
      - "5432:5432"
