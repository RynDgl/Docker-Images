FROM scratch
MAINTAINER https://github.com/RynDgl
ADD centos-7-docker.tar.xz /

LABEL name="CentOS Base Image" \
    build-date="20190323"
RUN yum update -y & yum install -y xvfb

RUN Xvfb :50 -screen 0 1024x768x16 &> xvfb.log  &
RUN DISPLAY=50.0

CMD ["export","DISPLAY"]

ENTRYPOINT ["/bin/bash"]
 