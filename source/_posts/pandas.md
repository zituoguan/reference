---

title: Pandas
date: 2024-07-04
background: bg-[#110750]
tags:
  - 数据分析
  - 数据操作
categories:
  - Python
intro: |
  [Pandas](https://pandas.pydata.org/) 是一个强大的 Python 数据分析和操作库。本速查表为 Pandas 初学者提供快速参考。
plugins:
  - copyCode

---

## 入门 {.cols-2}

### 简介

你需要导入 pandas 才能开始：

```python
import pandas as pd
```

### 创建 DataFrame

| -                                                              | -                                                   |
| -------------------------------------------------------------- | --------------------------------------------------- |
| `pd.DataFrame(data={'col1': [1, 2], 'col2': [3, 4]})`          | 从字典创建                                          |
| `pd.DataFrame(data=[{'a': 1, 'b': 2}, {'a': 3, 'b': 4}])`      | 从字典列表创建                                      |
| `pd.read_csv('file.csv')`                                      | 从 CSV 文件读取                                     |
| `pd.read_excel('file.xlsx')`                                   | 从 Excel 文件读取                                   |

### 检查数据 {.row-span-2}

| -                       | -                               |
| ----------------------- | ------------------------------- |
| `df.head()`             | 前 5 行                         |
| `df.tail()`             | 后 5 行                         |
| `df.shape`              | 行数和列数                      |
| `df.info()`             | DataFrame 信息                  |
| `df.describe()`         | 描述性统计                      |
| `df.columns`            | 列名                            |
| `df.index`              | 索引                            |
| `df.dtypes`             | 列数据类型                      |

### 选择数据

| -                        | -                                                 |
| ------------------------ | ------------------------------------------------- |
| `df['col1']`             | 选择列                                            |
| `df[['col1', 'col2']]`   | 选择多列                                          |
| `df.loc[0]`              | 按索引选择行                                      |
| `df.loc[:, 'col1']`      | 选择 'col1' 的所有行                              |
| `df.iloc[0]`             | 按位置选择行                                      |
| `df.iloc[0, 1]`          | 选择特定值                                        |
| `df[df['col1'] > 2]`     | 根据条件选择行                                    |

### 数据清洗

| -                            | -                                      |
| ---------------------------- | -------------------------------------- |
| `df.dropna()`                | 删除包含任何缺失值的行                 |
| `df.dropna(axis=1)`          | 删除包含任何缺失值的列                 |
| `df.fillna(0)`               | 用 0 替换缺失值                        |
| `df.drop_duplicates()`       | 删除重复行                             |
| `df.rename(columns={'old_name': 'new_name'})` | 重命名列             |
| `df.astype('int')`           | 更改数据类型                           |

### 添加/删除数据 {.row-span-2}

| -                                   | -                              |
| ----------------------------------- | ------------------------------ |
| `df['col3'] = df['col1'] + df['col2']` | 添加新列                       |
| `df.drop('col1', axis=1)`           | 删除列                         |
| `df.append(new_row)`                | 添加新行                       |
| `df.insert(2, 'new_col', new_data)` | 在位置 2 插入新列              |

### 合并数据

| -                                             | -                                                |
| --------------------------------------------- | ------------------------------------------------ |
| `pd.concat([df1, df2])`                       | 连接行                                           |
| `pd.concat([df1, df2], axis=1)`               | 连接列                                           |
| `pd.merge(df1, df2, on='key')`                | 根据键合并 DataFrame                             |
| `pd.merge(df1, df2, left_on='key1', right_on='key2')` | 根据不同键合并                               |
| `df1.join(df2, lsuffix='_left', rsuffix='_right')`    | 连接 DataFrame                               |

### 聚合数据

| -                                    | -                                                |
| ------------------------------------ | ------------------------------------------------ |
| `df['col1'].sum()`                   | 列中值的总和                                     |
| `df['col1'].mean()`                  | 列中值的平均值                                   |
| `df['col1'].count()`                 | 列中值的数量                                     |
| `df['col1'].min()`                   | 列中最小值                                       |
| `df['col1'].max()`                   | 列中最大值                                       |
| `df['col1'].std()`                   | 标准差                                           |
| `df['col1'].var()`                   | 方差                                             |
| `df.groupby('col1').sum()`           | 分组并求和                                       |
| `df.groupby('col1').mean()`          | 分组并求平均值                                   |
| `df.groupby(['col1', 'col2']).count()` | 按多列分组                                     |

### 应用函数 {.row-span-2}

| -                                  | -                                    |
| ---------------------------------- | ------------------------------------ |
| `df.apply(np.sqrt)`                | 对所有值应用函数                     |
| `df['col1'].apply(lambda x: x ** 2)`| 对列应用函数                         |
| `df.applymap(str)`                 | 对 DataFrame 元素应用函数            |
| `df['col1'].map({'a': 1, 'b': 2})` | 映射值                               |
| `df['col1'].replace('a', 1)`       | 替换值                               |

### 处理日期

| -                                    | -                                          |
| ------------------------------------ | ------------------------------------------ |
| `df['date'] = pd.to_datetime(df['date'])` | 转换为日期时间                             |
| `df['year'] = df['date'].dt.year`          | 提取年份                                   |
| `df['month'] = df['date'].dt.month`        | 提取月份                                   |
| `df['day'] = df['date'].dt.day`            | 提取日期                                   |
| `df.set_index('date', inplace=True)`       | 设置日期为索引                             |

### 输入/输出

| -                                    | -                                                |
| ------------------------------------ | ------------------------------------------------ |
| `df.to_csv('file.csv')`              | 保存 DataFrame 到 CSV                            |
| `df = pd.read_csv('file.csv')`       | 从 CSV 加载 DataFrame                          |
| `df.to_excel('file.xlsx')`           | 保存 DataFrame 到 Excel                          |
| `df = pd.read_excel('file.xlsx')`    | 从 Excel 加载 DataFrame                        |
| `from sqlalchemy import create_engine`| 导入 SQLAlchemy 进行 SQL 操作                  |
| `engine = create_engine('sqlite:///:memory:')` | 创建 SQL 引擎                             |
| `df.to_sql('table_name', engine)`    | 保存到 SQL 表                                  |
| `df = pd.read_sql('table_name', engine)` | 从 SQL 表加载                                  |

