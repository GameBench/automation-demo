FROM jenkins/jenkins:latest

USER root

RUN mkdir /Android \
	&& cd /Android \
	&& wget https://dl.google.com/android/repository/platform-tools-latest-linux.zip \
	&& unzip platform-tools-latest-linux.zip \
	&& wget http://storage.googleapis.com/release-application-artifacts/gba-client/gba-client-linux-amd64 \
        && mv gba-client-linux-amd64 /usr/local/bin/gba-client \
	&& chmod +x /usr/local/bin/gba-client \
	&& wget https://github.com/stedolan/jq/releases/download/jq-1.6/jq-linux64 \
	&& mv jq-linux64 /usr/local/bin/jq \
	&& chmod +x /usr/local/bin/jq

USER jenkins
