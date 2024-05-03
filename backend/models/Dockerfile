FROM alpine:latest

RUN echo "http://dl-cdn.alpine-linux.org/alpine/v3.9/main" >> sudo tee -a /etc/apk/repositories && \
echo "http://dl-cdn.alpine-linux.org/alpine/v3.9/community" >> sudo tee -a /etc/apk/repositories && \
apk add --update mongodb yaml-cpp=0.6.2-r2

RUN apk upgrade && apk add  -y mongodb-org 

CMD ["systemctl enable mongod"]


EXPOSE 27017