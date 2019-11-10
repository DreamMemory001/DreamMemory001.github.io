---
layout:     post
title:      总结Tensorflow版本与CUDA及CUDNN版本的对应关系、与keras版本对应关系
subtitle:   详细的总结了Tensorflow的版本对应情况，给自己总结一下。
date:       2019-10-29
author:     TkiChus
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - TkiChus
    - DreamMemory001 Blog
    - DeepLearning
---

# 总结Tensorflow版本与CUDA及CUDNN版本的对应关系、与keras版本对应关系

# Windows

## CPU

| Version           | Python version | Compiler           | Build tools  |
| ----------------- | -------------- | ------------------ | ------------ |
| tensorflow-1.11.0 | 3.5-3.6        | MSVC 2015 update 3 | Cmake v3.6.3 |
| tensorflow-1.10.0 | 3.5-3.6        | MSVC 2015 update 3 | Cmake v3.6.3 |
| tensorflow-1.9.0  | 3.5-3.6        | MSVC 2015 update 3 | Cmake v3.6.3 |
| tensorflow-1.8.0  | 3.5-3.6        | MSVC 2015 update 3 | Cmake v3.6.3 |
| tensorflow-1.7.0  | 3.5-3.6        | MSVC 2015 update 3 | Cmake v3.6.3 |
| tensorflow-1.6.0  | 3.5-3.6        | MSVC 2015 update 3 | Cmake v3.6.3 |
| tensorflow-1.5.0  | 3.5-3.6        | MSVC 2015 update 3 | Cmake v3.6.3 |
| tensorflow-1.4.0  | 3.5-3.6        | MSVC 2015 update 3 | Cmake v3.6.3 |
| tensorflow-1.3.0  | 3.5-3.6        | MSVC 2015 update 3 | Cmake v3.6.3 |
| tensorflow-1.2.0  | 3.5-3.6        | MSVC 2015 update 3 | Cmake v3.6.3 |
| tensorflow-1.1.0  | 3.5            | MSVC 2015 update 3 | Cmake v3.6.3 |
| tensorflow-1.0.0  | 3.5            | MSVC 2015 update 3 | Cmake v3.6.3 |

## GPU

| Version               | Python version | Compiler           | Build tools  | cuDNN | CUDA |
| --------------------- | -------------- | ------------------ | ------------ | ----- | ---- |
| tensorflow_gpu-1.11.0 | 3.5-3.6        | MSVC 2015 update 3 | Bazel 0.15.0 | 7     | 9    |
| tensorflow_gpu-1.10.0 | 3.5-3.6        | MSVC 2015 update 3 | Cmake v3.6.3 | 7     | 9    |
| tensorflow_gpu-1.9.0  | 3.5-3.6        | MSVC 2015 update 3 | Cmake v3.6.3 | 7     | 9    |
| tensorflow_gpu-1.8.0  | 3.5-3.6        | MSVC 2015 update 3 | Cmake v3.6.3 | 7     | 9    |
| tensorflow_gpu-1.7.0  | 3.5-3.6        | MSVC 2015 update 3 | Cmake v3.6.3 | 7     | 9    |
| tensorflow_gpu-1.6.0  | 3.5-3.6        | MSVC 2015 update 3 | Cmake v3.6.3 | 7     | 9    |
| tensorflow_gpu-1.5.0  | 3.5-3.6        | MSVC 2015 update 3 | Cmake v3.6.3 | 7     | 9    |
| tensorflow_gpu-1.4.0  | 3.5-3.6        | MSVC 2015 update 3 | Cmake v3.6.3 | 6     | 8    |
| tensorflow_gpu-1.3.0  | 3.5-3.6        | MSVC 2015 update 3 | Cmake v3.6.3 | 6     | 8    |
| tensorflow_gpu-1.2.0  | 3.5-3.6        | MSVC 2015 update 3 | Cmake v3.6.3 | 5.1   | 8    |
| tensorflow_gpu-1.1.0  | 3.5            | MSVC 2015 update 3 | Cmake v3.6.3 | 5.1   | 8    |
| tensorflow_gpu-1.0.0  | 3.5            | MSVC 2015 update 3 | Cmake v3.6.3 | 5.1   | 8    |

# Linux

## CPU

