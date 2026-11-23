# APTVserver 镜像中的第三方软件

APTVserver 镜像包含下列第三方软件，它们各自按原许可分发。镜像内的 `/licenses/` 目录有完整原文：

| 组件 | 版本 | 许可 | 镜像内原文 | 对应源码 |
| --- | --- | --- | --- | --- |
| Jellyfin FFmpeg | 8.1.3-2（Debian bookworm 官方包，按 SHA-256 固定） | GPL-3.0-or-later（该构建启用了 GPL 组件） | `/licenses/system/GPL-3`、`/licenses/system/jellyfin-ffmpeg8.copyright` | <https://github.com/jellyfin/jellyfin-ffmpeg/tree/v8.1.3-2> |
| SQLite | 3.54.1（从官方源码构建，见 `tools/build-sqlite-runtime.sh`） | Public Domain | — | <https://sqlite.org/download.html> |
| Python | 3.12（官方 `python:3.12-slim-bookworm` 镜像，按摘要固定） | PSF-2.0 | 镜像内 Python 自带 | <https://www.python.org/downloads/source/> |
| Debian bookworm 基础系统 | 随基础镜像 | 各包不同，见 `/usr/share/doc/*/copyright` | `/usr/share/doc/` | <https://sources.debian.org/> |
| Python 依赖（FastAPI、uvicorn、Pillow、cryptography、zeroconf 等） | 见 `/licenses/python-packages.txt` | MIT / BSD / Apache-2.0 / ISC / MPL-2.0 / LGPL-2.1（zeroconf）等 | `/licenses/python/<包名>/` | PyPI 上对应版本的源码包 |
| QR Code generator（Project Nayuki） | 1.8.0，已内嵌于 `aptvserver/vendor/qrcodegen.py` | MIT | 文件头 | <https://github.com/nayuki/QR-Code-generator> |

## GPL 组件说明

FFmpeg 以 Jellyfin 官方发行的独立程序（`/usr/lib/jellyfin-ffmpeg/ffmpeg`、`ffprobe`）形式存在。APTVserver 只以子进程方式调用它，
没有链接或修改它。上表给出的是对应版本的完整源码地址。如果该地址失效，可以向发行方索取同版本源码，
发行方会在三年内免费提供。

zeroconf 以未修改的 Python 包形式安装，可以用 pip 替换为其他兼容版本。

## 获取原文

```sh
docker run --rm --entrypoint ls <镜像> -R /licenses
docker run --rm --entrypoint cat <镜像> /licenses/python-packages.txt
```
