FROM asux/rails
MAINTAINER Alex Ulianytskyi <a.ulyanitsky@gmail.com>

# Packages
RUN apt-get update && apt-get -y -q install build-essential \
      g++ \
      flex \
      bison \
      gperf \
      perl \
      libsqlite3-dev \
      libfontconfig1-dev \
      libicu-dev \
      libfreetype6 \
      libssl-dev \
      libpng-dev \
      libjpeg-dev \
      libqt5webkit5-dev \
      --no-install-recommends && apt-get clean

# PhantomJS
ENV PHANTOM_JS_TAG 2.0.0

RUN cd /tmp && \
  curl -s https://codeload.github.com/ariya/phantomjs/tar.gz/$PHANTOM_JS_TAG | tar -xz && \
  cd phantomjs-$PHANTOM_JS_TAG && \
  ./build.sh --confirm && \
  mv bin/phantomjs /usr/local/bin && \
  rm -rf /tmp/phantomjs

WORKDIR /usr/src/app

EXPOSE 80 443
CMD foreman start
