FROM scratch
MAINTAINER https://github.com/RynDgl
ADD centos-7-docker.tar.xz /

LABEL name="CentOS Base Image" \
    build-date="20190323"
RUN yum update -y && yum install -y xorg-x11-server-Xvfb

CMD ["/bin/bash"]
 