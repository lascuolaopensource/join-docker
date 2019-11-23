ARG BASE_IMAGE_TAG
FROM openjdk:${BASE_IMAGE_TAG:-8u222-jdk-stretch}

# Env variables
ARG SCALA_VERSION
ENV SCALA_VERSION ${SCALA_VERSION:-2.13.1}
ARG SBT_VERSION
ENV SBT_VERSION ${SBT_VERSION:-1.3.3}

# Install sbt
RUN \
  curl -L -o sbt-$SBT_VERSION.deb https://dl.bintray.com/sbt/debian/sbt-$SBT_VERSION.deb && \
  dpkg -i sbt-$SBT_VERSION.deb && \
  rm sbt-$SBT_VERSION.deb && \
  apt-get update && \
  apt-get install sbt

# Install Scala
## Piping curl directly in tar
RUN \
  curl -fsL https://downloads.typesafe.com/scala/$SCALA_VERSION/scala-$SCALA_VERSION.tgz | tar xfz - -C /usr/share && \
  mv /usr/share/scala-$SCALA_VERSION /usr/share/scala && \
  chown -R root:root /usr/share/scala && \
  chmod -R 755 /usr/share/scala && \
  ln -s /usr/share/scala/bin/scala /usr/local/bin/scala

WORKDIR /root

COPY backend-variables.conf conf/

RUN git clone https://github.com/lascuolaopensource/join-backend.git \
&& mv conf/backend-variables.conf join-backend/conf/env/prod.conf \
&& cd join-backend \
&& sbt stage

WORKDIR /root/join-backend

CMD target/universal/stage/bin/sos -Dconfig.resource=env/prod.conf -Dhttp.port=9000 -Dlogger.resource=logback.xml -Dplay.evolutions.db.default.autoApply=true -Dplay.http.secret.key='QCY?tAnfk?aZ?iwrNwnxIlR6CTf:G3gf:90Latabg@5241ABR5W:1uDFN];Ik@n'