# Copyright 2016 The Kubernetes Authors.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# Includes git, gcloud, and bazel.
FROM ubuntu:16.04
MAINTAINER spxtr@google.com

RUN apt-get update && apt-get install -y \
    build-essential \
    openjdk-8-jdk \
    pkg-config \
    zip \
    unzip \
    zlib1g-dev \
    bash-completion \
    git \
    wget \
    python \
    python-pip && \
    apt-get clean

ENV BAZEL_VERSION 0.4.5
RUN wget "https://github.com/bazelbuild/bazel/releases/download/${BAZEL_VERSION}/bazel_${BAZEL_VERSION}-linux-x86_64.deb" && \
    dpkg -i "bazel_${BAZEL_VERSION}-linux-x86_64.deb" && \
    rm "bazel_${BAZEL_VERSION}-linux-x86_64.deb"

ENV GCLOUD_VERSION 149.0.0
RUN wget https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-$GCLOUD_VERSION-linux-x86_64.tar.gz && \
    tar xf google-cloud-sdk-$GCLOUD_VERSION-linux-x86_64.tar.gz && \
    rm google-cloud-sdk-$GCLOUD_VERSION-linux-x86_64.tar.gz && \
    ./google-cloud-sdk/install.sh
ENV PATH "/google-cloud-sdk/bin:${PATH}"

ENV NODE_VERSION 6.10.0
RUN wget https://nodejs.org/dist/v${NODE_VERSION}/node-v${NODE_VERSION}-linux-x64.tar.xz && \
    tar xf node-v${NODE_VERSION}-linux-x64.tar.xz --strip-components=1 -C /usr && \
    rm node-v${NODE_VERSION}-linux-x64.tar.xz && \
    npm install -g mocha

WORKDIR /workspace
ADD runner /
ENTRYPOINT ["/bin/bash", "/runner"]
