# 基础知识
1. 策略: 渐进增强 (progressive enhancement)

    - 厂商前缀: -webkit-transform, -moz-transform, -ms-transform, transform
    - 条件规则与检测脚本:
        - @supports 
        - JS检测

2. 基础: 创建结构化、语义化富HTML

    - ID 和 class 属性
        - 提倡使用 ID 来标识特定模块的特定实例(已有class)
        - ID 可以用于在文档中标识元素，但通常不用于添加样式
    
    - div 和 span
        - 确保只在额外提供样式接入的情况下才使用 div
        