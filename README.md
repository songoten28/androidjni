JNI_with_prebuilt_shared_library

This is example for JNI

Usage: 
1
- cd foolib_src && ndk-build
2 
 - Copy *.so file from foolib_src/libs to jni_src/jni/lib/<ABI>  (ABI can be x86, arm64v-...
3 
  - cd jni_src && ndk-build
4
  - Copy *.so file in jni_src/libs to jniLibs in [main] Android Studio
  
5 
in app build.gradle

    splits {
        abi {
            reset()
            universalApk false  // If true, also generate a universal APK
            include "armeabi-v7a", "arm64-v8a", "x86"
        }
    }

    sourceSets { main { jni.srcDirs = ['src/main/jni/','src/main/jniLibs/'] } }
  
    defaultConfig {
       ....
        ndk.abiFilters 'armeabi-v7a','arm64-v8a','x86','x86_64'
    }
