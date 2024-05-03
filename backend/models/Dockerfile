FROM alpine:3.9

RUN echo "http://dl-cdn.alpine-linux.org/alpine/v3.9/main" >> sudo tee -a /etc/apk/repositories && \
echo "http://dl-cdn.alpine-linux.org/alpine/v3.9/community" >> sudo tee -a /etc/apk/repositories


RUN apk add  mongodb yaml-cpp=0.6.2-r2

CMD ["systemctl enable mongod"]


EXPOSE 27017