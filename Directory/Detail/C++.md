### InsideUE4
[知乎大佬剖析UE4](https://zhuanlan.zhihu.com/insideue4)
### 命名
    + U
        继承于UObject
    + A
        继承与AActor
    + F
        类和结构
    + T
        模板
    + I
        接口
    + E
        枚举
### 宏
    + UCLASS
        包裹类
    + USTRUCT
        包裹结构
    + GENERATED_BODY  
        该宏标识的类使用无参数的构造函数
    + GENERATED_UCLASS_BODY
        该宏标识的类使用父类构造函数，参数为
        const FObjectInitializer& ObjectInitializer
    + UFUNCTION
        包裹功能
    + UPROPERTY
        包裹属性
    + TEXT
        ANSI编码（使用""包裹）
        Unicode编码（使用L""包裹）
        wchar_t appName[5]=TEXT("test");
### 类型
    + 基础类型
        int8(1)
        int16(2)
        int32(4)
        int64(8)
        uint8(1)
        uint16(2)
        uint32(4)
        uint64(8)
        float(4)
        double(8)
        bool
        TCHAR
        PTRINT
    + 字符串
        理解三种类型的本质，转换直接存在限制
        FString
            唯一允许操作的字符串类
            + FString TestString = FString(TEXT("This is my test FString"));
            ->TestName = FName(*TestString);
            ->TestText = FText::FromString(TestString);
        FName
            不区分大小写
            + FName TestName = FName(TEXT("ThisIsTestFName"));
            -> FString TestString = TestName.ToString();
            -> FText TestText = FText::FromName(TestName);
        FText
            显示字符串,本地化应用,KV
            + FText TestText = LOCTEXT("Your Ket", "Your Text");
            + FText TestText = NSLOCTEXT("Your Namespace", "Your Key", "Your Text");
            + FText TestText = FText::GetEmpty();
            + FText TestText = FText();
            -> TestString = TestText.ToString();
    + 容器
        TArray
        TMap
        TSet

        TQueue
        TSparseArray
        TLinkedList
        TDoubleLinkedList
    + 智能指针
        TSharedPtr
        TSharedRef
        TWeakPtr

        TWeakObjPtr
        TAutoPtr
        TScopedPtr
        TUniquePtr
### 模板
    + TSubclassOf
        提供 UClass 类型安全性的模板类
        UPROPERTY限定
        运行时与编译时的类型安全限定
### Actor生命周期
    + BeginPlay
    + EndPlay
    + Tick
### 类结构
### 反射
### 编译
    + UBT
    + UHT
### 网络
### 多线程

[<<<回主页](https://github.com/ora-cat/UE4Handbook)
