# Template Method

You use the Template Method when you have an algorithm that you want to vary.

The idea of the pattern is to build an abstract base class with a template method. The template method makes calls to abstract methods which are supplied by the concrete subclasses.

Try to keep the template method lean; avoid abstract methods and hooks that don't have any real purpose other than preparing your algorithm for every conceivable possibility.

## Example: Monthly Status Reports

### Starting Point

Inside [`v0/main.rb`](v0/main.rb), we have a `Report` class that generates a monthly status report formatted in HTML:

```ruby
report = Report.new
report.output_report
```

### 1st Iteration

In addition to HTML reports, now we need to also produce plain text reports. The code for this iteration can be found in [`v1/main.rb`](v1/main.rb).

The problem with our first iteration is that we're mixing code that formats HTML with code that formats plain text. Because we are mixing code this way we risk breaking the code for existing formats when we add support for new formats.

### 2nd Iteration

We rewrite `Report` so that it's only responsible for performing the basic steps for generating a report. We define two `Report` subclasses, `HTMLReport` and ` PlainTextReport`, that are responsible for the output format:

```ruby
report = HTMLReport.new
report.output_report

report = PlainTextReport.new
report.output_report
```

The code for this iteration can be found in [`v2/main.rb`](v2/main.rb).

### 3rd Iteration

We don't want `PlainTextReport` to define methods that it has no use for (e.g. `output_start`, `output_end`). We provide a hook method implementation for these methods inside the `Report` class in [`v3/main.rb`](v3/main.rb).
