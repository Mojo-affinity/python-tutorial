# Python研修
　Pythonの基本文法から，numpy, pandasの初歩的取り扱い，matplotlibを用いたデータの可視化までを行う。

## Python基本文法

### 変数とデータ型

Pythonは動的型付け言語であり，変数宣言時に型を指定する必要はない。

```python
# 整数 (int)
x = 10

# 浮動小数点数 (float)
y = 3.14

# 文字列 (str)
name = "Python"

# 真偽値 (bool)
flag = True

# 型の確認
print(type(x))     # <class 'int'>
print(type(y))     # <class 'float'>
print(type(name))  # <class 'str'>
```

### 演算子

```python
# 算術演算子
print(10 + 3)   # 13  (加算)
print(10 - 3)   # 7   (減算)
print(10 * 3)   # 30  (乗算)
print(10 / 3)   # 3.333... (除算)
print(10 // 3)  # 3   (整数除算)
print(10 % 3)   # 1   (余り)
print(10 ** 3)  # 1000 (べき乗)

# 比較演算子
print(10 == 10)  # True
print(10 != 5)   # True
print(10 > 5)    # True
print(10 < 5)    # False

# 論理演算子
print(True and False)  # False
print(True or False)   # True
print(not True)        # False
```

### データ構造

#### リスト (list)

順序を持つ変更可能なコレクション。

```python
fruits = ["apple", "banana", "cherry"]

# 要素アクセス (0始まり)
print(fruits[0])   # apple
print(fruits[-1])  # cherry (末尾から)

# スライス
print(fruits[0:2])  # ['apple', 'banana']

# 要素追加・削除
fruits.append("date")     # 末尾に追加
fruits.insert(1, "blueberry")  # 指定位置に追加
fruits.remove("banana")   # 値で削除
popped = fruits.pop()     # 末尾を取り出して削除

print(len(fruits))  # 要素数
```

#### タプル (tuple)

順序を持つ変更不可能なコレクション。

```python
point = (3, 5)
x, y = point  # アンパック

# タプルの要素は変更できない
# point[0] = 10  # TypeError が発生する
```

#### 辞書 (dict)

キーと値のペアを持つコレクション。

```python
person = {"name": "Alice", "age": 30, "city": "Tokyo"}

# 値へのアクセス
print(person["name"])          # Alice
print(person.get("age"))       # 30
print(person.get("email", "N/A"))  # N/A (キーがない場合のデフォルト値)

# 追加・更新・削除
person["email"] = "alice@example.com"  # 追加
person["age"] = 31                      # 更新
del person["city"]                      # 削除

# キー・値の一覧
print(list(person.keys()))    # ['name', 'age', 'email']
print(list(person.values()))  # ['Alice', 31, 'alice@example.com']
```

#### セット (set)

重複を持たない順序なしコレクション。

```python
nums = {1, 2, 3, 2, 1}
print(nums)  # {1, 2, 3} (重複が除かれる)

a = {1, 2, 3}
b = {2, 3, 4}
print(a | b)  # {1, 2, 3, 4} (和集合)
print(a & b)  # {2, 3}       (積集合)
print(a - b)  # {1}          (差集合)
```

### 条件分岐

```python
score = 75

if score >= 90:
    grade = "A"
elif score >= 70:
    grade = "B"
elif score >= 50:
    grade = "C"
else:
    grade = "F"

print(f"Grade: {grade}")  # Grade: B
```

### ループ

#### for ループ

```python
# リストの反復
for fruit in ["apple", "banana", "cherry"]:
    print(fruit)

# range を使った数値ループ
for i in range(5):       # 0, 1, 2, 3, 4
    print(i)

for i in range(2, 8, 2): # 2, 4, 6
    print(i)

# enumerate でインデックスも取得
for i, val in enumerate(["a", "b", "c"]):
    print(i, val)  # 0 a, 1 b, 2 c

# zip で複数リストを同時に反復
names = ["Alice", "Bob"]
scores = [90, 85]
for name, score in zip(names, scores):
    print(f"{name}: {score}")
```

#### while ループ

```python
count = 0
while count < 5:
    print(count)
    count += 1

# break と continue
for i in range(10):
    if i == 3:
        continue  # 3 をスキップ
    if i == 7:
        break     # 7 で終了
    print(i)
```

#### リスト内包表記

