# QM-Simplifier / 奎因-麦克拉斯基化简器

> 一个交互式网页工具，用于演示奎因-麦克拉斯基（Quine-McCluskey）逻辑化简算法，支持多种输入格式，并详细展示化简过程的每一步。

---

## 简介 / Introduction

**QM-Simplifier** 是一个纯前端实现的逻辑函数化简工具，采用经典的奎因-麦克拉斯基算法，能够将任意逻辑表达式或最小项列表化简为最简与或式，并分步骤展示合并、质蕴含项提取、覆盖表求解等过程，非常适合教学、自学及逻辑电路设计辅助。

**QM-Simplifier** is a pure front-end tool for logic function minimization using the classic Quine-McCluskey algorithm. It can simplify any logical expression or minterm list into a minimal sum-of-products form, and displays the entire process step by step, including merging, prime implicant extraction, and covering table solving. It is ideal for teaching, self-study, and logic circuit design assistance.

---

## 功能特点 / Features

- **双模式输入**：支持逻辑表达式（如 `(A+B)(A'+B)`）或十进制最小项列表（如 `∑m(0,1,2,3)`）。
- **自动变量识别**：自动检测输入中的变量名，按字母顺序排序。
- **分步骤展示**：从初始分组、合并、质蕴含项表到最小覆盖选择，每一步均可折叠/展开，清晰易懂。
- **多种测试用例**：内置多个测试用例，覆盖简单到复杂场景，帮助验证正确性。
- **无关项支持**：可输入无关项（`d`），参与合并但不强制覆盖。
- **交互友好**：一键化简，实时显示结果，错误提示清晰。
- **纯前端实现**：无需后端，所有运算均在浏览器中完成，数据安全。

- **Two input modes**: supports logical expressions (e.g., `(A+B)(A'+B)`) or decimal minterm lists (e.g., `∑m(0,1,2,3)`).
- **Automatic variable detection**: automatically identifies variables in the expression and sorts them alphabetically.
- **Step-by-step display**: from initial grouping, merging, prime implicant table to minimum covering selection, each step is collapsible/expandable for clear understanding.
- **Built-in test cases**: includes multiple test cases covering simple to complex scenarios to help verify correctness.
- **Don’t-care support**: accepts don’t-care terms (`d`) for merging, but they are not required to be covered.
- **Interactive and user-friendly**: one-click simplification, real-time result display, and clear error messages.
- **Pure front-end implementation**: no backend required; all calculations are done in the browser, ensuring data security.

---

## 使用方法 / Usage

1. 打开 `index.html` 文件（或访问在线地址）。
2. 在输入框中选择输入模式：
   - **逻辑表达式**：输入如 `(A+B)(A'+B)` 的表达式，变量需用大写字母，非运算用 `'` 表示。
   - **最小项列表**：输入十进制最小项，如 `0,1,2,3` 或 `∑m(0,1,2,3)`。若有无关项，可加 `d` 参数。
3. 点击 **“开始化简”** 按钮。
4. 查看最终化简结果，并可展开下方各步骤查看详细过程。

1. Open `index.html` in your browser (or visit the online link).
2. Select the input mode in the input box:
   - **Logical expression**: enter an expression like `(A+B)(A'+B)`. Variables must be uppercase, use `'` for NOT.
   - **Minterm list**: enter decimal minterms, e.g., `0,1,2,3` or `∑m(0,1,2,3)`. For don’t-care terms, add `d`.
3. Click the **“Simplify”** button.
4. View the final simplified result and expand the steps below to see the detailed process.

---

## 算法步骤 / Algorithm Steps

1. **解析输入**：将表达式转换为真值表，收集输出为 1 的最小项；或直接读取最小项列表。
2. **分组与合并**：按二进制中 1 的个数分组，逐组比较合并，重复直到无法合并，得到质蕴含项。
3. **质蕴含项表**：构建覆盖表，标记每个质蕴含项覆盖的最小项。
4. **必要质蕴含项**：找出只被一个质蕴含项覆盖的最小项，对应项为必要质蕴含项。
5. **最小覆盖求解**：移除必要项及其覆盖项后，使用 Petrick 方法（或回溯）找出剩余最小项的最少质蕴含项组合。
6. **输出最简式**：将选中的质蕴含项转换为逻辑表达式。

1. **Parse input**: convert expression to truth table and collect minterms with output 1; or directly read minterm list.
2. **Group and merge**: group minterms by number of 1s in binary, compare and merge adjacent groups, repeat until no further merging, obtain prime implicants.
3. **Prime implicant table**: construct a coverage table marking which minterms each prime implicant covers.
4. **Essential prime implicants**: find minterms covered by only one prime implicant; those implicants are essential.
5. **Minimum cover**: after removing essential implicants and their covered minterms, use Petrick’s method (or backtracking) to find the minimal set of prime implicants covering the remaining minterms.
6. **Output minimal form**: convert selected prime implicants into a logical expression.

---

## 示例 / Examples

### 示例 1：简单吸收律
输入：`(A+B)(A'+B)`  
预期输出：`B`  
步骤简述：
- 展开为 `A·A' + A·B + B·A' + B·B` → `0 + AB + A'B + B` → `B(A+A')+B` → `B+B` → `B`

### 示例 2：最小项列表
输入：`∑m(0,1,2,3,4,5,6,7,8,9,10,11,12,13,14)` （四变量，缺15）  
预期输出：`A' + B' + C' + D'`

### 示例 3：复杂覆盖
输入：`∑m(0,2,5,6,7,8,10,11,12,13,14,15)`  
预期输出之一：`A'C' + A'B + BC' + AB + AC`

---

## 测试用例 / Test Cases

项目内置了多个测试用例（位于 `testCases.js`），覆盖简单到复杂的场景，包括：
- 基本吸收律
- 全1函数
- 多数覆盖
- 奇偶模式
- 无关项处理

运行测试可验证算法的正确性。

The project includes multiple test cases (in `testCases.js`) covering simple to complex scenarios, such as:
- Basic absorption laws
- Constant 1 function
- Majority coverage
- Parity patterns
- Don’t-care handling

Running these tests ensures the correctness of the algorithm.

---

## 技术栈 / Tech Stack

- HTML5 / CSS3
- JavaScript (ES6)
- 无外部依赖，纯原生实现

- HTML5 / CSS3
- JavaScript (ES6)
- No external dependencies, pure native implementation

---


## 贡献 / Contributing

欢迎提交 Issue 和 Pull Request。如果你有改进建议或发现了 bug，请随时联系。

Issues and pull requests are welcome. If you have suggestions or find bugs, please feel free to contact.

---

## 许可证 / License

MIT License

---


**感谢使用 QM-Simplifier！**  
**Thank you for using QM-Simplifier!**
