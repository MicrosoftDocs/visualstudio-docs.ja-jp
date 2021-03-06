---
title: Manifest to Code | Microsoft Docs
description: Visual Studio イメージ サービスで使用する .imagemanifest ファイルを取得する Manifest from Code ツールを使用する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 17ecacea-397d-4a97-b003-01bd5d56e936
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e63349b27ec8ea5617f6d1836ce9ece3251662d3
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903166"
---
# <a name="manifest-to-code"></a>Manifest to Code
Manifest to Code ツールは、Visual Studio イメージ サービス用の .imagemanifest ファイルを取得し、Visual Studio 拡張機能の C++、C#、VB、または .vsct ファイルでイメージ マニフェストの値を参照するための 1 つ以上のラッパー ファイルを生成するコンソール アプリケーションです。 このツールでは、Visual Studio イメージ サービスから直接イメージを要求するために、またはコードが独自の UI およびレンダリングを処理しない場合に API を通じてマニフェスト値を渡すために使用できるラッパー ファイルを生成します。

## <a name="how-to-use-the-tool"></a>ツールの使用方法
 **構文**

 ManifestToCode /manifest:\<Image Manifest file> /language:\<Code Language> \<Optional Args>

 **引数**

|**スイッチ名**|**ノート**|**必須/省略可能**|
|-|-|-|
|/manifest|コード ラッパーを作成または更新するために使用するイメージマニフェストへのパス。|必須|
|/language|コード ラッパーを生成するときの言語。<br /><br /> 有効な値: CPP、C++、CS、CSharp、C#、VB、または VSCT。値では大文字と小文字が区別されません。<br /><br /> VSCT 言語オプションでは、/monikerClass、/classAccess、/namespace オプションは無視されます。|必須|
|/imageIdClass|ImageIdClass の名前と、ツールによって作成された関連ファイル。 C++ 言語オプションの場合、.h ファイルだけが生成されます。<br /><br /> 既定値: \<Manifest Path>\MyImageIds\<Lang Ext>。|オプション|
|/monikerClass|monikerClass の名前と、ツールによって作成された関連ファイル。 C++ 言語オプションの場合、.h ファイルだけが生成されます。 VSCT 言語の場合、これは無視されます。<br /><br /> 既定値: \<Manifest Path>\MyMonikers\<Lang Ext>。|オプション|
|/classAccess|imageIdClass と monikerClass のアクセス修飾子。 アクセス修飾子が指定の言語に対して有効であることを確認します。 VSCT 言語オプションでは、これは無視されます。<br /><br /> 既定値: Public|オプション|
|/namespace|コード ラッパーで定義されている名前空間。 VSCT 言語オプションでは、これは無視されます。 '.' または '::' は、選択した言語オプションに関係なく、名前空間の有効な区切り記号です。<br /><br /> 既定値: MyImages|オプション|
|/noLogo|このフラグを設定すると、製品および著作権情報は出力されなくなります。|オプション|
|/?|ヘルプ情報を出力します。|オプション|
|/help|ヘルプ情報を出力します。|オプション|

 **例**

- ManifestToCode /manifest:D:\MyManifest.imagemanifest                /language:CSharp

- ManifestToCode /manifest:D:\MyManifest.imagemanifest                /language:C++                /namespace:My::Namespace                /imageIdClass:MyImageIds                /monikerClass:MyMonikers                /classAccess:friend

- ManifestToCode /manifest:D:\MyManifest.imagemanifest                /language:VSCT                /imageIdClass:MyImageIds

## <a name="notes"></a>Notes

- このツールは、Manifest from Resources ツールで生成されたイメージ マニフェストとともに使用することをお勧めします。

- このツールは、コード ラッパーを生成するシンボル エントリのみを調べます。 イメージ マニフェストにシンボルが含まれない場合、生成されるコード ラッパーは空になります。 イメージ マニフェストにシンボルを使用しない 1 つのイメージまたはイメージ セットがある場合、コード ラッパーから除外されます。

## <a name="sample-output"></a>サンプル出力
 **C# ラッパー**

 C# の単純なイメージ ID とイメージ モニカー クラスのペアは、次のコードのようになります。

