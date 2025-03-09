load("@aspect_rules_js//js:defs.bzl", "js_library", "js_run_binary")
load("@aspect_rules_ts//ts:defs.bzl", "ts_project")
load("@npm//:defs.bzl", "npm_link_all_packages")
load("@npm//frontend:vite/package_json.bzl", "bin")

npm_link_all_packages(name = "node_modules")

ts_project(
    name = "project",
    srcs = glob(["src/**"]),
    assets = glob(["src/**/*.css"]),
    declaration = True,
    transpiler = "tsc",
    tsconfig = "tsconfig.json",
    deps = [
        ":node_modules/@types/react",
        ":node_modules/@types/react-dom",
        ":node_modules/react",
        ":node_modules/react-dom",
        ":node_modules/react-router-dom",
        ":node_modules/tailwindcss",
    ],
)

js_run_binary(
    name = "frontend",
    srcs = [
        "index.html",
        ":project",
    ],
    args = ["build"],
    mnemonic = "ViteBuild",
    out_dirs = ["dist"],
    tool = ":vite",
    visibility = ["//:__subpackages__"],
)

bin.vite_binary(
    name = "vite",
    chdir = package_name(),
    data = ["vite.config"],
)

js_library(
    name = "vite.config",
    srcs = ["vite.config.mjs"],
    data = [
        ":node_modules/@tailwindcss/vite",
        ":node_modules/@vitejs/plugin-react",
        ":node_modules/tailwindcss",
        ":node_modules/vite-plugin-svgr",
        ":node_modules/vitest",
    ],
)
