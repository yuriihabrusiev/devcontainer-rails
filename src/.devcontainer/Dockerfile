ARG VARIANT=3.2-bookworm
FROM ruby:${VARIANT}

# Install dependencies
RUN apt-get update -qq && apt-get install -y build-essential libvips gnupg2 curl git

# Ensure node.js 18 is available for apt-get
ARG NODE_MAJOR=18
RUN curl -L https://deb.nodesource.com/nsolid_setup_deb.sh | bash -s -- $NODE_MAJOR

# Install node and yarn
RUN apt-get update -qq && apt-get install -y nodejs && npm install -g yarn

# Ensure gems are installed on a persistent volume and available as bins
VOLUME /bundle
RUN bundle config set --global path '/bundle'
ENV PATH="/bundle/ruby/$RUBY_VERSION/bin:${PATH}"

# Install Rails
RUN gem install rails

# Ensure binding is always 0.0.0.0, even in development, to access server from outside container
ENV BINDING="0.0.0.0"

# Overwrite ruby image's entrypoint to provide open cli
ENTRYPOINT [""]
