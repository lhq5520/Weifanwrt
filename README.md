<img width="1491" height="780" alt="2353d235-66c9-41fa-86e7-6b789002f060" src="https://github.com/user-attachments/assets/fe0fb290-6967-4a96-9014-39fe810a4dbc" />

<img width="945" height="585" alt="d992f356-d2f6-4a81-a6f9-be8e3dc5dd7a" src="https://github.com/user-attachments/assets/ef04ccc3-2c17-42a2-99af-fdb80ca0fe46" />

Custom ImmortalWrt build configs by Weifan.  
Compiled firmware images are available under [Releases](../../releases).
Project: WeifanWrt

Purpose:
This repository stores personal OpenWrt/ImmortalWrt build configurations and usage notes.
Compiled firmware images are not committed to the branch; they are published under GitHub Releases.
To keep the repository lightweight, the official source code is linked as a submodule under ./upstream.

Downloads:
Firmware images, .config, diffconfig, feeds.conf.default, and SHA256SUMS are all uploaded to the Releases page.

Repo contents:

.config Full build configuration

diffconfig Minimal diff configuration (optional)

feeds.conf.default Feed source record

upstream/ Official source code (as a git submodule)

Other: README, scripts, .gitignore, etc.

Quick start (build locally):

Clone this repository with submodules (shallow clone for lightweight):
git clone --recurse-submodules --shallow-submodules https://github.com/lhq5520/WeifanWrt.git

cd WeifanWrt

If you already cloned the repo, initialize submodules with:
git submodule update --init --depth 1

Apply config and build:
cp .config upstream/
cd upstream
make defconfig
./scripts/feeds update -a
./scripts/feeds install -a
make -j$(nproc)

Default information (if not changed):
Login IP: 192.168.1.1
Username: root
Password: (empty)

Reproducible build (using diffconfig, optional):

Copy diffconfig into upstream:
cp diffconfig upstream/.config

Generate full config:
cd upstream
make defconfig

Continue with feeds update and build as above.

Release (for users):
All firmware images, .config/diffconfig, feeds.conf.default, and SHA256SUMS are provided in Releases.
Always download firmware from Releases instead of branch files.

Owner notes: Maintaining upstream (submodule workflow):
A) Update upstream to latest master (shallow):
cd upstream
git fetch --depth 1 origin master
git checkout -q FETCH_HEAD
cd ..
git add upstream
git commit -m "bump upstream to latest master"
git push

B) Switch upstream to official branch (example openwrt-23.05):
cd upstream
git fetch --depth 1 origin openwrt-23.05
git checkout -q FETCH_HEAD
cd ..
git add upstream
git commit -m "point upstream to openwrt-23.05"
git push

C) Pin upstream to a specific commit (reproducible build):
cd upstream
git fetch origin
git checkout <commit-sha>
cd ..
git add upstream
git commit -m "pin upstream to <commit-sha>"
git push

D) Daily developer notes:

After pulling this repo, always run:
git submodule update --init --depth 1

To update upstream: fetch + checkout inside upstream, then commit the updated submodule pointer in main repo.

Do not commit bin/, build_dir/, dl/, tmp/, etc. Build outputs belong in Releases only.

Lightweight tips:

Use .gitignore to exclude build_dir, staging_dir, tmp, dl, bin, etc. to prevent repo bloat.

Official repo links (reference only):
ImmortalWrt: https://github.com/immortalwrt/immortalwrt

OpenWrt: https://github.com/openwrt/openwrt

In descriptions, avoid sensitive keywords; simply describe them as “network tools” or “extensions”.

Troubleshooting:

If upstream folder is empty after clone:
git submodule update --init --depth 1

If build dependencies are missing:
Install required build tools (build-essential, gcc/g++, ncurses, zlib, openssl, etc.).

If submodule changes are not effective:
Run git add upstream and commit, then push so others get the same submodule pointer.

----------------------------------------------------------------------------------------------------------
Project: WeifanWrt

Purpose:
本仓库保存个人的 OpenWrt/ImmortalWrt 构建配置与说明。固件镜像不放在分支里，统一放到 GitHub Releases。为保持仓库轻量，官方源码以子模块（submodule）方式挂载在 ./upstream。

Downloads:
固件镜像、.config、diffconfig、SHA256SUMS 请到 Releases 页面下载。

Repo contents:

.config 构建用完整配置

diffconfig 可选，小型差异配置（如果有）

feeds.conf.default feed 源记录

upstream/ 官方源码（以 submodule 形式存在）

其他：README、脚本、.gitignore 等

Quick start (build locally):

克隆本仓库并初始化子模块（浅克隆，保持轻量）
git clone --recurse-submodules --shallow-submodules https://github.com/lhq5520/WeifanWrt.git

cd WeifanWrt

如果是已克隆的仓库，首次或拉取后请执行：
git submodule update --init --depth 1

将配置应用到源码并构建
cp .config upstream/
cd upstream
make defconfig
./scripts/feeds update -a
./scripts/feeds install -a
make -j$(nproc)

默认信息（如未更改）
管理地址: 192.168.1.1
账号: root
密码: 无（空）

Reproducible build (使用 diffconfig，可选):

在仓库根目录：
cp diffconfig upstream/.config

进入 upstream 并生成完整配置：
cd upstream
make defconfig

之后同 Quick start 的步骤继续更新 feeds 与构建。

Release（给使用者的说明）:
固件、.config/diffconfig、feeds.conf.default、SHA256SUMS 会在每次发布时一并上传到 Releases。请优先从 Releases 下载，不要从分支里找镜像文件。

Owner notes: 维护上游版本（submodule 工作流）
A) 将 upstream 指向官方最新提交（保持浅历史）
cd upstream
git fetch --depth 1 origin master
git checkout -q FETCH_HEAD
cd ..
git add upstream
git commit -m "bump upstream to latest master"
git push

B) 切换到官方指定分支（例如 openwrt-23.05）
cd upstream
git fetch --depth 1 origin openwrt-23.05
git checkout -q FETCH_HEAD
cd ..
git add upstream
git commit -m "point upstream to openwrt-23.05"
git push

C) 固定到某个具体提交（精确可复现）
cd upstream
git fetch origin
git checkout <commit-sha>
cd ..
git add upstream
git commit -m "pin upstream to <commit-sha>"
git push

D) 开发者同步日常提示

主仓库拉取后，务必执行：
git submodule update --init --depth 1

若需要更新到官方最新：
在 upstream 目录内 fetch + checkout 到最新，再回主仓库提交“子模块指针”变更。

不要把 bin/、build_dir/、dl/ 等编译产物加入版本库；镜像只放 Releases。

Lightweight tips:

使用 .gitignore 忽略 build_dir、staging_dir、tmp、dl、bin 等目录，避免仓库膨胀。

官方仓库链接（仅引用，不直接复制源码）：
ImmortalWrt: https://github.com/immortalwrt/immortalwrt

OpenWrt: https://github.com/openwrt/openwrt

描述中避免出现敏感词，统一称为“网络功能扩展 / network tools”。

Troubleshooting:

首次克隆后 upstream 目录为空：
运行 git submodule update --init --depth 1

构建依赖缺失：
根据官方文档安装编译依赖（build-essential、gcc/g++、ncurses、zlib、openssl 等）。

子模块改动未生效：
在主仓库执行 git add upstream 并提交，推送后他人拉取就会得到相同的 upstream 指针。
