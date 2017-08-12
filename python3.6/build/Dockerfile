FROM lambci/lambda-base:build

ENV PATH=/var/lang/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin \
    LD_LIBRARY_PATH=/var/lang/lib:/lib64:/usr/lib64:/var/runtime:/var/runtime/lib:/var/task:/var/task/lib \
    AWS_EXECUTION_ENV=AWS_Lambda_python3.6 \
    PYTHONPATH=/var/runtime

RUN rm -rf /var/runtime /var/lang && \
  curl https://lambci.s3.amazonaws.com/fs/python3.6.tgz | tar -xz -C / && \
  curl https://www.python.org/ftp/python/3.6.1/Python-3.6.1.tar.xz | tar -xJ && \
  cd Python-3.6.1 && \
  ./configure --prefix=/var/lang && \
  make -j$(getconf _NPROCESSORS_ONLN) libinstall inclinstall && \
  cd .. && \
  rm -rf Python-3.6.1 && \
  pip3 install awscli --no-cache-dir

RUN yum -y update && \
    yum -y install sudo openssh-server g++ gcc glibc-devel make && \
    yum clean all && \
    sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config && \
    sed -ri 's/#UsePAM no/UsePAM no/g' /etc/ssh/sshd_config && \
    echo "%wheel ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers && \
    useradd -u 1000 -G users,wheel -d /home/user --shell /bin/bash -m user && \
    usermod -p "*" user && \
    sed -i 's/requiretty/!requiretty/g' /etc/sudoers && \
    mkdir /projects && chown -R user:user /projects

EXPOSE 8080 

WORKDIR /projects

USER user

CMD tailf /dev/null
