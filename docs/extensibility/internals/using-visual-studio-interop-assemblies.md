---
title: Visual Studio 相互運用機能アセンブリの使用 | Microsoft Docs
description: Visual Studio の相互運用機能アセンブリによって、マネージド アプリケーションから、Visual Studio の機能拡張を提供する COM インターフェイスにアクセスできるようにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio, interop assemblies
- interop assemblies, Visual Studio
- managed VSPackages, interop assemblies
ms.assetid: 1043eb95-4f0d-4861-be21-2a25395b3b3c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fc5f1a01c406f2457eaaa6a58e214f06fbd31127
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106213655"
---
# <a name="using-visual-studio-interop-assemblies"></a>Visual Studio 相互運用機能アセンブリの使用
Visual Studio の相互運用機能アセンブリを使用すると、マネージド アプリケーションから、Visual Studio の機能拡張を提供する COM インターフェイスにアクセスすることができます。 通常の COM インターフェイスと、その相互運用バージョンには、いくつかの違いがあります。 たとえば、HRESULT は通常 int 値として表され、例外と同様に処理する必要があります。また、パラメーター (特に出力パラメーター) を異なる方法で処理する必要があります。

## <a name="handling-hresults-returned-to-managed-code-from-com"></a>COM からマネージド コードに返される HRESULT の処理
 マネージド コードから COM インターフェイスを呼び出す場合は、HRESULT 値を確認し、必要な場合に例外をスローします。 渡された HRESULT の値に応じて、<xref:Microsoft.VisualStudio.ErrorHandler> クラスには COM 例外をスローする <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> メソッドが含まれます。

 既定では、<xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> は、0 より小さい値を持つ HRESULT を渡されるたびに例外をスローします。 このような HRESULT が許容される値であり、例外をスローする必要がない場合は、値のテスト後に追加 HRESULT の値を <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> に渡す必要があります。 テスト対象の HRESULT が、<xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> に明示的に渡される HRESULT 値と一致する場合、例外はスローされません。

> [!NOTE]
> <xref:Microsoft.VisualStudio.VSConstants> クラスには、共通 HRESULT (<xref:Microsoft.VisualStudio.VSConstants.S_OK> や <xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL> など) および [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] HRESULT (<xref:Microsoft.VisualStudio.VSConstants.VS_E_INCOMPATIBLEDOCDATA> や <xref:Microsoft.VisualStudio.VSConstants.VS_E_UNSUPPORTEDFORMAT> など) の定数が含まれます。 また、<xref:Microsoft.VisualStudio.VSConstants> には、COM の SUCCEEDED および FAILED マクロに対応する <xref:Microsoft.VisualStudio.ErrorHandler.Succeeded%2A> および <xref:Microsoft.VisualStudio.ErrorHandler.Failed%2A> メソッドが用意されています。

 たとえば、<xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL> が許容可能な戻り値であり、ゼロ未満の他の HRESULT がエラーを表す次の関数呼び出しがあるとします。

 :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/vssdkhresultinformation/vb/vssdkhresultinformationpackage.vb" id="Snippet1":::
 :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/vssdkhresultinformation/cs/vssdkhresultinformationpackage.cs" id="Snippet1":::

 許容可能な戻り値が複数ある場合は、<xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> への呼び出しの一覧にのみ追加の HRESULT 値を追加することができます。

 :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VSSDK/vssdkhresultinformation/vb/vssdkhresultinformationpackage.vb" id="Snippet2":::
 :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VSSDK/vssdkhresultinformation/cs/vssdkhresultinformationpackage.cs" id="Snippet2":::

