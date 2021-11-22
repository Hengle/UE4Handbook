# UE4中json的相关应用

## json字符串的读写

+ 读
```cpp
//json对象
TSharedPtr<FJsonObject> jsonObject;
//目标字符串
FString JsonStr;
//添加字段
jsonObject->SetStringField("Key", "Value");
//写入字符串
TSharedRef< TJsonWriter<> > Writer = TJsonWriterFactory<>::Create(&JsonStr);
bool success = FJsonSerializer::Serialize(jsonObject.ToSharedRef(), Writer);
```
+ 写
```cpp
//源字符串
FString JsonStr = TEXT("{\"Key\":\"Value\"}");
//json对象
TSharedPtr<FJsonObject> jsonObject;
//解析字符串
TSharedRef< TJsonReader<> > Reader = TJsonReaderFactory<>::Create(JsonStr);
bool success = FJsonSerializer::Deserialize(Reader, jsonObject);
```

## C++中json与结构体互转

* 依赖模块 "Json","JsonUtilities"
* 示例：
``````cpp 
USTRUCT(BlueprintType)
struct FMyStruct {
	GENERATED_USTRUCT_BODY()
	UPROPERTY(BlueprintReadWrite) FString userid;
	UPROPERTY(BlueprintReadWrite) FString password;
};
``````

- Json2 to Struct
``````cpp 
FString JsonStrIn = TEXT("{\"userid\":\"123456\",\"password\":\"abc123\"}"); // Json字符串
FMyStruct MyStructOut;
FJsonObjectConverter::JsonObjectStringToUStruct(JsonStrIn, &MyStructOut, 0, 0);
``````

- Struct to Json
``````cpp 
FMyStruct MyStructIn;
FString JsonStrOut;
FJsonObjectConverter::UStructToJsonObjectString(FRequest_Login::StaticStruct(), &Info, JsonStrOut, 0, 0);
``````

## 蓝图中json与结构体互转
+ 涉及到蓝图泛型，参照泛型章节