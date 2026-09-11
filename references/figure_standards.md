# 图表规范与配色

> C题国奖论文的图表类型、配色方案、标注规范与排版技巧。图表是论文的"脸面"，专业的图表能让评委在几秒内建立好印象。

---

## 一、图表通用规范

### 1.1 编号规则
- **图**：按章节编号，如图3-1、图3-2... 图题在图下方
- **表**：按章节编号，如表3-1、表3-2... 表题在表上方
- 全文连续编号，不重号、不漏号

### 1.2 表格规范
- 统一使用**三线表**（顶线、表头底线、底线）
- 顶线和底线粗（1.5磅），表头底线细（1磅）
- 无竖线，无多余横线
- 数字右对齐，文字左对齐
- 数据小数位统一（建议保留2-4位）
- 单位统一标注在表头或表题中

### 1.3 坐标轴与标注
- X轴、Y轴必须有明确的**轴标签**（变量名 + 单位）
- 刻度清晰，刻度值字体适中
- 图例清晰可辨，位置不遮挡数据
- 多条线时使用不同线型（实线/虚线/点线）+ 不同颜色双重区分
- 有误差棒时，说明误差含义（标准差/标准误/置信区间）

### 1.4 字体与字号
- 图内字体：宋体/黑体（中文）+ Times New Roman/ Arial（英文数字）
- 轴标签字号：9-11号
- 图题字号：小五号（9号）
- 保持全文图表字体风格一致

---

## 二、C题高频图表类型与用法

### 2.1 折线图 / 曲线图

**适用场景**：趋势变化、收敛曲线、灵敏度响应、时间序列

**国奖论文中的典型用法**：
- 算法收敛曲线（横轴迭代次数，纵轴目标函数值）
- 预测结果对比（实际值 vs 预测值）
- 灵敏度分析曲线（参数变化 vs 输出变化）
- 时间趋势图（年份/月份 vs 指标值）

**设计要点**：
- 多条线时颜色对比度要高
- 关键位置加数据标注（极值点、拐点）
- 收敛曲线标注收敛点
- 预测区间用阴影表示置信带

---

### 2.2 柱状图 / 条形图

**适用场景**：排名对比、数量统计、结果展示、分类比较

**典型用法**：
- 综合得分排名条形图
- 各方案结果对比柱状图
- 误差对比柱状图
- 特征重要性条形图

**设计要点**：
- 排序后绘制（从大到小或从小到大）
- 数值标注在柱顶
- 分组柱状图加图例
- 水平条形图适合标签长的情况

---

### 2.3 热力图

**适用场景**：相关性矩阵、方案分布、混淆矩阵、密度分布

**典型用法**：
- 变量相关性热力图（颜色深浅表示相关系数）
- 种植方案/资源分配热力图
- 混淆矩阵热力图
- 二维参数扫描热力图

**配色方案**：
- 相关性热力图：红-蓝渐变色（红正蓝负，白色为0）
- 密度/强度热力图：单色渐变（浅到深）
- 混淆矩阵：蓝绿色系渐变

**设计要点**：
- 加数值标注（小格内显示具体数值）
- 颜色条（colorbar）清晰标注含义
- 行列标签完整

---

### 2.4 散点图 / 散点矩阵

**适用场景**：相关性分析、样本分布、聚类结果、灵敏度散点

**典型用法**：
- 两个变量的散点图+拟合线
- 多变量散点矩阵（pair plot）
- 聚类结果可视化
- 残差散点图（模型诊断）

**设计要点**：
- 加拟合线+置信带（展示趋势）
- 分组时用不同颜色/形状
- 散点矩阵对角线放直方图

---

### 2.5 箱线图

**适用场景**：数据分布、异常值检测、组间对比

**典型用法**：
- 多组数据分布对比
- 异常值检测结果
- 模型残差分布
- 不同方法的结果分布对比

**设计要点**：
- 箱体宽度适中
- 异常值用圆点标出
- 标注中位数/均值

---

### 2.6 流程图 / 架构图

**适用场景**：总体思路、算法流程、模型框架、技术路线

**典型用法**：
- 技术路线图（放在摘要后面，给人整体印象）
- 算法流程图
- 模型框架图
- 数据流图

**设计要点**：
- 用矩形表示处理步骤，菱形表示判断，圆角矩形表示开始/结束
- 箭头方向统一（从上到下或从左到右）
- 文字简洁（每框不超过15字）
- 配色统一，用2-3种颜色区分不同模块

---

