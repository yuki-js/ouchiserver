FROM debian:stretch-slim

ENV LANG C.UTF-8

ENV DEBIAN_FRONTEND noninteractive

ENV APP_ROOT /usr/src
WORKDIR $APP_ROOT
COPY src $APP_ROOT

RUN apt-get update -y && apt-get update -y \
    && apt-get install -y --no-install-recommends python3 \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN pip3 install --upgrade pip setuptools
RUN pip3 install jupyter

# Jupyter のデフォルトポート
EXPOSE 8888

CMD ["jupyter", "notebook"]
