8. `dir_3`ディレクトリにある`access_log`から2018/2/26 20:00～22:59までのユニーク（送信元IP）なアクセス数を出力するコマンドを記載しなさい（可能であればワンライナー）
```
grep -E '\[26/Feb/2018:2[0-2]' dir_3/access_log | awk '{print $1}' | wc -l
```