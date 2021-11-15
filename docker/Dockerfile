FROM node:14-alpine

RUN apk add --update --no-cache \
                            git \
                            libzmq \
                            zeromq-dev \
                            python \
                            make \
                            g++

WORKDIR /insight

# Copy core-node
RUN git clone --branch master --single-branch --depth 1 https://github.com/skeincurrency/core-node.git .

# Copy config file
COPY core-node.json .

ARG VERSION

# Install npm packages
RUN npm ci

# Install Insight API module
RUN bin/core-node install @skeincurrency/insight-api@${VERSION}

FROM node:14-alpine

LABEL maintainer="SkeinCurrency Developers <dev@dash.org>"
LABEL description="Dockerised Insight API"

WORKDIR /insight

# Copy project files
COPY --from=0 /insight/ .

EXPOSE 3001

CMD ["bin/core-node", "start"]
