# reパッケージ 説明問題と回答

## 概要

Pythonの `re` パッケージは正規表現（Regular Expression）を扱うための標準ライブラリです。
文字列の検索・抽出・置換・分割などを柔軟に行えます。

---

## 問題1: re.search() と re.match() の違いを説明せよ

**回答:**

| 関数 | 検索範囲 |
|------|----------|
| `re.match(pattern, string)` | 文字列の**先頭**からのみパターンを照合する |
| `re.search(pattern, string)` | 文字列の**どの位置でも**パターンを照合する |

```python
import re

text = "Hello Python"

# match は先頭から照合するため、"Python" は見つからない
print(re.match(r"Python", text))   # None

# search は文字列全体から探すため、"Python" が見つかる
print(re.search(r"Python", text))  # <re.Match object; span=(6, 12), match='Python'>
```

---

## 問題2: re.findall() の動作を説明し、使用例を示せ

**回答:**

`re.findall(pattern, string)` は、パターンに一致する**すべての部分文字列をリストで返す**。
一致がなければ空のリストを返す。

```python
import re

text = "電話番号: 090-1234-5678, 080-9876-5432"

# すべての電話番号を抽出
phones = re.findall(r"\d{3}-\d{4}-\d{4}", text)
print(phones)  # ['090-1234-5678', '080-9876-5432']

# グループを使うと、グループ内容のリストを返す
words = re.findall(r"[a-z]+", "apple Banana cherry")
print(words)  # ['apple', 'herry'] ← 大文字小文字を区別することに注意
```

---

## 問題3: 以下の主要なメタ文字の意味を説明せよ: `.` `^` `$` `*` `+` `?` `\d` `\w` `\s`

**回答:**

| メタ文字 | 意味 |
|----------|------|
| `.` | 改行以外の任意の1文字 |
| `^` | 文字列の先頭 |
| `$` | 文字列の末尾 |
| `*` | 直前の要素が0回以上繰り返す |
| `+` | 直前の要素が1回以上繰り返す |
| `?` | 直前の要素が0回または1回 |
| `\d` | 数字 `[0-9]` と同義 |
| `\w` | 英数字またはアンダースコア `[a-zA-Z0-9_]` と同義 |
| `\s` | 空白文字（スペース、タブ、改行など） |

```python
import re

# \d+ : 1桁以上の数字
print(re.findall(r"\d+", "abc 123 def 456"))  # ['123', '456']

# ^ と $ : 先頭・末尾
print(re.match(r"^\d+$", "12345"))   # Match（全体が数字）
print(re.match(r"^\d+$", "123ab"))   # None（末尾が数字でない）

# \w+ : 単語（英数字+アンダースコア）
print(re.findall(r"\w+", "hello_world 123"))  # ['hello_world', '123']
```

---

## 問題4: re.sub() の使い方を説明し、使用例を示せ

**回答:**

`re.sub(pattern, repl, string, count=0)` は、パターンに一致する部分を `repl` で**置換した新しい文字列を返す**。
`count` で最大置換回数を指定できる（デフォルト0は全置換）。

```python
import re

text = "2024年01月15日"

# 数字を * に置換
masked = re.sub(r"\d", "*", text)
print(masked)  # "****年**月**日"

# 連続する空白を1つのスペースに正規化
messy = "hello   world\t\tPython"
clean = re.sub(r"\s+", " ", messy)
print(clean)  # "hello world Python"

# count で置換回数を制限
limited = re.sub(r"\d+", "X", "a1 b2 c3", count=2)
print(limited)  # "aX bX c3"
```

---

## 問題5: グループ（括弧）の使い方を説明し、名前付きグループとの違いを示せ

**回答:**

`()` で囲んだ部分を**グループ**と呼び、マッチした部分を個別に取り出せる。
`(?P<name>...)` で**名前付きグループ**にすると、インデックスではなく名前でアクセスできる。

```python
import re

# 番号によるグループ参照
m = re.search(r"(\d{4})-(\d{2})-(\d{2})", "今日は2024-05-22です")
if m:
    print(m.group(0))  # '2024-05-22'（マッチ全体）
    print(m.group(1))  # '2024'（第1グループ）
    print(m.group(2))  # '05'（第2グループ）
    print(m.group(3))  # '22'（第3グループ）

# 名前付きグループ
m = re.search(r"(?P<year>\d{4})-(?P<month>\d{2})-(?P<day>\d{2})", "2024-05-22")
if m:
    print(m.group("year"))   # '2024'
    print(m.group("month"))  # '05'
    print(m.group("day"))    # '22'
```

---

## 問題6: re.compile() を使うメリットを説明せよ

**回答:**

`re.compile(pattern)` はパターンを**コンパイルして `Pattern` オブジェクトを返す**。
同じパターンを繰り返し使う場合に、コンパイルを1回にまとめることで**処理速度が向上する**。

```python
import re

# compile を使わない場合（ループ内で毎回パターンをコンパイル）
texts = ["apple123", "banana456", "cherry789"]
for t in texts:
    m = re.search(r"\d+", t)
    if m:
        print(m.group())

# compile を使う場合（パターンを一度だけコンパイル）
pattern = re.compile(r"\d+")
for t in texts:
    m = pattern.search(t)
    if m:
        print(m.group())
# 出力: 123, 456, 789
```

---

## 問題7: フラグ（flags）の代表的なものを3つ挙げ、それぞれ説明せよ

**回答:**

| フラグ | 省略形 | 説明 |
|--------|--------|------|
| `re.IGNORECASE` | `re.I` | 大文字・小文字を区別しない |
| `re.MULTILINE` | `re.M` | `^` と `$` が各行の先頭・末尾にもマッチする |
| `re.DOTALL` | `re.S` | `.` が改行文字にもマッチする |

```python
import re

# re.IGNORECASE
print(re.findall(r"python", "Python PYTHON python", re.I))
# ['Python', 'PYTHON', 'python']

# re.MULTILINE
text = "line1\nline2\nline3"
print(re.findall(r"^\w+", text, re.M))
# ['line1', 'line2', 'line3']

# re.DOTALL
text2 = "start\nmiddle\nend"
m = re.search(r"start.+end", text2, re.S)
print(m.group() if m else None)
# 'start\nmiddle\nend'
```

---

## 問題8: re.split() の使い方を説明せよ

**回答:**

`re.split(pattern, string, maxsplit=0)` は、パターンにマッチした箇所で文字列を**分割してリストを返す**。
`maxsplit` で最大分割回数を指定できる。

```python
import re

# 複数の区切り文字（カンマ、スペース、セミコロン）で分割
text = "apple, banana; cherry orange"
parts = re.split(r"[,;\s]+", text)
print(parts)  # ['apple', 'banana', 'cherry', 'orange']

# maxsplit で分割回数を制限
parts2 = re.split(r"\s+", "a b c d e", maxsplit=2)
print(parts2)  # ['a', 'b', 'c d e']
```

---

## まとめ: reパッケージの主要関数一覧

| 関数 | 説明 |
|------|------|
| `re.match(p, s)` | 先頭からパターンを照合、Matchオブジェクトまたは`None` |
| `re.search(p, s)` | 全体からパターンを照合、Matchオブジェクトまたは`None` |
| `re.findall(p, s)` | 全マッチをリストで返す |
| `re.finditer(p, s)` | 全マッチをイテレータで返す |
| `re.sub(p, r, s)` | パターンにマッチした部分を置換 |
| `re.split(p, s)` | パターンで文字列を分割 |
| `re.compile(p)` | パターンをコンパイルして再利用可能なオブジェクトを返す |
