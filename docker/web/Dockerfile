#Node.js & Yarn
FROM node:18-bullseye as node

#Ruby & Bundler & postgresql-client
FROM ruby:3.3.0-bookworm

COPY --from=node /usr/local/bin/node /usr/local/bin/node
COPY --from=node /opt/yarn-* /opt/yarn
RUN ln -fs /opt/yarn/bin/yarn /usr/local/bin/yarn

RUN apt-get update -qq && \
    apt-get install -y --no-install-recommends sudo && \
    apt-get install -y build-essential ruby-dev make gcc libc-dev libpq-dev default-mysql-client

RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/*
RUN apt update -qq && \
    apt install vim -y

RUN mkdir /app
WORKDIR /app

COPY ../../sample_app/Gemfile /app/Gemfile
COPY ../../sample_app/Gemfile.lock /app/Gemfile.lock

RUN bundle install

ADD . /app