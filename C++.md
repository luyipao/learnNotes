# C++

Eigen报错`no type named 'epsilon' in 'std::numeric_limits<double>'`，排查后发现是由于我定义了宏epsilon，应该与eigen的宏发生了冲突。将自己的宏删除后恢复正常。由此在定义宏的时候可以加上个性化的前缀来避免冲突，比如`yuedao_epsilon`。

尽可能多地使用`const`关键词。输出结果可以是常量，尽量前缀const；不需要改变input或class的成员值，尽量后缀const。

## Eigen

```c++
MatrixXd U = A.triangularView<Upper>(); 	// 上三角，包含对角线元素
MatrixXd L = A.triangularView<Lower>();		// 下三角
MatrixXd U = A.triangularView<StrictlyUpper>(); //严格上三角，不包含对角线元素
MatrixXd L = A.triangularView<StrictlyLower>(); //严格下三角，
MatrixXd D = A.diagonal().asDiagonal();		// 对角矩阵
A.inverse();	// 逆矩阵
A.transpose();		// 转置矩阵
```

```
Eigen::VectorXd my_eigen_vector = Eigen::Map<Eigen::VectorXd>(my_vector.data(), my_vector.size());		// vector -> VectorXd
```

## Json for Modern c++

传递向量

```json
///input.json
{
	"vec": [1, 2, 3, 4]		// 不能使用{1, 2, 3, 4}
}
/// test.cpp
ifstream file(input.json);
json data = json::parse(file);
vector<double> v = data["vec"];
```

## 输出

在数值分析中，我们的输出通常要求保留两位小数，并使用科学计数法表示。下面是实现代码。

```c++
#include <iomanip> // input/output manipulation
#define SET_FP_FMT std::cout << std::setprecision(2) << std::scientific << std::uppercase
double my_number = 1234.56789;
std::cout << SET_FP_FMT << my_number << std::endl;
```

