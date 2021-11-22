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
### 智能指针
    UE4中的智能指针主要用于管理原生对象，UObject自带GC不需要使用智能指针。
    智能指针的核心在于引用计数。
    正常情况下，自己new的指针可以使用智能指针管理。
    但某些指针，如FSocket之类，属于模块管理的指针，不可delete的，不要用智能指针管理，会引发异常崩溃。
    UE4的智能指针可选线程安全或非线程安全版本，根据需要选择。

    TSharedPtr 共享指针
        - 拥有对象
        - 可以为空
        - 非空时可转换为共享引用
    TSharedRef 共享引用(非空共享指针)
        - 拥有对象
        - 不可为空
        - 用于表明所有权
        - 可转换为共享指针
    TWeakPtr 弱指针
        - 不拥有对象
        - 可转换为共享指针
    TUniquePtr 唯一指针
        - 唯一拥有对象
        - 可转移所有权
        - 不应为共享指针或共享引用引用的对象创建唯一指针
    函数
        - MakeShared
        构造函数需要为公有
        - MakeShareable
        构造函数可以为私有，但效率较低
        自定义析构行为？
        - StaticCastSharedRef
        通常用于基类投射为衍生类
        - StaticCastSharedPtr
        通常用于基类投射为衍生类
        - ConstCastSharedRef
        作用于const智能引用
        - ConstCastSharedPtr
        作用于const智能指针
    侵入性访问器
        TSharedFromThis
        - 子类拥有 AsShared 和 SharedThis 方法
        - 非直接继承时，两个方法返回值不一致
        - AsShared 返回源类
        - SharedThis 返回当前类
        - 两个方法不可在构造函数中使用
        - 可以在外部直接调用两方法获得共享引用
        - 也可以用于工厂类
    投射：
    - StaticCastSharedPtr
    参数传递时：
    - 作为const &传递，减少引用计数操作
    其它：
        TWeakObjPtr
        TAutoPtr
        TScopedPtr
        
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
+ 多引脚节点  
```
UENUM(BlueprintType)
enum class Result : uint8
{
	Success,
	failed,
};
```
```
多出口
UFUNCTION(BlueprintCallable,meta=(ExpandEnumAsExecs="res"))
static void Test(Result& res);
```
```
多出口
UFUNCTION(BlueprintCallable,meta=(ExpandEnumAsExecs="res"))
static void Test(TEnumAsByte<Result> res);
```
### 编译
    + UBT
    + UHT
### 网络
### 多线程

[<<<回主页](https://github.com/ora-cat/UE4Handbook)
