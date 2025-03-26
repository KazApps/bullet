# はじめに

### Rust のインストール

[rustup](https://www.rust-lang.org/tools/install) を使って Rust をインストールしてください (これが Rust の公式インストール方法です)。

### 基本的な使い方

`bullet` はクレートとして使用できます。
```toml
bullet = { git = "https://github.com/jw1912/bullet" }
```
または、[examples](https://github.com/jw1912/bullet/tree/main/examples) のいずれかを編集して実行します。
```
cargo r -r --example <example name>
```

基本的な推論の例は [examples/simple](https://github.com/jw1912/bullet/tree/main/examples/simple.rs) に含まれています。NNUE をトレーニングしたことがない場合は、これと似たアーキテクチャとトレーニングスケジュールから始めることをお勧めします。

### ユーティリティ

`bullet-utils` は `cargo b -r --package bullet-utils` でビルドできます。これにより、次のことが可能になります。
- データ形式の変換
- 複数のデータファイルのインターリーブ
- データファイルのシャッフル
- データファイルの検証

具体的な使用方法については、`./target/release/bullet-utils[.exe] help` を使用してください。

これには CUDA または HIP は**必要ありません**。

### バックエンド

#### 一般
`bullet` をビルドするには、C++ コンパイラが必要です (`nvcc` または `hipcc` によって呼び出されます)。
- Windows では、これは `cl.exe` である必要があります (Visual Studio のインストールが必要です)。
- Linux では、`clang` を使用することをお勧めします。
    - 環境変数 `CXX` または `HOST_CXX` にコンパイラ名を指定する必要がある場合があります。

#### CUDA
`bullet_lib` をコンパイルする際のデフォルトのバックエンド。
- [CUDA Toolkit](https://developer.nvidia.com/cuda-toolkit) をインストールします。
- CUDA バージョン >= 12.2 が必要です。
- 環境変数 `CUDA_PATH` を CUDA のインストール場所 ( `bin`、`lib`、`include` ディレクトリを含む必要があります) に設定する必要があります。
- システムの `PATH` に `%CUDA_PATH%\bin` (または Linux の場合は同等のもの) を含める必要があります。

#### HIP
AMD GPU をお持ちのユーザー向け。
- `hip` 機能を有効にします。
- [HIP SDK](https://rocm.docs.amd.com/projects/install-on-windows/en/latest/how-to/install.html) をインストールします。
- 環境変数 `HIP_PATH` を HIP のインストール場所 ( `bin`、`lib`、`include` ディレクトリを含む必要があります) に設定する必要があります。
- システムの `PATH` に `%HIP_PATH%\bin` (または Linux の場合は同等のもの) を含める必要があります。
- Linux では、`GCN_ARCH_NAME` 環境変数を指定する必要があります。これは `rocminfo` を使用して見つけることができます。

#### CPU
CPU でトレーニングする必要がある場合は、[legacy branch](https://github.com/jw1912/bullet/tree/legacy) を使用できます。
