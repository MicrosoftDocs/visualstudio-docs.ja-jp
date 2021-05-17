---
title: MSBuild プロジェクト ファイルでのデータの保持 | Microsoft Docs
description: プロジェクト ファイルにデータを保存する方法と、IPersistXMLFragment を使用してプロジェクト ファイルのデータをプロジェクトのサブタイプ集計レベルで保持する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project files, persisting data in
ms.assetid: 6a920cb7-453d-4ffd-af1c-6f3084bd03f7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5e2cf082e4ca6a45bf42bd66ce34111d5c056787
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105095018"
---
# <a name="persisting-data-in-the-msbuild-project-file"></a>MSBuild プロジェクト ファイルでのデータの保持
プロジェクトのサブタイプでは、後で使用するために、サブタイプ固有のデータをプロジェクト ファイルに保存する必要がある場合があります。 プロジェクトのサブタイプでは、プロジェクト ファイルの永続化を使用して次の要件を満たします。

1. プロジェクトのビルドの一部として使用されるデータを保持すること。 Microsoft Build Engine の詳細については、「[MSBuild](../../msbuild/msbuild.md)」を参照してください。ビルド関連の情報は、次のいずれかになります。

    1. 構成に依存しないデータ。 つまり、条件ではない、または条件として不足している MSBuild 要素に格納されているデータです。

    2. 構成に依存するデータ。 つまり、特定のプロジェクト構成に条件づけられている MSBuild 要素に格納されているデータです。 次に例を示します。

        ```
        <PropertyGroup Condition=" '$(Configuration)' == 'Debug' ">
        ```

2. ビルドに関連しないデータを保持すること。 このデータは、XML スキーマに対して検証されない自由形式の XML で表すことができます。

    1. 構成に依存しないデータ。

    2. 構成に依存するデータ。

## <a name="persisting-build-related-information"></a>ビルド関連の情報の保持
 プロジェクトのビルドに役立つデータの保持には MSBuild を使用します。 MSBuild システムでは、ビルド関連の情報のマスター テーブルが保持されます。 プロジェクトのサブタイプでは、このデータにアクセスしてプロパティ値を取得および設定します。 また、プロジェクトのサブタイプでは、保持対象のプロパティを追加したり、保持しないプロパティを削除したりすることで、ビルド関連のデータ テーブルを拡張することもできます。

 MSBuild データを変更するために、プロジェクトのサブタイプでは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> を使用してベース プロジェクト システムから MSBuild プロパティ オブジェクトを取得します。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> は、コア プロジェクト システムに実装されたインターフェイスです。集計プロジェクト サブタイプでは、`QueryInterface` を実行してそれを照会します。

 次に、<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> を使用してプロパティを削除する手順について説明します。

#### <a name="to-remove-a-property-from-an-msbuild-project-file"></a>MSBuild プロジェクト ファイルからプロパティを削除するには

1. プロジェクトのサブタイプの <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> で `QueryInterface` を呼び出します。

2. 削除するプロパティに `pszPropName` を設定して <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.RemoveProperty%2A> を呼び出します。

### <a name="persisting-non-build-related-information"></a>ビルド関連以外の情報の保持
 ビルドに関係のない、プロジェクト ファイル内のデータの保持には <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> を使用します。

 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> はメインの `project subtype aggregator` オブジェクト、`project subtype project configuration` オブジェクト、またはその両方に実装できます。

 次に、ビルド関連以外の情報の保持に関する主な概念を示します。

- ベース プロジェクトでは、メイン プロジェクトのサブタイプ (つまり、最も外側のプロジェクト サブタイプ) のアグリゲーター オブジェクトが呼び出され、構成に依存しないデータの読み込みと保存が行われます。また、プロジェクトのサブタイプ プロジェクト構成オブジェクトが呼び出され、構成依存のデータの読み込みと保存が行われます。

- ベース プロジェクトでは、プロジェクトのサブタイプ集計の各レベルに対して <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> のメソッドが複数回呼び出され、各レベルの GUID が渡されます。

- ベース プロジェクトでは、特定のプロジェクトのサブタイプ専用の XML フラグメントを渡すか、それを受け取ります。このメカニズムは、集計レベル間で状態を保持する手段として使用されます。

- ベース プロジェクトでは、GUID を渡す最も外側のプロジェクト サブタイプの <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> 実装が呼び出されます。 GUID が最も外側のプロジェクトのサブタイプに属している場合は、呼び出し自体が処理されます。それ以外の場合は、内部プロジェクトのサブタイプなどへの呼び出しがデリゲートされます。これは、GUID が対応しているプロジェクトのサブタイプが検出されるまで続きます。

- また、プロジェクトのサブタイプでは、内部プロジェクトのサブタイプへの呼び出しがデリゲートされる前または後に、XML フラグメントを変更することもできます。 次の例は、プロジェクト ファイルの抜粋です。ここでは、プロジェクトのサブタイプに固有のプロパティを含むファイルの名前が、そのプロジェクトのサブタイプに渡されます。

    ```
    <ProjectExtensions>
        <VisualStudio>
          <FlavorProperties GUID="{<FlavorGUID>}">
            <FlavorProject TestFileFolder="TestFile" />
          </FlavorProperties>
        </VisualStudio>
      </ProjectExtensions>
    ```

## <a name="see-also"></a>関連項目
- [プロジェクト サブタイプ](../../extensibility/internals/project-subtypes.md)
