参入テスト
====

## 概要
本リポジトリをforkした上で、問題を解いてみて下さい。
解答を投稿する場合は、本リポジトリにPull Requestを送信して下さい。
挑戦者求む

## 問題

### Linux

1. ロードアベレージを表示しなさい

2. 空きメモリサイズを表示しなさい

3. プロセスの親子関係及びプロセス番号を表示しなさい

4. iノードの使用率を表示しなさい

5. httpリクエストを投げて、そのヘッダ情報のみ表示しなさい

6. /var/log/td-agent ディレクトリ内の拡張子logとなっているファイルに対して、ファイル毎に末尾5行分を表示させるコマンドを記載しなさい（可能であればワンライナー）

7. tmpディレクトリにある以下ファイルの中からファイル名が20180219から始まるファイル内に含まれる文字列`hoge`を全て`fuga`に置換するコマンドを記載しなさい（可能であればワンライナー）

  ```
  # ll /tmp
  -rw-r--r-- 1 root root 17 Feb 18 15:09 20180219_1.txt
  -rw-r--r-- 1 root root 17 Feb 18 15:11 20180219_2.txt
  -rw-r--r-- 1 root root 17 Feb 18 15:11 20180219_3.txt
  -rw-r--r-- 1 root root 17 Feb 18 15:11 20180220_1.txt
  -rw-r--r-- 1 root root 17 Feb 18 15:11 20180220_2.txt
  -rw-r--r-- 1 root root 17 Feb 18 15:12 20180220_3.txt
  -rw-r--r-- 1 root root 17 Feb 18 15:11 20180221_1.txt
  -rw-r--r-- 1 root root 17 Feb 18 15:11 20180221_2.txt
  -rw-r--r-- 1 root root 17 Feb 18 15:12 20180221_3.txt
  ```

8. 2014年5月12日 20時～23時までのユニーク（送信元IP）なアクセス数を出力するコマンドを記載しなさい（可能であればワンライナー）

  ```
  # tail /var/log/httpd/access_log
  192.168.0.101 - - [12/May/2014:21:14:56 +0900] "GET /index.html HTTP/1.1" 304 - "-" "Mozilla/5.0 (Windows NT 6.1; WOW64; rv:29.0) Gecko/20100101 Firefox/29.0"
  ```

### プログラミング

9. 以下の条件を満たすスクリプトを作成しなさい
- 条件
  - 標準入力からカンマ区切りでランダムな文字列or数値を受け取る
  - 受け取った値が、3桁の数字でない場合は、"unmach pattern: <受け取った値>"を表示する
  - 受け取った値が、3桁のぞろ目の数字であった場合は、"zorome: <受け取った値>"を表示する
  - 受け取った値が、上記に当てはまらない場合は、そのまま受け取った値を表示する
  - スクリプトの言語は、なんでも良い
- 例
  - 標準入力で受け取る値
  
    ```
    123,abc,3333,555,321
    ```

  - スクリプトの実行結果

    ```
    123
    unmatch pattern: abc
    unmatch pattern: 3333
    zorome: 555
    321
    ```

10. 以下のコードを読んだ上で、次の問いに答えなさい

 - コード
 
  ```
  #!/bin/bash
 
function help {
    cat <<- EOF
    overview：backup or restore
    usage：bak.sh [-h|-b|-r] filename ...
    option：
      -h  this message
      -b  backup
      -r  restore
    EOF
    exit 1
}
 
if [ "$#" -lt 1 ]; then
     help
fi
 
if [ "$1" = "-h" ]; then
    help
elif [ "$1" = "-b" ]; then
    IS_RESTORE=0
    shift
elif [ "$1" = "-r" ]; then
    IS_RESTORE=1
    shift
fi
 
for file in $*
do
    if [ "$IS_RESTORE" -eq 0 ]; then
        if [ ! -e "${file}.bak" ]; then
            echo "ERROR: A file doesn't exist. ${file}.bak"
            continue
        fi
        SRC=${file}.bak
        DST=${file}
    else
        if [ ! -e "${file}" ]; then
            echo "ERROR: A file doesn't exist. ${file}"
            continue
        fi
        SRC=${file}
        DST=${file}.bak
    fi
     
    echo -n "$SRC --> $DST  ...  "
    cp $SRC $DST &> /dev/null
 
    if [ "$?" -eq 0 ]
    then
        echo "OK"
    else
        echo "ERROR: It can't be copied."
    fi
done
  ```
  
  a. 上記スクリプトは、一部のコードが誤っており、実行すると意図した通りに動作しない。誤っているコードを修正しなさい
  
  b. 第一引数に、"-h", "-b", "-r"以外が指定された場合に、エラーメッセージを表示してスクリプトを終了させる処理を実装しなさい
  
