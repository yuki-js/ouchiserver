FROM debian:stable-slim

ENV LANG C.UTF-8

ENV DEBIAN_FRONTEND noninteractive

RUN mkdir jupyter
WORKDIR /jupyter

RUN apt-get update -y && apt-get upgrade -y
RUN apt-get install -y --no-install-recommends python3-pip build-essential python3-dev libzmq3-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN pip3 install --upgrade pip setuptools
RUN pip3 install jupyter && pip3 install jupyterlab

# Jupyter のデフォルトポート
EXPOSE 8888

CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--allow-root"]
