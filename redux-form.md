现状：每一个input或者select设置一个onChange方法，来监听表单value值的变化

1. 只有一份数据需要维护也就是 fields 里面的数据，fields 是一个数组，这里面的数据就是表单中的需要动态改变的项
2. 初始化设置 initialValues 属性
3. 数据校验方式，支持同步校验和异步校验
4. 获取表单数据，直接 handleSubmit 方法即可接收表单数据。