# dsh-plugin-doctor-action

> A GitHub Action that runs pre-publish health checks on any DeepSeek Harness plugin - powered by [dsh-plugin-doctor](https://github.com/zoahdev/dsh-plugin-doctor).

One line in your workflow turns "it loads" into "it is checked": manifest structure, patch validity, entry points, files allowlist, and (optionally) a full build + pack + fresh-profile install smoke.

## Usage

```yaml
name: plugin
on: [push, pull_request]

jobs:
  doctor:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: zoahdev/dsh-plugin-doctor-action@v1
        with:
          path: .
          # full: 'true'   # add build + pack + fresh-profile install smoke
```

## Inputs

| Input | Default | Meaning |
| --- | --- | --- |
| `path` | `.` | Plugin directory to check |
| `version` | `v1.13.0` | dsh-plugin-doctor release tag to install |
| `full` | `false` | Also run `--full` (build + pack + fresh-profile install) |

## Outputs

| Output | Meaning |
| --- | --- |
| `ok` | `true` when the plugin passed |

Failures and warnings are also surfaced as GitHub annotations (`::error::` / `::warning::`) and written to the run summary.

## Why

The DeepSeek Harness ecosystem ships plugins as source checkouts, npm packages, and GitHub tarballs - and "loads" is not "callable" (discussions #1965, #1697, #2002). This action makes the same checks the maintainers would run available to every plugin author before a user ever installs it.

## License

MIT
---

# 中文说明

一个 GitHub Action，对任意 DeepSeek Harness 插件跑发布前健康检查，底层是 [dsh-plugin-doctor](https://github.com/zoahdev/dsh-plugin-doctor)。

一行配置，把「能加载」变成「检查过」：清单结构、patch 有效性、入口文件、files 白名单，以及（可选）完整的 build + pack + 全新 profile 安装冒烟测试。

## 用法

```yaml
name: plugin
on: [push, pull_request]

jobs:
  doctor:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: zoahdev/dsh-plugin-doctor-action@v1
        with:
          path: .
          # full: 'true'   # 追加 build + pack + 全新 profile 安装冒烟
```

## 输入参数

| 参数 | 默认值 | 说明 |
| --- | --- | --- |
| `path` | `.` | 要检查的插件目录 |
| `version` | `v1.13.0` | 安装的 dsh-plugin-doctor release 标签 |
| `full` | `false` | 是否也跑 `--full`（build + pack + 全新 profile 安装）|

## 输出

| 输出 | 说明 |
| --- | --- |
| `ok` | 插件通过时为 `true` |

失败和警告会以 GitHub 注解（`::error::` / `::warning::`）呈现，并写入运行摘要。

## 为什么需要它

DeepSeek Harness 生态里的插件以源码、npm 包、git tarball 分发——而「能加载」不等于「能被调用」（讨论 #1965、#1697、#2002）。这个 Action 把维护者会跑的同一套检查，交到每个插件作者手里，在用户安装之前就先发现问题。

## 许可

MIT
