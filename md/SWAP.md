※ChatGPTより
4Gでも大丈夫だった。

## SWAP
スワップファイルの設定は、Raspberry Piのようなリソースが限られたデバイスで特に有効です。スワップファイルを設定することで、物理メモリが不足した場合にディスクを仮想メモリとして使用できるようになります。これにより、メモリ不足によるシステムのフリーズやクラッシュを防ぐことができます。

### スワップファイルの設定手順

以下の手順でスワップファイルを設定します。

#### 1. スワップファイルの作成

```bash
sudo fallocate -l 2G /swapfile
```

ここでは2GBのスワップファイルを作成しています。必要に応じてサイズを変更してください。

#### 2. スワップファイルのパーミッションを設定

```bash
sudo chmod 600 /swapfile
```

#### 3. スワップ領域を設定

```bash
sudo mkswap /swapfile
```

#### 4. スワップファイルを有効化

```bash
sudo swapon /swapfile
```

#### 5. スワップファイルの永続化

再起動後もスワップファイルが有効になるように、`/etc/fstab`にエントリを追加します。

```bash
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
```

### スワップの確認

スワップファイルが正しく設定されているか確認します。

```bash
sudo swapon --show
```

出力例：

```bash
NAME      TYPE SIZE  USED PRIO
/swapfile file 2G    0B   -2
```

### メモリ使用量の確認

スワップファイルを設定した後、システムのメモリ使用状況を確認します。

```bash
free -h
```

出力例：

```bash
              total        used        free      shared  buff/cache   available
Mem:           926M        400M        100M        6.5M        425M        457M
Swap:          2.0G         0B        2.0G
```

スワップファイルを設定することで、メモリ不足によるシステムの不安定性を軽減できます。特に、複数のDockerコンテナを実行している場合や、メモリを大量に使用するアプリケーションを実行している場合に有効です。
