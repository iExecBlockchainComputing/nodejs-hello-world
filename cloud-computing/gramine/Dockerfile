FROM docker-regis.iex.ec/iexec-graphene-base:0.6.0

RUN apt-get update \
    && apt-get install -y curl \
    && curl -fsSL https://deb.nodesource.com/setup_14.x | bash - \
    && apt-get install -y nodejs

ARG SOURCE_DIR=src
ARG GRAMINE_DIR=gramine

# get the code of app to /workplace/app
COPY $SOURCE_DIR/app.js /workplace/app

# set the main function for node app, no need for binnary app
RUN sed -i "s#MAIN_FUNC=#MAIN_FUNC=/workplace/app/app.js#" /apploader.sh

WORKDIR /workplace/app

### install needed node dependencies (needs to be ran after WORKDIR has been specified)
RUN npm install figlet@1.x

# finalize manifest
COPY $GRAMINE_DIR/entrypoint.manifest /
RUN python3 -B /var/tmp/finalize_manifest.py

# Dummy key

# sign image
RUN openssl genrsa -3 -out /signer-key.pem 3072
RUN /graphene/python/graphene-sgx-sign \
        -libpal /graphene/Runtime/libpal-Linux-SGX.so \
        -key /signer-key.pem \
        -manifest /entrypoint.manifest \
        -output /entrypoint.manifest.sgx

RUN rm -rf /var/tmp/* \
    && rm -rf /graphene/python/graphene-sgx-sign /graphene/python/graphenelibos/sgx_sign.py \
    && rm -rf /signer-key.pem \
    && rm -rf /var/lib/apt/lists/*
