# Embedding Projector plugin.

load("//tensorboard/defs:protos.bzl", "tb_proto_library")

package(default_visibility = ["//tensorboard:internal"])

licenses(["notice"])  # Apache 2.0

exports_files(["LICENSE"])

py_library(
    name = "projector_plugin",
    srcs = ["projector_plugin.py"],
    data = [
        "//tensorboard/plugins/projector/tf_projector_plugin:projector_assets",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":metadata",
        ":protos_all_py_pb2",
        "//tensorboard:expect_numpy_installed",
        "//tensorboard/backend:http_util",
        "//tensorboard/compat:tensorflow",
        "//tensorboard/plugins:base_plugin",
        "//tensorboard/util:tb_logging",
        "@org_pocoo_werkzeug",
    ],
)

py_library(
    name = "projector",
    srcs = ["__init__.py"],
    srcs_version = "PY2AND3",
    visibility = ["//visibility:public"],
    deps = [
        ":metadata",
        ":protos_all_py_pb2",
        "//tensorboard/compat:tensorflow",
    ],
)

py_test(
    name = "projector_api_test",
    size = "small",
    srcs = ["projector_api_test.py"],
    main = "projector_api_test.py",
    srcs_version = "PY2AND3",
    deps = [
        ":projector",
        "//tensorboard:expect_tensorflow_installed",
        "//tensorboard/util:test_util",
        "@org_pythonhosted_six",
    ],
)

py_test(
    name = "projector_plugin_test",
    size = "small",
    srcs = ["projector_plugin_test.py"],
    main = "projector_plugin_test.py",
    srcs_version = "PY2AND3",
    deps = [
        ":projector_plugin",
        "//tensorboard:expect_numpy_installed",
        "//tensorboard:expect_tensorflow_installed",
        "//tensorboard/backend:application",
        "//tensorboard/backend/event_processing:event_multiplexer",
        "//tensorboard/compat/proto:protos_all_py_pb2",
        "//tensorboard/plugins:base_plugin",
        "//tensorboard/util:test_util",
        "@org_pocoo_werkzeug",
    ],
)

# TODO(#2007): Remove this after pruning unnecessary TensorFlow deps in main test
py_test(
    name = "projector_plugin_notf_test",
    size = "small",
    srcs = ["projector_plugin_test.py"],
    main = "projector_plugin_test.py",
    srcs_version = "PY2AND3",
    deps = [
        ":projector_plugin",
        "//tensorboard:expect_numpy_installed",
        "//tensorboard:expect_tensorflow_installed",
        "//tensorboard/backend:application",
        "//tensorboard/backend/event_processing:event_multiplexer",
        "//tensorboard/compat:no_tensorflow",
        "//tensorboard/compat/proto:protos_all_py_pb2",
        "//tensorboard/plugins:base_plugin",
        "//tensorboard/util:test_util",
        "@org_pocoo_werkzeug",
    ],
)

py_library(
    name = "metadata",
    srcs = ["metadata.py"],
    srcs_version = "PY2AND3",
)

tb_proto_library(
    name = "protos_all",
    srcs = glob(["*.proto"]),
    visibility = ["//visibility:public"],
)

py_binary(
    name = "projector_demo",
    srcs = ["projector_demo.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":projector",
        "//tensorboard:expect_tensorflow_datasets_installed",
        "//tensorboard:expect_tensorflow_installed",
    ],
)