```python
# 通常のループ
squares = []
for x in range(10):
    squares.append(x ** 2)

# リスト内包表記 (同等の処理)
squares = [x ** 2 for x in range(10)]

# 条件付き
evens = [x for x in range(20) if x % 2 == 0]

# 辞書内包表記
word_lengths = {word: len(word) for word in ["apple", "banana", "cherry"]}
```

### 関数

```python
# 基本的な関数定義
def greet(name):
    return f"Hello, {name}!"

print(greet("Alice"))  # Hello, Alice!

# デフォルト引数
def power(base, exponent=2):
    return base ** exponent

print(power(3))     # 9  (exponent=2)
print(power(3, 3))  # 27

# キーワード引数
def describe(name, age, city="Tokyo"):
    return f"{name} is {age} years old and lives in {city}."

print(describe(age=25, name="Bob"))

# 可変長引数
def total(*args):
    return sum(args)

print(total(1, 2, 3, 4))  # 10

# キーワード可変長引数
def show_info(**kwargs):
    for key, value in kwargs.items():
        print(f"{key}: {value}")

show_info(name="Alice", age=30)

# lambda (無名関数)
square = lambda x: x ** 2
print(square(5))  # 25
```

### クラス

```python
class Animal:
    def __init__(self, name, sound):
        self.name = name
        self.sound = sound

    def speak(self):
        return f"{self.name} says {self.sound}!"

    def __repr__(self):
        return f"Animal(name={self.name!r})"


class Dog(Animal):  # 継承
    def __init__(self, name):
        super().__init__(name, "Woof")

    def fetch(self):
        return f"{self.name} fetches the ball!"


dog = Dog("Rex")
print(dog.speak())   # Rex says Woof!
print(dog.fetch())   # Rex fetches the ball!
print(dog)           # Animal(name='Rex')
```

---

## numpy

numpy は数値計算のための基本ライブラリであり，多次元配列（ndarray）と高速な演算を提供する。

```python
import numpy as np
```

### 配列の作成

```python
# リストから作成
a = np.array([1, 2, 3, 4, 5])
print(a)        # [1 2 3 4 5]
print(a.dtype)  # int64

# 2次元配列
matrix = np.array([[1, 2, 3],
                   [4, 5, 6]])
print(matrix.shape)  # (2, 3) -> 2行3列
print(matrix.ndim)   # 2      -> 次元数
print(matrix.size)   # 6      -> 総要素数

# 特殊な配列
zeros = np.zeros((3, 4))        # 全要素が 0
ones = np.ones((2, 3))          # 全要素が 1
eye = np.eye(3)                 # 単位行列
empty = np.empty((2, 2))        # 未初期化
full = np.full((3, 3), 7)       # 全要素が 7

# 連番配列
r1 = np.arange(10)              # [0, 1, ..., 9]
r2 = np.arange(0, 10, 2)        # [0, 2, 4, 6, 8]
r3 = np.linspace(0, 1, 5)       # [0. 0.25 0.5 0.75 1.] (等間隔5点)

# 乱数
rng = np.random.default_rng(seed=42)
rand_int = rng.integers(0, 10, size=(3, 3))   # 整数乱数
rand_float = rng.random(size=(2, 4))           # 0〜1の一様乱数
rand_normal = rng.normal(0, 1, size=1000)      # 正規分布
```

### インデックスとスライス

```python
a = np.array([10, 20, 30, 40, 50])

print(a[1])      # 20
print(a[-1])     # 50
print(a[1:4])    # [20 30 40]
print(a[::2])    # [10 30 50]  (1つおき)
print(a[::-1])   # [50 40 30 20 10] (逆順)

# 2次元配列のインデックス
m = np.array([[1, 2, 3],
              [4, 5, 6],
              [7, 8, 9]])

print(m[1, 2])    # 6     (1行2列)
print(m[0, :])    # [1 2 3] (0行全列)
print(m[:, 1])    # [2 5 8] (全行1列)
print(m[0:2, 1:]) # [[2 3] [5 6]]

# ブールインデックス
a = np.array([1, 5, 3, 8, 2, 7])
mask = a > 4
print(mask)   # [False  True False  True False  True]
print(a[mask])  # [5 8 7]
print(a[a > 4])  # 同上 (短縮形)
```

### 演算

