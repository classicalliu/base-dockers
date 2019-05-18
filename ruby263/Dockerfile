FROM classicalliu/ruby-base:0.3

# install ruby
ENV RUBY_VERSION "2.6.3"
ENV RUBYGEMS_VERSION 2.7.7
ENV BUNDLER_VERSION 2.0.1

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
