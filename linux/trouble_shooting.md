研究室の自分のマシンが Arch 
無知すぎるのが原因で, トラブル頻発. 

起動しなくなる系の致命的なものが１ヶ月くらいで２回起きた...

メモを残しておく. 

章題は一旦, 「どんなトラブルが起きたか」にする. 
もっといいのがあれば都度変更する. 

2017.10.07

## NFS のバインドがうまくいかずに起動しなくなる. 

### 起きたこと
起動時に, 「NFS のバインドができない」というエラーが出た. 

```
[FAILED] Failed to mount NFSD configuration filesystem.
...
```

ログインシェルに何も入力できなくなる. 

### これをしたら直った
`/etc/rc.conf` に

```
DAEMONS=(syslog-ng network nfs-common netfs rpcbind ypbind sshd crond)
```

これを書き足しら, 起動した. 

でも, エラーメッセージも出てた..

