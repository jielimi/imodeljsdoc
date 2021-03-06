# 并发控制

并发控制是一种在保持数据完整性的同时协调并发事务（公文包）的方法。并发控制是在应用程序的代码中实现的，并且基于公文包的身份。并发控制不应与用户访问控制混淆。要进行协调更改，应用必须遵循3条基本规则：

使用Code之前，请先保留Code。

根据iModel的并发控制策略，有选择地在修改模型和元素之前将其锁定

push之前需要先pull并merge。

iModel具有并发控制策略，该策略指定多个公文包如何修改模型和元素。该策略可能规定必须使用锁，迫使事务是顺序的，或者它可能指定具有冲突解决方案的变更合并以合并同时事务的结果。

应用程序使用BriefcaseDb和ConcurrencyControl遵循并发控制规则。

锁定和代码保留在进行更改时与公文包关联，并在推送时释放。

---

_注意：若需要参见更多，请详见源码ConcurrencyControl.ts。_

_github 源码地址_[_https://github.com/imodeljs/imodeljs/blob/master/core/backend/src/ConcurrencyControl.ts_](https://github.com/imodeljs/imodeljs/blob/master/core/backend/src/ConcurrencyControl.ts)

示例代码 github地址[https://github.com/imodeljs/imodeljs/blob/master/core/backend/src/test/integration/IModelWrite.test.ts](https://github.com/imodeljs/imodeljs/blob/master/core/backend/src/test/integration/IModelWrite.test.ts)

