FROM ruby:2.6.5
RUN apt update
RUN apt install -y nodejs gem git
RUN gem install rails -v 5.2.3
RUN gem install bundler
RUN git clone https://github.com/jiqarbac/testapp.git /opt/app
ONBUILD WORKDIR /opt/app
ONBUILD RUN bundle install
