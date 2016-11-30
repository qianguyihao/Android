
> 以下为Android Studio的常用配置，如果要查看完整的图文教程，请查看本人的博客：[第一次使用Android Studio时你应该知道的一切配置](http://www.cnblogs.com/smyhvae/p/4390905.html)



## Android Stuio的各种配置settings


### 代码自动提示&自动补齐 


AS默认具有代码自动补齐的功能，自动补齐的设置如下：

Editor --> General --> Code Completion，将`Autopopup code completion`选中即可。







## 历史版本


### 2016-10-10

- AS版本：2.1.2

新建一个工程，默认的gradle代码如下。


整个project的 gradle：

```bash
// Top-level build file where you can add configuration options common to all sub-projects/modules.

buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:2.1.2'

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}

allprojects {
    repositories {
        jcenter()
    }
}

task clean(type: Delete) {
    delete rootProject.buildDir
}
```

app这个module的 gradle：

```bash
apply plugin: 'com.android.application'

android {
    compileSdkVersion 23
    buildToolsVersion "23.0.3"

    defaultConfig {
        applicationId "com.smyhvae.test01"
        minSdkVersion 23
        targetSdkVersion 23
        versionCode 1
        versionName "1.0"
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
}

dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    testCompile 'junit:junit:4.12'
    compile 'com.android.support:appcompat-v7:23.4.0'
}
```






















