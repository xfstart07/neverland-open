# Android 开发最佳实践

[参考 Futurice Android-Best-Practices ](https://github.com/futurice/android-best-practices/blob/master/translations/Chinese/README.cn.md)

### 开发工具

使用 Android Studio + gradle 

### 工程结构

```
new-structure
├─ library-foobar
├─ app
│  ├─ libs
│  ├─ src
│  │  ├─ androidTest
│  │  │  └─ java
│  │  │     └─ com/futurice/project
│  │  └─ main
│  │     ├─ java
│  │     │  └─ com/futurice/project
│  │     ├─ res
│  │     └─ AndroidManifest.xml
│  ├─ build.gradle
│  └─ proguard-rules.pro
├─ build.gradle
└─ settings.gradle
```

主要的区别在于，新的结构明确的分开了'source sets' ( `main`, `androidTest` )，Gradle的一个理念。 你可以做到，例如，添加源组 ‘paid’ 和 ‘free’ 在 src 中，这将成为您的应用程序的付费和免费的两种模式的源代码。

你的项目引用第三方项目库时（例如，library-foobar ），拥有一个顶级包名 `app` 从第三方库项目区分你的应用程序是非常有用的。 然后 `settings.gradle` 不断引用这些库项目，其中 `app/build.gradle` 可以引用。

### Gradle 配置

**使用 Maven **依赖方案代替使用导入jar包方案 如果在你的项目中你明确使用 jar 文件，那么它们可能成为永久的版本，如 `2.1.1` .下载 jar 包更新它们是很繁琐的， 这个问题 Maven 很好的解决了，这在 Android Gradle 构建中也是推荐的方法。你可以指定版本的一个范围，如 `2.1.+` ,然后 Maven 会自动升级到制定的最新版本，例如：

```
dependencies {
    compile 'com.netflix.rxjava:rxjava-core:0.19.+'
    compile 'com.netflix.rxjava:rxjava-android:0.19.+'
    compile 'com.fasterxml.jackson.core:jackson-databind:2.4.+'
    compile 'com.fasterxml.jackson.core:jackson-core:2.4.+'
    compile 'com.fasterxml.jackson.core:jackson-annotations:2.4.+'
    compile 'com.squareup.okhttp:okhttp:2.0.+'
    compile 'com.squareup.okhttp:okhttp-urlconnection:2.0.+'
}
```

### 调试

#### Log 打印

每个 Activity, Fragment, Adapter 之类的文件中都以各自文件名为 Log 标识。

如:

```
TAG 定义

private final static String TAG = "ExampleActivity";

Log.debug(TAG, logMessage);

```

