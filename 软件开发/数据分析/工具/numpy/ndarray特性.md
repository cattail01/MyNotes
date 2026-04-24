## 1. 多维性

ndarray 是 N 维数组对象，可存储任意维度的数据。

```python
a = np.array([1, 2, 3])              # 一维向量
b = np.array([[1, 2], [3, 4]])       # 二维矩阵
c = np.array([[[1, 2], [3, 4]], [[5, 6], [7, 8]]])  # 三维张量
```

通过 `shape` 属性查看维度，通过 `ndim` 属性获取维度数。

## 2. 同质性

ndarray 要求所有元素类型相同，由 `dtype` 统一指定。这带来两个优势：

- 内存紧凑：连续内存存储，类型固定，开销小
- 计算高效：同一类型数据可批量 SIMD 指令处理

```python
arr = np.array([1, 2, 3], dtype=np.int32)
arr.dtype  # dtype('int32')
```

## 3. 高效性

ndarray 的运算高效源于三点：

### 3.1 连续内存存储

数组元素在内存中连续存储，访问效率高。

### 3.2 批量操作（向量化）

无需 Python 循环，直接对整个数组操作：

```python
a = np.arange(1000)
b = a * 2 + 1  # 一次完成，而非循环
```

### 3.3 广播机制

形状不同的数组可自动扩展后运算：

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])
arr + 10  # 自动将 10 广播到所有行
```

---

**参考资料：**

- [007-numpy-ndarray的特性_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1D9GLzyEL6?spm_id_from=333.788.videopod.episodes&vd_source=5f0f8adc7e5d3bc7e86930bcb6e1e799&p=7)

*整理时间：2026-04-24*
