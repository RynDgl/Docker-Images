FROM centos:latest

RUN yum update -y \
    && yum install -y \
        epel-release \
        wget \
        which \
        tar \
        xz \
    && yum groupinstall -y "Development Tools"

CMD ["/bin/bash"]