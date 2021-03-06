# TFX Basic Shared Libraries

[![Python](https://img.shields.io/pypi/pyversions/tfx-bsl.svg?style=plastic)](https://github.com/tensorflow/tfx-bsl)
[![PyPI](https://badge.fury.io/py/tfx-bsl.svg)](https://badge.fury.io/py/tfx-bsl)

TFX Basic Shared Libraries (`tfx_bsl`) contains libraries shared by many
[TensorFlow eXtended (TFX)](https://www.tensorflow.org/tfx) components.

__Only symbols exported by sub-modules under `tfx_bsl/public` are intended for
direct use by TFX users__, including by standalone TFX library (e.g. TFDV, TFMA,
TFT) users, TFX pipeline authors and TFX component authors. Those APIs will
become stable and follow semantic versioning once `tfx_bsl` goes beyond `1.0`.

APIs under other directories should be considered internal to TFX
(and therefore there is no backward or forward compatibility guarantee for
them).

Each minor version of a TFX library or TFX itself, if it needs to
depend on `tfx_bsl`, will depend on a specific minor version of it (e.g.
`tensorflow_data_validation` 0.14.\* will depend on, and only work with,
`tfx_bsl` 0.14.\*)

## Installing from PyPI

`tfx_bsl` is available as a [PyPI package](https://pypi.org/project/tfx-bsl/).

```bash
pip install tfx-bsl
```

### Nightly Packages

TFX-BSL also hosts nightly packages at https://pypi-nightly.tensorflow.org on
Google Cloud. To install the latest nightly package, please use the following
command:

```bash
pip install -i https://pypi-nightly.tensorflow.org/simple tfx-bsl
```

This will install the nightly packages for the major dependencies of TFX-BSL
such as TensorFlow Metadata (TFMD).

However it is a dependency of many TFX components and usually as a user you
don't need to install it directly.

## Build with Docker

If you want to build a TFX component from the master branch, past the latest
release, you may also have to build the latest `tfx_bsl`, as that TFX component
might have depended on new features introduced past the latest `tfx_bsl`
release.

Building from Docker is the recommended way to build `tfx_bsl` under Linux,
and is continuously tested at Google.

### 1. Install Docker

Please first install [`docker`](https://docs.docker.com/install/) and
[`docker-compose`](https://docs.docker.com/compose/install/) by following the
directions.

### 2. Clone the `tfx_bsl` repository

```shell
git clone https://github.com/tensorflow/tfx-bsl
cd tfx-bsl
```

Note that these instructions will install the latest master branch of `tfx-bsl`.
If you want to install a specific branch (such as a release branch), pass
`-b <branchname>` to the `git clone` command.

### 3. Build the pip package

Then, run the following at the project root:

```bash
sudo docker-compose build manylinux2010
sudo docker-compose run -e PYTHON_VERSION=${PYTHON_VERSION} manylinux2010
```
where `PYTHON_VERSION` is one of `{35, 36, 37, 38}`.

A wheel will be produced under `dist/`.

### 4. Install the pip package

```shell
pip install dist/*.whl
```

## Build from source

### 1. Prerequisites

#### Install NumPy

If NumPy is not installed on your system, install it now by following [these
directions](https://www.scipy.org/scipylib/download.html).

#### Install Bazel

If Bazel is not installed on your system, install it now by following [these
directions](https://bazel.build/versions/master/docs/install.html).


### 2. Clone the `tfx_bsl` repository

```shell
git clone https://github.com/tensorflow/tfx-bsl
cd tfx-bsl
```

Note that these instructions will install the latest master branch of `tfx_bsl`
If you want to install a specific branch (such as a release branch),
pass `-b <branchname>` to the `git clone` command.

### 3. Build the pip package

`tfx_bsl` wheel is Python version dependent -- to build the pip package that
works for a specific Python version, use that Python binary to run:
```shell
python setup.py bdist_wheel
```

You can find the generated `.whl` file in the `dist` subdirectory.

### 4. Install the pip package

```shell
pip install dist/*.whl
```

## Supported platforms

`tfx_bsl` is tested on the following 64-bit operating systems:

  * macOS 10.12.6 (Sierra) or later.
  * Ubuntu 16.04 or later.
  * Windows 7 or later.
