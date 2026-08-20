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

## Usage

```carp
(load "carp-diagnostics/diagnostics.carp")
(use Diagnostics)

(defn main []
  (let [diag (Diagnostics.new "app.log")]
    (do
      ;; 1. Logging
      (Diagnostics.log! &diag (LogLevel.Info) @"Application started")
      
      ;; 2. Profile a block using the with-zone macro
      (Diagnostics.with-zone &diag @"Total Frame Time"
        (do
          (Diagnostics.with-zone &diag @"Physics Update"
            (System.sleep-micros 5000))
          (Diagnostics.with-zone &diag @"Render Update"
            (System.sleep-micros 8000))))
      
      ;; 3. Print the performance profile report
      (Diagnostics.print-stats! &diag)
      
      ;; 4. Error reporting
      (Diagnostics.report-error! &diag 404 @"Asset not found")
      (if (Diagnostics.has-error &diag)
        (println* "Last error msg: " (Diagnostics.last-error-msg &diag))
        ()))))
```

## License
MIT
