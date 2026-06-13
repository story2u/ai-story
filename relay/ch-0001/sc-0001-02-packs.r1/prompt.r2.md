# R2 修订约束

r1 作废原因：`context_packs/sc-0001-02.shen-yan.md` 的“盲区”段写了“柯先生不是普通游方修士”“此人有修为且在观察他”，这会把沈砚不该知道的真相递给演员。

请重新生成两个完整认知包，沿用原任务与输入，但严格执行以下修订：

- 沈砚包中不得出现“修为”“观察他”“细作”“真实身份”“受雇”“上头”“开府”等关于柯九真相的字眼。
- 沈砚盲区只能写成：“你不知道柯先生的来历与目的。”不得展开。
- 沈砚可以知道：柯先生是游方修士打扮的外乡人，刚才插话像帮忙也像试探旧砚，因此需提防。
- 柯九包可以保留自己的真实任务、修为、上头与对沈砚的观察。
- 不要写入真实文件；只输出文本，格式仍为：

```
STATUS: packed
PACKS: [context_packs/sc-0001-02.shen-yan.md, context_packs/sc-0001-02.ke-jiu.md]
ISOLATION_NOTE: ...

---FILE: context_packs/sc-0001-02.shen-yan.md
<完整认知包 markdown>

---FILE: context_packs/sc-0001-02.ke-jiu.md
<完整认知包 markdown>
```
