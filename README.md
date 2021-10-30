# 概要

* VS CodeでC++を使った開発を行うためのサンプルプロジェクトです。
* VS Code上で以下の様な環境を手軽に構築することを目的にしています。
  * Dockerコンテナ上にUbuntu20.04の環境を構築する。
  * g++, clang++でビルドできる。
  * CMakeでビルドできる。
  * Clang-Formatを使用できる。

## 使い方

### Linuxの場合

#### 前提条件

* ホスト環境にはVS Codeをインストールし、拡張機能`Remote Development`もインストールしておいてください。
* プロジェクトの動作は以下の環境でのみ確認しています。

```text
user@user-ubuntu:~$ cat /etc/issue
Ubuntu 18.04.6 LTS \n \l
user@user-ubuntu:~$ docker version
Client: Docker Engine - Community
 Version:           20.10.10
 API version:       1.41
 Go version:        go1.16.9
 Git commit:        b485636
 Built:             Mon Oct 25 07:42:57 2021
 OS/Arch:           linux/amd64
 Context:           default
 Experimental:      true

Server: Docker Engine - Community
 Engine:
  Version:          20.10.10
  API version:      1.41 (minimum version 1.12)
  Go version:       go1.16.9
  Git commit:       e2f740d
  Built:            Mon Oct 25 07:41:06 2021
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.4.11
  GitCommit:        5b46e404f6b9f661a205e28d59c982d3634148f8
 runc:
  Version:          1.0.2
  GitCommit:        v1.0.2-0-g52b36a2
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
user@user-ubuntu:~$ code --version
1.61.2
6cba118ac49a1b88332f312a8f67186f7f3c1643
x64
```

#### コンテナ生成

* 本プロジェクトを適当な場所にCloneしてください。

```text
git clone https://github.com/nphsgw/vscode_cpp_sample
```

* VS Codeで本プロジェクトを開き右下に表示される`Reopen in Container`ボタンをクリックしてください。

* VS Codeが再起動し左下に`Dev Container: C++`と表示されたら終了です。
  * 初回はイメージのビルドが入るのしばらく時間がかかります。

#### コンテナ起動後

* 拡張機能について
  * VS Codeの拡張機能はデフォルトでは`C/C++`, `Docker`, `Language Pack`が有効になっています。
  * 必要に応じて`CMake Tools`, `Clang-Format`, `Visual Studio IntelliCode`, `GitLens`, `Git History`などをインストールしておくと便利です。
* clang-formatについて
  * 以下のコマンドでclang-format`ファイルを作成することでファイル保存時にフォーマットを適用してくれます。

```text
clang-format -dump-config -style=Google > .clang-format
```

* ビルドについて
  * g++とclang++で`main.cpp`がビルドでき、実行できるか確認してください。
    * `ctrl + shift + b`でどのビルド設定を使用するか選択できます。
    * `F5`でデバッガが起動することを確認してください。
  * CMakeでのビルドは以下のコマンドで実行します。
    * `CMake Tools`をインストールしていると、`CMake: Quick Start`を使うことで`build`フォルダと`CMakeLists.txt`を自動生成してくれるので便利です。

```text
# g++でビルドする場合
cd build
cmake ..
make

# clang++でビルドする場合
cd build
cmake -C ../clang-cmake.cmake ..
make
```

### Windowsの場合

* 確認できていませんが`WSL2`と`Docker Desktop`がインストールされていればLinux版と同様にできるはずです。
