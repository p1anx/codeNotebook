# 1 read and write `.csv` file
## 1.1 read file
在 MATLAB 中，读取 CSV 文件非常简单，通常使用 `readtable`、`readmatrix` 或 `csvread` 函数。以下是一些常用方法的示例：

### 使用 `readtable`

`readtable` 是最常用的方法，可以将 CSV 文件读取为一个表格数据类型，方便后续的数据处理。

```matlab
% 读取 CSV 文件
data = readtable('your_file.csv');

% 查看数据的前几行
head(data);
```

### 使用 `readmatrix`

`readmatrix` 可以将 CSV 文件读取为一个矩阵，适合数值数据。

```matlab
% 读取 CSV 文件
data = readmatrix('your_file.csv');

% 查看数据的前几行
disp(data(1:5, :));  % 显示前5行
```

### 示例 CSV 文件内容

假设你的 CSV 文件内容如下：

```
Time,Value
0,1.1
1,2.3
2,3.5
3,4.7
```

### 读取后数据处理

读取数据后，你可以通过变量名访问表格中的数据（如果使用 `readtable`），或者通过索引访问矩阵数据（如果使用 `readmatrix`）。

```matlab
% 如果使用 readtable
time = data.Time;   % 获取 Time 列
value = data.Value; % 获取 Value 列

% 如果使用 readmatrix
time = data(:, 1);  % 获取第一列
value = data(:, 2); % 获取第二列
```

### 处理缺失数据

如果你的 CSV 文件中包含缺失数据，使用 `readtable` 和 `readmatrix` 会自动处理这些缺失值。你可以使用 `rmmissing` 函数来删除包含缺失值的行。

```matlab
% 删除含有缺失值的行
cleanData = rmmissing(data);
```

## 1.2 write file
在 MATLAB 中，可以使用 `writetable`、`csvwrite` 或 `writematrix` 函数将数据保存为 CSV 文件。以下是几种常用方法：

### 1. 使用 `writetable`
如果你的数据以表格的形式存储，使用 `writetable` 是最方便的方式。

```matlab
% 创建示例表格
data = table([1; 2; 3], [4; 5; 6], 'VariableNames', {'Column1', 'Column2'});

% 保存为 CSV 文件
writetable(data, 'data.csv');
```


### 2. 使用 `writematrix`
`writematrix` 是一个更通用的函数，可以用来保存矩阵或数组。

```matlab
% 创建示例矩阵
data = [1, 4; 2, 5; 3, 6];

% 保存为 CSV 文件
writematrix(data, 'data.csv');
```



