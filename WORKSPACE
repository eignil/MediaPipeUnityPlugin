workspace(name = "mediapipe_api")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "bazel_skylib",
    sha256 = "1c531376ac7e5a180e0237938a2536de0c54d93f5c278634818e0efc952dd56c",
    type = "tar.gz",
    urls = [
        "https://github.com/bazelbuild/bazel-skylib/releases/download/1.0.3/bazel-skylib-1.0.3.tar.gz",
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-skylib/releases/download/1.0.3/bazel-skylib-1.0.3.tar.gz",
    ],
)

load("@bazel_skylib//:workspace.bzl", "bazel_skylib_workspace")

bazel_skylib_workspace()

load("@bazel_skylib//lib:versions.bzl", "versions")

versions.check(minimum_bazel_version = "4.2.1")

http_archive(
    name = "rules_pkg",
    sha256 = "62eeb544ff1ef41d786e329e1536c1d541bb9bcad27ae984d57f18f314018e66",
    url = "https://github.com/bazelbuild/rules_pkg/releases/download/0.6.0/rules_pkg-0.6.0.tar.gz",
)

load("@rules_pkg//:deps.bzl", "rules_pkg_dependencies")

rules_pkg_dependencies()

http_archive(
    name = "emsdk",
    sha256 = "8978a12172028542c1c4007745e5421cb018842ebf77dfc0f8555d1ae9b09234",
    strip_prefix = "emsdk-8e7b714a0b2137caca4a212c003f4eb9b9ba9667/bazel",
    url = "https://github.com/emscripten-core/emsdk/archive/8e7b714a0b2137caca4a212c003f4eb9b9ba9667.tar.gz",
    patch_args = [
        "-p1",
    ],
    patches = [
        "@//third_party:emsdk_bitcode_support.diff",
    ],
)

load("@emsdk//:deps.bzl", emsdk_deps = "deps")

emsdk_deps()

load("@emsdk//:emscripten_deps.bzl", emsdk_emscripten_deps = "emscripten_deps")

emsdk_emscripten_deps(emscripten_version = "2.0.22")

# mediapipe
http_archive(
    name = "com_google_mediapipe",
    patch_args = [
        "-p1",
    ],
    patches = [
        "@//third_party:mediapipe_opencv.diff",
        "@//third_party:mediapipe_workaround.diff",
        "@//third_party:mediapipe_visibility.diff",
        "@//third_party:mediapipe_model_path.diff",
        "@//third_party:mediapipe_extension.diff",
        # "@//third_party:mediapipe_emscripten_patch.diff",
    ],
    sha256 = "6b43a4304ca4aa3a698906e4b4ff696d698d0b788baffd8284c03632712b1020",
    strip_prefix = "mediapipe-0.8.10",
    urls = ["https://github.com/google/mediapipe/archive/v0.8.10.tar.gz"],
)

# ABSL cpp library lts_2021_03_24, patch 2.
http_archive(
    name = "com_google_absl",
    patch_args = [
        "-p1",
    ],
    # Remove after https://github.com/abseil/abseil-cpp/issues/326 is solved.
    patches = [
        "@com_google_mediapipe//third_party:com_google_absl_f863b622fe13612433fdf43f76547d5edda0c93001.diff",
    ],
    sha256 = "59b862f50e710277f8ede96f083a5bb8d7c9595376146838b9580be90374ee1f",
    strip_prefix = "abseil-cpp-20210324.2",
    urls = [
        "https://github.com/abseil/abseil-cpp/archive/refs/tags/20210324.2.tar.gz",
    ],
)

http_archive(
    name = "rules_cc",
    strip_prefix = "rules_cc-main",
    urls = ["https://github.com/bazelbuild/rules_cc/archive/main.zip"],
)

http_archive(
    name = "bazel_rules_dict",
    strip_prefix = "bazel_rules_dict-0.1.1",
    sha256 = "00adce0dc43d7ef39dcb7f59f8cc5644cde02766bb193f342ecff13d70f60b07",
    urls = [
        "https://github.com/homuler/bazel_rules_dict/archive/refs/tags/v0.1.1.tar.gz",
    ],
)

http_archive(
    name = "rules_foreign_cc",
    sha256 = "47f94195f144952c5a47245363d4a27b0e7ef3037a58ecf13aca8b5dbe3c2609",
    strip_prefix = "rules_foreign_cc-feat-cache_entries_target",
    url = "https://github.com/homuler/rules_foreign_cc/archive/feat/cache_entries_target.zip",
)

load("@rules_foreign_cc//foreign_cc:repositories.bzl", "rules_foreign_cc_dependencies")

rules_foreign_cc_dependencies()

