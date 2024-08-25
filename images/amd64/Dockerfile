FROM alpine:3.20 as downloader1

RUN apk add --no-cache curl
RUN wget -O kubectl "https://dl.k8s.io/release/$(wget -qO- https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

FROM alpine:3.20 as downloader2
RUN wget -O yq "https://github.com/mikefarah/yq/releases/download/v4.44.3/yq_linux_amd64"

#-------------------------------------------------------------------
FROM alpine:3.20
LABEL maintainer "Yellow Shine <sammy.huang@zilliz.com>"

COPY bin/tkn-linux-amd64 /usr/local/bin/tkn
RUN chmod +x /usr/local/bin/tkn

COPY --from=downloader1 kubectl /usr/local/bin/kubectl
RUN chmod +x /usr/local/bin/kubectl

COPY --from=downloader2 yq /usr/local/bin/yq
RUN chmod +x /usr/local/bin/yq

