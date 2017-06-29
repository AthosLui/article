### 分析

表单项可能最关心是字段 name，其次才是辅助的校验  
如果配置项太重，会喧宾夺主  
校验代码远大于组件本身，尤其多个表单项使用时候，使得整体表单会很庞杂

### redux-form 对表单项的定义

```jsx
// 引入
import { Field } from 'redux-form'

// 使用方式
<Field name="firstName" component="input" type="text" placeholder="First Name"/>
```
