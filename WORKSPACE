#Workspace for angular material
workspace(
    name = "angular_material",
)

# Point to the nested WORKSPACE we merged from github.com/angular/material.angular.io
# NB: even though this isn't referenced anywhere, it's required for Bazel to know about the
# nested workspace so that wildcard patterns like //... don't descend into it.
local_repository(
    name = "material_angular_io",
    path = "./material.angular.io",
)

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# Add NodeJS rules
http_archive(
    name = "build_bazel_rules_nodejs",
    sha256 = "709cc0dcb51cf9028dd57c268066e5bc8f03a119ded410a13b5c3925d6e43c48",
    urls = ["https://github.com/bazelbuild/rules_nodejs/releases/download/5.8.4/rules_nodejs-5.8.4.tar.gz"],
)

# Add sass rules
http_archive(
    name = "io_bazel_rules_sass",
    sha256 = "1c89680ca9cbbba33cb9cd462eb328e5782e14c0aa1286b794c71b5333385407",
    strip_prefix = "rules_sass-1.68.0",
    urls = [
        "https://github.com/bazelbuild/rules_sass/archive/1.68.0.zip",
    ],
)

# Add skylib which contains common Bazel utilities. Note that `rules_nodejs` would also
# bring in the skylib repository but with an older version that does not support shorthands
# for declaring Bazel build setting flags.
http_archive(
    name = "bazel_skylib",
    sha256 = "a9c5d3a22461ed7063aa7b088f9c96fa0aaaa8b6984b601f84d705adc47d8a58",
    strip_prefix = "bazel-skylib-8334f938c1574ef6f1f7a38a03550a31df65274e",
    urls = [
        "https://github.com/bazelbuild/bazel-skylib/archive/8334f938c1574ef6f1f7a38a03550a31df65274e.tar.gz",
    ],
)

http_archive(
    name = "rules_pkg",
    sha256 = "d94fd5b08dbdc227d66421cb9513f6c3b94bb3938fad276445a2d562f7df8f35",
    strip_prefix = "rules_pkg-61018b85819d57feb56886316e76e8ed8a4ce378",
    urls = [
        "https://github.com/bazelbuild/rules_pkg/archive/61018b85819d57feb56886316e76e8ed8a4ce378.tar.gz",
    ],
)

load("@rules_pkg//:deps.bzl", "rules_pkg_dependencies")

rules_pkg_dependencies()

load("@bazel_skylib//:workspace.bzl", "bazel_skylib_workspace")

bazel_skylib_workspace()

load("@build_bazel_rules_nodejs//:repositories.bzl", "build_bazel_rules_nodejs_dependencies")

build_bazel_rules_nodejs_dependencies()

http_archive(
    name = "aspect_rules_js",
    sha256 = "75c25a0f15a9e4592bbda45b57aa089e4bf17f9176fd735351e8c6444df87b52",
    strip_prefix = "rules_js-2.1.0",
    url = "https://github.com/aspect-build/rules_js/releases/download/v2.1.0/rules_js-v2.1.0.tar.gz",
)

load("@aspect_rules_js//js:repositories.bzl", "rules_js_dependencies")

rules_js_dependencies()

load("@rules_nodejs//nodejs:repositories.bzl", "nodejs_register_toolchains")

NODE_VERSION = "22.11.0"

