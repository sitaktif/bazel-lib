# Declare the local Bazel workspace.
# This is *not* included in the published distribution.
workspace(
    # see https://docs.bazel.build/versions/main/skylark/deploying.html#workspace
    name = "aspect_bazel_lib",
)

load(":internal_deps.bzl", "bazel_lib_internal_deps")

# Fetch deps needed only locally for development
bazel_lib_internal_deps()

load("@bazel_features//:deps.bzl", "bazel_features_deps")

bazel_features_deps()

load("@io_bazel_stardoc//:setup.bzl", "stardoc_repositories")

stardoc_repositories()

load("@rules_jvm_external//:repositories.bzl", "rules_jvm_external_deps")

rules_jvm_external_deps()

load("@rules_jvm_external//:setup.bzl", "rules_jvm_external_setup")

rules_jvm_external_setup()

load("@io_bazel_stardoc//:deps.bzl", "stardoc_external_deps")

stardoc_external_deps()

load("@stardoc_maven//:defs.bzl", stardoc_pinned_maven_install = "pinned_maven_install")

stardoc_pinned_maven_install()

load("//lib:repositories.bzl", "aspect_bazel_lib_dependencies", "aspect_bazel_lib_register_toolchains")

aspect_bazel_lib_dependencies()

aspect_bazel_lib_register_toolchains()

# For running our own unit tests
load("@bazel_skylib//lib:unittest.bzl", "register_unittest_toolchains")

register_unittest_toolchains()

# An external repository for test to use
local_repository(
    name = "external_test_repo",
    path = "./lib/tests/external_test_repo",
)

load("//lib:host_repo.bzl", "host_repo")

host_repo(name = "aspect_bazel_lib_host")

############################################
# rules_go

load("//:deps.bzl", "go_dependencies")

# gazelle:repository_macro deps.bzl%go_dependencies
# gazelle:repository go_repository name=org_golang_x_tools importpath=golang.org/x/tools
# https://github.com/bazelbuild/bazel-gazelle/issues/1217#issuecomment-1152236735
go_dependencies()

load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")

go_rules_dependencies()

go_register_toolchains(version = "1.18.3")

############################################
# Gazelle, for generating bzl_library targets

load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies")

gazelle_dependencies()

# Buildifier
load("@buildifier_prebuilt//:deps.bzl", "buildifier_prebuilt_deps")

buildifier_prebuilt_deps()

load("@buildifier_prebuilt//:defs.bzl", "buildifier_prebuilt_register_toolchains")

buildifier_prebuilt_register_toolchains()

# rules_lint
load(
    "@aspect_rules_lint//format:repositories.bzl",
    "fetch_shfmt",
)

fetch_shfmt()

load("//.aspect/workflows:deps.bzl", "fetch_workflows_deps")

fetch_workflows_deps()