```python
a = np.array([1, 2, 3, 4])
b = np.array([10, 20, 30, 40])

# 要素ごとの演算 (ブロードキャスト)
print(a + b)    # [11 22 33 44]
print(a * b)    # [10 40 90 160]
print(a ** 2)   # [1 4 9 16]
print(b / a)    # [10. 10. 10. 10.]

# スカラとの演算
print(a * 3)    # [3 6 9 12]
print(a + 100)  # [101 102 103 104]

# ブロードキャスト (形状の自動拡張)
m = np.ones((3, 4))
v = np.array([1, 2, 3, 4])
print(m + v)  # 各行に v が加算される

# 行列積
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])
print(A @ B)       # [[19 22] [43 50]]
print(np.dot(A, B))  # 同上
```

### 集計関数

```python
a = np.array([[1, 2, 3],
              [4, 5, 6]])

print(np.sum(a))         # 21 (全体の合計)
print(np.sum(a, axis=0)) # [5 7 9] (列ごとの合計)
print(np.sum(a, axis=1)) # [6 15]  (行ごとの合計)

print(np.mean(a))   # 3.5 (平均)
print(np.std(a))    # 標準偏差
print(np.min(a))    # 1
print(np.max(a))    # 6
print(np.argmin(a)) # 0 (最小値のインデックス)
print(np.argmax(a)) # 5 (最大値のインデックス)

# ソート
x = np.array([3, 1, 4, 1, 5, 9])
print(np.sort(x))    # [1 1 3 4 5 9]
print(np.argsort(x)) # ソート後のインデックス
```

### 形状変換

```python
a = np.arange(12)
print(a.shape)  # (12,)

b = a.reshape(3, 4)
print(b.shape)  # (3, 4)

c = b.reshape(2, -1)  # -1 は自動計算
print(c.shape)  # (2, 6)

print(b.flatten())    # 1次元に変換 (コピー)
print(b.ravel())      # 1次元に変換 (可能ならビュー)
print(b.T)            # 転置 (shape が (4, 3) になる)
```

---

## pandas

pandas はデータ分析のためのライブラリで，表形式データを扱う DataFrame を中心に提供する。

```python
import pandas as pd
import numpy as np
```

### Series

1次元のラベル付きデータ構造。

```python
# Series の作成
s = pd.Series([10, 20, 30, 40], index=["a", "b", "c", "d"])
print(s)
# a    10
# b    20
# c    30
# d    40
# dtype: int64

print(s["b"])    # 20
print(s[1])      # 20 (位置インデックスでもアクセス可)
print(s["b":"d"])  # b〜d をスライス

# 演算
print(s * 2)
print(s[s > 15])  # フィルタリング
```

### DataFrame

2次元のラベル付きデータ構造（表形式）。

```python
# 辞書から作成
data = {
    "name":   ["Alice", "Bob", "Charlie", "Diana"],
    "age":    [25, 30, 35, 28],
    "city":   ["Tokyo", "Osaka", "Tokyo", "Nagoya"],
    "salary": [300000, 450000, 380000, 420000],
}
df = pd.DataFrame(data)
print(df)
#       name  age    city  salary
# 0    Alice   25   Tokyo  300000
# 1      Bob   30   Osaka  450000
# 2  Charlie   35   Tokyo  380000
# 3    Diana   28  Nagoya  420000

# 基本情報
print(df.shape)    # (4, 4)
print(df.dtypes)   # 各列の型
print(df.info())   # 概要
print(df.describe())  # 数値列の統計量
```

### データの読み込みと書き込み

```python
# CSV の読み込み
df = pd.read_csv("data.csv")
df = pd.read_csv("data.csv", encoding="utf-8", index_col=0)

# Excel の読み込み
df = pd.read_excel("data.xlsx", sheet_name="Sheet1")

# CSV への書き出し
df.to_csv("output.csv", index=False, encoding="utf-8")

# 先頭・末尾の確認
print(df.head())   # 先頭5行
print(df.tail(3))  # 末尾3行
```

### CSV 読み込みの実践

`employees.csv` を使って実際のデータ読み込みと基本的な前処理を行う。

```
id,name,department,age,salary,hire_date,performance
1,Alice,Engineering,25,300000,2022-04-01,4.2
2,Bob,Sales,30,450000,2019-07-15,3.8
...
```

