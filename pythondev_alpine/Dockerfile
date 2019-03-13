## To build an image using this docker file
## 1. cd to folder of this docker file
## 2. docker build -t zimage:py-alpine . #don't forget the ending .
## 3. docker run -it --name=py-ubuntu \ 
##                   -v /fullpath/to/host/workdir:/docker/workdir \ 
##                   -v /tmp/.X11-unix:/tmp/.X11-unix \ 
##                   -p 8888:8888  \
##                   -e DISPLAY=192.168.0.105:0 \
##                    zimage:py-alpine
## When you want to re-start the docker container after exiting it, run:
## 4. docker start -i py-alpine

FROM alpine:3.9

LABEL MAINTAINER="ZLI"

RUN apk add --no-cache python3 && \
    python3 -m ensurepip && \
    rm -r /usr/lib/python3.6/ensurepip/ && \
    apk add --no-cache dumb-init musl build-base ca-certificates openblas gfortran python3-dev && \
    apk add --no-cache libpng freetype-dev python3-tkinter cmake && \
    ln -s /usr/include/locale.h /usr/include/xlocal.h 

RUN apk add --no-cache linux-headers openblas-dev && \
    python3 -m pip install --no-cache-dir --upgrade pip && \
    python3 -m pip install --no-cache-dir numpy matplotlib jupyter &&  \
    python3 -m pip install --no-cache-dir cvxpy

EXPOSE 8888

#TODO don't use root, create a non-privilaged user
COPY run_jupyter.sh /
COPY jupyter_notebook_config.py /root/.jupyter/

RUN chmod +x /run_jupyter.sh

CMD /bin/ash