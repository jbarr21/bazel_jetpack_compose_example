workspace(name = "bazel_jetpack_compose_example")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

_KOTLIN_COMPILER_VERSION = "1.8.20"

_COMPOSE_COMPILER_VERSION = "1.4.6"
_COMPOSE_VERSION = "1.3.0"

## JVM External

_RULES_JVM_EXTERNAL_VERSION = "4.5"

_RULES_JVM_EXTERNAL_SHA = "b17d7388feb9bfa7f2fa09031b32707df529f26c91ab9e5d909eb1676badd9a6"

http_archive(
    name = "rules_jvm_external",
    sha256 = _RULES_JVM_EXTERNAL_SHA,
    strip_prefix = "rules_jvm_external-{}".format(_RULES_JVM_EXTERNAL_VERSION),
    urls = [
        "https://github.com/bazelbuild/rules_jvm_external/archive/{}.zip".format(_RULES_JVM_EXTERNAL_VERSION),
    ],
)

load("@rules_jvm_external//:defs.bzl", "maven_install")

maven_install(
    artifacts = [
        "org.jetbrains.kotlin:kotlin-stdlib:{}".format(_KOTLIN_COMPILER_VERSION),
        "androidx.core:core-ktx:1.6.0",
        "androidx.appcompat:appcompat:1.3.1",
        "com.google.android.material:material:1.4.0",
        "androidx.activity:activity-compose:1.5.1",
        "androidx.compose.material:material:{}".format(_COMPOSE_VERSION),
        "androidx.compose.ui:ui:{}".format(_COMPOSE_VERSION),
        "androidx.compose.ui:ui-tooling:{}".format(_COMPOSE_VERSION),
        "androidx.compose.compiler:compiler:{}".format(_COMPOSE_COMPILER_VERSION),
        "androidx.compose.runtime:runtime:{}".format(_COMPOSE_VERSION),
        "com.uber.rib:rib-android-compose:0.12.0",
    ],
    override_targets = {
        # "org.jetbrains.kotlinx:kotlinx-coroutines-core-jvm": "@//:kotlinx_coroutines_core_jvm",
    },
    repositories = [
        "https://maven.google.com",
        "https://repo1.maven.org/maven2",
    ],
)

# Secondary maven repository used mainly for workarounds
maven_install(
    name = "maven_secondary",
    artifacts = [
        # Workaround to add missing 'sun.misc' dependencies to 'kotlinx-coroutines-core-jvm' artifact
        # Check root BUILD file and 'override_targets' arg of a primary 'maven_install'
        "org.jetbrains.kotlinx:kotlinx-coroutines-core-jvm:1.5.1",
    ],
    fetch_sources = True,
    repositories = ["https://repo1.maven.org/maven2"],
)

## Android

_RULES_ANDROID_VERSION = "0.1.1"

_RULES_ANDROID_SHA = "cd06d15dd8bb59926e4d65f9003bfc20f9da4b2519985c27e190cddc8b7a7806"

http_archive(
    name = "build_bazel_rules_android",
    sha256 = _RULES_ANDROID_SHA,
    strip_prefix = "rules_android-{}".format(_RULES_ANDROID_VERSION),
    urls = [
        "https://github.com/bazelbuild/rules_android/archive/v{}.zip".format(_RULES_ANDROID_VERSION),
    ],
)

load("@build_bazel_rules_android//android:rules.bzl", "android_sdk_repository")

android_sdk_repository(
    name = "androidsdk",
    api_level = 33,
    build_tools_version = "33.0.0",
)

## Kotlin

http_archive(
    name = "io_bazel_rules_kotlin",
    sha256 = "01293740a16e474669aba5b5a1fe3d368de5832442f164e4fbfc566815a8bc3a",
    urls = ["https://github.com/bazelbuild/rules_kotlin/releases/download/v1.8/rules_kotlin_release.tgz"],
)

load("@io_bazel_rules_kotlin//kotlin:repositories.bzl", "kotlin_repositories", "kotlinc_version")

kotlin_repositories(
    compiler_release = kotlinc_version(
        release = "1.8.20",
        sha256 = "10df74c3c6e2eafd4c7a5572352d37cbe41774996e42de627023cb4c82b50ae4",
    ),
)

register_toolchains("//:kotlin_toolchain")

# Skylib

http_archive(
    name = "bazel_skylib",
    sha256 = "c6966ec828da198c5d9adbaa94c05e3a1c7f21bd012a0b29ba8ddbccb2c93b0d",
    urls = [
        "https://github.com/bazelbuild/bazel-skylib/releases/download/1.1.1/bazel-skylib-1.1.1.tar.gz",
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-skylib/releases/download/1.1.1/bazel-skylib-1.1.1.tar.gz",
    ],
)
