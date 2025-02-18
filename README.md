# ML.NETを使ってみる

## 概要

ML.NETは現在、.NET8にのみ対応しているため、まずはバージョンを確認します。

```bash
dotnet --version
```

実行結果
8.0.406

```bash
sudo dotnet workload update
```

インストールを実行します。今回はmacOS上で対応するため、osx版をインストールします。

```bash
dotnet tool install -g mlnet-osx-x64
```

```bash
dotnet tool install -g mlnet-osx-arm64
```

実行結果
```
ツール ディレクトリ '/Users/ymd65536/.dotnet/tools' は現在、PATH 環境変数にありません。
zsh を使用している場合、次のコマンドを実行してプロファイルに追加できます:

cat << \EOF >> ~/.zprofile
# .NET Core SDK tools
export PATH="$PATH:/Users/ymd65536/.dotnet/tools"
EOF

`zsh -l` を実行して現在のセッションで利用できるようにします。

これは、次のコマンドを実行することによってのみ、現行のセッションに追加できます:

export PATH="$PATH:/Users/ymd65536/.dotnet/tools"

次のコマンドを使用してツールを呼び出せます。mlnet
ツール 'mlnet-osx-x64' (バージョン '16.18.2') が正常にインストールされました。
```

パスを追加します。

```
# .NET Core SDK tools
export PATH="$PATH:$HOME/.dotnet/tools"
```
動作確認

```bash
mlnet --version
```

実行結果
16.18.2+255dca7057095f9c073a8031db28ddf3a2a4ee27

```bash
mkdir myMLApp
cd myMLApp
```

以下のURLからデータセットをダウンロードします。これはサンプルのデータセットがアップロードされているサイトです。
https://archive.ics.uci.edu/dataset/331/sentiment+labelled+sentences

以下のURLからデータセットをダウンロードします。
https://archive.ics.uci.edu/ml/machine-learning-databases/00331/sentiment%20labelled%20sentences.zip

ダウンロードしたデータからyelp_labelled.txtをmyMLAppにコピーします。

```bash
cp ~/Downloads/sentiment\ labelled\ sentences/yelp_labelled.txt .
```

モデルを学習を実行します。
https://dotnet.microsoft.com/ja-jp/learn/ml-dotnet/get-started-tutorial/train

```bash
mlnet classification --dataset "yelp_labelled.txt" --label-col 1 --has-header false --name SentimentModel  --train-time 60
```

モデルを確認するため、ディレクトリを変更します。

```bash
cd SentimentModel
```

SentimentModel.ConsoleApp を実行します。

```bash
dotnet run
```
