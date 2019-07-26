# desugar
Standalone version of Android's desugar tool that works for both Android and JRE

## Notes

To allow for easier updates, the command line arguments are preserved from the original tool. 
This means the `--min_sdk_version` argument expects an Android version. Please see the following table for the corresponding JRE versions.

| Java Version  | Android Version  |
|:----:|:----:|
| 6 | 1  |
| 7 | 19 |
| 8  | 26  |
| 11  |  28 |

## Usage

```
.\bin\desugar.bat
bin/desugar

  --[no]allow_empty_bootclasspath (a boolean; default: "false")
  --[no]best_effort_tolerate_missing_deps (a boolean; default: "true")
    Whether to tolerate missing dependencies on the classpath in some cases.
    You should strive to set this flag to false.
  --bootclasspath_entry (a valid filesystem path; may be used multiple times)
    Bootclasspath that was used to compile the --input Jar with, like javac's -
    bootclasspath flag (required).
  --classpath_entry (a valid filesystem path; may be used multiple times)
    Ordered classpath (Jar or directory) to resolve symbols in the --input Jar,
    like javac's -cp flag.
  --[no]copy_bridges_from_classpath (a boolean; default: "false")
    Copy bridges from classpath to desugared classes.
  --[no]core_library (a boolean; default: "false")
    Enables rewriting to desugar java.* classes.
  --[no]desugar_interface_method_bodies_if_needed (a boolean; default: "true")
    Rewrites default and static methods in interfaces if --min_sdk_version <
    24. This only works correctly if subclasses of rewritten interfaces as well
    as uses of static interface methods are run through this tool as well.
  --[no]desugar_supported_core_libs (a boolean; default: "false")
    Enable core library desugaring, which requires configuration with related
    flags.
  --[no]desugar_try_with_resources_if_needed (a boolean; default: "true")
    Rewrites try-with-resources statements if --min_sdk_version < 19.
  --[no]desugar_try_with_resources_omit_runtime_classes (a boolean; default: "false")
    Omits the runtime classes necessary to support try-with-resources from the
    output. This property has effect only if --
    desugar_try_with_resources_if_needed is used.
  --dont_rewrite_core_library_invocation (a string; may be used multiple times)
    Method invocations not to rewrite, given as "class/Name#method".
  --[no]emit_dependency_metadata_as_needed (a boolean; default: "false")
    Whether to emit META-INF/desugar_deps as needed for later consistency
    checking.
  --emulate_core_library_interface (a string; may be used multiple times)
    Assume the given java.* interfaces are emulated.
  --input [-i] (a valid filesystem path; may be used multiple times)
    Input Jar or directory with classes to desugar (required, the n-th input is
    paired withthe n-th output).
  --[no]legacy_jacoco_fix (a boolean; default: "false")
    Consider setting this flag if you're using JaCoCo versions prior to 0.7.9
    to work around issues with coverage instrumentation in default and static
    interface methods. This flag may be removed when no longer needed.
  --min_sdk_version (an integer; default: "19")
    Minimum targeted sdk version.  If >= 24, enables default methods in
    interfaces.
  --[no]only_desugar_javac9_for_lint (a boolean; default: "false")
    A temporary flag specifically for android lint, subject to removal anytime
    (DO NOT USE)
  --output [-o] (a valid filesystem path; may be used multiple times)
    Output Jar or directory to write desugared classes into (required, the n-th
    output is paired with the n-th input, output must be a Jar if input is a
    Jar).
  --retarget_core_library_member (a string; may be used multiple times)
    Method invocations to retarget, given as "class/Name#member-
    >new/class/Name".  The new owner is blindly assumed to exist.
  --[no]rewrite_calls_to_long_compare (a boolean; default: "false")
    Rewrite calls to Long.compare(long, long) to the JVM instruction lcmp
    regardless of --min_sdk_version.
  --rewrite_core_library_prefix (a string; may be used multiple times)
    Assume the given java.* prefixes are desugared.
  --[no]verbose [-v] (a boolean; default: "false")
    Enables verbose debugging output.
```

## As Dependency

__Gradle__

```
compile "com.viridiansoftware:desugar:1.0.0"
```

__Maven__

```
<dependency>
    <groupId>com.viridiansoftware</groupId>
    <artifactId>desugar</artifactId>
    <version>1.0.0</version>
</dependency>
```
