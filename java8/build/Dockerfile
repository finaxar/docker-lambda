FROM lambci/lambda-base:build

ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin \
    LD_LIBRARY_PATH=/lib64:/usr/lib64:/var/runtime:/var/runtime/lib:/var/task:/var/task/lib \
    AWS_EXECUTION_ENV=AWS_Lambda_java8

RUN rm -rf /var/runtime /var/lang && \
  curl https://lambci.s3.amazonaws.com/fs/java8.tgz | tar -zx -C / && \
  yum remove -y java-1.8.0-openjdk java-1.8.0-openjdk-headless && \
  yum install -y java-1.8.0-openjdk java-1.8.0-openjdk-devel

# The Java version on Lambda seems to be slightly different to the latest available
