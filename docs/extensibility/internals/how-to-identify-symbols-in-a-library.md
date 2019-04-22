---
title: '方法: ライブラリ内のシンボルの識別 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Call Browser tool, identifying symbols in the library
- Call Browser tool
ms.assetid: 8fb0de61-71e7-42d1-8b41-2ad915474384
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b74eaab3edb205b5218cad5a61556f4803614d94
ms.sourcegitcommit: 53aa5a413717a1b62ca56a5983b6a50f7f0663b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59651968"
---
# <a name="how-to-identify-symbols-in-a-library"></a>方法: ライブラリ内のシンボルを識別します。
シンボル参照ツールでは、シンボルの階層ビューを表示します。 シンボルは、名前空間、オブジェクト、クラス、クラスのメンバー、およびその他の言語要素を表します。

 階層内の各シンボルをシンボル ライブラリによって渡されたナビゲーション情報で識別できます、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]次のインターフェイスを介してオブジェクト マネージャー。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfoNode>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumNavInfoNodes>。

 階層内の記号の場所は、シンボルを区別します。 これにより、特定のシンボルに移動する、シンボル参照ツールができます。 シンボルに一意な完全修飾パスは、場所を決定します。 パス内の各要素は、ノードです。 パスは、最上位のノードから始まり、特定のシンボルで終わります。 たとえば、M1 メソッドは、C1 クラスのメンバー、C1 が N1 の名前空間にある場合は、M1 メソッドの完全なパスは N1 です。C1 します。M1 します。 このパスには、3 つのノードが含まれています。N1、C1、および M1 します。

 ナビゲーション情報により、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]検索を選択すると、選択したシンボルに注意してください、階層にオブジェクトのマネージャー。 別に 1 つの参照ツールから移動することができます。 使用中に**オブジェクト ブラウザー**でシンボルを参照する、[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]プロジェクト、メソッドを右クリックし、開始できる、**呼び出しブラウザー**呼び出し先のメソッドを表示するツール。

 2 つの形式では、シンボルの場所について説明します。 正規の形式は、記号の完全修飾パスに基づきます。 階層の一意の記号の位置を表します。 これは、シンボル参照ツールの依存しません。 正規の形式の情報を取得する、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]オブジェクト マネージャー呼び出し<xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumCanonicalNodes%2A>メソッド。 プレゼンテーションのフォームでは、特定のシンボル参照ツール内でシンボルの場所について説明します。 階層内の他の記号の位置に対する相対パス、記号の位置です。 特定のシンボルは、1 つだけの既定のパスが、いくつかのプレゼンテーション パスにあります。 たとえば、C1 クラス C2 クラスから継承され、両方のクラスは、N1 の名前空間には、**オブジェクト ブラウザー**次の階層ツリーを表示します。

```
N1
    C1
        Bases and Interfaces
            C2
    C2
        Bases and Interfaces
. . . . . . . . . . .

```

 この例での C2 クラスの既定のパスには、N1 + C2 です。 C2 のプレゼンテーション パスには、C1 と「ベースおよびインターフェイス」のノードが含まれます。N1 + C1 +「ベースおよびインターフェイス」+ C2 します。

 プレゼンテーションのフォームはをオブジェクトの manager 呼び出しを取得する<xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumPresentationNodes%2A>メソッド。

## <a name="to-obtain-canonical-and-presentation-forms-information"></a>正規の取得、およびプレゼンテーションのフォーム情報

1.  <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumCanonicalNodes%2A> メソッドを実装します。

     オブジェクト マネージャーは、シンボルの既定のパスに含まれるノードの一覧を取得するには、このメソッドを呼び出します。

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

2.  <xref:Microsoft.VisualStudio.Shell.Interop.IVsNavInfo.EnumPresentationNodes%2A> メソッドを実装します。

     オブジェクト マネージャーは、シンボルのプレゼンテーションのパスに含まれるノードの一覧を取得するには、このメソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [シンボル参照ツールをサポートします。](../../extensibility/internals/supporting-symbol-browsing-tools.md)
- [方法: オブジェクト マネージャーにライブラリを登録します。](../../extensibility/internals/how-to-register-a-library-with-the-object-manager.md)
- [方法: オブジェクト マネージャーにライブラリによって提供されるシンボルのリストを公開します。](../../extensibility/internals/how-to-expose-lists-of-symbols-provided-by-the-library-to-the-object-manager.md)