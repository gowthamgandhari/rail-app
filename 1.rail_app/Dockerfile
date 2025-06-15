FROM ruby:3.2
RUN apt-get update -qq && \ apt-get install -y curl gnupg postgresql-client
RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash - && \ 
    apt-get install -y nodejs
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian stable main" | tee  /etc/apt/sources.list.d/yarn.list && \ apt-get update && \ apt-get install -y yarn
WORKDIR /railruby_app
ENV RAILS_ENV=development
ENV BUNDLER_VERSION=2.3.26
COPY Gemfile Gemfile.lock ./
RUN gem install bundler -v "$BUNDLER_VERSION" && bundle install
COPY . .
EXPOSE 3000
CMD ["rails", "server", "-b", "0.0.0.0"]