## <a name="returning-hresults-to-com-from-managed-code"></a>マネージド コードから COM に HRESULT を返す
 例外が発生しない場合、マネージド コードは呼び出し元の COM 関数に <xref:Microsoft.VisualStudio.VSConstants.S_OK> を返します。 COM 相互運用では、マネージド コードで厳密に型指定される一般的な例外がサポートされます。 たとえば、受け入れられない `null` 引数を受け取るメソッドは、<xref:System.ArgumentNullException> をスローします。

 スローする例外が不明であり、COM に戻す HRESULT がわかっている場合は、<xref:System.Runtime.InteropServices.Marshal.ThrowExceptionForHR%2A> メソッドを使用して、適切な例外をスローすることができます。 これは、<xref:Microsoft.VisualStudio.VSConstants.VS_E_INCOMPATIBLEDOCDATA> などの非標準のエラーでも機能します。 <xref:System.Runtime.InteropServices.Marshal.ThrowExceptionForHR%2A> では、渡された HRESULT を厳密に型指定された例外にマップすることを試みます。 できない場合は、代わりに一般的な COM 例外をスローします。 最終的な結果では、マネージド コードから <xref:System.Runtime.InteropServices.Marshal.ThrowExceptionForHR%2A> に渡す HRESULT が呼び出し元の COM 関数に返されます。

> [!NOTE]
> 例外によって、パフォーマンスが低下します。例外は、異常なプログラムの条件を示すことを目的としています。 頻繁に発生する条件は、スローされた例外ではなく、インラインで処理をする必要があります。

## <a name="iunknown-parameters-passed-as-type-void"></a>void** 型として渡された IUnknown パラメーター
 COM インターフェイスでは `void **` 型として定義されているにも関わらず、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 相互運用機能アセンブリのメソッド プロトタイプでは `[``iid_is``]` として定義されている [out] パラメーターを探してください。

 場合によっては、COM インターフェイスで `IUnknown` オブジェクトが生成され、それが、その COM インターフェイスによって `void **` 型として渡されます。 これらのインターフェイスは特に重要です。IDL で変数が [out] として定義されている場合、`IUnknown` オブジェクトは `AddRef` メソッドを使用して参照カウントされるからです。 オブジェクトが正しく処理されなかった場合は、メモリ リークが発生します。

> [!NOTE]
> COM インターフェイスによって作成され、[out] 変数で返される `IUnknown` オブジェクトは、明示的に解放されなかった場合、メモリ リークの原因となります。

 このようなオブジェクトを処理するマネージド メソッドでは、<xref:System.IntPtr> を `IUnknown` オブジェクトへのポインターとして扱い、<xref:System.Runtime.InteropServices.Marshal.GetObjectForIUnknown%2A> メソッドを呼び出してオブジェクトを取得する必要があります。 その後、呼び出し元で、戻り値を適切な型にキャストする必要があります。 オブジェクトが不要になった場合は、<xref:System.Runtime.InteropServices.Marshal.Release%2A> を呼び出して解放します。

 次に示すのは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.QueryViewInterface%2A> メソッドを呼び出し、`IUnknown` オブジェクトを正しく処理する方法の例です。

```
MyClass myclass;
Object object;
IntPtr pObj;
Guid iid = Typeof(MyClass).Guid;
int hr = windowFrame.QueryViewInterface(ref iid, out pObj);
if (NativeMethods.Succeeded(hr))
{
    try
    {
        object = Marshal.GetObjectForIUnknown(pObj);
        myclass = object;
    }
    finally
    {
        Marshal.Release(pObj);
    }
}
else
{
    // error calling QueryViewInterface
}
```

> [!NOTE]
> 次のメソッドは、`IUnknown` オブジェクト ポインターを <xref:System.IntPtr> 型として渡すことがわかっています。 これらは、このセクションで説明されている方法で処理してください。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.InitializeForOwner%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetNestedHierarchy%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.CreateProject%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.QueryViewInterface%2A>

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2.get_CfgType%2A>

