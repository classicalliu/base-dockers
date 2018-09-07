FROM ubuntu:18.04

# install base packages
#ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update -qq && \
 DEBIAN_FRONTEND=noninteractive apt-get install -y software-properties-common build-essential libpq-dev libsqlite3-dev libmysqlclient-dev git autoconf locales locales-all curl wget vim openssl libssl-dev libyaml-dev libxslt1-dev libevent-dev cmake htop libreadline7 libreadline-dev libtool automake bzip2 ca-certificates libffi-dev procps zlib1g-dev xz-utils libxml2-dev libncurses5-dev libglib2.0-dev libbz2-dev tzdata && \
 curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
 curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
 echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
 apt-get update -qq && \
 apt-get install -y nodejs yarn && \
 apt-get clean && \
 rm -rf /var/lib/apt/lists/*

# set language
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8
ENV LC_ALL en_US.UTF-8

# install ruby
ENV RUBY_VERSION "2.5.1"
ENV RUBYGEMS_VERSION 2.7.7
ENV BUNDLER_VERSION 1.16.4

RUN echo 'gem: --no-document' >> /usr/local/etc/gemrc &&\
    mkdir /src && cd /src && git clone https://github.com/rbenv/ruby-build.git --depth 1 &&\
    cd /src/ruby-build && ./install.sh &&\
    cd / && rm -rf /src/ruby-build &&\
    ruby-build $RUBY_VERSION /usr/local/
RUN gem update --system "$RUBYGEMS_VERSION" && \
 gem install bundler --version "$BUNDLER_VERSION" --force

# set path
ENV GEM_HOME /usr/local/bundle
ENV BUNDLE_PATH="$GEM_HOME" \
	BUNDLE_BIN="$GEM_HOME/bin" \
	BUNDLE_SILENCE_ROOT_WARNING=1 \
	BUNDLE_APP_CONFIG="$GEM_HOME"
ENV PATH $BUNDLE_BIN:$PATH
RUN mkdir -p "$GEM_HOME" "$BUNDLE_BIN" && \
 chmod 777 "$GEM_HOME" "$BUNDLE_BIN"

CMD [ "irb" ]
