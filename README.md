# baseplate.go

[Baseplate][baseplate.py] implemented in go.

## Documentation

[Code documentation][godev]

## IDE/Editor setup

See [here](Editor.md).

## Code style guide

See [here](Style.md).

## Thrift generated files

The `internal/gen-go/` directory contains thrift generated files,
with `*-remote` directories removed.
They are excluded from the linter.
DO NOT EDIT.

They were generated with [thrift compiler c2ddaf0][thrift-version] against
[`baseplate.thrift`][baseplate.thrift] and
[`edgecontext.thrift`][edgecontext.thrift]
using the following commands under `internal/`:

```
thrift --gen go:package_prefix=github.com/reddit/baseplate.go/ path/to/baseplate.thrift
thrift --gen go:package_prefix=github.com/reddit/baseplate.go/ path/to/edgecontext.thrift
find gen-go -depth -name "*-remote" -type d -exec rm -Rf {} \;
```

They are needed by some of the Baseplate.go packages.
We did not include those thrift files into this repo to avoid duplications.
This directory will be regenerated when either thrift compiler or the thrift
files changed significantly.

## Bazel support

This project also comes with *optional* [Bazel][bazel] support.
It's optional as in you can totally ignore Bazel and still use the go toolchain,
but the added support will make it easier for projects using Bazel to add this
project as a dependency.

When you made a change to `go.mod` file,
please run the following command to reflect the changes in Bazel:

```
bazel run //:gazelle -- update-repos -from_file=go.mod -prune
```

Or just use the script we used in CI:

```
./scripts/bazel_cleanup.sh
```

To run tests via Bazel, use the following command:

```
bazel test //...:all
```


[baseplate.py]: https://github.com/reddit/baseplate.py

[baseplate.thrift]: https://github.com/reddit/baseplate.py/blob/c7fd98cea3865159690c07301b9ff12aabb8e61e/baseplate/thrift/baseplate.thrift

[edgecontext.thrift]: https://github.com/reddit/edgecontext.py/blob/420e58728ee7085a2f91c5db45df233142b251f9/reddit_edgecontext/edgecontext.thrift

[bazel]: https://bazel.build/

[godev]: https://pkg.go.dev/github.com/reddit/baseplate.go

[thrift-version]: https://github.com/apache/thrift/tree/c2ddaf0766499ab522cb7c0ca011d579707fcb5f
