---
title: 単一ファイル ジェネレーターの登録 | Microsoft Docs
description: Visual Studio でカスタム ツールを登録して、インスタンス化し、特定のプロジェクト タイプに関連付ける方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- registration, custom tools
- custom tools, defining registry settings
ms.assetid: db7592c0-1273-4843-9617-6e2ddabb6ca8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ee110defb06d308c017230a36cebc2b04b3c63b9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062682"
---
# <a name="registering-single-file-generators"></a>単一ファイル ジェネレーターの登録
カスタム ツールを [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] で使用できるようにするには、そのツールを登録して、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] によってインスタンスが作成され、特定のプロジェクト タイプに関連付けられる必要があります。

### <a name="to-register-a-custom-tool"></a>カスタム ツールを登録するには

1. カスタム ツール DLL は、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ローカル レジストリまたはシステム レジストリの HKEY_CLASSES_ROOT の下に登録します。

    たとえば、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に付属しているマネージド MSDataSetGenerator カスタム ツールの登録情報を次に示します。

   ```
   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\CLSID\{E76D53CC-3D4F-40A2-BD4D-4F3419755476}]
   @="COM+ class: Microsoft.VSDesigner.CodeGenerator.TypedDataSourceGenerator.DataSourceGeneratorWrapper"
   "InprocServer32"="C:\\WINDOWS\\system32\\mscoree.dll"
   "ThreadingModel"="Both"
   "Class"="Microsoft.VSDesigner.CodeGenerator.TypedDataSourceGenerator.DataSourceGeneratorWrapper"
   "Assembly"="Microsoft.VSDesigner, Version=14.0.0.0, Culture=Neutral, PublicKeyToken=b03f5f7f11d50a3a"
   ```

2. Generators\\*GUID* の下にある目的の [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ハイブにレジストリ キーを作成します。ここで *GUID* は、特定の言語のプロジェクト システムまたはサービスで定義された GUID です。 キーの名前は、カスタム ツールのプログラム的な名前になります。 カスタム ツール キーの値は次のとおりです。

   - (既定値)。

        省略可能。 カスタム ツールについてのわかりやすい説明を提供します。 このパラメーターは省略可能ですが、使用することをお勧めします。

   - CLSID

        必須。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> を実装する COM コンポーネントのクラス ライブラリの識別子を指定します。

   - GeneratesDesignTimeSource

        必須。 このカスタム ツールで生成されたファイルからの型をビジュアル デザイナーで使用できるようにするかどうかを示します。 このパラメーターの値は、ビジュアル デザイナーで使用できない型の場合は 0、ビジュアル デザイナーで使用できる型の場合は 1 である必要があります。

   > [!NOTE]
   > カスタム ツールを使用できるようにする言語ごとに、カスタム ツールを個別に登録する必要があります。

    たとえば、MSDataSetGenerator は、言語ごとに 1 回登録します。

   ```
   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\Generators\{164b10b9-b200-11d0-8c61-00a0c91e29d5}\MSDataSetGenerator]
   @="Microsoft VB Code Generator for XSD"
   "CLSID"="{E76D53CC-3D4F-40a2-BD4D-4F3419755476}"
   "GeneratesDesignTimeSource"=dword:00000001

   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\Generators\{fae04ec1-301f-11d3-bf4b-00c04f79efbc}\MSDataSetGenerator]
   @="Microsoft C# Code Generator for XSD"
   "CLSID"="{E76D53CC-3D4F-40a2-BD4D-4F3419755476}"
   "GeneratesDesignTimeSource"=dword:00000001
   ```

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>
- [単一ファイル ジェネレーターの実装](../../extensibility/internals/implementing-single-file-generators.md)
- [ビジュアル デザイナーへのタイプの公開](../../extensibility/internals/exposing-types-to-visual-designers.md)
- [BuildManager オブジェクトの概要](/previous-versions/8f9kffa8(v=vs.140))