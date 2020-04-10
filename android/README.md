## Dockerfile for android

### Dockerfile takes three ARGs:

   1. ANDROID_SDK_TOOLS
   2. ANDROID_COMPILE_SDK
   3. ANDROID_BUILD_TOOLS

### For build use this command with your ARG versions

```
docker build -t okassov/android-openjdk8:28.0.3 \
--build-arg ANDROID_SDK_TOOLS=4333796 \
--build-arg ANDROID_COMPILE_SDK=28 \
--build-arg ANDROID_BUILD_TOOLS=28.0.3 .
```


