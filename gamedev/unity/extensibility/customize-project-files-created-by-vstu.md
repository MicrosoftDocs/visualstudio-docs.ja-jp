---
title: VSTU によって作成されるプロジェクト ファイルのカスタマイズ | Microsoft Docs
description: Visual Studio Tools for Unity (VSTU) によって作成されたプロジェクト ファイルをカスタマイズする方法について説明します。 C# コードの例を確認します。
ms.custom: ''
ms.date: 04/19/2021
ms.technology: vs-unity-tools
ms.prod: visual-studio-dev16
ms.topic: conceptual
ms.assetid: 60b8cc1d-cacc-404d-b768-77e81bc354f8
author: conceptdev
ms.author: crdun
manager: crdun
ms.workload:
- unity
ms.openlocfilehash: a4a5973863877db2d071f9be8d4689928b21a689
ms.sourcegitcommit: 3e1ff87fba290f9e60fb4049d011bb8661255d58
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2021
ms.locfileid: "107879318"
---
# <a name="customize-project-files-created-by-vstu"></a>VSTU によって作成されたプロジェクト ファイルのカスタマイズ
Unity によって、プロジェクト ファイルの生成中にコールバックが提供されます。 [`AssetPostprocessor`](https://docs.unity3d.com/ScriptReference/AssetPostprocessor.html) を使用して `OnGeneratedSlnSolution` および `OnGeneratedCSProject` メソッドを実装し、プロジェクトまたはソリューション ファイルが再生成されるたびにそれを変更します。

## <a name="demonstrates"></a>対象
Visual Studio Tools for Unity によって生成された Visual Studio プロジェクト ファイルをカスタマイズする方法について示します。

## <a name="example"></a>例

```csharp
using System;
using UnityEditor;
using UnityEngine;

public class ProjectFilePostprocessor : AssetPostprocessor
{
  public static string OnGeneratedSlnSolution(string path, string content)
  {
    // TODO: process solution content
    return content;
  }

  public static string OnGeneratedCSProject(string path, string content)
  {
    // TODO: process project content
    return content;
  }
}
```