NODE_REPOSITORIES = {
    "22.11.0-darwin_arm64": ("node-v22.11.0-darwin-arm64.tar.gz", "node-v22.11.0-darwin-arm64", "2e89afe6f4e3aa6c7e21c560d8a0453d84807e97850bbb819b998531a22bdfde"),
    "22.11.0-darwin_amd64": ("node-v22.11.0-darwin-x64.tar.gz", "node-v22.11.0-darwin-x64", "668d30b9512137b5f5baeef6c1bb4c46efff9a761ba990a034fb6b28b9da2465"),
    "22.11.0-linux_arm64": ("node-v22.11.0-linux-arm64.tar.xz", "node-v22.11.0-linux-arm64", "6031d04b98f59ff0f7cb98566f65b115ecd893d3b7870821171708cdbaf7ae6e"),
    "22.11.0-linux_ppc64le": ("node-v22.11.0-linux-ppc64le.tar.xz", "node-v22.11.0-linux-ppc64le", "d1d49d7d611b104b6d616e18ac439479d8296aa20e3741432de0e85f4735a81e"),
    "22.11.0-linux_s390x": ("node-v22.11.0-linux-s390x.tar.xz", "node-v22.11.0-linux-s390x", "f474ed77d6b13d66d07589aee1c2b9175be4c1b165483e608ac1674643064a99"),
    "22.11.0-linux_amd64": ("node-v22.11.0-linux-x64.tar.xz", "node-v22.11.0-linux-x64", "83bf07dd343002a26211cf1fcd46a9d9534219aad42ee02847816940bf610a72"),
    "22.11.0-windows_amd64": ("node-v22.11.0-win-x64.zip", "node-v22.11.0-win-x64", "905373a059aecaf7f48c1ce10ffbd5334457ca00f678747f19db5ea7d256c236"),
}

nodejs_register_toolchains(
    name = "nodejs",
    node_repositories = NODE_REPOSITORIES,
    node_version = NODE_VERSION,
)

load("@aspect_rules_js//js:toolchains.bzl", "rules_js_register_toolchains")

rules_js_register_toolchains(
    node_repositories = NODE_REPOSITORIES,
    node_version = NODE_VERSION,
)

load("@build_bazel_rules_nodejs//:index.bzl", "yarn_install")
load("//tools:integration.bzl", "create_npm_package_archive_build_file")

yarn_install(
    name = "npm",
    # We add the postinstall patches file here so that Yarn will rerun whenever
    # the file is modified.
    data = [
        "//:.yarn/releases/yarn-1.22.17.cjs",
        "//:.yarnrc",
        "//:tools/postinstall/apply-patches.js",
        "//:tools/postinstall/patches/@angular+bazel+20.0.0-next.3.patch",
        "//:tools/postinstall/patches/@angular+build-tooling+0.0.0-1ebf18a3a60b182a3dbad12e9a149fd93af5c29b.patch",
        "//:tools/postinstall/patches/tsec+0.2.2.patch",
        "//src/cdk:package.json",
    ],
    # Currently disabled due to:
    #  1. Missing Windows support currently.
    #  2. Incompatibilites with the `ts_library` rule.
    exports_directories_only = False,
    # Add archive targets for some NPM packages that are needed in integration tests.
    manual_build_file_contents = create_npm_package_archive_build_file(),
    package_json = "//:package.json",
    quiet = False,
    yarn = "//:.yarn/releases/yarn-1.22.17.cjs",
    yarn_lock = "//:yarn.lock",
)

load("@npm//@bazel/protractor:package.bzl", "npm_bazel_protractor_dependencies")

npm_bazel_protractor_dependencies()

# Setup web testing. We need to setup a browser because the web testing rules for TypeScript need
# a reference to a registered browser (ideally that's a hermetic version of a browser)
load("@io_bazel_rules_webtesting//web:repositories.bzl", "web_test_repositories")

web_test_repositories()

# Setup the Sass rule repositories.
load("@io_bazel_rules_sass//:defs.bzl", "sass_repositories")

sass_repositories(
    yarn_script = "//:.yarn/releases/yarn-1.22.17.cjs",
)

# Setup repositories for browsers provided by the shared dev-infra package.
load(
    "@npm//@angular/build-tooling/bazel/browsers:browser_repositories.bzl",
    _dev_infra_browser_repositories = "browser_repositories",
)

_dev_infra_browser_repositories()

load("@build_bazel_rules_nodejs//toolchains/esbuild:esbuild_repositories.bzl", "esbuild_repositories")

esbuild_repositories(
    npm_repository = "npm",
)

load("@aspect_rules_js//npm:repositories.bzl", "npm_translate_lock")