## <a name="optional-out-parameters"></a>省略可能な [out] パラメーター
 COM インターフェイスでは [out] データ型 (`int`、`object` など) として定義されているにも関わらず、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 相互運用機能アセンブリのメソッド プロトタイプでは同じデータ型の配列として定義されているパラメーターを探してください。

 一部の COM インターフェイス (<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgs%2A> など) では、[out] パラメーターがオプションとして扱われます。 オブジェクトが必須でない場合、これらの COM インターフェイスは、[out] オブジェクトを作成するのではなく、そのパラメーターの値として `null` ポインターを返します。 これは仕様です。 これらのインターフェイスでは、`null` ポインターは VSPackage の正しい動作の一部と見なされ、エラーは返されません。

 CLR では [out] パラメーターの値を `null` にすることが許可されていないため、これらのインターフェイスの設計された動作の一部は、マネージド コード内で直接使用することができません。 影響を受けるインターフェイスの [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 相互運用機能アセンブリ メソッドでは、関連するパラメーターを配列として定義することで、この問題が回避されます。`null` 配列を渡すことなら、CLR で許可されるためです。

 これらのメソッドのマネージド実装では、返されるものがない場合、`null` 配列をパラメーター内に配置するようにしてください。 それ以外の場合は、正しい型の単一要素配列を作成し、戻り値を配列に格納します。

 省略可能な [out] パラメーターを使ってインターフェイスから情報を受け取るマネージド メソッドは、パラメーターを配列として受け取ります。 まずは、配列の最初の要素の値を確認してください。 それが `null` でない場合は、最初の要素を元のパラメーターであるかのように扱ってください。

## <a name="passing-constants-in-pointer-parameters"></a>ポインター パラメーターでの定数の引き渡し
 COM インターフェイスでは [in] ポインターとして定義されているにも関わらず、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 相互運用機能アセンブリのメソッド プロトタイプでは <xref:System.IntPtr> 型として定義されているパラメーターを探してください。

 同様の問題は、COM インターフェイスがオブジェクト ポインターではなく、0、-1、-2 などの特殊な値を渡した場合にも発生します。 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] とは異なり、CLR では、定数をオブジェクトとしてキャストすることはできません。 代わりに、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 相互運用機能アセンブリでは、パラメーターが <xref:System.IntPtr> 型として定義されます。

 これらのメソッドのマネージド実装では、<xref:System.IntPtr> クラスに `int` と `void *` の両方のコンストラクターがあって、必要に応じてオブジェクトまたは整数定数から <xref:System.IntPtr> が作成されるという事実を利用する必要があります。

 この型の <xref:System.IntPtr> パラメーターを受け取るマネージド メソッドでは、<xref:System.IntPtr> 型変換演算子を使って結果を処理する必要があります。 まずは、<xref:System.IntPtr> を `int` に変換し、それを関連する整数定数に対してテストします。 一致する値がない場合は、必要な型のオブジェクトに変換して続行します。

 この例については、「<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>」および「<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenSpecificEditor%2A>」を参照してください。

## <a name="ole-return-values-passed-as-out-parameters"></a>[out] パラメーターとして渡される OLE 戻り値
 COM インターフェイスでは戻り値 `retval` があるにも関わらず、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 相互運用機能アセンブリのメソッド プロトタイプでは、戻り値 `int` と追加の [out] 配列パラメーターがあるメソッドを探してください。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 相互運用機能アセンブリのメソッド プロトタイプには COM インターフェイスのメソッドよりも 1 つ多くのパラメーターがあるため、これらのメソッドでは特別な処理が必要であることを理解する必要があります。

 OLE アクティビティを処理する多くの COM インターフェイスでは、OLE 状態に関する情報が、インターフェイスの戻り値 `retval` に格納されている呼び出し元プログラムに送信されます。 対応する [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 相互運用機能アセンブリ メソッドでは、戻り値を使用するのではなく、[out] 配列パラメーターに格納されている呼び出し元プログラムに情報が送り返されます。

 これらのメソッドのマネージド実装では、[out] パラメーターと同じ型の単一要素配列を作成し、それをパラメーター内に配置する必要があります。 配列要素の値は、適切な COM `retval` と同じである必要があります。

 この型のインターフェイスを呼び出すマネージド メソッドでは、[out] 配列から最初の要素を取得する必要があります。 この要素は、対応する COM インターフェイスからの戻り値 `retval` であるかのように扱うことができます。

## <a name="see-also"></a>関連項目
- [アンマネージ コードとの相互運用](/dotnet/framework/interop/index)
