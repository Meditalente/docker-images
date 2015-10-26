FROM ruby:2.2
MAINTAINER Alex Ulianytskyi <a.ulyanitsky@gmail.com>

# Packages
ENV MAIN_PACKAGES git postgresql-client python python-pip
ENV BUILD_DEPENDENCIES python-dev
# Gems to install
ENV DEFAULT_GEMS rails slack-notifier puma pg

# Install main packages
RUN apt-get update
RUN apt-get install -yq ${MAIN_PACKAGES} ${BUILD_DEPENDENCIES}

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

# throw errors if Gemfile has been modified since Gemfile.lock
# RUN bundle config --global frozen 1

RUN mkdir -p /usr/src/app

WORKDIR /usr/src/app

RUN mkdir -p public log tmp tmp/sockets tmp/pids tmp/cache

COPY 502.html 503.html public/

# Add default unicorn config
COPY puma.rb config/

EXPOSE 3000
CMD puma
