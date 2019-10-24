# `cint` - a confidence interval calculator

`cint` is a simple script to calculate the confidence interval of a collection
of numbers.

The motivation behind it comes from the need to calculate confidence intervals
of program runtime samples. This is a very common task when working to improve
the performance of a program. With that in mind, `cint` aims to solve a very
localized and niche problem but doing it as simple and user friendly as
possible.

## Installation

Just place `cint` somewhere covered by your `$PATH`.

## Using

### **tl;dr**

```
$ cint -n 1 2 3

> 2.0 ± 2.484 (confidence of 0.95)
```

or

```
$ cint --confidence 0.99
1, 2;  3

> 2.0 ± 2.484 (confidence of 0.95)
```

`cint --help` will list all the valid options.

### Confidence level

By default, a confidence level of 0.95 (95%) is used. You can override that
with the `--confidence`/`-c` option.

### Input options

The numbers can be given through three different ways:

- `stdin` (default);
- A csv-like file, using the `--file`/`-f` option; or
- By CLI, using the `--numbers`/`-n` option.

The first two options accept float numbers separated by `\s`, `\n`, `,` or `;`,
and ending with an EOF (for `stdin`, that's `ctrl+D` in most terminals).

The third option only accepts `\s` as separators and the numbers must **not** be
surrounded by quotes.

### Output options

The default output is in the format `mean ± margin of error`. But you can adjust
the output format as you like, using the following tokens:

- `%M`: sample mean
- `%S`: sample standard deviation
- `%E`: margin of error
- `%L`: lower limit of the confidence interval
- `%U`: upper limit of the confidente interval
- `%C`: the confidence level used as decimal
- `%c`: the confidence level as a percentage
- `%[1-4]`: use one of the predefined formats (see bellow)
- `%%`: a single '%' character

To control how many decimal digits to display in the output, use the `--digits`
option.

### Predefined formats

The current predefined formats available are:

- `%1`: '%M ± %E (confidence of %C)'
- `%2`: '\[%L, %U\] (confidence of %C)'
- `%3`: '%L, %U'
- `%4`: 'With %c%% of confidence, the population mean is between %L and %U.'

