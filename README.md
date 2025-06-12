# README

## 项目概述

本项目基于 Mathematica 实现了 Lorenz 系统的数值模拟与 Lyapunov 指数计算，包含：

* 四阶 Runge-Kutta 算法求解 Lorenz 系统主轨道；
* 构造变分方程与 Jacobian 矩阵，追踪微小扰动演化；
* 使用 Gram-Schmidt 正交化法稳定计算 Lyapunov 指数谱；
* 绘制 Lyapunov 指数收敛曲线与三维相空间轨迹。

## 环境依赖

* Mathematica 12.0 及以上版本

## 目录结构

```
README.md               # 项目说明文档
lorenz_simulation.nb    # Mathematica Notebook 示例
lorenz_functions.m      # 包含函数定义的脚本文件
```

## 使用说明

1. 打开 `lorenz_simulation.nb`，或在 Mathematica 中加载 `lorenz_functions.m`。
2. 设置系统参数：

   ```mathematica
   σ = 16; ρ = 45.92; β = 4;
   x0 = {19, 20, 50}; stepsize = 0.01;
   ```
3. 调用主轨道演化函数：

   ```mathematica
   {xT, PhiT} = IntVarEq[F[x], DPhi, x, Phi, x0, Phi0, {T, stepsize}];
   ```
4. 计算并绘制 Lyapunov 指数：

   ```mathematica
   lces = ComputeLyapunovExponents[...]    
   ConvergencePlot[lces]
   ```
5. 绘制相空间轨迹：

   ```mathematica
   PhaseSpaceC[F, x0, 100, 20, stepsize, {1,2,3}]
   ```

## 函数说明

* `JacobianMtx[funs, vars]`：计算雅可比矩阵。
* `RKStep`、`RKPoint`、`RKList`：实现 RK4 数值积分。
* `IntVarEq`：联合模拟主系统与变分方程。
* `GramSchm`：执行 Gram-Schmidt 正交化。
* `ComputeLyapunovExponents`：批量计算并返回 Lyapunov 指数谱。
* `ConvergencePlot`：绘制 Lyapunov 指数收敛曲线。
* `PhaseSpaceC`：可视化三维相空间轨迹。

## 示例

```mathematica
<< lorenz_functions.m
(* 运行示例 *)
{lces, attractor} = RunLorenzAnalysis[{19,20,50}, {σ,ρ,β}, 0.01, 800];
ConvergencePlot[lces]
```

## 许可证

本项目基于 MIT 协议开源，详情见 LICENSE。
