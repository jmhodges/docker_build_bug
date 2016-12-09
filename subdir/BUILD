load("@bazel_tools//tools/build_defs/docker:docker.bzl", "docker_build")

filegroup(
    name = "two_dir",
    srcs = glob(["**"])
)

docker_build(
    name = "buggy_flatten_image",
    base = "wheezy",
    files = ["two_dir"],
)

docker_build(
    name = "has_subdirs_image",
    base = "wheezy",
    files = ["two_dir"],
    data_path = "."
)

genrule(
    name = "wheezy_tar",
    srcs = ["@debian_wheezy//file"],
    outs = ["wheezy_tar.tar"],
    cmd = "cat $< | xzcat >$@",
)

docker_build(
    name = "wheezy",
    tars = [":wheezy_tar"],
    visibility = ["//visibility:public"],
)
