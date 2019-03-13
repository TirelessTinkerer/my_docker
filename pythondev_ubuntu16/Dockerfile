## To build an image using this docker file
## 1. cd to folder of this docker file
## 2. docker build -t zimage:py-ubuntu . #don't forget the ending .
## 3. docker run -it --name=py-ubuntu \ 
##                   -v /fullpath/to/host/workdir:/docker/workdir \ 
##                   -v /tmp/.X11-unix:/tmp/.X11-unix \ 
##                   -p 8888:8888  \
##                   -e DISPLAY=192.168.0.105:0 \
##                    zimage:py-ubuntu
## When you want to re-start the docker container after exiting it, run:
## 4. docker start -i py-ubuntu

FROM ubuntu:16.04

LABEL MAINTAINER="ZLI"

RUN apt-get update && \ 
    apt-get install -y python3 python3-pip git python3-tk && \ 
    apt-get clean && \ 
    rm -rf /var/lib/apt/lists/*

RUN python3 -m pip install --no-cache-dir --upgrade pip && \
    python3 -m pip install --no-cache-dir numpy scipy matplotlib jupyter &&  \
    python3 -m pip install --no-cache-dir cvxpy

EXPOSE 8888

#TODO don't use root, create a non-privilaged user
COPY run_jupyter.sh /
COPY jupyter_notebook_config.py /root/.jupyter/

RUN chmod +x /run_jupyter.sh

CMD /bin/bash