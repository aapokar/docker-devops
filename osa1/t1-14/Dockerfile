FROM ruby:2.6

COPY . .
RUN ["gem", "install", "bundler"]
RUN ["bundle", "install"]

RUN ["rails", "db:migrate"]
EXPOSE 3000
CMD ["rails", "s"]
