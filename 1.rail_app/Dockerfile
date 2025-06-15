FROM ruby:3.2

# Install dependencies
RUN apt-get update -qq && \
    apt-get install -y curl gnupg postgresql-client

# Install Node.js
RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash - && \
    apt-get install -y nodejs

# Install Yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && \
    apt-get install -y yarn

# Set working directory
WORKDIR /railruby_app

# Set environment
ENV RAILS_ENV=development
ENV BUNDLER_VERSION=2.3.26

# Copy Gemfile and Gemfile.lock before running bundle install
COPY Gemfile Gemfile.lock ./

# Install bundler and gems
RUN gem install bundler -v "$BUNDLER_VERSION" && bundle install

# Copy the rest of the app
COPY . .

# Expose Rails default port
EXPOSE 3000

# Start Rails server
CMD ["rails", "server", "-b", "0.0.0.0"]
