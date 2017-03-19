# SIGNAL SUPPORT PAGE

## Startup Magenta!

この節ではMagentaの実行環境のセットアップ手順が記載されていますが、さすがに書籍を見てコマンドを一から叩いていくのはつらすぎると思うので、copy & pasteできるようコマンドを以下に掲載します。

**Let's Try! Magentaを動かそう**

```
GCP_PROJECT_ID=$(gcloud config list project --format "value(core.project)")
```

```
docker-machine create --driver google \
  --google-project $GCP_PROJECT_ID \
  --google-zone asia-northeast1-a \
  --google-machine-type n1-standard-1 \
  --google-machine-image https://www.googleapis.com/compute/v1/projects/ubuntu-os-cloud/global/images/ubuntu-1404-trusty-v20161109 \
  tensorflow-magenta
```

**Let's Try! Magentaで音楽生成しよう**

```
sudo docker run -it -p 6006:6006 -v /tmp/magenta:/magenta-data tensorflow/magenta
```

```
melody_rnn_generate \
  --config=lookback_rnn \
  --bundle_file=/magenta-models/lookback_rnn.mag \
  --output_dir=/magenta-data/lookback_rnn/generated \
  --num_outputs=10 \
  --num_steps=128 \
  --primer_melody="[60]"
```

```
sudo su
# cd /magenta-data/lookback_rnn
# zip -r midi.zip generated/
```

環境の削除

```
docker-machine stop tensorflow-magenta
docker-machine rm tensorflow-magenta
```
