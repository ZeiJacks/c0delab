FROM ruby:3.1.2-alpine

ENV LANG=C.UTF-8
ENV TZ=Asia/Tokyo

RUN apk update && \
    apk upgrade && \
    apk add alpine-sdk \
    build-base \
    postgresql-dev \
    postgresql-client \
    libpq-dev \
    tzdata
#    apk add --update --no-cache --virtual=.build-dependencies \
#      build-base \
#      curl-dev \
#      linux-headers \
#      libxml2-dev \
#      libxslt-dev \
#      postgresql-dev \
#      ruby-dev \
#      yaml-dev \
#      zlib-dev && \
#    apk add --update --no-cache \
#      bash \
#      git \
#      openssh \
#      postgresql \
#      ruby-json \
#      tzdata \
#      yaml
WORKDIR /c0delab

COPY Gemfile /c0delab/Gemfile
COPY Gemfile.lock /c0delab/Gemfile.lock

RUN gem update --system
RUN bundle update --bundler
RUN bundle install

COPY entrypoint.sh /usr/bin
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]

EXPOSE 8000
CMD ["rails", "server", "-b", "0.0.0.0"]
