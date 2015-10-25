FROM ruby:2.2
MAINTAINER Alex Ulianytskyi <a.ulyanitsky@gmail.com>

# Nginx key
RUN apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62

RUN curl --silent --location http://nginx.org/keys/nginx_signing.key | apt-key add -

# Add nginx mainline repository
COPY nginx-mainline.list /etc/apt/sources.list.d/nginx.list

# Install NodeJs 0.12
RUN curl --silent --location https://deb.nodesource.com/setup_0.12 | bash -

# Packages
RUN apt-get -y -q install git nginx nodejs mysql-client postgresql-client \
      python-pip python-dev --no-install-recommends

# AWS CLI & EB CLi
RUN pip install --upgrade awscli awsebcli

# Pre-install gems
RUN gem install slack-notifier foreman puma pg mysql2 rails

# Install npm packages
RUN npm install --global dredd aglio && npm cache clear

# throw errors if Gemfile has been modified since Gemfile.lock
# RUN bundle config --global frozen 1

# Nginx
RUN echo "\ndaemon off;" >> /etc/nginx/nginx.conf
# RUN chown -R www-data:www-data /var/lib/nginx
# Add default nginx config
COPY nginx-sites.conf /etc/nginx/conf.d/default.conf

# PhantomJS from https://github.com/fgrehm/docker-phantomjs2/blob/master/Dockerfile.buildphantomjs
# Dependencies we just need for building phantomjs
ENV buildDependencies\
  wget unzip python build-essential g++ flex bison gperf\
  ruby perl libsqlite3-dev libssl-dev libpng-dev

# Dependencies we need for running phantomjs
ENV phantomJSDependencies\
  libicu-dev libfontconfig1-dev libjpeg-dev libfreetype6

# Installing phantomjs
RUN \
    # Installing dependencies
apt-get install -fyqq ${buildDependencies} ${phantomJSDependencies}\
    # Downloading src, unzipping & removing zip
&&  mkdir phantomjs \
&&  cd phantomjs \
&&  wget https://github.com/ariya/phantomjs/archive/2.0.0.zip -O phantomjs.zip \
&&  unzip phantomjs.zip \
&&  rm -rf /phantomjs/phantomjs.zip \
    # Building phantom
&&  mv phantomjs-* phantomjs \
&&  cd phantomjs \
&&  ./build.sh --confirm --silent \
    # Removing everything but the binary
&&  ls -A | grep -v bin | xargs rm -rf \
    # Symlink phantom so that we are able to run `phantomjs`
&&  ln -s /phantomjs/phantomjs/bin/phantomjs /usr/local/share/phantomjs \
&&  ln -s /phantomjs/phantomjs/bin/phantomjs /usr/local/bin/phantomjs \
&&  ln -s /phantomjs/phantomjs/bin/phantomjs /usr/bin/phantomjs \
    # Removing build dependencies, clean temporary files
&&  apt-get purge -yqq ${buildDependencies} \
&&  apt-get autoremove -yqq \
&&  apt-get clean \
&&  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    # Checking if phantom works
&&  phantomjs -v

CMD \
    echo "phantomjs binary is located at /phantomjs/phantomjs-2.0.0/bin/phantomjs"\
&&  echo "just run 'phantomjs' (version `phantomjs -v`)"

RUN mkdir -p /usr/src/app

WORKDIR /usr/src/app

RUN mkdir -p public log log/nginx tmp tmp/sockets tmp/pids tmp/cache

COPY 502.html 503.html public/

# Add default unicorn config
COPY puma.rb config/

# Add default foreman config
COPY Procfile Procfile

ONBUILD COPY Gemfile /usr/src/app/
ONBUILD COPY Gemfile.lock /usr/src/app/
ONBUILD RUN bundle install --jobs 8
ONBUILD COPY . /usr/src/app
# ONBUILD RUN chown www-data:www-data -R /usr/src/app

EXPOSE 80 443
CMD foreman start