# GoogleTest/GoogleMock framework. Used by most unit-tests.
# Last updated 2021-07-02.
http_archive(
    name = "com_google_googletest",
    sha256 = "de682ea824bfffba05b4e33b67431c247397d6175962534305136aa06f92e049",
    strip_prefix = "googletest-4ec4cd23f486bf70efcc5d2caa40f24368f752e3",
    urls = ["https://github.com/google/googletest/archive/4ec4cd23f486bf70efcc5d2caa40f24368f752e3.zip"],
)

# Google Benchmark library v1.6.1 released on 2022-01-10.
http_archive(
    name = "com_google_benchmark",
    build_file = "@com_google_mediapipe//third_party:benchmark.BUILD",
    sha256 = "6132883bc8c9b0df5375b16ab520fac1a85dc9e4cf5be59480448ece74b278d4",
    strip_prefix = "benchmark-1.6.1",
    urls = ["https://github.com/google/benchmark/archive/refs/tags/v1.6.1.tar.gz"],
)

# gflags needed by glog
http_archive(
    name = "com_github_gflags_gflags",
    sha256 = "19713a36c9f32b33df59d1c79b4958434cb005b5b47dc5400a7a4b078111d9b5",
    strip_prefix = "gflags-2.2.2",
    url = "https://github.com/gflags/gflags/archive/v2.2.2.zip",
)

# 2020-08-21
http_archive(
    name = "com_github_glog_glog",
    sha256 = "58c9b3b6aaa4dd8b836c0fd8f65d0f941441fb95e27212c5eeb9979cfd3592ab",
    strip_prefix = "glog-0a2e5931bd5ff22fd3bf8999eb8ce776f159cda6",
    urls = [
        "https://github.com/google/glog/archive/0a2e5931bd5ff22fd3bf8999eb8ce776f159cda6.zip",
    ],
)

http_archive(
    name = "com_github_glog_glog_no_gflags",
    build_file = "@com_google_mediapipe//third_party:glog_no_gflags.BUILD",
    patch_args = [
        "-p1",
    ],
    patches = [
        "@//third_party:com_github_glog_glog_no_gflags_fixes.diff",
    ],
    sha256 = "58c9b3b6aaa4dd8b836c0fd8f65d0f941441fb95e27212c5eeb9979cfd3592ab",
    strip_prefix = "glog-0a2e5931bd5ff22fd3bf8999eb8ce776f159cda6",
    urls = [
        "https://github.com/google/glog/archive/0a2e5931bd5ff22fd3bf8999eb8ce776f159cda6.zip",
    ],
)

# easyexif
http_archive(
    name = "easyexif",
    build_file = "@com_google_mediapipe//third_party:easyexif.BUILD",
    strip_prefix = "easyexif-master",
    url = "https://github.com/mayanklahiri/easyexif/archive/master.zip",
)

# libyuv
http_archive(
    name = "libyuv",
    build_file = "@com_google_mediapipe//third_party:libyuv.BUILD",
    # Error: operand type mismatch for `vbroadcastss' caused by commit 8a13626e42f7fdcf3a6acbb0316760ee54cda7d8.
    urls = ["https://chromium.googlesource.com/libyuv/libyuv/+archive/2525698acba9bf9b701ba6b4d9584291a1f62257.tar.gz"],
)

# Note: protobuf-javalite is no longer released as a separate download, it's included in the main Java download.
# ...but the Java download is currently broken, so we use the "source" download.
http_archive(
    name = "com_google_protobuf_javalite",
    sha256 = "87407cd28e7a9c95d9f61a098a53cf031109d451a7763e7dd1253abf8b4df422",
    strip_prefix = "protobuf-3.19.1",
    urls = ["https://github.com/protocolbuffers/protobuf/archive/v3.19.1.tar.gz"],
)

http_archive(
    name = "com_google_protobuf",
    patch_args = [
        "-p1",
    ],
    patches = [
        "@com_google_mediapipe//third_party:com_google_protobuf_fixes.diff",
    ],
    sha256 = "87407cd28e7a9c95d9f61a098a53cf031109d451a7763e7dd1253abf8b4df422",
    strip_prefix = "protobuf-3.19.1",
    urls = ["https://github.com/protocolbuffers/protobuf/archive/v3.19.1.tar.gz"],
)

http_archive(
    name = "com_google_audio_tools",
    strip_prefix = "multichannel-audio-tools-master",
    urls = ["https://github.com/google/multichannel-audio-tools/archive/master.zip"],
)

# 2020-07-09
http_archive(
    name = "pybind11_bazel",
    sha256 = "75922da3a1bdb417d820398eb03d4e9bd067c4905a4246d35a44c01d62154d91",
    strip_prefix = "pybind11_bazel-203508e14aab7309892a1c5f7dd05debda22d9a5",
    urls = ["https://github.com/pybind/pybind11_bazel/archive/203508e14aab7309892a1c5f7dd05debda22d9a5.zip"],
)

