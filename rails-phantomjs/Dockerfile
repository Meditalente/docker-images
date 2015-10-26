FROM ruby:2.2
MAINTAINER Alex Ulianytskyi <a.ulyanitsky@gmail.com>

# Packages
ENV MAIN_PACKAGES git postgresql-client python python-pip
# PhantomJS from https://github.com/fgrehm/docker-phantomjs2/blob/master/Dockerfile.buildphantomjs
# Dependencies we just need for building phantomjs

ENV BUILD_DEPENDENCIES\
  wget tar gzip build-essential g++ flex bison gperf\
  ruby perl libsqlite3-dev libssl-dev libpng-dev python-dev

# Dependencies we need for running phantomjs
ENV PHANTOM_JS_DEPENDENCIES\
  libicu-dev libfontconfig1-dev libjpeg-dev libfreetype6

ENV PHANTOM_JS_TAG 2.0.0

# Gems to install
ENV DEFAULT_GEMS rails slack-notifier puma pg

# Installing phantomjs
# Installing dependencies
RUN apt-get update
RUN apt-get install -fyq ${MAIN_PACKAGES} ${BUILD_DEPENDENCIES} ${PHANTOM_JS_DEPENDENCIES}

# Downloading src, unzipping & removing zip
RUN mkdir /phantomjs \
  &&  cd /phantomjs \
  &&  wget -q https://github.com/ariya/phantomjs/archive/${PHANTOM_JS_TAG}.tar.gz -O phantomjs.tar.gz \
  &&  tar xzf phantomjs.tar.gz \
  &&  rm -rf /phantomjs/phantomjs.tar.gz \
  # Building phantom
  &&  mv phantomjs-* phantomjs

WORKDIR /phantomjs/phantomjs

RUN ./build.sh --confirm --silent \
  # Removing everything but the binary
  && ls -A | grep -v bin | xargs rm -rf \
  # Symlink phantom so that we are able to run `phantomjs`
  && ln -s /phantomjs/phantomjs/bin/phantomjs /usr/local/share/phantomjs \
  && ln -s /phantomjs/phantomjs/bin/phantomjs /usr/local/bin/phantomjs \
  && ln -s /phantomjs/phantomjs/bin/phantomjs /usr/bin/phantomjs

RUN echo "phantomjs binary is located at `which phantomjs`" \
  && echo "just run 'phantomjs' (version `phantomjs -v`)"

# AWS CLI & EB CLi
RUN pip install --upgrade awscli awsebcli

# Pre-install gems
RUN gem install ${DEFAULT_GEMS}

# Removing build dependencies, clean temporary files
RUN apt-get purge -yq ${BUILD_DEPENDENCIES}

# Make sure main packages installed
RUN apt-get install -yq ${MAIN_PACKAGES}
RUN apt-get autoremove -yq \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN aws --version
RUN eb --version
RUN rails --version
RUN puma --version
RUN phantomjs -v

# throw errors if Gemfile has been modified since Gemfile.lock
# RUN bundle config --global frozen 1

RUN mkdir -p /usr/src/app

WORKDIR /usr/src/app

RUN mkdir -p public log tmp tmp/sockets tmp/pids tmp/cache

COPY 502.html 503.html public/

# Add default unicorn config
COPY puma.rb config/

ONBUILD COPY Gemfile /usr/src/app/
ONBUILD COPY Gemfile.lock /usr/src/app/
ONBUILD RUN bundle install --jobs 8
ONBUILD COPY . /usr/src/app

EXPOSE 3000
CMD puma
