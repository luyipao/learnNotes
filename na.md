Θ，读音：theta、西塔；既是上界也是下界(tight)，等于的意思。

Ο，读音：big-oh、欧米可荣（大写）；表示上界(tightness unknown)，小于等于的意思。

ο，读音：small-oh、欧米可荣（小写）；表示上界(not tight)，小于的意思。

Ω，读音：big omega、欧米伽（大写）；表示下界(tightness unknown)，大于等于的意思。

ω，读音：small omega、欧米伽（小写）；表示下界(not tight)，大于的意思

## 稳定性初窥

稳定性(Stability)是数值格式的一种属性，表示我们的数值格式在合理的设置下不会胡来，即数值解是有收敛性的；

在某种意义下，格式的稳定性配合上"格式与问题的一致性(Consistency)"，就能推出数值格式对于原问题的估计的收敛性(Convergence)。

然而很多时候一致性是非常好验证的，因此为了得到收敛性，我们必须对稳定性进行研究。

> 这里插一句，数值格式虽然都是基于问题产生的，但是一旦写出数值格式，它便描述了一种独立于原问题的计算行为。这种行为在某些合理的设置下可能是对原问题的一种逼近。
>
> 这种把格式行为和原问题独立开思考的方式，是 modified equation 方法分析方程的一个出发点。

## 为什么有这么多的稳定性

这里首先按强弱排个序：Zero Stability/Absolute Stability/A-Stability/L-Stability，再逐个介绍。

1. Zero Stability: 在一致性保证下，等价于收敛性，于是指截断误差(LTE)随计算步长趋向0而趋向0；[资格考试前一小时更新：这个stability 应该是对测试函数$u' = 0$分析得到的
2. Absolute Stability: 上述稳定性仅保证步长趋向0时收敛，但并没有对步长给出建议，这个稳定性通过分析测试问题$u' = \lambda u$，对步长给出建议；
3. A-Stability: 然而在PDE 问题里，简单的半离散我们就能得到$\lambda \to \infty$的系统，于是我们希望Absolute Stability能覆盖整个左半复平面，这种情况叫A-Stability；
4. L-Stability: 注意A-Stability包含一类情况是Absolute Stability Region 恰好为左半平面，这种时候无穷远处的点是边界点，其对应的收敛性是marginal convergence，于是我们希望无穷远处也是内点，即A-Stability +$\lim_{z\to\infty}R(z) = 0$。