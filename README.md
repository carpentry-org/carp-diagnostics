# carp-diagnostics

A high-performance, robust, and extensible diagnostics, logging, and error tracking library for the [Carp](https://github.com/carp-lang/Carp) programming language.

This library provides structured logging (to console and/or file) and hierarchical performance profiling with statistical analysis (average, min/max, standard deviation/jitter, frame budget spikes, and percentage contribution).

## Features
- **Structured Logging**: Multiple severity levels (`Debug`, `Info`, `Warning`, `Error`, `Critical`) outputting timestamps.
- **Error Tracking**: Global error code and message tracking.
- **Performance Profiling**: 
  - Dynamic zone-based microsecond timing.
  - Automatic computation of runs count, average execution time, standard deviation, and min/max bounds.
  - Spikes tracking (specifically flags runs taking longer than 16.67ms, which would drop frames under a 60 FPS target).
  - Relative frame time percentages.

## Examples

See [examples.md](examples.md) for usage examples.

## License
MIT
