FROM iexechub/iexec-gramine-base:0.10.0

RUN apt-get update \
    && apt-get install -y curl \
    && curl -fsSL https://deb.nodesource.com/setup_14.x | bash - \
    && apt-get install -y nodejs \
    && rm -rf /var/lib/apt/lists/*

ARG SOURCE_DIR=src
ARG GRAMINE_DIR=gramine

# get the code of app to /workplace/app
COPY $SOURCE_DIR/app.js /workplace/app

# set the main function for node app, no need for binnary app
RUN sed -i "s#MAIN_FUNC=#MAIN_FUNC=/workplace/app/app.js#" /apploader.sh

WORKDIR /workplace/app

### install needed node dependencies (needs to be ran after WORKDIR has been specified)
RUN npm install figlet@1.x

RUN ls /

# Copy the manifest to use from within the base image
# or create your own
RUN cp /common-manifests/nodejs.entrypoint.manifest /entrypoint.manifest

# Finalize app (finalize manifest and sign app)
RUN /finalize-app.sh
