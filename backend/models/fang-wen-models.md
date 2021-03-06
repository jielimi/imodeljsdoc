# IModelDb.Models

该类表示iModel数据文件中所有model的集合，使用该类可以对指定model执行创建，查询，更改，删除等具体操作。通过IModelDb.models即可访问该接口。

其主要包含以下方法\(_**仅供参考，若需要了解更多，请查看相关源码，见文件IModelDb.d.ts或IModelDb.ts**_\):

---

```js
//获取具有指定标识符的ModelProps。
getModelProps<T extends ModelProps>(modelId: Id64String): T

//获取具有指定标识符的ModelProps。
tryGetModelProps<T extends ModelProps>(modelId: Id64String): T | undefined

//查询指定模型的上次修改时间。
queryLastModifiedTime(modelId: Id64String): string

//获取具有指定标识符的模型。
getModel<T extends Model>(modelId: Id64String): T

//获取具有指定标识符的模型。
tryGetModel<T extends Model>(modelId: Id64String): T

//将模型的属性读取为json字符串。
getModelJson(modelIdArg: string): string

//将模型的属性读取为json字符串。
tryGetModelJson(modelIdArg: string): string | undefined

//获取指定Element的子模型。
getSubModel<T extends Model>(modeledElementId: Id64String | GuidString | Code): T

//获取指定Element的子模型。
tryGetSubModel<T extends Model>(modeledElementId: Id64String | GuidString | Code): T | undefined

//在内存中创建一个新模型。
createModel<T extends Model>(modelProps: ModelProps): T

//插入新模型。
insertModel(props: ModelProps): Id64String

//更新现有模型。
updateModel(props: UpdateModelOptions): void

//删除一个或多个现有模型。
deleteModel(ids: Id64Arg): void
```

---

# 查询Model示例

根据模型Id可以从iModel数据文件中查询到指定的模型\(如果存在\)。具体查询方式如下所示：

```
    //查询方式一
    const modelId = "0x38";//模型Id
    const model = this.imodelDb.models.tryGetModel(modelId);
    if (model) {
      //显示模型基本属性;
      console.log("找到模型");
      console.log(model.parentModel);
      console.log(model.classFullName);
      console.log(model.jsonProperties);

      //显示具体模型特有属性;
      const m2 = model as SheetModel;
      if (m2) {
        console.log("表单模型");
        console.log(SheetModel.className);
      }
    }

    //查询方式二
    const modelId = "0x38";//模型Id
    const model: SheetModel | undefined = this.imodelDb.models.tryGetModel<SheetModel>(modelId);
    if (model) {
      //显示模型基本属性;
      console.log("找到模型");
      console.log(model.parentModel);
      console.log(model.classFullName);
      console.log(model.jsonProperties);

      //显示具体模型特有属性;
      console.log(model.globalOrigin);
    }
```



