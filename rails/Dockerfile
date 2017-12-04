FROM ruby:2
LABEL maintainer="Alex Ulianytskyi <a.ulyanitsky@gmail.com>"

# Packages
ENV MAIN_PACKAGES curl git postgresql-client mysql-client nodejs yarn
ENV BUILD_DEPENDENCIES build-essential libpq-dev
# Gems to install
ENV DEFAULT_GEMS rails slack-notifier puma pg mysql2 bcrypt

# Add Yarn
ADD https://dl.yarnpkg.com/debian/pubkey.gpg /tmp/yarn-pubkey.gpg
RUN apt-key add /tmp/yarn-pubkey.gpg && rm /tmp/yarn-pubkey.gpg
RUN echo 'deb http://dl.yarnpkg.com/debian/ stable main' > /etc/apt/sources.list.d/yarn.list

# Install build dependencies
RUN apt-get update && apt-get install -qq -y --no-install-recommends ${BUILD_DEPENDENCIES}
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -

# Install main packages
RUN apt-get install -yq ${MAIN_PACKAGES}

# Pre-install gems
RUN gem install ${DEFAULT_GEMS}

# Removing build dependencies, clean temporary files
RUN apt-get purge -yq ${BUILD_DEPENDENCIES}

# Make sure main packages installed
RUN apt-get install -yq ${MAIN_PACKAGES}

RUN apt-get autoremove -yq \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN rails --version
RUN puma --version
RUN psql --version
RUN mysql --version
RUN node --version
RUN yarn --version

# throw errors if Gemfile has been modified since Gemfile.lock
# RUN bundle config --global frozen 1

RUN mkdir -p /usr/src/app

WORKDIR /usr/src/app

EXPOSE 3000
CMD bin/start.sh