### 2.7 饼图 / 环形图

**适用场景**：占比结构、品类分布

**注意**：饼图容易被滥用。类别超过6个时不要用饼图，改用条形图。

**设计要点**：
- 类别控制在5-6个以内
- 标注百分比
- 不要使用3D效果（显得不专业）

---

### 2.8 直方图

**适用场景**：变量分布特征、参数分布、误差分布

**典型用法**：
- 关键变量的分布展示（正态性检验的直观验证）
- Z值分布（异常检测类问题）
- 残差分布直方图

**设计要点**：
- 加上拟合的正态分布曲线对比
- 组数适中（10-30组）
- 标注均值和标准差

---

### 2.9 雷达图

**适用场景**：多维度综合评价（4-8个指标时）

**典型用法**：
- 多个评价对象的多维度对比
- 方案的多指标综合展示

**设计要点**：
- 指标数量4-8个为宜
- 2-3个对象对比效果最好
- 指标方向统一（都是越大越好或越小越好）

---

## 三、学术配色方案

### 3.1 经典学术配色（首选）

**主色调：深蓝 + 橙色对比**
- 深蓝：#2E5A88 / rgb(46, 90, 136)
- 浅蓝：#7BAFD4 / rgb(123, 175, 212)
- 橙色：#E8842B / rgb(232, 132, 43)
- 浅橙：#F5C79B / rgb(245, 199, 155)
- 灰色：#666666 / rgb(102, 102, 102)

**适用**：折线图、柱状图、流程图。沉稳专业，适合正式论文。

### 3.2 多分类配色（6类以内）

**Set1风格（Matplotlib默认）改良版**：
1. #4C72B0（蓝）
2. #DD8452（橙）
3. #55A868（绿）
4. #C44E52（红）
5. #8172B3（紫）
6. #937860（棕）

**适用**：多类别对比图。颜色区分度高，色盲友好度尚可。

### 3.3 渐变配色（热力图专用）

**相关性热力图（RdBu reversed）**：
- 负相关（深蓝）→ 零（白）→ 正相关（深红）
- 范围：[-1, 1]，对称色阶

**密度/强度热力图（YlOrRd或Blues）**：
- 浅色→深色的单色渐变
- 显得干净专业

### 3.4 避坑配色

❌ 不要用的配色：
- 彩虹配色（rainbow）—— 渐变不均，视觉误导
- 荧光色/高饱和度亮色系 —— 刺眼，不学术
- 纯红+纯绿组合 —— 红绿色盲无法区分
- 3D效果 —— 干扰数据解读

---

## 四、Python绘图规范代码

### 4.1 全局样式设置

```python
import matplotlib.pyplot as plt
import matplotlib
import numpy as np

# 全局字体设置（中英文混排）
matplotlib.rcParams['font.family'] = ['SimHei', 'Times New Roman']
matplotlib.rcParams['axes.unicode_minus'] = False  # 解决负号显示问题
matplotlib.rcParams['font.size'] = 10
matplotlib.rcParams['axes.titlesize'] = 11
matplotlib.rcParams['axes.labelsize'] = 10
matplotlib.rcParams['xtick.labelsize'] = 9
matplotlib.rcParams['ytick.labelsize'] = 9
matplotlib.rcParams['legend.fontsize'] = 9

# 分辨率设置
matplotlib.rcParams['figure.dpi'] = 300
matplotlib.rcParams['savefig.dpi'] = 300
matplotlib.rcParams['savefig.bbox'] = 'tight'
matplotlib.rcParams['savefig.pad_inches'] = 0.05

# 专业学术配色
COLORS = ['#2E5A88', '#E8842B', '#55A868', '#C44E52', '#8172B3', '#937860']

# 图尺寸（按论文版面调整，单位：英寸）
FIG_SINGLE = (6, 4)      # 单图
FIG_DOUBLE = (12, 4)     # 并排两图
FIG_SQUARE = (5, 5)      # 正方形图（热力图/散点图）
```

### 4.2 折线图模板

```python
fig, ax = plt.subplots(figsize=FIG_SINGLE)

ax.plot(x, y1, color=COLORS[0], linewidth=2, marker='o', markersize=4, label='方法A')
ax.plot(x, y2, color=COLORS[1], linewidth=2, marker='s', markersize=4, label='方法B')

ax.set_xlabel('自变量X', fontsize=10)
ax.set_ylabel('因变量Y', fontsize=10)
ax.set_title('图3-X XX对比图', fontsize=11, fontweight='bold', pad=10)
ax.legend(loc='best', framealpha=0.9)
ax.grid(True, alpha=0.3, linestyle='--')

plt.tight_layout()
plt.savefig('fig3_x_comparison.png')
plt.close()
```

