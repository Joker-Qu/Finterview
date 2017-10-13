### 浏览器事件模型
事件发生分为三个阶段
1. 捕获
2. 目标
3. 冒泡
例如点击span元素 捕获阶段：window-document-body-...目标：span-冒泡：div-...body-document-window
- 捕获：从window逐步向下直到目标元素
- 目标：触发事件的元素
- 冒泡：逐级向上冒泡事件直到window

绑定在目标元素上的事件，不会遵循先捕获后冒泡的规则，而是哪种先绑定哪种先触发

e.target:真正触发事件的元素

e.currentTarget 事件绑定的元素

ie低版本的浏览器是用attachEvent，而高版本ie和标准浏览器用的是addEventListener