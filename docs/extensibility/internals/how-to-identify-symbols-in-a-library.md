---
title: '方法: ライブラリでのシンボルの識別 | Microsoft Docs'
description: シンボル ライブラリから Visual Studio オブジェクト マネージャーにナビゲーション情報を渡すメソッドを実装することによって、ライブラリ内のシンボルを識別する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Call Browser tool, identifying symbols in the library
- Call Browser tool
ms.assetid: 8fb0de61-71e7-42d1-8b41-2ad915474384
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c6c897801b98857f4a310323d4e00583c98245d5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078878"
---
# <a name="how-to-identify-symbols-in-a-library"></a>方法: ライブラリでのシンボルの識別
シンボル参照ツールには、シンボルの階層ビューが表示されます。 シンボルは、名前空間、オブジェクト、クラス、クラス メンバー、およびその他の言語要素を表します。

 階層内の各シンボルは、シンボル ライブラリから次のインターフェイスを介して [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] オブジェクト マネージャーに渡されるナビゲーション情報によって識別できます。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfoNode>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumNavInfoNodes>.

 階層内のシンボルの場所によって、シンボルが区別されます。 これにより、シンボル参照ツールで特定のシンボルに移動できるようになります。 シンボルへの一意の完全修飾パスによって場所が決まります。 パス内の各要素はノードです。 パスは最上位ノードから始まり、特定のシンボルで終わります。 たとえば、M1 メソッドが C1 クラスのメンバーで、C1 が N1 名前空間にある場合、M1 メソッドの完全パスは N1.C1.M1 です。 このパスには、N1、C1、および M1 の 3 つのノードが含まれています。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] オブジェクト マネージャーでは、ナビゲーション情報を使用して、階層内のシンボルを検索、選択、および選択して維持することができます。 参照ツール間を移動できます。 **オブジェクト ブラウザー** を使用して [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] プロジェクトのシンボルを参照するときに、メソッドを右クリックし、**呼び出しブラウザー** ツールを起動して、呼び出し先のメソッドを表示することができます。

 2 つの形式でシンボルの場所を記述します。 正規形式は、シンボルの完全修飾パスに基づきます。 階層内におけるシンボルの一意の場所を表します。 シンボル参照ツールに依存しません。 正規形式の情報を取得するために、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] オブジェクト マネージャーでは <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumCanonicalNodes%2A> メソッドを呼び出します。 表示形式では、特定のシンボル参照ツール内におけるシンボルの場所を記述します。 シンボルの位置は、階層内における他のシンボルの位置を基準とします。 あるシンボルに対して、複数の表示パスを使用できますが、正規パスは 1 つだけです。 たとえば、C1 クラスが C2 クラスから継承され、両方のクラスが N1 名前空間にある場合、**オブジェクト ブラウザー** には次の階層ツリーが表示されます。

```
N1
    C1
        Bases and Interfaces
            C2
    C2
        Bases and Interfaces
. . . . . . . . . . .

```

 C2 クラスの正規パスは、この例では N1 + C2 です。 C2 の表示パスは、C1 および "Bases and Interfaces" ノードが含まれ、N1 + C1 + "Bases and Interfaces" + C2 になります。

 表示形式の情報を取得するために、オブジェクト マネージャーでは <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumPresentationNodes%2A> メソッドを呼び出します。

## <a name="to-obtain-canonical-and-presentation-forms-information"></a>正規および表示形式の情報を取得するには

1. <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumCanonicalNodes%2A> メソッドを実装します。

     オブジェクト マネージャーでは、このメソッドを呼び出して、シンボルの正規パスに含まれるノードの一覧を取得します。

    ```vb
    Public Function EnumCanonicalNodes(ByRef ppEnum As Microsoft.VisualStudio.Shell.Interop.IVsEnumNavInfoNodes) As Integer
        Dim EnumNavInfoNodes As CallBrowserEnumNavInfoNodes = _New CallBrowserEnumNavInfoNodes(m_strMethod)
        ppEnum = CType(EnumNavInfoNodes, IVsEnumNavInfoNodes)
        Return 0
    End Function
    ```

    ```csharp
    public int EnumCanonicalNodes(out Microsoft.VisualStudio.Shell.Interop.IVsEnumNavInfoNodes ppEnum)
    {
        CallBrowserEnumNavInfoNodes EnumNavInfoNodes =
            new CallBrowserEnumNavInfoNodes(m_strMethod);
        ppEnum = (IVsEnumNavInfoNodes)(EnumNavInfoNodes);
        return 0;
    }

    ```

2. <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumPresentationNodes%2A> メソッドを実装します。

     オブジェクト マネージャーでは、このメソッドを呼び出して、シンボルの表示パスに含まれるノードの一覧を取得します。

## <a name="see-also"></a>関連項目
- [シンボル参照ツールのサポート](../../extensibility/internals/supporting-symbol-browsing-tools.md)
- [方法: オブジェクト マネージャーを使用したライブラリの登録](../../extensibility/internals/how-to-register-a-library-with-the-object-manager.md)
- [方法: ライブラリによって提供されるシンボルのリストをオブジェクト マネージャーに公開する](../../extensibility/internals/how-to-expose-lists-of-symbols-provided-by-the-library-to-the-object-manager.md)
