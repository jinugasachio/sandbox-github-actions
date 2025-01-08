FROM alpine:3.21.2

ARG GLIBC_VER=2.34-r0
RUN apk update \
  && apk --no-cache add bash curl git jq \
  # install awscli
  && curl -sL https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub -o /etc/apk/keys/sgerrand.rsa.pub \
  && curl -sLO https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_VER}/glibc-${GLIBC_VER}.apk \
  && curl -sLO https://github.com/sgerrand/alpine-pkg-glibc/releases/download/${GLIBC_VER}/glibc-bin-${GLIBC_VER}.apk \
  && apk add --no-cache glibc-${GLIBC_VER}.apk glibc-bin-${GLIBC_VER}.apk \
  && curl -sL https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip -o awscliv2.zip \
  && unzip awscliv2.zip \
  && aws/install \
  # remove unnecesary files
  && rm -rf \
      awscliv2.zip \
      aws \ 
      /usr/local/aws-cli/v2/current/dist/aws_completer \
      /usr/local/aws-cli/v2/current/dist/awscli/data/ac.index \
      /usr/local/aws-cli/v2/current/dist/awscli/examples \
      glibc-*.apk \
  && find /usr/local/aws-cli/v2/current/dist/awscli/botocore/data -name examples-1.json -delete \
  && rm -rf /var/cache/apk/*

CMD ["/bin/bash"]
ENTRYPOINT [""]