```python
# CSV の読み込みと日付パース
df = pd.read_csv("employees.csv", parse_dates=["hire_date"])
print(df.head())
#    id     name   department  age   salary  hire_date  performance
# 0   1    Alice  Engineering   25  300000.0 2022-04-01          4.2
# 1   2      Bob        Sales   30  450000.0 2019-07-15          3.8
# ...

# 基本情報の確認
print(df.shape)    # (12, 7)
print(df.dtypes)
# id                      int64
# name                   object
# department             object
# age                     int64
# salary                float64
# hire_date      datetime64[ns]
# performance           float64

df.info()
# <class 'pandas.core.frame.DataFrame'>
# RangeIndex: 12 entries, 0 to 11
# ...Non-Null Count  Dtype
# salary      11 non-null   float64   ← 1件 欠損
# performance 10 non-null   float64   ← 2件 欠損

print(df.describe())
```

```python
# 欠損値の確認と補完
print(df.isna().sum())
# salary         1
# performance    2

df["salary"]      = df["salary"].fillna(df["salary"].median())
df["performance"] = df["performance"].fillna(df["performance"].mean())

# 入社年の抽出 (datetime 列の活用)
df["hire_year"] = df["hire_date"].dt.year
print(df["hire_year"].value_counts().sort_index())
```

```python
# 部署ごとの集計
summary = df.groupby("department").agg(
    人数=("name", "count"),
    平均年齢=("age", "mean"),
    平均給与=("salary", "mean"),
    平均評価=("performance", "mean"),
).round(1)
print(summary)
#              人数  平均年齢     平均給与  平均評価
# department
# Engineering    5    31.0  388000.0     4.4
# HR             3    35.3  460000.0     4.0
# Sales          4    27.5  377500.0     3.6

# CSV への書き出し
df.to_csv("employees_cleaned.csv", index=False)
```

### 列・行の操作

```python
# 列の選択
print(df["name"])           # Series として取得
print(df[["name", "age"]])  # 複数列は DataFrame として取得

# 列の追加・更新・削除
df["bonus"] = df["salary"] * 0.1
df["age"] = df["age"] + 1
df.drop(columns=["bonus"], inplace=True)

# 行の選択
print(df.loc[0])           # ラベルで行選択
print(df.iloc[0])          # 位置で行選択
print(df.loc[1:3])         # ラベルのスライス
print(df.iloc[1:3, 0:2])   # 位置のスライス (行, 列)
```

### フィルタリング

```python
# 条件でフィルタリング
print(df[df["age"] > 28])
print(df[df["city"] == "Tokyo"])

# 複数条件
print(df[(df["age"] > 25) & (df["city"] == "Tokyo")])
print(df[(df["city"] == "Tokyo") | (df["city"] == "Osaka")])

# isin を使った絞り込み
print(df[df["city"].isin(["Tokyo", "Nagoya"])])

# query メソッド
print(df.query("age > 28 and city == 'Tokyo'"))
```

### 欠損値の処理

```python
import numpy as np

df = pd.DataFrame({
    "A": [1, np.nan, 3, np.nan],
    "B": [4, 5, np.nan, 7],
    "C": [8, 9, 10, 11],
})

print(df.isna())           # 欠損値の位置 (True/False)
print(df.isna().sum())     # 列ごとの欠損数

df.dropna()                # 欠損のある行を削除
df.dropna(subset=["A"])    # 特定列が欠損の行のみ削除
df.fillna(0)               # 欠損を 0 で埋める
df["A"].fillna(df["A"].mean())  # 平均値で補完
```

### 集計・グループ化

```python
# 基本集計
print(df["salary"].mean())
print(df["salary"].sum())
print(df.describe())

# groupby
grouped = df.groupby("city")["salary"].mean()
print(grouped)

# 複数集計
agg = df.groupby("city").agg(
    avg_salary=("salary", "mean"),
    count=("name", "count"),
    max_age=("age", "max"),
)
print(agg)

# pivot_table
pt = df.pivot_table(values="salary", index="city", aggfunc="mean")
print(pt)
```

### ソート・変換

```python
# ソート
df.sort_values("age", ascending=False)
df.sort_values(["city", "salary"], ascending=[True, False])

# 文字列操作
df["name_upper"] = df["name"].str.upper()
df["name_len"] = df["name"].str.len()
df[df["city"].str.startswith("T")]  # 前方一致フィルタ

# apply で関数を適用
df["level"] = df["salary"].apply(lambda x: "high" if x >= 400000 else "low")

# map で値を置換
city_map = {"Tokyo": "東京", "Osaka": "大阪", "Nagoya": "名古屋"}
df["city_jp"] = df["city"].map(city_map)
```