### 4.3 柱状图模板

```python
fig, ax = plt.subplots(figsize=FIG_SINGLE)

bars = ax.bar(categories, values, color=COLORS[0], width=0.6, edgecolor='white', linewidth=0.5)

# 在柱顶标注数值
for bar, val in zip(bars, values):
    height = bar.get_height()
    ax.text(bar.get_x() + bar.get_width()/2., height + max(values)*0.01,
            f'{val:.2f}', ha='center', va='bottom', fontsize=9)

ax.set_xlabel('类别', fontsize=10)
ax.set_ylabel('数值', fontsize=10)
ax.set_title('图3-X XX柱状图', fontsize=11, fontweight='bold', pad=10)
ax.set_ylim(0, max(values) * 1.15)  # 留出标注空间

plt.tight_layout()
plt.savefig('fig3_x_bar.png')
plt.close()
```

### 4.4 热力图模板

```python
import seaborn as sns

fig, ax = plt.subplots(figsize=FIG_SQUARE)

sns.heatmap(corr_matrix, annot=True, fmt='.2f', cmap='RdBu_r',
            center=0, vmin=-1, vmax=1, square=True,
            linewidths=0.5, linecolor='white',
            cbar_kws={'shrink': 0.8, 'label': '相关系数'},
            ax=ax)

ax.set_title('图3-X XX相关性热力图', fontsize=11, fontweight='bold', pad=10)
ax.set_xticklabels(ax.get_xticklabels(), rotation=45, ha='right')

plt.tight_layout()
plt.savefig('fig3_x_heatmap.png')
plt.close()
```

### 4.5 三线表模板（Python生成LaTeX）

```python
# 生成LaTeX三线表代码
def make_three_line_table(headers, data, caption, label, column_align=None):
    """
    headers: 表头列表
    data: 二维数据列表
    caption: 表题
    label: 表标签（用于引用）
    column_align: 列对齐方式，如 'lcccr'
    """
    n = len(headers)
    if column_align is None:
        column_align = 'l' + 'c' * (n-1)
    
    lines = []
    lines.append(r'\begin{table}[htbp]')
    lines.append(r'  \centering')
    lines.append(r'  \caption{' + caption + r'}')
    lines.append(r'  \label{tab:' + label + r'}')
    lines.append(r'  \begin{tabular}{' + column_align + r'}')
    lines.append(r'    \toprule')
    lines.append('    ' + ' & '.join(headers) + r' \\')
    lines.append(r'    \midrule')
    for row in data:
        lines.append('    ' + ' & '.join([str(x) for x in row]) + r' \\')
    lines.append(r'    \bottomrule')
    lines.append(r'  \end{tabular}')
    lines.append(r'\end{table}')
    return '\n'.join(lines)
```

---

## 五、图表在论文中的排版技巧

### 5.1 位置
- 图表紧跟在第一次提到它的文字后面
- 不要跨章节放图
- 尽量放在页顶或页底，不要插在段落中间

### 5.2 大小
- 单栏图：宽度约8cm（小论文版面）
- 双栏图：宽度约16-17cm
- 保持图片纵横比，不要拉伸变形

### 5.3 图题规范
- 格式："图X-X 图题内容"
- 位置：图下方，居中
- 字号：小五号（比正文小一号）
- 图题要能独立看懂（不看正文也知道图在说什么）

### 5.4 常见图表问题
- ❌ 图片模糊/锯齿（分辨率不够）
- ❌ 坐标轴没有标签和单位
- ❌ 图例不清楚或被遮挡
- ❌ 颜色太多太杂
- ❌ 图题太简单（"结果图"三个字等于没说）
- ❌ 表格不是三线表（框线太多）

---

## 六、图表密度参考

国一论文的图表密度（按每千字符统计）：

| 部分 | 图密度 | 表密度 |
|------|--------|--------|
| 数据处理 | 高（2-3图/节） | 中（1-2表/节） |
| 模型建立 | 中（1-2图/节） | 高（2-3表/节） |
| 结果分析 | 很高（3-5图/节） | 中（1-2表/节） |
| 灵敏度分析 | 高（2-3图/节） | 中（1表/节） |

**总体**：平均每1000字配1-2张图 + 0.5-1张表。
