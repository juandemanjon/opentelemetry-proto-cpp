load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
load("@bazel_tools//tools/build_defs/repo:utils.bzl", "maybe")

load(
    "@bazel_tools//tools/build_defs/repo:git.bzl",
    "git_repository",
    "new_git_repository",
)

# Load gRPC dependency
maybe(
    http_archive,
    name = "com_github_grpc_grpc",
    sha256 = "f40bde4ce2f31760f65dc49a2f50876f59077026494e67dccf23992548b1b04f",
    strip_prefix = "grpc-1.62.0",
    urls = [
        "https://github.com/grpc/grpc/archive/refs/tags/v1.62.0.tar.gz",
    ],
)

# OTLP Protocol definition
# maybe(
#     http_archive,
#     name = "com_github_opentelemetry_proto",
#     build_file = "@io_opentelemetry_cpp//bazel:opentelemetry_proto.BUILD",
#     sha256 = "53cd32cedb27762ea2060a9c8d83e4b822de13d73b5d5d37a2db3cf55018d694",
#     strip_prefix = "opentelemetry-proto-1.4.0",
#     urls = [
#         "https://github.com/open-telemetry/opentelemetry-proto/archive/v1.4.0.tar.gz",
#     ],
# )

new_git_repository(
    name = "com_github_opentelemetry_proto",
    build_file_content = """
exports_files(
    srcs = ["opentelemetry/proto/common/v1/common.proto"],
    visibility = ["//visibility:public"]
)""",
    commit = "2080d87c780b5a8c65c9ae2771130fd669cef480",
    remote = "https://github.com/open-telemetry/opentelemetry-proto.git",

)

# Load gRPC dependencies after load.
load("@com_github_grpc_grpc//bazel:grpc_deps.bzl", "grpc_deps")

grpc_deps()

# Load extra gRPC dependencies due to https://github.com/grpc/grpc/issues/20511
load("@com_github_grpc_grpc//bazel:grpc_extra_deps.bzl", "grpc_extra_deps")

grpc_extra_deps()