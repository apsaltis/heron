package(default_visibility = ["//visibility:public"])

load("/tools/rules/jarjar_rules", "jarjar_binary")

storm_deps_files = [
    "//heron/api/src/java:api-java",
    "//heron/common/src/java:basics-java",
    "//heron/simulator/src/java:simulator-java",
    "@com_googlecode_json_simple_json_simple//jar",
    "//third_party/java:kryo-neverlink",
]

# Kryo is bundled here for integration test
java_library(
    name='storm-compatibility-java',
    srcs = glob(["**/*.java"]),
    deps = storm_deps_files + ["//third_party/java:kryo"],
)

java_binary(
    name="storm-compatibility-unshaded",
    srcs = glob(["**/*.java"]),
    deps = storm_deps_files,
)

jarjar_binary(
    name = "heron-storm",
    src = ":storm-compatibility-unshaded_deploy.jar",
    shade = "shade.conf",
    deps = ["@org_sonatype_plugins_jarjar_maven_plugin//jar"]
)
