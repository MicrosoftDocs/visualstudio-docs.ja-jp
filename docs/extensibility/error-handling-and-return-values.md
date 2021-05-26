---
title: エラー処理と戻り値 | Microsoft Docs
description: Visual Studio SDK によって、エラー通知を受信したときに豊富なエラー情報を記録するための相互運用機能アセンブリを提供する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- errors [Visual Studio SDK], handling
- error handling
- return values
ms.assetid: b2d9079d-39a6-438a-8010-290056694b5c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ac9c027623b34afa532f62b4b4c9443f219343e9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075264"
---
# <a name="error-handling-and-return-values"></a>エラー処理と戻り値
Vspackage と COM では、エラーに同じアーキテクチャが使用されています。 `SetErrorInfo` 関数と `GetErrorInfo` 関数は、Win32 アプリケーション プログラミング インターフェイス (API) の一部です。 統合開発環境 (IDE) のすべての VSPackage では、これらのグローバル Win32 API を呼び出して、エラー通知を受け取ったときに豊富なエラー情報を記録できます。 [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] には、エラー情報を管理するための相互運用機能アセンブリが用意されています。

## <a name="interop-methods"></a>相互運用機能メソッド
 便宜上、IDE には、Win32 API を呼び出す代わりに使用するメソッド <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> が用意されています。 マネージド コードで <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> を使用します。 エラー メッセージを表示する必要があるレベルでエラー `HRESULT` が到着すると (これは多くの場合、<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> コマンド ハンドラーを実装しているオブジェクトです)、IDE では別のメソッド <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> を使用して、適切なメッセージ ボックスが表示されます。 マネージド コードで <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> メソッドを使用します。

 VSPackage の実装者として、COM オブジェクトによって、通常 `ISupportErrorInfo` が実装されます。 `ISupportErrorInfo`インターフェイスにより、豊富なエラー情報を呼び出しチェーンの上方に移動させることができます。 プロセス間またはスレッド間で使用される可能性のあるオブジェクトでは `ISupportErrorInfo` をサポートし、豊富なエラー情報が呼び出し元に正しくマーシャリングされるようにする必要があります。

 エディター ファクトリ、エディター、階層、提供されているサービスなど、VSPackage に関連し、IDE の拡張に関係するすべてのオブジェクトで、豊富なエラー情報をサポートしている必要があります。 IDE では、`ISupportErrorInfo` を実装するために、これらの VSPackage オブジェクトを実装している必要はありませんが、常に推奨されます。

 IDE には、`HRESULT` が IDE に伝達されるたびに、エラー情報をレポートして、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] のユーザーに表示する役割があります。 さらに IDE は、`ErrorInfo` オブジェクトを作成するためのメカニズムでもあります。

## <a name="general-guidelines"></a>一般的なガイドライン
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> メソッドと <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> メソッドを使用して、VSPackage 実装の内部のエラーを設定し、報告することもできます。 ただし、原則として、VSPackage でエラー メッセージを処理する場合は、次のガイドラインに従ってください。

- VSPackage COM オブジェクトに `ISupportErrorInfo` を実装します。

- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> を実装するオブジェクトで <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> メソッドを呼び出すエラー報告メカニズムを作成します。

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> メソッドによって、IDE で、ユーザーにエラーを表示させます。

## <a name="error-information-in-the-ide"></a>IDE のエラー情報
 次の規則は、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] IDE でのエラー情報の処理方法を示しています。

- 古いエラー情報が確実にユーザーに報告されないようにするための防御戦略として、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> メソッドを呼び出す関数では、最初に <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> メソッドを呼び出す必要があります。 新しいエラー情報を設定する可能性のあるものを呼び出す前に、`null` を渡して、キャッシュされたエラー メッセージをクリアします。

- エラー メッセージを直接報告しない関数では、エラー `HRESULT` を返す場合に <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> メソッドを呼び出すことのみが許可されます。 関数に入るとき、または <xref:Microsoft.VisualStudio.VSConstants.S_OK> を返すときに、`ErrorInfo` をクリアすることができます。 この規則の唯一の例外は、受信パーティが明示的に回復できるか、または安全に無視できるエラー `HRESULT` を、呼び出しが返す場合です。

- エラー `HRESULT` を明示的に無視するすべてのパーティは、<xref:Microsoft.VisualStudio.VSConstants.S_OK> で <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> メソッドを呼び出す必要があります。 そうしないと、別のパーティが独自の `ErrorInfo` を提供せずに、エラーを生成するときに、`ErrorInfo` オブジェクトが誤って使用されることがあり ます。

- `HRESULT` エラーを生成するすべてのメソッドでは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> メソッドを呼び出して、豊富なエラー情報を提供することが推奨されます。 返された `HRESULT` が特殊な `FACILITY_ITF` エラーである場合は、メソッドが適切な `ErrorInfo` オブジェクトを提供する必要があります。 返されたエラーが標準システム エラー (<xref:Microsoft.VisualStudio.VSConstants.E_OUTOFMEMORY>、<xref:Microsoft.VisualStudio.VSConstants.E_ABORT>、<xref:Microsoft.VisualStudio.VSConstants.E_INVALIDARG>、<xref:Microsoft.VisualStudio.VSConstants.E_UNEXPECTED> など) の場合は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> メソッドを明示的に呼び出すことなく、エラー コードを返すことができます。 防御的なコーディング方法として、エラー `HRESULT` (システム エラーを含む) を生成する場合は、エラーを詳細に説明する `ErrorInfo` か、または `null` を使用して、常に <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> メソッドを呼び出します。

- 別の呼び出しによって生成されたエラーを返すすべての関数は、`ErrorInfo` オブジェクトを変更せずに、失敗した呼び出しから受け取った情報を `HRESULT` で渡す必要があります。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- [SetErrorInfo (コンポーネント オートメーション)](/previous-versions/windows/desktop/api/oleauto/nf-oleauto-seterrorinfo)
- [GetErrorInfo](/previous-versions/windows/desktop/api/oleauto/nf-oleauto-geterrorinfo)
- [ISupportErrorInfo インターフェイス](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-isupporterrorinfo)
