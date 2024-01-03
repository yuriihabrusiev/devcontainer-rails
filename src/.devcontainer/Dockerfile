ARG VARIANT=3.3.0-bookworm
FROM ruby:${VARIANT}

# Install dependencies
RUN export DEBIAN_FRONTEND=noninteractive && apt-get update -qq \
    && apt-get install -y build-essential libvips gnupg2 curl git

# Ensure node.js 18 is available for apt-get
ARG NODE_MAJOR=18
RUN curl -L https://deb.nodesource.com/nsolid_setup_deb.sh | bash -s -- $NODE_MAJOR

# Install node and yarn
RUN apt-get update -qq && apt-get install -y nodejs && npm install -g yarn

# Ensure binding is always 0.0.0.0, even in development, to access server from outside container
ENV BINDING="0.0.0.0"
