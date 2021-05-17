---
title: サービスの基本情報 | Microsoft Docs
description: 別の VSPackage で使用するインターフェイスであるサービスについて説明します。 VSPackage のサービスでは、組み込みまたはその他のサービスをオーバーライドできます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- services, essentials
ms.assetid: fbe84ad9-efe1-48b1-aba3-b50b90424d47
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 69e7e1c5b18019c4ff063ec504fc702f47f7e023
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080828"
---
# <a name="service-essentials"></a>サービスの基本情報
サービスは、2 つの VSPackage 間のコントラクトです。 ある VSPackage で、別の VSPackage で使用するインターフェイスの特定のセットが提供されます。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 自体は、他の VSPackage にサービスを提供する VSPackage のコレクションです。

 たとえば、SVsActivityLog サービスを使用して IVsActivityLog インターフェイスを取得することができます。このインターフェイスを使用して、アクティビティ ログに書き込むことができます。 詳細については、「[方法: アクティビティ ログを使用する](../../extensibility/how-to-use-the-activity-log.md)」を参照してください。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] には、登録されていない組み込みのサービスもいくつか用意されています。 VSPackage では、サービス オーバーライドを提供することによって、組み込みまたはその他のサービスを置き換えることができます。 サービスに対して許可されるサービス オーバーライドは 1 つだけです。

 サービスには探索可能性はありません。 そのため、使用するサービスのサービス識別子 (SID) と、どのインターフェイスが提供されるかを把握しておく必要があります。 この情報は、本サービスのリファレンス ドキュメントに記載されています。

- サービスを提供する VSPackage は、サービス プロバイダーと呼ばれます。

- 他の VSPackage に提供されるサービスは、グローバル サービスと呼ばれます。

- それらを実装する VSPackage、または作成した任意のオブジェクトでのみ使用できるサービスは、ローカル サービスと呼ばれます。

- 組み込みのサービスや他のパッケージによって提供されるサービスを置き換えるサービスは、サービス オーバーライドと呼ばれます。

- サービスまたはサービス オーバーライドは、要求時に読み込まれます。つまり、サービス プロバイダーは、提供されるサービスが別の VSPackage によって要求されたときに読み込まれます。

- オンデマンド読み込みをサポートするには、サービス プロバイダーでグローバル サービスを [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に登録します。 詳細については、「[方法: サービスを提供する](../../extensibility/how-to-provide-a-service.md)」を参照してください。

- サービスを取得した後、必要なインターフェイスを取得するには、[QueryInterface](/cpp/atl/queryinterface) (アンマネージド コード) またはキャスト (マネージド コード) を使用します。次に例を示します。

  ```vb
  TryCast(GetService(GetType(SVsActivityLog)), IVsActivityLog)
  ```

  ```csharp
  GetService(typeof(SVsActivityLog)) as IVsActivityLog;
  ```

- マネージド コードでは、その型によってサービスを参照します。一方、アンマネージド コードでは GUID によってサービスを参照します。

- [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] で VSPackage が読み込まれると、サービス プロバイダーが VSPackage に渡され、VSPackage でグローバル サービスにアクセスできるようになります。 これを、VSPackage の "サイト設定" と呼びます。

- VSPackage は、作成するオブジェクトのサービス プロバイダーにすることができます。 たとえば、フォームでカラー サービスの要求をそのフレームに送信すると、要求が [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に渡されることがあります。

- 深い入れ子になっている、またはまったくサイト設定されていないマネージド オブジェクトでは、グローバル サービスに直接アクセスするために <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> を呼び出すことができます。

<a name="how-to-use-getglobalservice"></a>

## <a name="use-getglobalservice"></a>GetGlobalService を使用する

サイト設定されていないか、必要なサービスを認識していないサービス プロバイダーでサイト設定されているツール ウィンドウまたはコントロール コンテナーからサービスを取得する必要がある場合があります。 たとえば、コントロール内からアクティビティ ログに書き込みたい場合があります。 これらのシナリオとその他のシナリオの詳細については、「[方法: サービスのトラブルシューティング](../../extensibility/how-to-troubleshoot-services.md)」を参照してください。

ほとんどの Visual Studio サービスは、静的 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> メソッドを呼び出すことによって取得できます。

<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> は、パッケージから派生した VSPackage が最初にサイト設定されるときに初期化される、キャッシュされたサービス プロバイダーに依存します。 この条件を満たしていることを保証するか、null サービス用に準備する必要があります。

幸い、<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> はほとんどの場合正常に動作します。

- VSPackage で、別の VSPackage だけを認識するサービスが提供される場合、サービスを要求する VSPackage は、サービスを提供する VSPackage が読み込まれる前にサイト設定されます。

- ツール ウィンドウが VSPackage によって作成された場合、ツール ウィンドウが作成される前に VSPackage がサイト設定されます。

- コントロール コンテナーが、VSPackage によって作成されたツール ウィンドウによってホストされている場合、VSPackage はコントロール コンテナーが作成される前にサイト設定されます。

### <a name="to-get-a-service-from-within-a-tool-window-or-control-container"></a>ツール ウィンドウまたはコントロール コンテナー内からサービスを取得するには

- コンストラクター、ツール ウィンドウ、またはコントロール コンテナーに次のコードを挿入します。

    ```csharp
    IVsActivityLog log = Package.GetGlobalService(typeof(SVsActivityLog)) as IVsActivityLog;
        if (log == null) return;
    ```

    ```vb
    Dim log As IVsActivityLog = TryCast(Package.GetGlobalService(GetType(SVsActivityLog)), IVsActivityLog)
    If log Is Nothing Then
        Return
    End If
    ```

    このコードでは、SVsActivityLog サービスを取得し、アクティビティ ログに書き込むために使用できる IVsActivityLog インターフェイスにキャストします。 例については、「[方法: アクティビティ ログを使用する](../../extensibility/how-to-use-the-activity-log.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [使用可能なサービスの一覧](../../extensibility/internals/list-of-available-services.md)
- [サービスの使用と提供](../../extensibility/using-and-providing-services.md)
- [キャストと型変換](/dotnet/csharp/programming-guide/types/casting-and-type-conversions)
- [キャスト](/cpp/cpp/casting)
