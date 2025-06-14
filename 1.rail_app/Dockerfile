FROM ruby:3.2  
RUN apt-get update -qq && apt-get install -y nodejs postgresql-client  
WORKDIR /app  
ENV RAILS_ENV=development
ENV BUNDLER_VERSION=2.3.26
COPY Gemfile Gemfile.lock ./  
RUN gem install bundler -v "$BUNDLER_VERSION" && bundle install
COPY . .  
EXPOSE 3000
CMD ["rails", "server", "-b", "0.0.0.0"]  

