FROM alpine:3.9

RUN echo "http://dl-cdn.alpine-linux.org/alpine/v3.9/main" >> sudo tee -a /etc/apk/repositories && \
echo "http://dl-cdn.alpine-linux.org/alpine/v3.9/community" >> sudo tee -a /etc/apk/repositories


RUN apk add  mongodb yaml-cpp=0.6.2-r2  && rm -vrf /var/cache/apk/*


ENV MONGO_DKR_DATA_DIR '/var/lib/mongodb'
ENV MONGO_DKR_LOG_DIR '/var/log/mongodb'
ENV ADD_USER_CMD "${MONGO_DKR_DATA_DIR}/add-user.sh"
ENV ADD_USER_FILE "${MONGO_DKR_DATA_DIR}/add-mongo-user.js"
ENV MONGO_RUN_PID_FILE '/var/run/mongodb/mongod.pid'

COPY mongod.conf /etc/
COPY add-user.sh "${MONGO_DKR_DATA_DIR}/"
COPY start-mongod.sh /usr/local/bin/

RUN chmod +x /usr/local/bin/start-mongod.sh \
 && mkdir -p /run/mongodb \
 && chown mongodb:mongodb /run/mongodb \
 && ln -sf /dev/stderr "${MONGO_DKR_LOG_DIR}/mongod.log" \
 && mongo -version

USER mongodb

VOLUME $MONGO_DKR_DATA_DIR

WORKDIR $MONGO_DKR_DATA_DIR




EXPOSE 27017

ENTRYPOINT []
CMD ["start-mongod.sh"]

#reference 1: https://stackoverflow.com/questions/53850369/issue-installing-mongodb-on-alpine/53888440#53888440
#reference 2: https://gist.github.com/ecarlson94/76733ef7a93cbde74d918d6a4c9452e9
# main reference for adding users: https://github.com/b01/docker-images/blob/main/alpine-mongodb/Dockerfile