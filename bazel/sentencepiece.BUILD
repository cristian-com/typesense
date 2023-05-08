load("@rules_foreign_cc//foreign_cc:defs.bzl", "cmake")

package(default_visibility = ["//visibility:public"])


filegroup(
    name = "sentencepiece_src",
    srcs = glob(["**"]),
    visibility = ["//visibility:public"],
)

cc_library(
    name = "sentencepiece_headers",
    hdrs = glob(["src/**/*.h"]),
    includes = ["src"],
    visibility = ["//visibility:public"],
    strip_include_prefix = "src"
)


cmake(
    name = "sentencepiece",
    lib_source = "//:sentencepiece_src",
    out_static_libs = ["libsentencepiece.a"],
    out_include_dir = "include",
    build_args = [
        "--config Release",
        "--target sentencepiece-static",
    ],
    install = False,
    cache_entries = {
        'SPM_USE_BUILTIN_PROTOBUF': 'OFF',
        'Protobuf_LIBRARY': '$EXT_BUILD_ROOT/bazel-out/k8-fastbuild/bin/external/com_google_protobuf/',
        'Protobuf_LITE_LIBRARY': '$EXT_BUILD_ROOT/bazel-out/k8-fastbuild/bin/external/com_google_protobuf/',
        'Protobuf_INCLUDE_DIR': '$EXT_BUILD_ROOT/external/com_google_protobuf/src',
    },
    deps = [
        "@com_google_protobuf//:protobuf_lite",
        "@com_google_protobuf//:protobuf",
        "@com_google_protobuf//:protobuf_headers",
    ],
    postfix_script= """
echo "Intstalling sentencepiece"
cp $BUILD_TMPDIR/src/libsentencepiece.a $INSTALLDIR/lib/libsentencepiece.a
"""
)
