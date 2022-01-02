FROM ruby:3.0

RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -
RUN apt-get update -qq && apt-get install -qq --no-install-recommends \
    nodejs \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*
RUN npm install -g yarn@1

ENV APP_PATH /myapp

RUN mkdir $APP_PATH
WORKDIR $APP_PATH

ADD Gemfile $APP_PATH/Gemfile
ADD Gemfile.lock $APP_PATH/Gemfile.lock
RUN bundle install
ADD . $APP_PATH

# Nginxと通信を行うための準備
RUN mkdir -p tmp/sockets
RUN mkdir -p tmp/pids

VOLUME $APP_PATH/public
VOLUME $APP_PATH/tmp

RUN yarn install --check-files
RUN SECRET_KEY_BASE=placeholder bundle exec rails assets:precompile

