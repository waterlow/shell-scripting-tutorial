変数を引き継げない。`#!/bin/sh` で新しいシェルを開いているから。

```
$ MYVAR=hello
$ ./myvar2.sh
MYVAR is:
MYVAR is: hi there
```

`export`すればよい
```
$ export MYVAR
$ ./myvar2.sh
MYVAR is: hello
MYVAR is: hi there
```

しかしスクリプトから戻ってくると値が変わらない
```
$ echo $MYVAR
hello
```

`.`コマンドを使うと良い
```
$ MYVAR=hello
$ echo $MYVAR
hello
$ . ./myvar2.sh
MYVAR is: hello
MYVAR is: hi there
$ echo $MYVAR
hi there
```

 よくやるミスとして
 ```
 #!/bin/sh
echo "What is your name?"
read USER_NAME
echo "Hello $USER_NAME"
echo "I will create you a file called $USER_NAME_file"
touch $USER_NAME_file
```

`touch $USER_NAME_file` でUSER_NAME_fileという変数がないとなる。空白区切りでない場合は`{}`で区切る

```
#!/bin/sh
echo "What is your name?"
read USER_NAME
echo "Hello $USER_NAME"
echo "I will create you a file called ${USER_NAME}_file"
touch "${USER_NAME}_file"
```
