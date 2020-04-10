FROM openjdk:8-jdk
MAINTAINER Okassov Marat <okasov.marat@gmail.com>

#Arguments for install SDK
ARG ANDROID_SDK_TOOLS
ARG ANDROID_COMPILE_SDK
ARG ANDROID_BUILD_TOOLS

#Install required packages and libraries
RUN apt-get --quiet update -y \
  && apt-get --quiet install -y lib32stdc++6 lib32z1 ca-certificates \
  && /usr/sbin/update-ca-certificates

#Install android SDK
RUN wget --quiet --output-document=android-sdk.zip \
    https://dl.google.com/android/repository/sdk-tools-linux-$ANDROID_SDK_TOOLS.zip \
  && unzip -d android-sdk-linux android-sdk.zip \
  && echo y | android-sdk-linux/tools/bin/sdkmanager \
    "platforms;android-$ANDROID_COMPILE_SDK" > /dev/null \
  && echo y | android-sdk-linux/tools/bin/sdkmanager \
    "platform-tools" > /dev/null \
  && echo y | android-sdk-linux/tools/bin/sdkmanager \
    "build-tools;$ANDROID_BUILD_TOOLS" > /dev/null \
  && /bin/bash -c 'set -o pipefail' \
  && yes | android-sdk-linux/tools/bin/sdkmanager --licenses \
  && /bin/bash -c 'set +o pipefail' \
  && rm -rf *.zip

#Add SDK environments 
ENV ANDROID_HOME=$PWD/android-sdk-linux
ENV PATH=$PATH:$PWD/android-sdk-linux/platform-tools/

