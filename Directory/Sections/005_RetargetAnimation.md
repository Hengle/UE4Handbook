# Retarget Animation - 重定向动画
1. 动画重定向(Animation Retargeting)

    将A骨骼的动画，应用于B骨骼之上
    + 相同骨架
        - 导出-导入-选定骨骼
        - 重定向选项

            骨架树>左上角>选项>显示重定向选项>勾选
        - 三种骨骼平移重定位
            1. 动画(Animation)
            2. 骨架(Skeleton)
            3. 比例动画(AnimationScaled)
        - 两足生物官方建议设置

            ```
            · 根骨骼、IK骨骼、武器骨骼和任何一种将使用动画模式的标记。

            · 骨盆将使用比例动画，以确保其在正确的高度，同时仍能动作。

                · 您希望平移和重定位动画的其他任何骨骼也应该使用比例动画。

            · 所有其他骨骼都应使用骨架。它们将使用来自目标骨架的静态平移。
            ```
            + 递归地设置平移重定位骨架(Recursively Set Translation Retargeting ...)
    + 不同骨架
        - 重定向管理器(Retarget Manager)
            + 管理重定位源(Manage Retarget Source)
                - 找到要重定位的动画
                - 选择对应骨骼
                - 打开重定位管理器
                - 选择目标骨架
            + 设置绑定(Set up Rig)
                - 选中类人骨骼
                - 自动映射
                - 手动映射
                - 高级选项
            + 管理重定位基本姿势(Manage Retarget Base Pose)
                - 显示姿势
                - 手动调整
                - 导入姿势
                - 使用当前姿势(修改生效)
        - 重定位动画资源(Retarget Anim Assets)
            + 复制动画资源并重定位(Duplicate Anim Assets and Retarget)
                - 应用骨架预览
                - 选择骨架
                - 更换保存路径
                - 重定向
2. 设置重定位源

    动画序列(Animation Sequence)>
    资源细节(Asset Details)>
    动画(Animation)>
    重定位源(Retarget Source)

## 学习目标
    1. 导出导入让动画指定同一骨骼
    2. 调整重定向选项使动画正常
    3. 导入虚幻争霸角色
    4. 重定向使虚幻争霸角色可以使用Mannequin的动画

[<<<回主页](https://github.com/ora-cat/UE4Handbook)