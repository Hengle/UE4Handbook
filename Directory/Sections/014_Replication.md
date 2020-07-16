# Replication 复制
1. 客户端-服务端模型
    + 服务端永远是权威(中心化)
2. 信息分类
    + 基础游戏交互  
        碰撞、移动、伤害
    + 美化效果  
        视觉效果、音效
    + 私人玩家信息  
        HUD
2. 网络模式
    + 独立  
        即玩家数为1或者分屏游戏，纯本地无网络交互
    + 客户端  
        玩家数大于1时，标记为clinet的端
    + 聆听服务器  
        玩家数大于1，未开启专属服务器时，标记未server的端
    + 专属服务器  
        专属服务器运行时，不具备图形、音效、输入的server端
3. 网络同步
    * 对象复制(从拥有者复制到任意端，或从服务端复制至任意端)  
        + Actor的Replicate标记  
            - 创建  
                客户端创建并未在服务端标记拥有所以无法同步
            - 销毁
        + Actor的ReplicateMovement标记  
            - 移动  
            不一定需要移动组件，会同步位置信息
        + Actor的bAlwaysRelevant标记
            - 强制相关性，总是同步
        + Actor的OnlyRelevantToOwner标记
            - 只更新其拥有者的对象
        + Actor的NetLoadOnClient标记
            - 客户端地图加载
        + Actor的NetUseOwnerRelevancy标记
            - 使用其拥有者的关联性和优先级
        + Actor的ReplayRewindable标记
            - 暂未研究
        + 复制模式的标记(Role\RemoteRole)
            + ROLE_AutonomousProxy  拥有
            + ROLE_SimulatedProxy   未拥有
    * 组件复制
        + 等同于actor
        + 子对象也可以复制
    * 变量复制(只从服务端复制到任意端)
        + replicated
        + repNotify
            - 自动生成对应onrep回调函数
            - 发生改变时触发回调
    * RPC(对象需要有replicate标记，客户端调用需要是拥有者)
        + 判断是否为服务端  
            Switch Has Authority
        + Server  
            客户端调用，服务端执行
        + Client  
            服务端调用，拥有者客户端执行
        + NetMulticast  
            服务端调用，所有客户端执行
        + Reliable 
            + 重传
            + 验证函数
4. 网络同步之关键——拥有  
    是否拥有的标记以服务端为准
    拥有标记是NetConnection一脉相承的结果
5. 相关性与优先级
    - 相关性NetRelevant
      + 网络模块关联
      + 骨架层级相关
      + 可见可碰相关
      + 距离剔除相关
    - 优先级NetPriority
      + 采用饥饿算法
   