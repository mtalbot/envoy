load(
    "//bazel:envoy_build_system.bzl",
    "envoy_cc_extension",
    "envoy_cc_library",
    "envoy_extension_package",
    "envoy_proto_library",
)

licenses(["notice"])  # Apache 2

## Pluggable HTTP cache filter

envoy_extension_package()

envoy_cc_library(
    name = "cache_filter_lib",
    srcs = ["cache_filter.cc"],
    hdrs = ["cache_filter.h"],
    deps = [
        ":cache_custom_headers",
        ":cache_headers_utils_lib",
        ":cacheability_utils_lib",
        ":http_cache_lib",
        "//source/common/common:enum_to_int",
        "//source/common/common:logger_lib",
        "//source/common/common:macros",
        "//source/common/http:header_map_lib",
        "//source/common/http:headers_lib",
        "//source/common/http:utility_lib",
        "//source/extensions/filters/http/common:pass_through_filter_lib",
        "@envoy_api//envoy/extensions/filters/http/cache/v3alpha:pkg_cc_proto",
    ],
)

envoy_cc_library(
    name = "cacheability_utils_lib",
    srcs = ["cacheability_utils.cc"],
    hdrs = ["cacheability_utils.h"],
    deps = [
        ":cache_custom_headers",
        ":cache_headers_utils_lib",
        "//source/common/common:utility_lib",
        "//source/common/http:headers_lib",
    ],
)

envoy_cc_library(
    name = "cache_policy_lib",
    hdrs = ["cache_policy.h"],
    deps = [
        ":cache_headers_utils_lib",
        ":http_cache_lib",
        "//source/common/http:header_map_lib",
        "//source/common/stream_info:filter_state_lib",
    ],
)

envoy_proto_library(
    name = "key",
    srcs = ["key.proto"],
)

envoy_cc_library(
    name = "http_cache_lib",
    srcs = ["http_cache.cc"],
    hdrs = ["http_cache.h"],
    deps = [
        ":cache_custom_headers",
        ":cache_headers_utils_lib",
        ":key_cc_proto",
        "//envoy/buffer:buffer_interface",
        "//envoy/common:time_interface",
        "//envoy/config:typed_config_interface",
        "//envoy/http:codes_interface",
        "//envoy/http:header_map_interface",
        "//source/common/common:assert_lib",
        "//source/common/http:header_utility_lib",
        "//source/common/http:headers_lib",
        "//source/common/protobuf:utility_lib",
        "@envoy_api//envoy/extensions/filters/http/cache/v3alpha:pkg_cc_proto",
    ],
)

envoy_cc_library(
    name = "cache_headers_utils_lib",
    srcs = ["cache_headers_utils.cc"],
    hdrs = ["cache_headers_utils.h"],
    external_deps = ["abseil_optional"],
    deps = [
        ":cache_custom_headers",
        "//envoy/common:time_interface",
        "//envoy/http:header_map_interface",
        "//source/common/common:matchers_lib",
        "//source/common/http:header_map_lib",
        "//source/common/http:header_utility_lib",
        "//source/common/http:headers_lib",
        "//source/common/protobuf",
        "@com_google_absl//absl/container:btree",
        "@envoy_api//envoy/extensions/filters/http/cache/v3alpha:pkg_cc_proto",
    ],
)

envoy_cc_library(
    name = "cache_custom_headers",
    srcs = ["cache_custom_headers.cc"],
    hdrs = ["cache_custom_headers.h"],
    deps = [
        "//source/common/http:headers_lib",
    ],
)

envoy_cc_extension(
    name = "config",
    srcs = ["config.cc"],
    hdrs = ["config.h"],
    deps = [
        ":cache_filter_lib",
        "//source/extensions/filters/http/common:factory_base_lib",
        "@envoy_api//envoy/extensions/filters/http/cache/v3alpha:pkg_cc_proto",
    ],
)
