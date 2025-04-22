# 利用 Substance Painter 制作 Smoothness Map

## 引言

本文档中生成粗糙度贴图的流程大致采用该视频的前13分30秒的教学：

[(1512) 🦜Best Roughness Skin techniques in Substance - YouTube](https://www.youtube.com/watch?v=Sn53wo-47aA&t=533s)

**和教程中选择的背景贴图不同，在substance painter中把背景贴图改成 Over Clouds会更接近Unity游戏内效果**

![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1GXn4B6vWg3KODQ4/img/6bfeadbc-ab96-4712-95be-ca98ec913ce2.png)

此流程相对于之前的人物头模粗糙度贴图制作要精准许多，质感也有不小提升；并且更重要的是可以避免之前直接转颜色贴图为粗糙度中的a经典问题：白人很滑，黑人太糙

### 相对准确的光滑度（Smoothness）贴图范围标准

![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1GXn4B6vWg3KODQ4/img/491f00fa-ae6b-447b-aff4-5f7065378de1.png)

![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1GXn4B6vWg3KODQ4/img/ecf1d1cf-cce8-4c0d-8bec-3c23512d62d2.png)

#### 使用该流程以及直接转换颜色贴图为粗糙度的效果对比：（该文档写成之前最新制作的头模）

![iwEdAqNnaWYDAQTRAX4F0QLUBrAQnRT0vph-1AdTZoRxo78AB9MAAAAA6VrbHwgACaJpbQoAC9IA-eJ3.gif_720x720q90.gif](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1GXn4B6vWg3KODQ4/img/93b273a4-5a3b-4859-beb8-b2ef659a5066.gif)

Fig1. 本文档中介绍的流程

![iwEcAqNnaWYDAQTRAX4F0QLUBrA10ShnBz4q3gdTZtayjugAB9MAAAAA6VrbHwgACaJpbQoAC9IAyldr.gif_720x720q90.gif](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1GXn4B6vWg3KODQ4/img/75f81355-35e4-4aa5-8e1c-5166694f0fc5.gif)

Fig2. 直接使用颜色图转为粗糙度（）

![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1GXn4B6vWg3KODQ4/img/c3038a1e-bf20-4996-baef-25cc137b458f.png)![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1GXn4B6vWg3KODQ4/img/35aef998-1147-4647-ac2e-0bbf5009675d.png)

Fig3. 自然状态下无流汗的参考角色

---

## 前提条件

在开始之前，请确保具备以下条件：

*   一个 **导入到 Substance Painter 中的 3D 角色模型，不要包含\_model后缀**。
    
*   角色的 **法线贴图**，用于生成cavity map。
    
*   角色真人的皮肤的参考图。
    

---

## 步骤 1：收集参考图像

#### Roughness base：

可以用化完妆的额头作为base roughness参考（一般来说化妆师会压掉该位置的高光），或者使用球员高光最弱的照片为参考：

![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1GXn4B6vWg3KODQ4/img/98bf9dd8-ba6d-4c9e-9528-8f1882c8d248.png)

Fig4. 黑人roughness base

![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1GXn4B6vWg3KODQ4/img/c319262c-c917-470a-985c-748921ee61ef.png)

Fig5. 白人roughness base

![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1GXn4B6vWg3KODQ4/img/7c58bd51-8fb4-4166-8412-0d5e7b802e13.png)

Fig6. 亚洲人roughness base

![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1GXn4B6vWg3KODQ4/img/5a02f7da-32f4-4c1d-a1af-8a78062470c1.png)

Fig7. 拉丁裔roughness base

#### roughness Greasy（自然状态下出油较多部分）参考：

尽量找人物在冷静的，自然的状态下的照片（不是商业棚拍）作为参考，而不要使用角色满头大汗的图

![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1GXn4B6vWg3KODQ4/img/ed866244-052a-4f29-9e23-121c0f7fc19c.png)![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1GXn4B6vWg3KODQ4/img/f82e920f-2af0-44e9-b2f6-1afa6c1aca37.png)

---

## 步骤 2：设置 Roughness 基础层

**目的：** 建立一个基础的 Roughness 值，为整个皮肤纹理提供一致的起点，在添加变化之前确保统一性。

**操作步骤：**

1.  **添加新的填充层：**
    
    *   在 **图层** 面板中，点击 **添加填充层** 按钮。
        
2.  **设置基础 Roughness：**
    
    *   选择填充层后，导航到 **属性** 面板。
        
    *   找到 **Roughness** 参数，具体参考值在文档一开始（**注意**：sp的数值为粗糙度，文档一开始的为最终验收的光滑度，换算关系为：光滑度 = 1 - 粗糙度）。此中等值为大多数皮肤类型提供了平衡的表面反射。
        
3.  **命名图层：**
    
    *   将图层重命名为 **“Base Roughness”**，以便清晰识别。
        

**参考：**

![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1GXn4B6vWg3KODQ4/img/683ebc2a-fa49-46a1-8c53-aa7fd0ef8d36.png)

---

## 步骤 3：使用黑色遮罩添加油脂细节

**目的：** 识别并详细描述油腻区域，如内唇、T 区和眼睑周围，通过模拟自然皮肤变化来增强真实感。

**操作步骤：**

1.  **创建新的填充层：**
    
    *   在基础 Roughness 层上方添加另一个 **填充层**。
        
2.  **应用黑色遮罩：**
    
    *   右键点击新填充层，选择 **添加黑色遮罩**。此遮罩默认隐藏该层。
        
3.  **绘制油腻区域：**
    
    *   选择 **绘画** 工具，使用合适的画笔在以下区域显示遮罩：
        
        *   **内唇**
            
        *   **T 区（额头和鼻子区域）**
            
        *   **眼睑周围**
            

![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1GXn4B6vWg3KODQ4/img/1504b0da-4736-4904-b84c-b86eac650b03.png)

4.  **设置油腻区域的 Roughness 值：**
    
    *   在该填充层的 **属性** 面板中，将 **Roughness** 调成和角色参考图相近的样子。
        
5.  **细化遮罩：**
    
    *   使用软画笔和调整不透明度，创建油腻和非油腻区域之间的平滑过渡。
        

**参考：**

![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1GXn4B6vWg3KODQ4/img/106229bf-185f-4d08-8aba-b0741a5c9f56.png)

**提示：**

*   建议利用参考图像指导油腻区域的放置和范围。
    

---

## 步骤 4：生成并应用用于毛孔的腔体贴图

**目的：** 从法线贴图生成的腔体贴图突出显示毛孔等小表面细节，通过调整粗糙度在必要的地方创建细微变化。

**操作步骤：**

**具体操作描述起来较为复杂，可直接参考引言中视频的7分50到13分30秒的内容**

**Roughness值和base roughness保持一致即可，即0.6左右**

**参考：**

![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1GXn4B6vWg3KODQ4/img/9439468e-ce3a-41de-8bdf-7ec658817c7b.png)

**提示：**

*   确保腔体贴图准确地表示毛孔分布。
    
*   避免过度绘制毛孔，以保持自然的皮肤外观。
    

---

## 步骤 5：创建并调整头发遮罩

**目的：** 准确定义头发的 Roughness，根据参考角色的照片来调整反光或哑光。

**操作步骤：**

1.  **添加另一个填充层：**
    
    *   在前面的图层上方创建一个 **填充层**。
        
2.  **创建头发遮罩：**
    
    *   为此图层添加 **黑色遮罩**。
        
    *   使用选择工具或手动绘制，定义存在头发的区域。
        

![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1GXn4B6vWg3KODQ4/img/08ebd302-317c-48ff-8c0a-d1b12adcf6d6.png)

3.  **设置头发的 Roughness 值：**
    
    *   在 **属性** 面板中，如果是黑人的寸头，可将 **Roughness** 设置为 **1**；如果是比较顺滑的头发可以适当降低一点点粗糙度。具体以实机效果为准
        

**参考：**

![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/1GXn4B6vWg3KODQ4/img/93b8c8dd-e552-439d-8525-f6c6d3765a63.png)

---

## 步骤 6：导出 Multi 贴图

**TODO: 等待所有的贴图格式，内容以及通道确认之后，给定一个output template一键导出所需格式。**

---