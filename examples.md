# Examples

## Basic Usage

Logging messages, timing execution zones, printing stats reports, and tracking errors:

```clojure
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
