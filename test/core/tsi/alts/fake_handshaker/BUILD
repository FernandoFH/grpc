# Copyright 2018 gRPC authors.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

load("//bazel:grpc_build_system.bzl", "grpc_cc_binary", "grpc_cc_library", "grpc_package", "grpc_proto_library")

licenses(["notice"])

grpc_package(
    name = "test/core/tsi/alts/fake_handshaker",
    visibility = "public",
)

grpc_proto_library(
    name = "transport_security_common_proto",
    srcs = ["transport_security_common.proto"],
    has_services = False,
)

grpc_proto_library(
    name = "handshaker_proto",
    srcs = ["handshaker.proto"],
    has_services = True,
    deps = [
        "transport_security_common_proto",
    ],
)

grpc_cc_library(
    name = "fake_handshaker_lib",
    testonly = True,
    srcs = ["fake_handshaker_server.cc"],
    hdrs = ["fake_handshaker_server.h"],
    external_deps = [
        "absl/log:check",
    ],
    language = "C++",
    deps = [
        "handshaker_proto",
        "transport_security_common_proto",
        "//:grpc++",
    ],
)

grpc_cc_binary(
    name = "fake_handshaker_server",
    testonly = True,
    srcs = ["fake_handshaker_server_main.cc"],
    external_deps = [
        "absl/flags:flag",
        "absl/log:check",
    ],
    language = "C++",
    deps = [
        "fake_handshaker_lib",
        "//test/core/util:grpc_test_util",
        "//test/cpp/util:test_config",
    ],
)
