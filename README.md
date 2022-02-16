## Problem
If a swift module is built from sources and then integrated as a prebuilt .framework, previously generated .swiftmodule is still visible to swiftc (e.g via some other target that is still built from sources in a module) ->  the historical version is always used, even the new one is correctly exposed via apple_static_framework_import.

## Steps to reproduce

* `bazel build parent`
* [BUILD.bazel] Comment out the existing 'MyModule' above and uncomment 'MyModule' that uses if from .framework
* To emulate new version, MyModule.framework has new API - align it in Sources/Parent.swift (comment out Step 1)
* `bazel build parent` fails ❌
* `bazel clean`
* `bazel build parent` succeeds  ✅
