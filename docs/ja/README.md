<div align="center">

# bullet

</div>

ドメイン固有のMLライブラリで、一般的に世界最強のチェスエンジンのためにNNUEスタイルのネットワークをトレーニングするために使用されます。

### クレート

- **bullet_core**
    - バックエンドに依存しない汎用的なMLフレームワーク：
    - ネットワークグラフは`GraphBuilder`を使って構築されます。
    - これは`GraphIR`に変換され、最適化パスが実行されます。
    - `GraphIR`は、特定のバックエンドデバイス用の`Graph<D: Device>`にコンパイルされます。
        - これにより、順伝播と逆伝播、重み/入力の編集などが実行できます。
        - グラフを取り込み、その更新メソッドを提供する（構成可能な）オプティマイザの小さなセットが含まれています。
    - クレートの正確性および他のバックエンド実装を検証するために、トークンシングルスレッドCPUバックエンドが含まれています。
- **bullet_hip_backend**
    - 現在、HIP（AMD GPU用）とCUDAバックエンドの両方が含まれています。HIPバックエンドを使用するには、`hip`機能を有効にします。
- **bullet_lib**
    - チェス（および他のゲーム、例えばAtaxx）関連のネットワークを簡単にトレーニングするために、上記のクレートの周りに高レベルのラッパーを提供します。
- **bullet-utils**
    - データの処理に関する様々なユーティリティ

### NNUE/Value Networkトレーニングでの使用法

使用する前に、[ドキュメント](0-contents.md)を確認してください。
これらには、bulletの構築、トレーニングデータの管理、ネットワーク出力形式に関するすべての主要な情報が含まれています。

ほとんどの人は単にリポジトリをクローンし、[examples](../../examples)のいずれかを好みに合わせて編集します。
アップストリームからプルしやすいように独自のサンプルファイルを作成する場合は、[`bullet_lib`の`Cargo.toml`](../../crates/bullet_lib/Cargo.toml)にサンプルを追加する必要があります。

または、`bullet_lib`クレートを次のようにインポートします。
```toml
bullet = { git = "https://github.com/jw1912/bullet", package = "bullet_lib" }
```

特定のAPIドキュメントは、Rustのドキュメンテーション文字列でカバーされています。

### ヘルプ/フィードバック

- バグ報告/機能リクエストを提出するには、issueを開いてください。
- 問題が発生した場合は、[Engine Programming](https://discord.com/invite/F6W6mMsTGN) discordサーバーの専用`#bullet`チャンネルを自由に使用してください。
- 一般的なトレーニングに関する議論については、Engine Programmingの`#bullet`以外のチャンネル、または[Stockfish](https://discord.gg/GWDRS3kU6R) discordの`#engines-dev`が適切です。
