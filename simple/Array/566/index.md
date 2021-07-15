# 566. 重塑矩阵

在MATLAB中，有一个非常有用的函数 reshape，它可以将一个矩阵重塑为另一个大小不同的新矩阵，但保留其原始数据。

给出一个由二维数组表示的矩阵，以及两个正整数r和c，分别表示想要的重构的矩阵的行数和列数。

重构后的矩阵需要将原始矩阵的所有元素以相同的行遍历顺序填充。

如果具有给定参数的reshape操作是可行且合理的，则输出新的重塑矩阵；否则，输出原始矩阵。

示例 1:

```text
输入: 
nums = 
[[1,2],
 [3,4]]
r = 1, c = 4
输出: 
[[1,2,3,4]]
解释:
行遍历nums的结果是 [1,2,3,4]。新的矩阵是 1 * 4 矩阵, 用之前的元素值一行一行填充新矩阵。
```

示例 2:

```text
输入: 
nums = 
[[1,2],
 [3,4]]
r = 2, c = 4
输出: 
[[1,2],
 [3,4]]
解释:
没有办法将 2 * 2 矩阵转化为 2 * 4 矩阵。 所以输出原矩阵。
```

注意：

给定矩阵的宽和高范围在 [1, 100]。

给定的 r 和 c 都是正数。

## 解法

### 题目分析

- 通过题目和示例分析出：重塑的矩阵行和列的积和给出的二维数组表示的矩阵行和列的积一致，否则返回原二维数组；所以需要将二维数组的矩阵转换为新的行和列的二维矩阵

### 解题思路

#### 解题方法1

- 硬解
- 先判断二维数组的行列积与需要转换的新矩阵的行列积是否一致，一致走下面的步骤，否则返回原数组
- 对原二维数组进行遍历，然后将新矩阵数组最后一个元素的长度和新矩阵的列相比，小于放进去，大于的话则push一个包含当前数值的新数组

代码：

```js
/**
 * @param {number[][]} mat
 * @param {number} r
 * @param {number} c
 * @return {number[][]}
 */
var matrixReshape = function(mat, r, c) {
    const matLength = mat[0].length * mat.length;
    let result = [[]];
    if(matLength !== r * c) {
        return mat;
    } else {
        for(let i=0; i< mat.length; i++) {
            for(let j=0; j< mat[i].length; j++) {
                if(result[result.length-1].length < c) {
                    result[result.length-1].push(mat[i][j])
                } else {
                    result.push([mat[i][j]])
                }
            }
        }
    }
    return result;
};
```

#### 解题方法2

- 先判断二维数组的行列积与需要转换的新矩阵的行列积是否一致，一致走下面的步骤，否则返回原数组
- 将原二维数组当成一维数组进行解答，然后创建新矩阵要求的列数据和行数的二维组，再进行循环，将一维数组的数据填充到新的二维矩阵中

代码：

```js
/**
 * @param {number[][]} mat
 * @param {number} r
 * @param {number} c
 * @return {number[][]}
 */
var matrixReshape = function(mat, r, c) {
    let n = mat[0].length;
    const matLength = n * mat.length;
    let result = new Array(r).fill(0).map(item => new Array(c).fill(0));
    if(matLength !== r * c) {
        return mat;
    } else {
        for(let i=0; i< matLength; i++) {
           result[Math.floor(i / c)][i % c] = mat[Math.floor(i / n)][i % n]
        }
    }
    return result;
};
```
