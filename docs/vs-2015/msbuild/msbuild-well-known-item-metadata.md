---
title: MSBuild 既知のアイテム メタデータ | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, item metadata
- MSBuild, well-known item metadata
ms.assetid: b5e791b5-c68f-4978-ad8a-9247d03bb6c0
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: abf45460ec924aea7a6c1c18244aa7661c52d42f
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54790188"
---
# <a name="msbuild-well-known-item-metadata"></a>MSBuild 既知のアイテム メタデータ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
次の表は、作成時にすべてのアイテムに割り当てられたメタデータの説明です。 それぞれの例で、ファイル `C:\MyProject\Source\Program.cs` をプロジェクトに含めるために次のアイテム宣言が使用されました。  
  
```  
<ItemGroup>  
    <MyItem Include="Source\Program.cs" />  
</ItemGroup>  
```  
  
|アイテム メタデータ|説明|  
|-------------------|-----------------|  
|%(FullPath)|アイテムの完全パスが含まれます。 次に例を示します。<br /><br /> `C:\MyProject\Source\Program.cs`|  
|%(RootDir)|アイテムのルート ディレクトリが含まれます。 次に例を示します。<br /><br /> `C:\`|  
|%(Filename)|拡張子の付かない、アイテムのファイル名が含まれます。 次に例を示します。<br /><br /> `Program`|  
|%(Extension)|アイテムのファイル名の拡張子が含まれます。 次に例を示します。<br /><br /> `.cs`|  
|%(RelativeDir)|`Include` 属性に指定されたパスが最後の円記号 (\\) まで含まれます。 次に例を示します。<br /><br /> `Source\`|  
|%(Directory)|ルート ディレクトリのないアイテムのディレクトリが含まれます。 次に例を示します。<br /><br /> `MyProject\Source\`|  
|%(RecursiveDir)|`Include` 属性にワイルドカード \*\* が含まれる場合、このメタデータはワイルドカードを置き換えるパスの一部を指定します。 ワイルドカードの詳細については、「[方法: ビルドするファイルを選択する](../msbuild/how-to-select-the-files-to-build.md)」を参照してください。<br /><br /> *C:\MySolution\MyProject\Source\\\* フォルダーに Program.cs ファイルが格納されている場合、およびプロジェクト ファイルに次のアイテムが含まれている場合:<br /><br /> `<ItemGroup>`<br /><br /> `<MyItem Include="C:\**\Program.cs" />`<br /><br /> `</ItemGroup>`<br /><br /> `%(MyItem.RecursiveDir)` の値は *MySolution\MyProject\Source\\* です。|  
|%(Identity)|`Include` 属性で指定されたアイテム。 次に例を示します。<br /><br /> `Source\Program.cs`|  
|%(ModifiedTime)|アイテムが最後に変更された時間からのタイムスタンプが含まれます。 次に例を示します。<br /><br /> `2004-07-01 00:21:31.5073316`|  
|%(CreatedTime)|アイテムが作成された時間からのタイムスタンプが含まれます。 次に例を示します。<br /><br /> `2004-06-25 09:26:45.8237425`|  
|%(AccessedTime)|アイテムが最後にアクセスされた時間からのタイムスタンプが含まれます。<br /><br /> `2004-08-14 16:52:36.3168743`|  
  
## <a name="see-also"></a>関連項目
 [項目](../msbuild/msbuild-items.md)   
 [バッチ](../msbuild/msbuild-batching.md)   
 [MSBuild リファレンス](../msbuild/msbuild-reference.md)
