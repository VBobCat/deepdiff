# DeepDiff v 8.0.1

![Downloads](https://img.shields.io/pypi/dm/deepdiff.svg?style=flat)
![Python Versions](https://img.shields.io/pypi/pyversions/deepdiff.svg?style=flat)
![License](https://img.shields.io/pypi/l/deepdiff.svg?version=latest)
[![Build Status](https://github.com/seperman/deepdiff/workflows/Unit%20Tests/badge.svg)](https://github.com/seperman/deepdiff/actions)
[![codecov](https://codecov.io/gh/seperman/deepdiff/branch/master/graph/badge.svg?token=KkHZ3siA3m)](https://codecov.io/gh/seperman/deepdiff)

## Modules

- [DeepDiff](https://zepworks.com/deepdiff/current/diff.html): Deep Difference of dictionaries, iterables, strings, and ANY other object.
- [DeepSearch](https://zepworks.com/deepdiff/current/dsearch.html): Search for objects within other objects.
- [DeepHash](https://zepworks.com/deepdiff/current/deephash.html): Hash any object based on their content.
- [Delta](https://zepworks.com/deepdiff/current/delta.html): Store the difference of objects and apply them to other objects.
- [Extract](https://zepworks.com/deepdiff/current/extract.html): Extract an item from a nested Python object using its path.
- [commandline](https://zepworks.com/deepdiff/current/commandline.html): Use DeepDiff from commandline.

Tested on Python 3.8+ and PyPy3.

- **[Documentation](https://zepworks.com/deepdiff/8.0.1/)**

## What is new?

Please check the [ChangeLog](CHANGELOG.md) file for the detailed information.

DeepDiff 8-0-1

- Bugfix. Numpy should be optional.

DeepDiff 8-0-0

With the introduction of `threshold_to_diff_deeper`, the values returned are different than in previous versions of DeepDiff. You can still get the older values by setting `threshold_to_diff_deeper=0`. However to signify that enough has changed in this release that the users need to update the parameters passed to DeepDiff, we will be doing a major version update.

- `use_enum_value=True` makes it so when diffing enum, we use the enum's value. It makes it so comparing an enum to a string or any other value is not reported as a type change.
- `threshold_to_diff_deeper=float` is a number between 0 and 1. When comparing dictionaries that have a small intersection of keys, we will report the dictionary as a `new_value` instead of reporting individual keys changed. If you set it to zero, you get the same results as DeepDiff 7.0.1 and earlier, which means this feature is disabled. The new default is 0.33 which means if less that one third of keys between dictionaries intersect, report it as a new object.
- Deprecated `ordered-set` and switched to `orderly-set`. The `ordered-set` package was not being maintained anymore and starting Python 3.6, there were better options for sets that ordered. I forked one of the new implementations, modified it, and published it as `orderly-set`.
- Added `use_log_scale:bool` and `log_scale_similarity_threshold:float`. They can be used to ignore small changes in numbers by comparing their differences in logarithmic space. This is different than ignoring the difference based on significant digits.
- json serialization of reversed lists.
- Fix for iterable moved items when `iterable_compare_func` is used.
- Pandas and Polars support.

DeepDiff 7-0-1

- Fixes the translation between Difflib opcodes and Delta flat rows.

DeepDiff 7-0-0

- DeepDiff 7 comes with an improved delta object. [Delta to flat dictionaries](https://zepworks.com/deepdiff/current/serialization.html#delta-serialize-to-flat-dictionaries) have undergone a major change. We have also introduced [Delta serialize to flat rows](https://zepworks.com/deepdiff/current/serialization.html#delta-serialize-to-flat-rows).
- Subtracting delta objects have dramatically improved at the cost of holding more metadata about the original objects.
- When `verbose=2`, and the "path" of an item has changed in a report between t1 and t2, we include it as `new_path`.
- `path(use_t2=True)` returns the correct path to t2 in any reported change in the [`tree view`](https://zepworks.com/deepdiff/current/view.html#tree-view)
- Python 3.7 support is dropped and Python 3.12 is officially supported.


DeepDiff 6-7-1

- Support for subtracting delta objects when iterable_compare_func is used.
- Better handling of force adding a delta to an object. 
- Fix for [`Can't compare dicts with both single and double quotes in keys`](https://github.com/seperman/deepdiff/issues/430)
- Updated docs for Inconsistent Behavior with math_epsilon and ignore_order = True

DeepDiff 6-7-0

- Delta can be subtracted from other objects now.
- verify_symmetry is deprecated. Use bidirectional instead.
- always_include_values flag in Delta can be enabled to include values in the delta for every change.
- Fix for Delta.__add__ breaks with esoteric dict keys.
- You can load a delta from the list of flat dictionaries.

DeepDiff 6-6-1

- Fix for [DeepDiff raises decimal exception when using significant digits](https://github.com/seperman/deepdiff/issues/426)
- Introducing group_by_sort_key
- Adding group_by 2D. For example `group_by=['last_name', 'zip_code']`


## Installation

### Install from PyPi:

`pip install deepdiff`

If you want to use DeepDiff from commandline:

`pip install "deepdiff[cli]"`

If you want to improve the performance of DeepDiff with certain functionalities such as improved json serialization:

`pip install "deepdiff[optimize]"`

Install optional packages:
- [yaml](https://pypi.org/project/PyYAML/)
- [tomli](https://pypi.org/project/tomli/) (python 3.10 and older) and [tomli-w](https://pypi.org/project/tomli-w/) for writing
- [clevercsv](https://pypi.org/project/clevercsv/) for more rubust CSV parsing
- [orjson](https://pypi.org/project/orjson/) for speed and memory optimized parsing
- [pydantic](https://pypi.org/project/pydantic/)


# Documentation

<https://zepworks.com/deepdiff/current/>

### A message from Sep, the creator of DeepDiff

> 👋 Hi there,
>
> Thank you for using DeepDiff!
> As an engineer, I understand the frustration of wrestling with **unruly data** in pipelines.
> That's why I developed a new tool - [Qluster](https://qluster.ai/solution) to empower non-engineers to control and resolve data issues at scale autonomously and **stop bugging the engineers**! 🛠️
>
> If you are going through this pain now, I would love to give you [early access](https://www.qluster.ai/try-qluster) to Qluster and get your feedback.


# ChangeLog

Please take a look at the [CHANGELOG](CHANGELOG.md) file.

# Survey

:mega: **Please fill out our [fast 5-question survey](https://forms.gle/E6qXexcgjoKnSzjB8)** so that we can learn how & why you use DeepDiff, and what improvements we should make. Thank you! :dancers:

# Contribute

1. Please make your PR against the dev branch
2. Please make sure that your PR has tests. Since DeepDiff is used in many sensitive data driven projects, we strive to maintain around 100% test coverage on the code.

Please run `pytest --cov=deepdiff --runslow` to see the coverage report. Note that the `--runslow` flag will run some slow tests too. In most cases you only want to run the fast tests which so you wont add the `--runslow` flag.

Or to see a more user friendly version, please run: `pytest --cov=deepdiff --cov-report term-missing --runslow`.

Thank you!

# Authors

Please take a look at the [AUTHORS](AUTHORS.md) file.
