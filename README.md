# K1T Typst Template

## 環境構築

cargoを用いた方法

```bash
# latest
cargo install --locked typst-cli
# develop version
cargo install --git https://github.com/typst/typst --locked typst-cli
```

## コンパイル・監視

コンパイル: `typst compile ./sample.typ ./sample.pdf`

監視: `typst watch ./sample.typ ./sample.pdf`

## チャプター分割

```md
== タイトル

説明

// 目次
#outline()

// ファイル名のタプルを作成。
#let chapters = (
  "chapter/01-chapter.typ",
  "chapter/02-chapter.typ"
)

// For Loopで各チャプターを読み込む
#for chapter in (chapters) {
  include(chapter)
} 
```

## 参考文献の追加

参考文献リストをYAMLで作成する。

```yml
harry:
  type: Book
  title: Harry Potter and the Order of the Phoenix
  author: Rowling, J. K.
  volume: 5
  page-total: 768
  date: 2003-06-21

electronic:
  type: Web
  title: Ishkur's Guide to Electronic Music
  serial-number: v2.5
  author: Ishkur
  url: http://www.techno.org/electronic-music-guide/
```

メインのtypファイルで参考文献の呼び出しをする。`ref.yml`というファイル名と仮定。

`#bibliography("ref.yml", title: "参考文献")`

チャプターで引用した項目を`#cite(<harry>)`や`#cite(<electronic>)`で表記できる。

`@harry`や`@electronic`でも可

yamlファイル以外にbibファイルでも同じことが可能。

## 画像の挿入について

画像はメインのtypstファイルと同じディレクトリに入れる必要がある。
