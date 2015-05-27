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

结构明确的分开了 'source sets' ( `main`, `androidTest` )

例如，添加源组 `paid` 和 `free` 在 src 中，这将成为您的应用程序的付费和免费的两种模式的源代码。

你的项目引用第三方项目库时（例如，library-foobar ），拥有一个顶级包名 `app` 从第三方库项目区分你的应用程序是非常有用的. 然后 `settings.gradle` 不断引用这些库项目，其中 `app/build.gradle` 可以引用。

### Java 包结构 

与后端交互负责网络处理类，放在 `network` 包下面。

一些控制器角色的类是应用程序级别的，同时是接近系统的。 这些类放在 `managers` 包下面。

一些繁杂的数据处理类，比如说 "DateUtils", 放在 `utils` 包下面。

一些自定义的视图放在 `widgets` 包下面。

适配器 Adapter 是在数据和视图之间。然而他们通常需要通过 `getView()` 方法来导出一些视图， 所以你可以将 `adapters` 包放在 `views` 包里面。

总而言之，以最接近用户而不是最接近后端去安排他们。

```
com.futurice.project
├─ activites
├─ network
├─ models
├─ managers
├─ utils
├─ fragments
└─ views
   ├─ adapters
   ├─ actionbar
   ├─ widgets
   └─ notifications
```

### Gradle 配置

**使用 Maven 或 [JCenter](https://bintray.com/bintray/jcenter)** 依赖方案代替使用导入 jar 包方案, 如果在你的项目中明确使用 jar 文件，那么它们可能成为永久的版本，如 `2.1.1` 。下载 jar 包更新它们是很繁琐的， 这个问题 Maven 很好的解决了，这在 Android Gradle 构建中也是推荐的方法。你可以指定版本的一个范围，如 `2.1.+` , 然后 Maven 会自动升级到制定的最新版本. 例如：

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

每个 Activity, Fragment, Adapter 之类的文件中需要打印最好以各自文件名为 Log 标识。

如:

```
TAG 定义

private final static String TAG = ExampleClass.class.getSimpleName();

Log.d(TAG, logMessage);

```

### 命名

##### 变量名

以 `m` 开头的驼峰命名规则。

例如: `mExample`

尽量不要用 `_` 下划线命名。

##### 常量

例如:  `private static final int TYPE_FOO_BAR = 1;`

##### 参数名

驼峰命名规则。

例如: `fooBar`

##### 方法名

驼峰命名规则。

例如: `fooBar`

### 资源文件 Resources

**命名** 遵循前缀表明类型的习惯，形如 `type_foo_bar.xml`。

例如：`fragment_contact_details.xml`, `view_primary_button.xml`, `activity_main.xml`.

**ID** 同样前缀表明类型的习惯，如 '@+id/tx_foo_bar'

#### 颜色

统一由设计给出颜色定义。开发者不允许定义颜色。

#### 图片

统一由设计给出图片命名。

### 注释

- Model 中的字段需要有注释
- 对于较复杂的逻辑或重要代码块，尽量加上注释

##### 注释方式

例如：

```
  /**
   * Initializes this store with the given context.
   */
  private void initWithContext(Context context, String sharedPrefsName) {
    // Time ourselves
    long start = SystemClock.uptimeMillis();
  }
```
对于注释的态度要想写文档一样，这样团队的其他人容易明白代码的意图和想法。注释还是一种团队的离线交流方式。

##### 文字提示

所有文字提示，都应该使用 `strings.xml` 配置文件。