# Point to the commit that deprecates the usage of Eigen::MappedSparseMatrix.
http_archive(
    name = "pybind11",
    build_file = "@pybind11_bazel//:pybind11.BUILD",
    sha256 = "b971842fab1b5b8f3815a2302331782b7d137fef0e06502422bc4bc360f4956c",
    strip_prefix = "pybind11-70a58c577eaf067748c2ec31bfd0b0a614cffba6",
    urls = [
        "https://github.com/pybind/pybind11/archive/70a58c577eaf067748c2ec31bfd0b0a614cffba6.zip",
    ],
)

# Point to the commit that deprecates the usage of Eigen::MappedSparseMatrix.
http_archive(
    name = "ceres_solver",
    patch_args = [
        "-p1",
    ],
    patches = [
        "@com_google_mediapipe//third_party:ceres_solver_compatibility_fixes.diff",
    ],
    sha256 = "8b7b16ceb363420e0fd499576daf73fa338adb0b1449f58bea7862766baa1ac7",
    strip_prefix = "ceres-solver-123fba61cf2611a3c8bddc9d91416db26b10b558",
    url = "https://github.com/ceres-solver/ceres-solver/archive/123fba61cf2611a3c8bddc9d91416db26b10b558.zip",
)

http_archive(
    name = "opencv",
    build_file = "@//third_party:opencv.BUILD",
    sha256 = "5e37b791b2fe42ed39b52d9955920b951ee42d5da95f79fbc9765a08ef733399",
    strip_prefix = "opencv-3.4.16",
    urls = ["https://github.com/opencv/opencv/archive/3.4.16.tar.gz"],
)

new_local_repository(
    name = "linux_opencv",
    build_file = "@//third_party:opencv_linux.BUILD",
    path = "/usr",
)

new_local_repository(
    name = "linux_ffmpeg",
    build_file = "@//third_party:ffmpeg_linux.BUILD",
    path = "/usr",
)

new_local_repository(
    name = "macos_opencv",
    build_file = "@com_google_mediapipe//third_party:opencv_macos.BUILD",
    path = "/usr/local",
)

new_local_repository(
    name = "macos_arm64_opencv",
    build_file = "@com_google_mediapipe//third_party:opencv_macos.BUILD",
    path = "/opt/homebrew",
)

new_local_repository(
    name = "macos_ffmpeg",
    build_file = "@//third_party:ffmpeg_macos.BUILD",
    path = "/usr/local/opt/ffmpeg",
)

new_local_repository(
    name = "windows_opencv",
    build_file = "@//third_party:opencv_windows.BUILD",
    path = "C:\\opencv\\build",
)

new_local_repository(
    name = "wasm_opencv",
    build_file = "@//third_party:opencv_wasm.BUILD",
    path = "/usr",
)

http_archive(
    name = "android_opencv",
    build_file = "@com_google_mediapipe//third_party:opencv_android.BUILD",
    sha256 = "cdb0e190c3734edd4052a3535d9e4310af912a9f70a421b1621711942a1028d5",
    strip_prefix = "OpenCV-android-sdk",
    type = "zip",
    url = "https://github.com/opencv/opencv/releases/download/3.4.3/opencv-3.4.3-android-sdk.zip",
)

# After OpenCV 3.2.0, the pre-compiled opencv2.framework has google protobuf symbols, which will
# trigger duplicate symbol errors in the linking stage of building a mediapipe ios app.
# To get a higher version of OpenCV for iOS, opencv2.framework needs to be built from source with
# '-DBUILD_PROTOBUF=OFF -DBUILD_opencv_dnn=OFF'.
http_archive(
    name = "ios_opencv",
    build_file = "@com_google_mediapipe//third_party:opencv_ios.BUILD",
    sha256 = "7dd536d06f59e6e1156b546bd581523d8df92ce83440002885ec5abc06558de2",
    type = "zip",
    url = "https://github.com/opencv/opencv/releases/download/3.2.0/opencv-3.2.0-ios-framework.zip",
)

http_archive(
    name = "stblib",
    build_file = "@com_google_mediapipe//third_party:stblib.BUILD",
    patch_args = [
        "-p1",
    ],
    patches = [
        "@com_google_mediapipe//third_party:stb_image_impl.diff",
    ],
    sha256 = "13a99ad430e930907f5611325ec384168a958bf7610e63e60e2fd8e7b7379610",
    strip_prefix = "stb-b42009b3b9d4ca35bc703f5310eedc74f584be58",
    urls = ["https://github.com/nothings/stb/archive/b42009b3b9d4ca35bc703f5310eedc74f584be58.tar.gz"],
)

load("//third_party:android_configure.bzl", "android_configure")
android_configure(name = "local_config_android")

