FROM ubuntu:16.04

WORKDIR /scripts
COPY script.sh .
RUN apt-get update && apt-get install -y curl

CMD ["/bin/bash"]
