
##unite.vim設定メモ

###インストール方法

注:NeoBundleがインストールし設定されていることが前提

.vimrcに以下の設定を追加

```
NeoBundle 'Shougo/unite.vim'
```

Vimでインストールコマンドを実行

```
:NeoBundleInstall
```

###unite.vimの使用方法

uniteのコマンドの基本は以下の通り

```
:Unite [{options}] {source}
```

`source`にて選択された情報に対して操作を行う
下記に例を示す

```
:Unite file
```

上記が実行された場合、ファイルの一覧が表示される。

```
:Unite file buffer
```

また上記のように複数の`source`を指定することで、
ファイルとバッファーをまとめて表示することも可能。

###主なsource

|source|説明|
|:-----|:---|
|file|カレントディレクトリのファイル一覧|
|file_mru|最近開いたファイルの一覧|
|buffer|バッファの一覧|
|register|レジスタの一覧|
|source|uniteの使用可能なsourceの一覧|

###unite.vimの操作

|キー|動作|
|:---|:---|
|Ctrl+p|上の候補に移動|
|Ctrl+n|下の候補に移動|
|Enter|default の Action を実行|
|Tab|Action 選択画面に移行|

###unite.vimの設定

```
let g:unite_enable_start_insert=1
let g:unite_source_history_yank_enable =1
let g:unite_source_file_mru_limit = 200
```

###キーバインディング

```
nnoremap <silent> ,ub :<C-u>Unite buffer<CR>
nnoremap <silent> ,uf :<C-u>UniteWithBufferDir -buffer-name=files file<CR>
nnoremap <silent> ,ur :<C-u>Unite -buffer-name=register register<CR>
nnoremap <silent> ,uu :<C-u>Unite file_mru buffer<CR>
nnoremap <silent> ,ua :<C-u>UniteWithBufferDir -buffer-name=files buffer file_mru bookmark file<CR>
au FileType unite nnoremap <silent> <buffer> <expr> <C-j> unite#do_action('split')
au FileType unite inoremap <silent> <buffer> <expr> <C-j> unite#do_action('split')
au FileType unite nnoremap <silent> <buffer> <expr> <C-l> unite#do_action('vsplit')
au FileType unite inoremap <silent> <buffer> <expr> <C-l> unite#do_action('vsplit')
au FileType unite nnoremap <silent> <buffer> <ESC><ESC> q
au FileType unite inoremap <silent> <buffer> <ESC><ESC> <ESC>q
```

