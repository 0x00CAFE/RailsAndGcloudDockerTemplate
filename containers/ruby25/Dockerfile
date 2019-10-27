FROM ruby:2.5

# bash
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

# essential
RUN apt-get update -qq && apt-get install -y build-essential libpq-dev

# yarn
RUN apt-get update && apt-get install -y curl apt-transport-https wget && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && apt-get install -y yarn

# Node.js
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
    apt-get install nodejs

RUN mkdir /app
WORKDIR /app
ADD Gemfile /app/Gemfile

# bundle install
RUN bundle install

CMD bash
