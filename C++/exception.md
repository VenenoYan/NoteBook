## C++内部异常
| 异常名 | 说明 |
| -- | -- |
| exception | 最常见的问题 |
| runtime_error | 运行时错误：仅在运行时才能检测到的问题 |
| range_error | 运行时错误：结果超出范围 |
| overflow_error | 运行时错误：计算上溢 |
| underflow_error | 运行时错误：计算下溢 |
| logic_error | 逻辑错误：运行前检测到的问题 |
| domain_error | 逻辑错误：参数结果值不存在 |
| invalid_argument | 逻辑错误：不适合的参数 |
| length_error | 逻辑错误：试图超出类型最大长度的对象 |
| out_of_range | 逻辑错误：使用的值超出范围 |


### 自定义异常：一般继承自exception


