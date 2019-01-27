# Apache_Flink_ksu

This is a repository for researcher in ksu.

Edited WordCount.java to use Contention Aware Metrics.

使い方 / To Use
前準備：Apache Mavenをbash_profileなどで使える状態にする
このパッケージを
$ mvn clean package -DskipTests
でコンパイルすると, "/build-target"という実行用ファイルができる.
/build-targetに移動して, 
$ ./bin/start-cluster.sh
を2回でローカルサーバーを2つ起動. 

netcatのローカルサーバーに2GBあるasfi.txtを突っ込む
$ nc -l 9000 < asfi.txt 
これはasfi.txtｄがあるディレクトリでやればいい.
WordCountをパラレル2でポート9000で起動する.
$ ./bin/flink run -p 2 examples/streaming/SocketWindowWordCount.jar --port 9000
ログをターミナルに吐くように別窓で実行する
$ tail -f log/flink-*-taskexecutor-*.out
合計3窓で実行する. このBackPressureを確認するため, ブラウザで
localhost:8081
を開く. BackPressureを確認するには, 実行中のジョブを開いてBackPressureをというタブを開いたら, 
Samplingと出て, 調べ終わるのを待って, Show subtaskでRatioを確認できる. 
BackPressureの値は実行中の最中しか確認できないので, 
何分あたりでどう変わったかをメモかなんかに書いとくべし.