```csharp
//-----------------------------------------------------------------------------
// <auto-generated>
//     This code was generated by the ManifestToCode tool.
//     Tool Version: 14.0.15198
// </auto-generated>
//-----------------------------------------------------------------------------

using System;

namespace MyImages
{
    public static class MyImageIds
    {
        public static readonly Guid AssetsGuid = new Guid("{442d8739-efde-46a4-8f29-e3a1e5e7f8b4}");

        public const int MyImage1 = 0;
        public const int MyImage2 = 1;
    }
}
//-----------------------------------------------------------------------------
// <auto-generated>
//     This code was generated by the ManifestToCode tool.
//     Tool Version: 14.0.15198
// </auto-generated>
//-----------------------------------------------------------------------------

using Microsoft.VisualStudio.Imaging.Interop;

namespace MyImages
{
    public static class MyMonikers
    {
        public static ImageMoniker MyImage1 { get { return new ImageMoniker { Guid = MyImageIds.AssetsGuid, Id = MyImageIds.MyImage1 }; } }
        public static ImageMoniker MyImage2 { get { return new ImageMoniker { Guid = MyImageIds.AssetsGuid, Id = MyImageIds.MyImage2 }; } }
    }
}
```

 **C++ ラッパー**

 C++ の単純なイメージ ID とイメージ モニカー クラスのペアは、次のコードのようになります。

```cpp
//-----------------------------------------------------------------------------
// <auto-generated>
//     This code was generated by the ManifestToCode tool.
//     Tool Version: 14.0.15198
// </auto-generated>
//-----------------------------------------------------------------------------

#pragma once

#include <guiddef.h>

namespace MyImages {

class MyImageIds {
public:

    static const GUID AssetsGuid;

    static const int MyImage1 = 0;
    static const int MyImage2 = 1;

};

__declspec(selectany) const GUID MyImageIds::AssetsGuid = {0x442d8739,0xefde,0x46a4,{0x8f,0x29,0xe3,0xa1,0xe5,0xe7,0xf8,0xb4}};

}
//-----------------------------------------------------------------------------
// <auto-generated>
//     This code was generated by the ManifestToCode tool.
//     Tool Version: 14.0.15198
// </auto-generated>
//-----------------------------------------------------------------------------

#pragma once

#include "ImageParameters140.h"
#include "MyImageIds.h"

namespace MyImages {

class MyMonikers {
public:

    static const ImageMoniker MyImage1;
    static const ImageMoniker MyImage2;

};

__declspec(selectany) const ImageMoniker MyMonikers::MyImage1 = { MyImageIds::AssetsGuid, MyImageIds::MyImage1 };
__declspec(selectany) const ImageMoniker MyMonikers::MyImage2 = { MyImageIds::AssetsGuid, MyImageIds::MyImage2 };

}
```

 **Visual Basic ラッパー**

 Visual Basic の単純なイメージ ID とイメージ モニカー クラスのペアは、次のコードのようになります。

```vb
' -----------------------------------------------------------------------------
'  <auto-generated>
'      This code was generated by the ManifestToCode tool.
'      Tool Version: 14.0.15198
'  </auto-generated>
' -----------------------------------------------------------------------------

Imports System

Namespace MyImages

    Public Module MyImageIds

        Public Shared ReadOnly AssetsGuid As Guid = New Guid("{442d8739-efde-46a4-8f29-e3a1e5e7f8b4}")

        Public Const MyImage1 As Integer = 0
        Public Const MyImage2 As Integer = 1

    End Module

End Namespace
' -----------------------------------------------------------------------------
'  <auto-generated>
'      This code was generated by the ManifestToCode tool.
'      Tool Version: 14.0.15198
'  </auto-generated>
' -----------------------------------------------------------------------------

Imports Microsoft.VisualStudio.Imaging.Interop

Namespace MyImages

    Public Module MyMonikers

        Public Readonly Property MyImage1
            Get
                Return New ImageMoniker With {.Guid = MyImageIds.AssetsGuid, .Id = MyImageIds.MyImage1}
            End Get
        End Property

        Public Readonly Property MyImage2
            Get
                Return New ImageMoniker With {.Guid = MyImageIds.AssetsGuid, .Id = MyImageIds.MyImage2}
            End Get
        End Property

    End Module

End Namespace
```

 **VSCT ラッパー**

 .vsct ファイルのイメージ ID のセットは次のようになります。

```xml
<?xml version='1.0' encoding='utf-8'?>
<!--
- [auto-generated]
     This code was generated by the ManifestToCode tool.
     Tool Version: 14.0.15198
- [/auto-generated]
-->
<CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable">
  <Symbols>
    <GuidSymbol name="AssetsGuid" value="{442d8739-efde-46a4-8f29-e3a1e5e7f8b4}">
      <IDSymbol name="MyImage1" value="0" />
      <IDSymbol name="MyImage2" value="1" />
    </GuidSymbol>
  </Symbols>
</CommandTable>
```
