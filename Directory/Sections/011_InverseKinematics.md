# Inverse kinematics - 反向动力学

1. 反向动力学
    + 角色蓝图部分
        - 获取缩放比例与半高
        - 射线检测计算距离
    + 动画蓝图事件图表部分
        - 获取角色蓝图变量
        - 保存为动画蓝图变量
    + 动画蓝图动画图表部分
        - 局部空间>组件空间
        - IK设置
        - 组件空间>局部空间
2. 虚拟骨骼
    用于控制骨骼的骨骼。作用于两骨骼之间。
    + 选择起始骨骼
    + 添加虚拟骨骼(Add Virtual Bone)
    + 选择目标骨骼
3. 骨架控制节点(Skeletal Controls)
    + 输入姿势(Component Pose)
    + 权重值(Alpha)
    + 输出姿势(Pose/Blank)
## 学习目标
    1. 用IK实现走楼梯
    2. 利用虚拟骨骼简化动画迭代

[<<<回主页](https://github.com/ora-cat/UE4Handbook)