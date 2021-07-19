# 原创

： python打包apk闪退问题以及美化

# python打包apk闪退问题以及美化

### python打包apk闪退问题以及美化

# 一、闪退问题

## （一）闪退原因

运行出现错误，可以尝试使用源文件在python环境中运行就会发现其错误

## （二）解决方法

我此处的错误在于缺失了某些包，<br/> 类似于Plaggable的这篇博客<br/>
《Buildozer生成的APP闪退+PermissionError故障排除记录》，链接: [Buildozer生成的APP闪退+PermissionError故障排除记录](https://blog.csdn.net/weixin_42269667/article/details/106517353)
.

也是在这篇博客中发现了可能是本来运行时缺少了某些东西（因为自己实在pycharm中编译的，在打包的linux中就没有在试运行了）以及buildozer.spec文件的重要性

buildozer.spec文件内容的具体含义可见<br/> evil-tomato：《使用Buildozer部署Kivy到移动设备上》，<br/>
链接: [使用Buildozer部署Kivy到移动设备上](https://blog.csdn.net/fangxuejiang/article/details/49405277).

## （三）修改的地方

除了必须要修改的app

```
# (str) Title of your application 
title = Photos
#(str) Package name 更改2
package.name = photos
# (str) Package domain (needed for android/ios packaging)

```

title自然不用说了<br/> 而package name 和Package domain 是什么了？

就是下面这个东西，其实就是包名，直接在手机中应该是找不到的，因为需要root权限，我这个实在夜神模拟器中找到了，因为自带root<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200814163049105.png#pic_center"/><br/>
进入是会询问权限问题<br/> <img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200814163257416.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3B5dGhvbl9fcmVwb3J0ZWQ=,size_16,color_FFFFFF,t_70#pic_center"/><br/>
一般是用不上，只有在调试的时候需要拥有这个权限，只有这样才能使用adb命令进入根目录（具体的我没有实测，因为是在模拟器上完成的，不过之前试图修改过系统证书，发现大部分涉及安卓调试的都是需要root权限的）<br/>
将之前缺失的requests以及lxml添加进去后即可<br/> 即

```
# (list) Application requirements 更改4
requirements =python3,kivy,requests,lxml，

```

然后是网络权限

```
# (list) Permissions
android.permissions = INTERNET

```

# 二、美化问题

美化其实就是将图标以及导入的图片换掉

```
# (str) Presplash of the application
presplash.filename = %(source.dir)s/hourse.png

# (str) Icon of the application
icon.filename = %(source.dir)s/title.png

```

均为512*512格式的png图片

## （一）打包后的图标

<img alt="在这里插入图片描述" src="https://img-blog.csdnimg.cn/20200814165643519.png#pic_center"/><br/> 第三个first_movie就是更换图标后的app

## （二）运行界面

## 三、完整的buildozer.spec文件

修改的地方就是上述地方

```
[app]

# (str) Title of your application
title = first_movie

# (str) Package name
package.name = requests_first_movie

# (str) Package domain (needed for android/ios packaging)
package.domain = org.kivydev

# (str) Source code where the main.py live
source.dir =.

# (list) Source files to include (let empty to include all the files)
source.include_exts = py, png, jpg, kv, atlas, ttf

# (list) List of inclusions using pattern matching
# source.include_patterns = assets/*,images/*.png

# (list) Source files to exclude (let empty to not exclude anything)
# source.exclude_exts = spec

# (list) List of directory to exclude (let empty to not exclude anything)
# source.exclude_dirs = tests, bin

# (list) List of exclusions using pattern matching
# source.exclude_patterns = license,images/*/*.jpg

# (str) Application versioning (method 1)
version = 0.1

# (str) Application versioning (method 2)
# version.regex = __version__ = ['"](.*)['"]
# version.filename = %(source.dir)s/main.py

# (list) Application requirements
# comma separated e.g. requirements = sqlite3,kivy
requirements = python3, kivy, requests, lxml

# (str) Custom source folders for requirements
# Sets custom source for any requirements with recipes
# requirements.source.kivy = ../../kivy

# (list) Garden requirements
# garden_requirements =

# (str) Presplash of the application
presplash.filename = % (source.dir)
s / hourse.png

# (str) Icon of the application
icon.filename = % (source.dir)
s / title.png

# (str) Supported orientation (one of landscape, sensorLandscape, portrait or all)
orientation = portrait

# (list) List of service to declare
# services = NAME:ENTRYPOINT_TO_PY,NAME2:ENTRYPOINT2_TO_PY

#
# OSX Specific
#

#
# author = © Copyright Info

# change the major version of python used by the app
osx.python_version = 3

# Kivy version to use
osx.kivy_version = 1.9
.1

#
# Android specific
#

# (bool) Indicate if the application should be fullscreen or not
fullscreen = 0

# (string) Presplash background color (for new android toolchain)
# Supported formats are: #RRGGBB #AARRGGBB or one of the following names:
# red, blue, green, black, white, gray, cyan, magenta, yellow, lightgray,
# darkgray, grey, lightgrey, darkgrey, aqua, fuchsia, lime, maroon, navy,
# olive, purple, silver, teal.
# android.presplash_color = #FFFFFF

# (list) Permissions
android.permissions = INTERNET

# (int) Target Android API, should be as high as possible.
android.api = 27

# (int) Minimum API your APK will support.
android.minapi = 21

# (int) Android SDK version to use
# android.sdk = 27

# (str) Android NDK version to use
android.ndk = 19
c

# (int) Android NDK API to use. This is the minimum API your app will support, it should usually match android.minapi.
android.ndk_api = 21

# (bool) Use --private data storage (True) or --dir public storage (False)
# android.private_storage = True

# (str) Android NDK directory (if empty, it will be automatically downloaded.)
android.ndk_path = / home / kivydev / andr / android - ndk - r19c

# (str) Android SDK directory (if empty, it will be automatically downloaded.)
android.sdk_path = / home / kivydev / andr / android - sdk - linux

# (str) ANT directory (if empty, it will be automatically downloaded.)
android.ant_path = / home / kivydev / andr / apache - ant - 1.9
.4

# (bool) If True, then skip trying to update the Android sdk
# This can be useful to avoid excess Internet downloads or save time
# when an update is due and you just want to test/build your package
# android.skip_update = False

# (bool) If True, then automatically accept SDK license
# agreements. This is intended for automation only. If set to False,
# the default, you will be shown the license when first running
# buildozer.
# android.accept_sdk_license = False

# (str) Android entry point, default is ok for Kivy-based app
# android.entrypoint = org.renpy.android.PythonActivity

# (str) Android app theme, default is ok for Kivy-based app
# android.apptheme = "@android:style/Theme.NoTitleBar"

# (list) Pattern to whitelist for the whole project
# android.whitelist =

# (str) Path to a custom whitelist file
# android.whitelist_src =

# (str) Path to a custom blacklist file
# android.blacklist_src =

# (list) List of Java .jar files to add to the libs so that pyjnius can access
# their classes. Don't add jars that you do not need, since extra jars can slow
# down the build process. Allows wildcards matching, for example:
# OUYA-ODK/libs/*.jar
# android.add_jars = foo.jar,bar.jar,path/to/more/*.jar

# (list) List of Java files to add to the android project (can be java or a
# directory containing the files)
# android.add_src =

# (list) Android AAR archives to add (currently works only with sdl2_gradle
# bootstrap)
# android.add_aars =

# (list) Gradle dependencies to add (currently works only with sdl2_gradle
# bootstrap)
# android.gradle_dependencies =

# (list) add java compile options
# this can for example be necessary when importing certain java libraries using the 'android.gradle_dependencies' option
# see https://developer.android.com/studio/write/java8-support for further information
# android.add_compile_options = "sourceCompatibility = 1.8", "targetCompatibility = 1.8"

# (list) Gradle repositories to add {can be necessary for some android.gradle_dependencies}
# please enclose in double quotes 
# e.g. android.gradle_repositories = "maven { url 'https://kotlin.bintray.com/ktor' }"
# android.add_gradle_repositories =

# (list) packaging options to add 
# see https://google.github.io/android-gradle-dsl/current/com.android.build.gradle.internal.dsl.PackagingOptions.html
# can be necessary to solve conflicts in gradle_dependencies
# please enclose in double quotes 
# e.g. android.add_packaging_options = "exclude 'META-INF/common.kotlin_module'", "exclude 'META-INF/*.kotlin_module'"
# android.add_gradle_repositories =

# (list) Java classes to add as activities to the manifest.
# android.add_activites = com.example.ExampleActivity

# (str) OUYA Console category. Should be one of GAME or APP
# If you leave this blank, OUYA support will not be enabled
# android.ouya.category = GAME

# (str) Filename of OUYA Console icon. It must be a 732x412 png image.
# android.ouya.icon.filename = %(source.dir)s/data/ouya_icon.png

# (str) XML file to include as an intent filters in &lt;activity&gt; tag
# android.manifest.intent_filters =

# (str) launchMode to set for the main activity
# android.manifest.launch_mode = standard

# (list) Android additional libraries to copy into libs/armeabi
# android.add_libs_armeabi = libs/android/*.so
# android.add_libs_armeabi_v7a = libs/android-v7/*.so
# android.add_libs_arm64_v8a = libs/android-v8/*.so
# android.add_libs_x86 = libs/android-x86/*.so
# android.add_libs_mips = libs/android-mips/*.so

# (bool) Indicate whether the screen should stay on
# Don't forget to add the WAKE_LOCK permission if you set this to True
# android.wakelock = False

# (list) Android application meta-data to set (key=value format)
# android.meta_data =

# (list) Android library project to add (will be added in the
# project.properties automatically.)
# android.library_references =

# (list) Android shared libraries which will be added to AndroidManifest.xml using &lt;uses-library&gt; tag
# android.uses_library =

# (str) Android logcat filters to use
# android.logcat_filters = *:S python:D

# (bool) Copy library instead of making a libpymodules.so
# android.copy_libs = 1

# (str) The Android arch to build for, choices: armeabi-v7a, arm64-v8a, x86, x86_64
android.arch = armeabi - v7a

#
# Python for android (p4a) specific
#

# (str) python-for-android fork to use, defaults to upstream (kivy)
# p4a.fork = kivy

# (str) python-for-android branch to use, defaults to master
# p4a.branch = master

# (str) python-for-android git clone directory (if empty, it will be automatically cloned from github)
# p4a.source_dir = 

# (str) The directory in which python-for-android should look for your own build recipes (if any)
# p4a.local_recipes =

# (str) Filename to the hook for p4a
# p4a.hook =

# (str) Bootstrap to use for android builds
# p4a.bootstrap = sdl2

# (int) port number to specify an explicit --port= p4a argument (eg for bootstrap flask)
# p4a.port =

#
# iOS specific
#

# (str) Path to a custom kivy-ios folder
# ios.kivy_ios_dir = ../kivy-ios
# Alternately, specify the URL and branch of a git checkout:
ios.kivy_ios_url = https: // github.com / kivy / kivy - ios
ios.kivy_ios_branch = master

# Another platform dependency: ios-deploy
# Uncomment to use a custom checkout
# ios.ios_deploy_dir = ../ios_deploy
# Or specify URL and branch
ios.ios_deploy_url = https: // github.com / phonegap / ios - deploy
ios.ios_deploy_branch = 1.7
.0

# (str) Name of the certificate to use for signing the debug version
# Get a list of available identities: buildozer ios list_identities
# ios.codesign.debug = "iPhone Developer: &lt;lastname&gt; &lt;firstname&gt; (&lt;hexstring&gt;)"

# (str) Name of the certificate to use for signing the release version
# ios.codesign.release = %(ios.codesign.debug)s

[buildozer]

# (int) Log level (0 = error only, 1 = info, 2 = debug (with command output))
log_level = 2

# (int) Display warning if buildozer is run as root (0 = False, 1 = True)
warn_on_root = 1

# (str) Path to build artifact storage, absolute or relative to spec file
build_dir = / home / kivydev / test /.buildozer

# (str) Path to build output (i.e. .apk, .ipa) storage
# bin_dir = ./bin

#    -----------------------------------------------------------------------------
#    List as sections
#
#    You can define all the "list" as [section:key].
#    Each line will be considered as a option to the list.
#    Let's take [app] / source.exclude_patterns.
#    Instead of doing:
#
# [app]
# source.exclude_patterns = license,data/audio/*.wav,data/images/original/*
#
#    This can be translated into:
#
# [app:source.exclude_patterns]
# license
# data/audio/*.wav
# data/images/original/*
#

#    -----------------------------------------------------------------------------
#    Profiles
#
#    You can extend section / key with a profile
#    For example, you want to deploy a demo version of your application without
#    HD content. You could first change the title to add "(demo)" in the name
#    and extend the excluded directories to remove the HD content.
#
# [app@demo]
# title = My Application (demo)
#
# [app:source.exclude_patterns@demo]
# images/hd/*
#
#    Then, invoke the command line with the "demo" profile:
#
# buildozer --profile demo android debug

```