---

## matplotlib

matplotlib はPythonの標準的なグラフ描画ライブラリ。`pyplot` モジュールを使うことで手軽にグラフを作成できる。

```python
import matplotlib.pyplot as plt
import numpy as np
```

### 基本的なグラフ構造

```python
fig, ax = plt.subplots()  # Figure (キャンバス) と Axes (グラフ領域) を作成
ax.plot([1, 2, 3], [4, 5, 6])
ax.set_title("タイトル")
ax.set_xlabel("X軸ラベル")
ax.set_ylabel("Y軸ラベル")
plt.show()
```

### 折れ線グラフ

```python
x = np.linspace(0, 2 * np.pi, 100)

fig, ax = plt.subplots(figsize=(8, 4))
ax.plot(x, np.sin(x), label="sin(x)", color="blue", linewidth=2)
ax.plot(x, np.cos(x), label="cos(x)", color="red", linestyle="--")
ax.set_title("三角関数")
ax.set_xlabel("x")
ax.set_ylabel("y")
ax.legend()
ax.grid(True)
plt.tight_layout()
plt.savefig("line_plot.png", dpi=150)
plt.show()
```

### 散布図

```python
rng = np.random.default_rng(42)
x = rng.normal(0, 1, 100)
y = 2 * x + rng.normal(0, 0.5, 100)

fig, ax = plt.subplots()
scatter = ax.scatter(x, y, c=y, cmap="viridis", alpha=0.7, s=50)
fig.colorbar(scatter, ax=ax, label="y の値")
ax.set_title("散布図")
ax.set_xlabel("x")
ax.set_ylabel("y")
plt.show()
```

### 棒グラフ

```python
categories = ["東京", "大阪", "名古屋", "福岡"]
values = [300000, 450000, 380000, 420000]

fig, ax = plt.subplots()
bars = ax.bar(categories, values, color=["#4C72B0", "#DD8452", "#55A868", "#C44E52"])
ax.bar_label(bars, fmt="{:,.0f}")  # バーの上に値を表示
ax.set_title("都市別平均給与")
ax.set_ylabel("給与 (円)")
ax.set_ylim(0, 500000)
plt.show()
```

### ヒストグラム

```python
rng = np.random.default_rng(42)
data = rng.normal(loc=170, scale=10, size=500)

fig, ax = plt.subplots()
ax.hist(data, bins=30, edgecolor="black", color="steelblue", alpha=0.8)
ax.axvline(data.mean(), color="red", linestyle="--", label=f"平均: {data.mean():.1f}")
ax.set_title("身長の分布")
ax.set_xlabel("身長 (cm)")
ax.set_ylabel("頻度")
ax.legend()
plt.show()
```

### 複数グラフの配置

```python
x = np.linspace(0, 2 * np.pi, 100)
rng = np.random.default_rng(42)

fig, axes = plt.subplots(2, 2, figsize=(10, 8))
fig.suptitle("グラフのギャラリー", fontsize=16)

# 折れ線
axes[0, 0].plot(x, np.sin(x))
axes[0, 0].set_title("折れ線グラフ")

# 散布図
axes[0, 1].scatter(rng.random(50), rng.random(50), alpha=0.7)
axes[0, 1].set_title("散布図")

# 棒グラフ
axes[1, 0].bar(["A", "B", "C"], [3, 7, 5])
axes[1, 0].set_title("棒グラフ")

# ヒストグラム
axes[1, 1].hist(rng.normal(0, 1, 200), bins=20)
axes[1, 1].set_title("ヒストグラム")

plt.tight_layout()
plt.show()
```

### 日本語フォントの設定

matplotlib はデフォルトで日本語を表示できないため，フォントを指定する必要がある。

```python
import matplotlib.pyplot as plt
import matplotlib
matplotlib.rcParams["font.family"] = "IPAexGothic"  # Linux
# matplotlib.rcParams["font.family"] = "Hiragino Sans"  # macOS
# matplotlib.rcParams["font.family"] = "MS Gothic"      # Windows

plt.rcParams["axes.unicode_minus"] = False  # マイナス記号の文字化け防止
```

または `japanize_matplotlib` ライブラリを使う方法が簡便。

```bash
pip install japanize-matplotlib
```

```python
import japanize_matplotlib  # import するだけで日本語が使えるようになる
import matplotlib.pyplot as plt
```