npm_translate_lock(
    name = "npm2",
    custom_postinstalls = {
        "@angular/animations": "node ../../@nginfra/angular-linking/index.mjs",
        "@angular/common": "node ../../@nginfra/angular-linking/index.mjs",
        "@angular/forms": "node ../../@nginfra/angular-linking/index.mjs",
        "@angular/platform-browser": "node ../../@nginfra/angular-linking/index.mjs",
        "@angular/router": "node ../../@nginfra/angular-linking/index.mjs",
        "@angular/localize": "node ../../@nginfra/angular-linking/index.mjs",
    },
    data = [
        "//:package.json",
        "//:patches/@angular__compiler-cli.patch",
        "//:pnpm-workspace.yaml",
        "//src/cdk:package.json",
    ],
    npmrc = "//:.npmrc",
    pnpm_lock = "//:pnpm-lock.yaml",
    update_pnpm_lock = True,
    verify_node_modules_ignored = "//:.bazelignore",
    yarn_lock = "//:yarn.lock",
)

load("@npm2//:repositories.bzl", "npm_repositories")

npm_repositories()

http_archive(
    name = "aspect_rules_ts",
    sha256 = "9acd128abe77397505148eaa6895faed57839560dbf2177dd6285e51235e2724",
    strip_prefix = "rules_ts-3.3.1",
    url = "https://github.com/aspect-build/rules_ts/releases/download/v3.3.1/rules_ts-v3.3.1.tar.gz",
)

load("@aspect_rules_ts//ts:repositories.bzl", "rules_ts_dependencies")

rules_ts_dependencies(
    # Obtained by: curl --silent https://registry.npmjs.org/typescript/5.8.2 | jq -r '.dist.integrity'
    ts_integrity = "sha512-aJn6wq13/afZp/jT9QZmwEjDqqvSGp1VT5GVg+f/t6/oVyrgXM6BY1h9BRh/O5p3PlUPAe+WuiEZOmb/49RqoQ==",
    ts_version_from = "//:package.json",
)

http_archive(
    name = "aspect_rules_rollup",
    sha256 = "c4062681968f5dcd3ce01e09e4ba73670c064744a7046211763e17c98ab8396e",
    strip_prefix = "rules_rollup-2.0.0",
    url = "https://github.com/aspect-build/rules_rollup/releases/download/v2.0.0/rules_rollup-v2.0.0.tar.gz",
)

http_archive(
    name = "aspect_rules_jasmine",
    sha256 = "0d2f9c977842685895020cac721d8cc4f1b37aae15af46128cf619741dc61529",
    strip_prefix = "rules_jasmine-2.0.0",
    url = "https://github.com/aspect-build/rules_jasmine/releases/download/v2.0.0/rules_jasmine-v2.0.0.tar.gz",
)

load("@aspect_rules_jasmine//jasmine:dependencies.bzl", "rules_jasmine_dependencies")

rules_jasmine_dependencies()

load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")

git_repository(
    name = "devinfra",
    commit = "cc73dde52b557f831cc3b6e48daf8c3b542a33df",
    remote = "https://github.com/angular/dev-infra.git",
)

load("@devinfra//bazel:setup_dependencies_1.bzl", "setup_dependencies_1")

setup_dependencies_1()

load("@devinfra//bazel:setup_dependencies_2.bzl", "setup_dependencies_2")

setup_dependencies_2()

git_repository(
    name = "rules_angular",
    commit = "92127883c3a3714e63782a51bac1a7c03ec8b0f5",
    remote = "https://github.com/devversion/rules_angular.git",
)

load("@rules_angular//setup:step_1.bzl", "rules_angular_step1")

rules_angular_step1()

load("@rules_angular//setup:step_2.bzl", "rules_angular_step2")

rules_angular_step2()

load("@rules_angular//setup:step_3.bzl", "rules_angular_step3")

rules_angular_step3(
    angular_compiler_cli = "//:node_modules/@angular/compiler-cli",
    typescript = "//:node_modules/typescript",
)
