---
title: The Node.js Runtime v8 options list
description: "All the possible options you can use when you start a Node.js program"
date: 2019-02-15T15:00:00+02:00
tags: node
---

Node.js can be invoked with an incredibly various set of options.

Most of those options are used to configure the v8 engine behavior.

Some of the options here are disabled by default, as you cna see in the `Default` column. You can enable them by running `node` and passing the flag, for example `node --experimental-extras`.

If an option is enabled by default, you can disable it by prepending `--no-` to the flag name, for example `node --no-harmony-shipping`.

Some can be used to optimize performance, like `--optimize-for-size`, `--max_old_space_size` and `--gc_interval`, like [Heroku suggests](https://blog.heroku.com/node-habits-2016#7-avoid-garbage).

Some others are used to enable or disable specific features. I use them often to try out new proposed JavaScript features that have been implemented in beta. Like `--harmony-public-fields`.

> Note: options names allow words to be separated by both dashes (`-`) or underscores (`_`), or a mix of those. On tutorials you'll find a mix of both, to it can be confusing. There is no difference.

I got the following list by running the command `node --v8-options`, and it's relative to Node.js `11.9.0`, the latest Node.js version at the time of writing.

| Option | Description | Type | Default |
|------|----| -----|----|
| --experimental-extras | enable code compiled in via v8_experimental_extra_library_files | bool | false |
| --use-strict | enforce strict mode | bool | false |
| --es-staging | enable test-worthy harmony features | for internal use only | bool | false |
| --harmony | enable all completed harmony features | bool | false |
| --harmony-shipping | enable all shipped harmony features | bool | true |
| --harmony-do-expressions | enable "harmony do-expressions" | in progress | bool | false |
| --harmony-class-fields | enable "harmony fields in class literals" | in progress | bool | false |
| --harmony-static-fields | enable "harmony static fields in class literals" | in progress | bool | false |
| --harmony-await-optimization | enable "harmony await taking 1 tick" | in progress | bool | false |
| --harmony-locale | enable "Intl.Locale" | in progress | bool | false |
| --harmony-intl-list-format | enable "Intl.ListFormat" | in progress | bool | false |
| --harmony-intl-relative-time-format | enable "Intl.RelativeTimeFormat" | in progress | bool | false |
| --harmony-public-fields | enable "harmony public fields in class literals" | bool | false |
| --harmony-private-fields | enable "harmony private fields in class literals" | bool | false |
| --harmony-numeric-separator | enable "harmony numeric separator between digits" | bool | false |
| --harmony-string-matchall | enable "harmony String.prototype.matchAll" | bool | false |
| --harmony-global | enable "harmony global" | bool | false |
| --harmony-string-trimming | enable "harmony String.prototype.trim{Start,End}" | bool | true |
| --harmony-sharedarraybuffer | enable "harmony sharedarraybuffer" | bool | true |
| --harmony-function-tostring | enable "harmony Function.prototype.toString" | bool | true |
| --harmony-import-meta | enable "harmony import.meta property" | bool | true |
| --harmony-bigint | enable "harmony arbitrary precision integers" | bool | true |
| --harmony-dynamic-import | enable "harmony dynamic import" | bool | true |
| --harmony-array-prototype-values | enable "harmony Array.prototype.values" | bool | true |
| --harmony-array-flat | enable "harmony Array.prototype.{flat,flatMap}" | bool | true |
| --harmony-symbol-description | enable "harmony Symbol.prototype.description" | bool | true |
| --icu-timezone-data | get information about timezones from ICU | bool | true |
| --future | Implies all staged features that we want to ship in the not-too-far future | bool | false |
| --allocation-site-pretenuring | pretenure with allocation sites | bool | true |
| --page-promotion | promote pages based on utilization | bool | true |
| --page-promotion-threshold | min percentage of live bytes on a page to enable fast evacuation | int | 70 |
| --trace-pretenuring | trace pretenuring decisions of HAllocate instructions | bool | false |
| --trace-pretenuring-statistics | trace allocation site pretenuring statistics | bool | false |
| --track-fields | track fields with only smi values | bool | true |
| --track-double-fields | track fields with double values | bool | true |
| --track-heap-object-fields | track fields with heap values | bool | true |
| --track-computed-fields | track computed boilerplate fields | bool | true |
| --track-field-types | track field types | bool | true |
| --trace-block-coverage | trace collected block coverage information | bool | false |
| --feedback-normalization | feed back normalization to constructors | bool | false |
| --optimize-for-size | Enables optimizations which favor memory size over execution speed | bool | false |
| --enable-one-shot-optimization | Enable size optimizations for the code that will only be executed once | bool | true |
| --unbox-double-arrays | automatically unbox arrays of doubles | bool | true |
| --interrupt-budget | interrupt budget which should be used for the profiler counter | int | 147456 |
| --ignition-elide-noneffectful-bytecodes | elide bytecodes which won't have any external effect | bool | true |
| --ignition-reo | use ignition register equivalence optimizer | bool | true |
| --ignition-filter-expression-positions | filter expression positions before the bytecode pipeline | bool | true |
| --ignition-share-named-property-feedback | share feedback slots when loading the same named property from the same object | bool | true |
| --print-bytecode | print bytecode generated by ignition interpreter | bool | false |
| --print-bytecode-filter | filter for selecting which functions to print bytecode | string | * |
| --trace-ignition-codegen | trace the codegen of ignition interpreter bytecode handlers | bool | false |
| --trace-ignition-dispatches | traces the dispatches to bytecode handlers by the ignition interpreter | bool | false |
| --trace-ignition-dispatches-output-file | the file to which the bytecode handler dispatch table is written | by default, the table is not written to a file | string | nullptr |
| --fast-math | faster | but maybe less accurate  math functions | bool | true |
| --trace-track-allocation-sites | trace the tracking of allocation sites | bool | false |
| --trace-migration | trace object migration | bool | false |
| --trace-generalization | trace map generalization | bool | false |
| --concurrent-recompilation | optimizing hot functions asynchronously on a separate thread | bool | true |
| --trace-concurrent-recompilation | track concurrent recompilation | bool | false |
| --concurrent-recompilation-queue-length | the length of the concurrent compilation queue | int | 8 |
| --concurrent-recompilation-delay | artificial compilation delay in ms | int | 0 |
| --block-concurrent-recompilation | block queued jobs until released | bool | false |
| --concurrent-compiler-frontend | run optimizing compiler's frontend phases on a separate thread | bool | false |
| --strict-heap-broker | fail on incomplete serialization | bool | false |
| --trace-heap-broker | trace the heap broker | bool | false |
| --stress-runs | number of stress runs | int | 0 |
| --deopt-every-n-times | deoptimize every n times a deopt point is passed | int | 0 |
| --print-deopt-stress | print number of possible deopt points | bool | false |
| --turbo-sp-frame-access | use stack pointer-relative access to frame wherever possible | bool | false |
| --turbo-preprocess-ranges | run pre-register allocation heuristics | bool | true |
| --turbo-filter | optimization filter for TurboFan compiler | string | * |
| --trace-turbo | trace generated TurboFan IR | bool | false |
| --trace-turbo-path | directory to dump generated TurboFan IR to | string | nullptr |
| --trace-turbo-filter | filter for tracing turbofan compilation | string | * |
| --trace-turbo-graph | trace generated TurboFan graphs | bool | false |
| --trace-turbo-scheduled | trace TurboFan IR with schedule | bool | false |
| --trace-turbo-cfg-file | trace turbo cfg graph | for C1 visualizer  to a given file name | string | nullptr |
| --trace-turbo-types | trace TurboFan's types | bool | true |
| --trace-turbo-scheduler | trace TurboFan's scheduler | bool | false |
| --trace-turbo-reduction | trace TurboFan's various reducers | bool | false |
| --trace-turbo-trimming | trace TurboFan's graph trimmer | bool | false |
| --trace-turbo-jt | trace TurboFan's jump threading | bool | false |
| --trace-turbo-ceq | trace TurboFan's control equivalence | bool | false |
| --trace-turbo-loop | trace TurboFan's loop optimizations | bool | false |
| --trace-alloc | trace register allocator | bool | false |
| --trace-all-uses | trace all use positions | bool | false |
| --trace-representation | trace representation types | bool | false |
| --turbo-verify | verify TurboFan graphs at each phase | bool | false |
| --turbo-verify-machine-graph | verify TurboFan machine graph before instruction selection | string | nullptr |
| --trace-verify-csa | trace code stubs verification | bool | false |
| --csa-trap-on-node | trigger break point when a node with given id is created in given stub. The format is: StubName,NodeId | string | nullptr |
| --turbo-stats | print TurboFan statistics | bool | false |
| --turbo-stats-nvp | print TurboFan statistics in machine-readable format | bool | false |
| --turbo-stats-wasm | print TurboFan statistics of wasm compilations | bool | false |
| --turbo-splitting | split nodes during scheduling in TurboFan | bool | true |
| --function-context-specialization | enable function context specialization in TurboFan | bool | false |
| --turbo-inlining | enable inlining in TurboFan | bool | true |
| --max-inlined-bytecode-size | maximum size of bytecode for a single inlining | int | 500 |
| --max-inlined-bytecode-size-cumulative | maximum cumulative size of bytecode considered for inlining | int | 1000 |
| --max-inlined-bytecode-size-absolute | maximum cumulative size of bytecode considered for inlining | int | 5000 |
| --reserve-inline-budget-scale-factor | maximum cumulative size of bytecode considered for inlining | float | 1.2 |
| --max-inlined-bytecode-size-small | maximum size of bytecode considered for small function inlining | int | 30 |
| --min-inlining-frequency | minimum frequency for inlining | float | 0.15 |
| --polymorphic-inlining | polymorphic inlining | bool | true |
| --stress-inline | set high thresholds for inlining to inline as much as possible | bool | false |
| --trace-turbo-inlining | trace TurboFan inlining | bool | false |
| --inline-accessors | inline JavaScript accessors | bool | true |
| --inline-into-try | inline into try blocks | bool | true |
| --turbo-inline-array-builtins | inline array builtins in TurboFan code | bool | true |
| --use-osr | use on-stack replacement | bool | true |
| --trace-osr | trace on-stack replacement | bool | false |
| --analyze-environment-liveness | analyze liveness of environment slots and zap dead values | bool | true |
| --trace-environment-liveness | trace liveness of local variable slots | bool | false |
| --turbo-load-elimination | enable load elimination in TurboFan | bool | true |
| --trace-turbo-load-elimination | trace TurboFan load elimination | bool | false |
| --turbo-profiling | enable profiling in TurboFan | bool | false |
| --turbo-verify-allocation | verify register allocation in TurboFan | bool | false |
| --turbo-move-optimization | optimize gap moves in TurboFan | bool | true |
| --turbo-jt | enable jump threading in TurboFan | bool | true |
| --turbo-loop-peeling | Turbofan loop peeling | bool | true |
| --turbo-loop-variable | Turbofan loop variable optimization | bool | true |
| --turbo-cf-optimization | optimize control flow in TurboFan | bool | true |
| --turbo-escape | enable escape analysis | bool | true |
| --turbo-allocation-folding | Turbofan allocation folding | bool | true |
| --turbo-instruction-scheduling | enable instruction scheduling in TurboFan | bool | false |
| --turbo-stress-instruction-scheduling | randomly schedule instructions to stress dependency tracking | bool | false |
| --turbo-store-elimination | enable store-store elimination in TurboFan | bool | true |
| --trace-store-elimination | trace store elimination | bool | false |
| --turbo-rewrite-far-jumps | rewrite far to near jumps | ia32,x64 | bool | true |
| --experimental-inline-promise-constructor | inline the Promise constructor in TurboFan | bool | true |
| --untrusted-code-mitigations | Enable mitigations for executing untrusted code | bool | false |
| --branch-load-poisoning | Mask loads with branch conditions. | bool | false |
| --minimal | simplifies execution model to make porting easier | e.g. always use Ignition, never optimize | bool | false |
| --expose-wasm | expose wasm interface to JavaScript | bool | true |
| --assume-asmjs-origin | force wasm decoder to assume input is internal asm-wasm format | bool | false |
| --wasm-disable-structured-cloning | disable wasm structured cloning | bool | false |
| --wasm-num-compilation-tasks | number of parallel compilation tasks for wasm | int | 10 |
| --wasm-write-protect-code-memory | write protect code memory on the wasm native heap | bool | false |
| --wasm-trace-serialization | trace serialization/deserialization | bool | false |
| --wasm-async-compilation | enable actual asynchronous compilation for WebAssembly.compile | bool | true |
| --wasm-test-streaming | use streaming compilation instead of async compilation for tests | bool | false |
| --wasm-max-mem-pages | maximum number of 64KiB memory pages of a wasm instance | uint | 32767 |
| --wasm-max-table-size | maximum table size of a wasm instance | uint | 10000000 |
| --wasm-tier-up | enable wasm baseline compilation and tier up to the optimizing compiler | bool | true |
| --trace-wasm-ast-start | start function for wasm AST trace | inclusive | int | 0 |
| --trace-wasm-ast-end | end function for wasm AST trace | exclusive | int | 0 |
| --liftoff | enable Liftoff, the baseline compiler for WebAssembly | bool | true |
| --wasm-trace-memory | print all memory updates performed in wasm code | bool | false |
| --wasm-tier-mask-for-testing | bitmask of functions to compile with TurboFan instead of Liftoff | int | 0 |
| --validate-asm | validate asm.js modules before compiling | bool | true |
| --suppress-asm-messages | don't emit asm.js related messages | for golden file testing | bool | false |
| --trace-asm-time | log asm.js timing info to the console | bool | false |
| --trace-asm-scanner | log tokens encountered by asm.js scanner | bool | false |
| --trace-asm-parser | verbose logging of asm.js parse failures | bool | false |
| --stress-validate-asm | try to validate everything as asm.js | bool | false |
| --dump-wasm-module-path | directory to dump wasm modules to | string | nullptr |
| --experimental-wasm-mv | enable prototype multi-value support for wasm | bool | false |
| --experimental-wasm-eh | enable prototype exception handling opcodes for wasm | bool | false |
| --experimental-wasm-se | enable prototype sign extension opcodes for wasm | bool | true |
| --experimental-wasm-sat-f2i-conversions | enable prototype saturating float conversion opcodes for wasm | bool | false |
| --experimental-wasm-threads | enable prototype thread opcodes for wasm | bool | false |
| --experimental-wasm-simd | enable prototype SIMD opcodes for wasm | bool | false |
| --experimental-wasm-anyref | enable prototype anyref opcodes for wasm | bool | false |
| --experimental-wasm-mut-global | enable prototype import/export mutable global support for wasm | bool | true |
| --wasm-opt | enable wasm optimization | bool | false |
| --wasm-no-bounds-checks | disable bounds checks | performance testing only | bool | false |
| --wasm-no-stack-checks | disable stack checks | performance testing only | bool | false |
| --wasm-shared-engine | shares one wasm engine between all isolates within a process | bool | true |
| --wasm-shared-code | shares code underlying a wasm module when it is transferred | bool | true |
| --wasm-trap-handler | use signal handlers to catch out of bounds memory access in wasm | currently Linux x86_64 only | bool | true |
| --wasm-trap-handler-fallback | Use bounds checks if guarded memory is not available | bool | false |
| --wasm-fuzzer-gen-test | Generate a test case when running a wasm fuzzer | bool | false |
| --print-wasm-code | Print WebAssembly code | bool | false |
| --wasm-interpret-all | Execute all wasm code in the wasm interpreter | bool | false |
| --asm-wasm-lazy-compilation | enable lazy compilation for asm-wasm modules | bool | true |
| --wasm-lazy-compilation | enable lazy compilation for all wasm modules | bool | false |
| --frame-count | number of stack frames inspected by the profiler | int | 1 |
| --type-info-threshold | percentage of ICs that must have type info to allow optimization | int | 25 |
| --stress-sampling-allocation-profiler | Enables sampling allocation profiler with X as a sample interval | int | 0 |
| --min-semi-space-size | min size of a semi-space | in MBytes), the new space consists of two semi-spaces | size_t | 0 |
| --max-semi-space-size | max size of a semi-space | in MBytes), the new space consists of two semi-spaces | size_t | 0 |
| --semi-space-growth-factor | factor by which to grow the new space | int | 2 |
| --experimental-new-space-growth-heuristic | Grow the new space based on the percentage of survivors instead of their absolute value. | bool | false |
| --max-old-space-size | max size of the old space | in Mbytes | size_t | 0 |
| --initial-old-space-size | initial old space size | in Mbytes | size_t | 0 |
| --gc-global | always perform global GCs | bool | false |
| --random-gc-interval | Collect garbage after random(0, X  allocations. It overrides gc_interval. | int | 0 |
| --gc-interval | garbage collect after <n> allocations | int | -1 |
| --retain-maps-for-n-gc | keeps maps alive for <n> old space garbage collections | int | 2 |
| --trace-gc | print one trace line following each garbage collection | bool | false |
| --trace-gc-nvp | print one detailed trace line in name=value format after each garbage collection | bool | false |
| --trace-gc-ignore-scavenger | do not print trace line after scavenger collection | bool | false |
| --trace-idle-notification | print one trace line following each idle notification | bool | false |
| --trace-idle-notification-verbose | prints the heap state used by the idle notification | bool | false |
| --trace-gc-verbose | print more details following each garbage collection | bool | false |
| --trace-allocation-stack-interval | print stack trace after <n> free-list allocations | int | -1 |
| --trace-duplicate-threshold-kb | print duplicate objects in the heap if their size is more than given threshold | int | 0 |
| --trace-fragmentation | report fragmentation for old space | bool | false |
| --trace-fragmentation-verbose | report fragmentation for old space | detailed | bool | false |
| --trace-evacuation | report evacuation statistics | bool | false |
| --trace-mutator-utilization | print mutator utilization, allocation speed, gc speed | bool | false |
| --incremental-marking | use incremental marking | bool | true |
| --incremental-marking-wrappers | use incremental marking for marking wrappers | bool | true |
| --trace-unmapper | Trace the unmapping | bool | false |
| --parallel-scavenge | parallel scavenge | bool | true |
| --trace-parallel-scavenge | trace parallel scavenge | bool | false |
| --write-protect-code-memory | write protect code memory | bool | true |
| --concurrent-marking | use concurrent marking | bool | true |
| --parallel-marking | use parallel marking in atomic pause | bool | true |
| --ephemeron-fixpoint-iterations | number of fixpoint iterations it takes to switch to linear ephemeron algorithm | int | 10 |
| --trace-concurrent-marking | trace concurrent marking | bool | false |
| --black-allocation | use black allocation | bool | true |
| --concurrent-store-buffer | use concurrent store buffer processing | bool | true |
| --concurrent-sweeping | use concurrent sweeping | bool | true |
| --parallel-compaction | use parallel compaction | bool | true |
| --parallel-pointer-update | use parallel pointer update during compaction | bool | true |
| --detect-ineffective-gcs-near-heap-limit | trigger out-of-memory failure to avoid GC storm near heap limit | bool | true |
| --trace-incremental-marking | trace progress of the incremental marking | bool | false |
| --trace-stress-marking | trace stress marking progress | bool | false |
| --trace-stress-scavenge | trace stress scavenge progress | bool | false |
| --track-gc-object-stats | track object counts and memory usage | bool | false |
| --trace-gc-object-stats | trace object counts and memory usage | bool | false |
| --trace-zone-stats | trace zone memory usage | bool | false |
| --track-retaining-path | enable support for tracking retaining path | bool | false |
| --concurrent-array-buffer-freeing | free array buffer allocations on a background thread | bool | true |
| --gc-stats | Used by tracing internally to enable gc statistics | int | 0 |
| --track-detached-contexts | track native contexts that are expected to be garbage collected | bool | true |
| --trace-detached-contexts | trace native contexts that are expected to be garbage collected | bool | false |
| --move-object-start | enable moving of object starts | bool | true |
| --memory-reducer | use memory reducer | bool | true |
| --heap-growing-percent | specifies heap growing factor as | 1 + heap_growing_percent/100 | int | 0 |
| --v8-os-page-size | override OS page size | in KBytes | int | 0 |
| --always-compact | Perform compaction on every full GC | bool | false |
| --never-compact | Never perform compaction on full GC - testing only | bool | false |
| --compact-code-space | Compact code space on full collections | bool | true |
| --use-marking-progress-bar | Use a progress bar to scan large objects in increments when incremental marking is active. | bool | true |
| --force-marking-deque-overflows | force overflows of marking deque by reducing it's size to 64 words | bool | false |
| --stress-compaction | stress the GC compactor to flush out bugs | implies --force_marking_deque_overflows | bool | false |
| --stress-compaction-random | Stress GC compaction by selecting random percent of pages as evacuation candidates. It overrides stress_compaction. | bool | false |
| --stress-incremental-marking | force incremental marking for small heaps and run it more often | bool | false |
| --fuzzer-gc-analysis | prints number of allocations and enables analysis mode for gc fuzz testing, e.g. --stress-marking, --stress-scavenge | bool | false |
| --stress-marking | force marking at random points between 0 and X | inclusive  percent of the regular marking start limit | int | 0 |
| --stress-scavenge | force scavenge at random points between 0 and X | inclusive  percent of the new space capacity | int | 0 |
| --disable-abortjs | disables AbortJS runtime function | bool | false |
| --manual-evacuation-candidates-selection | Test mode only flag. It allows an unit test to select evacuation candidates pages | requires --stress_compaction). | bool | false |
| --fast-promotion-new-space | fast promote new space on high survival rates | bool | false |
| --clear-free-memory | initialize free memory with 0 | bool | false |
| --young-generation-large-objects | allocates large objects by default in the young generation large object space | bool | false |
| --debug-code | generate extra code | assertions  for debugging | bool | false |
| --code-comments | emit comments in code disassembly; for more readable source positions you should add --no-concurrent_recompilation | bool | false |
| --enable-sse3 | enable use of SSE3 instructions if available | bool | true |
| --enable-ssse3 | enable use of SSSE3 instructions if available | bool | true |
| --enable-sse4-1 | enable use of SSE4.1 instructions if available | bool | true |
| --enable-sahf | enable use of SAHF instruction if available | X64 only | bool | true |
| --enable-avx | enable use of AVX instructions if available | bool | true |
| --enable-fma3 | enable use of FMA3 instructions if available | bool | true |
| --enable-bmi1 | enable use of BMI1 instructions if available | bool | true |
| --enable-bmi2 | enable use of BMI2 instructions if available | bool | true |
| --enable-lzcnt | enable use of LZCNT instruction if available | bool | true |
| --enable-popcnt | enable use of POPCNT instruction if available | bool | true |
| --arm-arch | generate instructions for the selected ARM architecture if available: armv6, armv7, armv7+sudiv or armv8 | string | armv8 |
| --force-long-branches | force all emitted branches to be in long mode | MIPS/PPC only | bool | false |
| --mcpu | enable optimization for specific cpu | string | auto |
| --partial-constant-pool | enable use of partial constant pools | X64 only | bool | true |
| --enable-armv7 | deprecated | use --arm_arch instead | maybe_bool | unset |
| --enable-vfp3 | deprecated | use --arm_arch instead | maybe_bool | unset |
| --enable-32dregs | deprecated | use --arm_arch instead | maybe_bool | unset |
| --enable-neon | deprecated | use --arm_arch instead | maybe_bool | unset |
| --enable-sudiv | deprecated | use --arm_arch instead | maybe_bool | unset |
| --enable-armv8 | deprecated | use --arm_arch instead | maybe_bool | unset |
| --enable-regexp-unaligned-accesses | enable unaligned accesses for the regexp engine | bool | true |
| --script-streaming | enable parsing on background | bool | true |
| --disable-old-api-accessors | Disable old-style API accessors whose setters trigger through the prototype chain | bool | false |
| --expose-natives-as | expose natives in global object | string | nullptr |
| --expose-free-buffer | expose freeBuffer extension | bool | false |
| --expose-gc | expose gc extension | bool | false |
| --expose-gc-as | expose gc extension under the specified name | string | nullptr |
| --expose-externalize-string | expose externalize string extension | bool | false |
| --expose-trigger-failure | expose trigger-failure extension | bool | false |
| --stack-trace-limit | number of stack frames to capture | int | 10 |
| --builtins-in-stack-traces | show built-in functions in stack traces | bool | false |
| --enable-experimental-builtins | enable new csa-based experimental builtins | bool | false |
| --disallow-code-generation-from-strings | disallow eval and friends | bool | false |
| --expose-async-hooks | expose async_hooks object | bool | false |
| --allow-unsafe-function-constructor | allow invoking the function constructor without security checks | bool | false |
| --force-slow-path | always take the slow path for builtins | bool | false |
| --inline-new | use fast inline allocation | bool | true |
| --trace | trace function calls | bool | false |
| --lazy | use lazy compilation | bool | true |
| --trace-opt | trace lazy optimization | bool | false |
| --trace-opt-verbose | extra verbose compilation tracing | bool | false |
| --trace-opt-stats | trace lazy optimization statistics | bool | false |
| --trace-deopt | trace optimize function deoptimization | bool | false |
| --trace-file-names | include file names in trace-opt/trace-deopt output | bool | false |
| --trace-interrupts | trace interrupts when they are handled | bool | false |
| --opt | use adaptive optimizations | bool | true |
| --always-opt | always try to optimize functions | bool | false |
| --always-osr | always try to OSR functions | bool | false |
| --prepare-always-opt | prepare for turning on always opt | bool | false |
| --trace-serializer | print code serializer trace | bool | false |
| --compilation-cache | enable compilation cache | bool | true |
| --cache-prototype-transitions | cache prototype transitions | bool | true |
| --compiler-dispatcher | enable compiler dispatcher | bool | false |
| --trace-compiler-dispatcher | trace compiler dispatcher activity | bool | false |
| --trace-compiler-dispatcher-jobs | trace progress of individual jobs managed by the compiler dispatcher | bool | false |
| --cpu-profiler-sampling-interval | CPU profiler sampling interval in microseconds | int | 1000 |
| --trace-js-array-abuse | trace out-of-bounds accesses to JS arrays | bool | false |
| --trace-external-array-abuse | trace out-of-bounds-accesses to external arrays | bool | false |
| --trace-array-abuse | trace out-of-bounds accesses to all arrays | bool | false |
| --trace-side-effect-free-debug-evaluate | print debug messages for side-effect-free debug-evaluate for testing | bool | false |
| --hard-abort | abort by crashing | bool | true |
| --expose-inspector-scripts | expose injected-script-source.js for debugging | bool | false |
| --stack-size | default size of stack region v8 is allowed to use | in kBytes | int | 984 |
| --max-stack-trace-source-length | maximum length of function source code printed in a stack trace. | int | 300 |
| --clear-exceptions-on-js-entry | clear pending exceptions when entering JavaScript | bool | false |
| --histogram-interval | time interval in ms for aggregating memory histograms | int | 600000 |
| --heap-profiler-trace-objects | Dump heap object allocations/movements/size_updates | bool | false |
| --heap-profiler-use-embedder-graph | Use the new EmbedderGraph API to get embedder nodes | bool | true |
| --heap-snapshot-string-limit | truncate strings to this length in the heap snapshot | int | 1024 |
| --sampling-heap-profiler-suppress-randomness | Use constant sample intervals to eliminate test flakiness | bool | false |
| --use-idle-notification | Use idle notification to reduce memory footprint. | bool | true |
| --use-ic | use inline caching | bool | true |
| --trace-ic | trace inline cache state transitions for tools/ic-processor | bool | false |
| --ic-stats | inline cache state transitions statistics | int | 0 |
| --native-code-counters | generate extra code for manipulating stats counters | bool | false |
| --thin-strings | Enable ThinString support | bool | true |
| --trace-prototype-users | Trace updates to prototype user tracking | bool | false |
| --use-verbose-printer | allows verbose printing | bool | true |
| --trace-for-in-enumerate | Trace for-in enumerate slow-paths | bool | false |
| --trace-maps | trace map creation | bool | false |
| --trace-maps-details | also log map details | bool | true |
| --allow-natives-syntax | allow natives syntax | bool | false |
| --lazy-inner-functions | enable lazy parsing inner functions | bool | true |
| --aggressive-lazy-inner-functions | even lazier inner function parsing | bool | true |
| --preparser-scope-analysis | perform scope analysis for preparsed inner functions | bool | true |
| --trace-sim | Trace simulator execution | bool | false |
| --debug-sim | Enable debugging the simulator | bool | false |
| --check-icache | Check icache flushes in ARM and MIPS simulator | bool | false |
| --stop-sim-at | Simulator stop after x number of instructions | int | 0 |
| --sim-stack-alignment | Stack alingment in bytes in simulator | 4 or 8, 8 is default | int | 8 |
| --sim-stack-size | Stack size of the ARM64, MIPS64 and PPC64 simulator in kBytes | default is 2 MB | int | 2048 |
| --log-colour | When logging, try to use coloured output. | bool | true |
| --ignore-asm-unimplemented-break | Don't break for ASM_UNIMPLEMENTED_BREAK macros. | bool | false |
| --trace-sim-messages | Trace simulator debug messages. Implied by --trace-sim. | bool | false |
| --stack-trace-on-illegal | print stack trace when an illegal exception is thrown | bool | false |
| --abort-on-uncaught-exception | abort program | dump core  when an uncaught exception is thrown | bool | false |
| --abort-on-stack-or-string-length-overflow | Abort program when the stack overflows or a string exceeds maximum length | as opposed to throwing RangeError). This is useful for fuzzing where the spec behaviour would introduce nondeterminism. | bool | false |
| --randomize-hashes | randomize hashes to avoid predictable hash collisions | with snapshots this option cannot override the baked-in seed | bool | true |
| --rehash-snapshot | rehash strings from the snapshot to override the baked-in seed | bool | true |
| --hash-seed | Fixed seed to use to hash property keys | 0 means random)(with snapshots this option cannot override the baked-in seed | uint64 | 0 |
| --random-seed | Default seed for initializing random generator | 0, the default, means to use system random). | int | 0 |
| --fuzzer-random-seed | Default seed for initializing fuzzer random generator | 0, the default, means to use v8's random number generator seed). | int | 0 |
| --trace-rail | trace RAIL mode | bool | false |
| --print-all-exceptions | print exception object and stack trace on each thrown exception | bool | false |
| --runtime-call-stats | report runtime call counts and times | bool | false |
| --runtime-stats | internal usage only for controlling runtime statistics | int | 0 |
| --print-embedded-builtin-candidates | Prints builtins that are not yet embedded but could be. | bool | false |
| --lazy-deserialization | Deserialize code lazily from the snapshot. | bool | true |
| --lazy-handler-deserialization | Deserialize bytecode handlers lazily from the snapshot. | bool | true |
| --trace-lazy-deserialization | Trace lazy deserialization. | bool | false |
| --profile-deserialization | Print the time it takes to deserialize the snapshot. | bool | false |
| --serialization-statistics | Collect statistics on serialized objects. | bool | false |
| --serialization-chunk-size | Custom size for serialization chunks | uint | 4096 |
| --regexp-optimization | generate optimized regexp code | bool | true |
| --regexp-mode-modifiers | enable inline flags in regexp. | bool | false |
| --testing-bool-flag | testing_bool_flag | bool | true |
| --testing-maybe-bool-flag | testing_maybe_bool_flag | maybe_bool | unset |
| --testing-int-flag | testing_int_flag | int | 13 |
| --testing-float-flag | float-flag | float | 2.5 |
| --testing-string-flag | string-flag | string | Hello, world! |
| --testing-prng-seed | Seed used for threading test randomness | int | 42 |
| --embedded-src | Path for the generated embedded data file. | mksnapshot only | string | nullptr |
| --embedded-variant | Label to disambiguate symbols in embedded data file. | mksnapshot only | string | nullptr |
| --startup-src | Write V8 startup as C++ src. | mksnapshot only | string | nullptr |
| --startup-blob | Write V8 startup blob file. | mksnapshot only | string | nullptr |
| --help | Print usage message, including flags, on console | bool | true |
| --dump-counters | Dump counters on exit | bool | false |
| --dump-counters-nvp | Dump counters as name-value pairs on exit | bool | false |
| --use-external-strings | Use external strings for source code | bool | false |
| --map-counters | Map counters to a file | string | |
| --js-arguments | Pass all remaining arguments to the script. Alias for "--". | arguments | |
| --mock-arraybuffer-allocator | Use a mock ArrayBuffer allocator for testing. | bool | false |
| --log | Minimal logging | no API, code, GC, suspect, or handles samples). | bool | false |
| --log-all | Log all events to the log file. | bool | false |
| --log-api | Log API events to the log file. | bool | false |
| --log-code | Log code events to the log file without profiling. | bool | false |
| --log-handles | Log global handle events. | bool | false |
| --log-suspect | Log suspect operations. | bool | false |
| --log-source-code | Log source code. | bool | false |
| --log-function-events | Log function events | parse, compile, execute  separately. | bool | false |
| --prof | Log statistical profiling information | implies --log-code). | bool | false |
| --detailed-line-info | Always generate detailed line information for CPU profiling. | bool | false |
| --prof-sampling-interval | Interval for --prof samples | in microseconds). | int | 1000 |
| --prof-cpp | Like --prof, but ignore generated code. | bool | false |
| --prof-browser-mode | Used with --prof, turns on browser-compatible mode for profiling. | bool | true |
| --logfile | Specify the name of the log file. | string | v8.log |
| --logfile-per-isolate | Separate log files for each isolate. | bool | true |
| --ll-prof | Enable low-level linux profiler. | bool | false |
| --interpreted-frames-native-stack | Show interpreted frames on the native stack | useful for external profilers). | bool | false |
| --perf-basic-prof | Enable perf linux profiler | basic support). | bool | false |
| --perf-basic-prof-only-functions | Only report function code ranges to perf | i.e. no stubs). | bool | false |
| --perf-prof | Enable perf linux profiler | experimental annotate support). | bool | false |
| --perf-prof-unwinding-info | Enable unwinding info for perf linux profiler | experimental). | bool | false |
| --gc-fake-mmap | Specify the name of the file for fake gc mmap used in ll_prof | string | /tmp/__v8_gc__ |
| --log-internal-timer-events | Time internal events. | bool | false |
| --log-timer-events | Time events including external callbacks. | bool | false |
| --log-instruction-stats | Log AArch64 instruction statistics. | bool | false |
| --log-instruction-file | AArch64 instruction statistics log file. | string | arm64_inst.csv |
| --log-instruction-period | AArch64 instruction statistics logging period. | int | 4194304 |
| --redirect-code-traces | output deopt information and disassembly into file code-<pid>-<isolate id>.asm | bool | false |
| --redirect-code-traces-to | output deopt information and disassembly into the given file | string | nullptr |
| --print-opt-source | print source code of optimized and inlined functions | bool | false |
| --trace-elements-transitions | trace elements transitions | bool | false |
| --trace-creation-allocation-sites | trace the creation of allocation sites | bool | false |
| --print-code-stubs | print code stubs | bool | false |
| --test-secondary-stub-cache | test secondary stub cache by disabling the primary one | bool | false |
| --test-primary-stub-cache | test primary stub cache by disabling the secondary one | bool | false |
| --test-small-max-function-context-stub-size | enable testing the function context size overflow path by making the maximum size smaller | bool | false |
| --print-code | print generated code | bool | false |
| --print-opt-code | print optimized code | bool | false |
| --print-opt-code-filter | filter for printing optimized code | string | * |
| --print-code-verbose | print more information for code | bool | false |
| --print-builtin-code | print generated code for builtins | bool | false |
| --print-builtin-code-filter | filter for printing builtin code | string | * |
| --print-builtin-size | print code size for builtins | bool | false |
| --sodium | print generated code output suitable for use with the Sodium code viewer | bool | false |
| --print-all-code | enable all flags related to printing code | bool | false |
| --predictable | enable predictable mode | bool | false |
| --single-threaded | disable the use of background tasks | bool | false |
| --single-threaded-gc | disable the use of background gc tasks | bool | false |


<style>
@media
only screen and (max-width: 1500px) {
	table, thead, tbody, th, td, tr {
		display: block;
	}
	thead tr {
		position: absolute;
		top: -9999px;
		left: -9999px;
	}
	tr { border: 1px solid #ccc; }
	td {
		border: none;
		border-bottom: 1px solid #eee;
		position: relative;
		padding-left: 200px;
		margin-left: 150px;
	}
	td:before {
		position: absolute;
		top: 12px;
		left: 6px;
		width: 200px;
		padding-right: 40px;
		white-space: nowrap;
		margin-left: -150px;
	}
	td:nth-of-type(1):before { content: "Option"; }
	td:nth-of-type(2):before { content: "Description"; }
	td:nth-of-type(3):before { content: "Type"; }
	td:nth-of-type(4):before { content: "Default";}
}
</style>