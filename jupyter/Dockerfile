FROM debian:stable-slim

ENV LANG C.UTF-8

ENV DEBIAN_FRONTEND noninteractive

RUN mkdir jupyter
WORKDIR /jupyter

RUN apt-get update -y && apt-get upgrade -y \
    && apt-get install -y --no-install-recommends python3 \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN pip3 install --upgrade pip setuptools
RUN pip3 install jupyter

# Jupyter のデフォルトポート
EXPOSE 8888

CMD ["jupyter", "notebook"]
