# 蓝图

Paper.js是一个年轻的库，但会计划提供更多功能。 虽然很多核心功能已经存在并且运行良好，但仍然缺少某些功能。 这里是计划添加的概述。可能在阅读本文时，其中一些功能已经实现但是列表尚未更新，所以你也可以查看每日构建。

# 已支持

* SVG 导入/导出。
* 持久化的 JSON 数据格式。
* 使用贝塞尔粗线剪裁技术快速获取[路径交叉点](http://scriptographer.org/tutorials/paths/geometric-tests/#finding-path-intersections)。
* [布尔几何路径操作](http://scriptographer.org/tutorials/paths/geometric-operations/)，例如并集，交集，排除等。
* 图形项目的[命中测试](http://scriptographer.org/tutorials/document-items/hit-tests/)，并为它们添加鼠标事件处理，以实现简单而强大的交互性。
* 在 [Node.js](http://nodejs.org/) 中运行 Paper.js。

## 即将完成

* [简单的用户界面](http://scriptographer.org/tutorials/user-interface/interface-components/)，允许用户调整脚本中的值。

# 计划

* 可参数化的路径偏移/笔划，将笔划扩展到轮廓，可轻松选择各种笔划表现。
* 与 CSS 类似的选择器，用于匹配 Paper.js 文档中的物体。
* 通过 JSON 和 ExtendScript 直接从 Adobe Illustrator 导入图形。
* 使用 SVG 字体排版，支持高级排版功能，比如在图形形状和路径沿边键入文字，可控制文本子范围的样式。
* PDF 导入/导出。
* 通过一种嵌入 Javascript 引擎的原生的支持硬件加速的运行环境，独立运行的 Paper.js 应用。



