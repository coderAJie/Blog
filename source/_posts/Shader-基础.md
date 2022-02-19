---
title: Shader-基础
categories: [Shader]
---

简介

分类

-   固定管线着色器（没有嵌套CG语言 代码中没有CGPROGARAM的）
-   顶点shader（顶点片段着色器 代码段中有surf函数）
    干预顶点位置 改变模型形态
-   像素shader（表面着色器 代码段中有#pargma vertex name 和#pragma fragment frag）
    干预顶点上色 哪个点贴哪个纹理

语法

    Shader “name” { // name shader名字
    // 定义的一些属性，定义在这里的会在属性查看器里面显示; 
    [Propeties] 
    // 子着色器列表，一个Shader必须至少有一个子着色器; 
    Subshaders: {....}
    // 如果子着色器显卡不支持，就会降级,即Fallback操作;
    [Fallback]

---

属性

    _Range (“range value”, Range(0, 1)) = 0.3; // 定义一个范围
    _Color(“color”, Color) = (1, 1, 1, 1); // 定义一个颜色
    _FloatValue(“float value”, Float) = 1 // 定义一个浮点
    _MainTex (“Albedo”, Cube) = “skybox” {TexGen CubeReflect} // 定义一个立方贴图纹理属性;

1.  类型 多种多样
    -   Float,Int,Vector(4维向量),Range(start,end)
    -   Color(n,n,n,n)(0-1)
    -   2D,3D,Cube,Rect：纹理属性
2.  options：纹理属性选项
    -   TexGen：纹理生成模式（纹理自动生成纹理坐标）类型多样，有ObjectLinear,EyeLinear,SphereMap,CubeReflect,CubeNormal
    -   LightmapMod：光照贴图模式（纹理会被渲染器的光线贴图影响）

---

子着色器

着色器使用Tags来告诉他们如何和何时会被渲染到渲染引擎，包含多个Pass，依次执行

        SubShader { [Tags] [CommonState] Passdef [Passdef ...] }

        SubShader
        {
            Pass 
            {
                Lighting Off        // 关闭灯光
                SetTexture [_MainTex] { }
            }
        }

-   SubShader Tags
            Tags { "TagName1" = "Value1" "TagName2" = "Value2" }

指定 TagName1 的值为 Value1, TagName2 的值为 Value2。你可以有尽可能多的标签。

标签基本上是键值对。在SubShader标签是用来确定SubShader呈现顺序和其他参数。注意，下面的标签必须是SubShader部分，而不是在Pass内部！

Unity除了内置标签,你可以使用你自己的标签和使用Material.GetTag函数查询它们。

---

Pass

        Pass { [Name and Tags] [RenderSetup] }

-   Name and Tags：Pass 可以定义它的名称和任意数量的标签-传递给渲染引擎的传递意图的名称 / 值的字符串。
-   RenderSetup：设置图形硬件的各种状态，例如α混合应打开，深度测试应使用，等等。
    -   Cull：设置多边形剔除模式
                Cull Back | Front | Off
    -   ZTest：设置深度缓冲测试模式
                ZTest (Less | Greater | LEqual | GEqual | Equal | NotEqual | Always)
    -   ZWrite：设置深度缓冲的写模式
                ZWrite On | Off
    -   Blend：设置α混合模式
                Blend SourceBlendMode DestBlendMode
                Blend SourceBlendMode DestBlendMode, AlphaSourceBlendMode AlphaDestBlendMode
    -   ColorMask：设置彩色通道写掩码。设置为0将关闭所有渲染的颜色通道。默认模式是写所有通道（RGBA），但是对于一些特殊的效果，你可能想离开一定的渠道不被修改，或完全禁用颜色写
                ColorMask RGB | A | 0 | any combination of R, G, B, A
    -   Offset：设置Z缓冲深度偏移量
                Offset OffsetFactor, OffsetUnits
-   固定功能着色器命令
                Lighting On | Off
                Material { Material Block }
                SeparateSpecular On | Off
                Color Color-value
                ColorMaterial AmbientAndDiffuse | Emission
                //所有这些控制固定功能，每个顶点照明：打开它，设置材料的颜色，打开高光的亮点，提供默认的颜色，如果顶点光照关闭，并控制网格顶点颜色如何影响照明
    -   Fog：
                Fog { Fog Block }
    -   AlphaTest：
                AlphaTest ( Less | Greater | LEqual | GEqual | Equal | NotEqual | Always ) CutoffValue
    -   Texture Combiners：
                SetTexture textureProperty { combine options }