| Version           | Python version | Compiler | Build tools  |
| ----------------- | -------------- | -------- | ------------ |
| tensorflow-1.11.0 | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.15.0 |
| tensorflow-1.10.0 | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.15.0 |
| tensorflow-1.9.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.11.0 |
| tensorflow-1.8.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.10.0 |
| tensorflow-1.7.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.10.0 |
| tensorflow-1.6.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.9.0  |
| tensorflow-1.5.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.8.0  |
| tensorflow-1.4.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.5.4  |
| tensorflow-1.3.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.4.5  |
| tensorflow-1.2.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.4.5  |
| tensorflow-1.1.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.4.2  |
| tensorflow-1.0.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.4.2  |

## GPU

| Version               | Python version | Compiler | Build tools  | cuDNN | CUDA |
| --------------------- | -------------- | -------- | ------------ | ----- | ---- |
| tensorflow_gpu-1.11.0 | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.15.0 | 7     | 9    |
| tensorflow_gpu-1.10.0 | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.15.0 | 7     | 9    |
| tensorflow_gpu-1.9.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.11.0 | 7     | 9    |
| tensorflow_gpu-1.8.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.10.0 | 7     | 9    |
| tensorflow_gpu-1.7.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.9.0  | 7     | 9    |
| tensorflow_gpu-1.6.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.9.0  | 7     | 9    |
| tensorflow_gpu-1.5.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.8.0  | 7     | 9    |
| tensorflow_gpu-1.4.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.5.4  | 6     | 8    |
| tensorflow_gpu-1.3.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.4.5  | 6     | 8    |
| tensorflow_gpu-1.2.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.4.5  | 5.1   | 8    |
| tensorflow_gpu-1.1.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.4.2  | 5.1   | 8    |
| tensorflow_gpu-1.0.0  | 2.7, 3.3-3.6   | GCC 4.8  | Bazel 0.4.2  | 5.1   | 8    |

# kreas

| Framework        | Env name (--env parameter) | Description                                    | Docker Image                                                 | Packages and Nvidia Settings                                 |
| ---------------- | -------------------------- | ---------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| TensorFlow 1.14  | tensorflow-1.14            | TensorFlow 1.14.0 + Keras 2.2.5 on Python 3.6. | [floydhub/tensorflow](https://hub.docker.com/r/floydhub/tensorflow/) | [TensorFlow-1.14](https://docs.floydhub.com/guides/tensorflow/#tensorflow-114) |
| TensorFlow 1.13  | tensorflow-1.13            | TensorFlow 1.13.0 + Keras 2.2.4 on Python 3.6. | [floydhub/tensorflow](https://hub.docker.com/r/floydhub/tensorflow/) | [TensorFlow-1.13](https://docs.floydhub.com/guides/tensorflow/#tensorflow-113) |
| TensorFlow 1.12  | tensorflow-1.12            | TensorFlow 1.12.0 + Keras 2.2.4 on Python 3.6. | [floydhub/tensorflow](https://hub.docker.com/r/floydhub/tensorflow/) | [TensorFlow-1.12](https://docs.floydhub.com/guides/tensorflow/#tensorflow-112) |
|                  | tensorflow-1.12:py2        | TensorFlow 1.12.0 + Keras 2.2.4 on Python 2.   | [floydhub/tensorflow](https://hub.docker.com/r/floydhub/tensorflow/) |                                                              |
| TensorFlow 1.11  | tensorflow-1.11            | TensorFlow 1.11.0 + Keras 2.2.4 on Python 3.6. | [floydhub/tensorflow](https://hub.docker.com/r/floydhub/tensorflow/) | [TensorFlow-1.11](https://docs.floydhub.com/guides/tensorflow/#tensorflow-111) |
|                  | tensorflow-1.11:py2        | TensorFlow 1.11.0 + Keras 2.2.4 on Python 2.   | [floydhub/tensorflow](https://hub.docker.com/r/floydhub/tensorflow/) |                                                              |
| TensorFlow 1.10  | tensorflow-1.10            | TensorFlow 1.10.0 + Keras 2.2.0 on Python 3.6. | [floydhub/tensorflow](https://hub.docker.com/r/floydhub/tensorflow/) | [TensorFlow-1.10](https://docs.floydhub.com/guides/tensorflow/#tensorflow-110) |
| TensorFlow 1.4.0 | tensorflow-1.4.0           | TensorFlow 1.4.0 + Keras 2.0.8 on Python 3.5.  |                                                              |                                                              |
| TensorFlow 1.7.0 | tensorflow-1.7.0           | TensorFlow 1.7.0 + Keras 2.0.8 on Python 3.6.  |                                                              |                                                              |
| Tensorflow 1.6.0 | tensorflow-1.6.0           | TensorFlow 1.6.0 + Keras 2.1.5 on Python 3.6.  |                                                              |                                                              |