load("@local_config_android//:android_configure.bzl", "android_workspace")
android_workspace()

# iOS basic build deps.

http_archive(
    name = "build_bazel_rules_apple",
    patch_args = [
        "-p1",
    ],
    patches = [
        # Bypass checking ios unit test runner when building MP ios applications.
        "@com_google_mediapipe//third_party:build_bazel_rules_apple_bypass_test_runner_check.diff",
        "@//third_party:build_bazel_rules_apple_validation.diff",
    ],
    sha256 = "77e8bf6fda706f420a55874ae6ee4df0c9d95da6c7838228b26910fc82eea5a2",
    url = "https://github.com/bazelbuild/rules_apple/releases/download/0.32.0/rules_apple.0.32.0.tar.gz",
)

load(
    "@build_bazel_rules_apple//apple:repositories.bzl",
    "apple_rules_dependencies",
)

apple_rules_dependencies()

load(
    "@build_bazel_rules_swift//swift:repositories.bzl",
    "swift_rules_dependencies",
)

swift_rules_dependencies()

http_archive(
    name = "build_bazel_apple_support",
    sha256 = "741366f79d900c11e11d8efd6cc6c66a31bfb2451178b58e0b5edc6f1db17b35",
    urls = [
        "https://github.com/bazelbuild/apple_support/releases/download/0.10.0/apple_support.0.10.0.tar.gz",
    ],
)

load(
    "@build_bazel_apple_support//lib:repositories.bzl",
    "apple_support_dependencies",
)

apple_support_dependencies()

# More iOS deps.

http_archive(
    name = "google_toolbox_for_mac",
    build_file = "@com_google_mediapipe//third_party:google_toolbox_for_mac.BUILD",
    sha256 = "e3ac053813c989a88703556df4dc4466e424e30d32108433ed6beaec76ba4fdc",
    strip_prefix = "google-toolbox-for-mac-2.2.1",
    url = "https://github.com/google/google-toolbox-for-mac/archive/v2.2.1.zip",
)

# Needed by TensorFlow
http_archive(
    name = "io_bazel_rules_closure",
    sha256 = "e0a111000aeed2051f29fcc7a3f83be3ad8c6c93c186e64beb1ad313f0c7f9f9",
    strip_prefix = "rules_closure-cf1e44edb908e9616030cc83d085989b8e6cd6df",
    urls = [
        "http://mirror.tensorflow.org/github.com/bazelbuild/rules_closure/archive/cf1e44edb908e9616030cc83d085989b8e6cd6df.tar.gz",
        "https://github.com/bazelbuild/rules_closure/archive/cf1e44edb908e9616030cc83d085989b8e6cd6df.tar.gz",  # 2019-04-04
    ],
)

# Tensorflow repo should always go after the other external dependencies.
# 2022-02-15
_TENSORFLOW_GIT_COMMIT = "a3419acc751dfc19caf4d34a1594e1f76810ec58"

_TENSORFLOW_SHA256 = "b95b2a83632d4055742ae1a2dcc96b45da6c12a339462dbc76c8bca505308e3a"

http_archive(
    name = "org_tensorflow",
    patch_args = [
        "-p1",
    ],
    patches = [
        "@com_google_mediapipe//third_party:org_tensorflow_compatibility_fixes.diff",
        # Diff is generated with a script, don't update it manually.
        "@com_google_mediapipe//third_party:org_tensorflow_custom_ops.diff",
        # "@//third_party:tensorflow_xnnpack_emscripten_fixes.diff",
    ],
    sha256 = _TENSORFLOW_SHA256,
    strip_prefix = "tensorflow-%s" % _TENSORFLOW_GIT_COMMIT,
    urls = [
        "https://github.com/tensorflow/tensorflow/archive/%s.tar.gz" % _TENSORFLOW_GIT_COMMIT,
    ],
)

load("@org_tensorflow//tensorflow:workspace3.bzl", "tf_workspace3")

tf_workspace3()

load("@org_tensorflow//tensorflow:workspace2.bzl", "tf_workspace2")

tf_workspace2()

# Edge TPU
http_archive(
    name = "libedgetpu",
    sha256 = "14d5527a943a25bc648c28a9961f954f70ba4d79c0a9ca5ae226e1831d72fe80",
    strip_prefix = "libedgetpu-3164995622300286ef2bb14d7fdc2792dae045b7",
    urls = [
        "https://github.com/google-coral/libedgetpu/archive/3164995622300286ef2bb14d7fdc2792dae045b7.tar.gz",
    ],
)

load("@libedgetpu//:workspace.bzl", "libedgetpu_dependencies")

libedgetpu_dependencies()

load("@coral_crosstool//:configure.bzl", "cc_crosstool")

cc_crosstool(name = "crosstool")
