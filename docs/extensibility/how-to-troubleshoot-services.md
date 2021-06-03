---
title: '方法: サービスのトラブルシューティング | Microsoft Docs'
description: Visual Studio SDK でサービスを取得しようとしたときに発生する可能性のあるいくつかの一般的な問題をトラブルシューティングする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: troubleshooting
helpviewer_keywords:
- services, troubleshooting
ms.assetid: 001551da-4847-4f59-a0b2-fcd327d7f5ca
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a105f38166ecea958bb0e5bbfe790170b020e354
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079216"
---
# <a name="how-to-troubleshoot-services"></a>方法: サービスのトラブルシューティング
サービスを取得しようとしたときに、いくつかの一般的な問題が発生する可能性があります。

- サービスが [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] に登録されていない。

- サービスが、サービスの種類ではなく、インターフェイスの種類によって要求された。

- サービスを要求している VSPackage が配置されていない。

- 間違ったサービス プロバイダーが使用されている。

  要求されたサービスを取得できない場合、<xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> を呼び出すと null が返されます。 サービスを要求した後に、必ず null をテストする必要があります。

```csharp
IVsActivityLog log =
    GetService(typeof(SVsActivityLog)) as IVsActivityLog;
if (log == null) return;
```

## <a name="to-troubleshoot-a-service"></a>サービスをトラブルシューティングするには

1. システム レジストリを調べて、サービスが正しく登録されているかどうかを確認します。 詳細については、「[方法: サービスを提供する](../extensibility/how-to-provide-a-service.md)」を参照してください。

    次の *.reg* ファイルの断片は、SVsTextManager サービスを登録する方法を示しています。

   ```
   [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\<version number>\Services\{F5E7E71D-1401-11d1-883B-0000F87579D2}]
   @="{F5E7E720-1401-11d1-883B-0000F87579D2}"
   "Name"="SVsTextManager"
   ```

    上記の例で、バージョン番号は [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] のバージョン (12.0 や 14.0 など)、キー {F5E7E71D-1401-11d1-883B-0000F87579D2} は SVsTextManager サービスのサービス識別子 (SID)、既定値 {F5E7E720-1401-11d1-883B-0000F87579D2} はサービスを提供するテキスト マネージャー VSPackage のパッケージ GUID です。

2. GetService を呼び出すときは、インターフェイスの種類ではなくサービスの種類を使用します。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] からサービスを要求するときに、<xref:Microsoft.VisualStudio.Shell.Package> によって種類から GUID が推論されます。 次の状況の場合、サービスは見つかりません。

   1. サービスの種類ではなく、インターフェイスの種類が GetService に渡された。

   2. インターフェイスに明示的に割り当てられている GUID がない。 そのため、必要に応じて、システムによってオブジェクトの既定の GUID が作成される。

3. サービスを要求する VSPackage を確実に配置してください。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] によって、VSPackage の作成後にそれが配置され、その後、<xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> が呼び出されます。

    サービスを必要とする VSPackage コンストラクターにコードがある場合は、それを `Initialize` メソッドに移動します。

4. 正しいサービス プロバイダーを使用していることを確認してください。

    すべてのサービス プロバイダーが同じというわけではありません。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] によってツール ウィンドウに渡されるサービス プロバイダーは、VSPackage に渡されるものとは異なります。 ツール ウィンドウのサービス プロバイダーでは、<xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> が認識されていますが、<xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable> は認識されません。 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> を呼び出すことによって、ツール ウィンドウ内から VSPackage サービス プロバイダーを取得できます。

    ツール ウィンドウでユーザー コントロールまたはその他のコントロールのコンテナーをホストしている場合、このコンテナーは Windows コンポーネント モデルによって配置され、どの [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] サービスにもアクセスできません。 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> を呼び出すことによって、コントロールのコンテナー内から VSPackage サービス プロバイダーを取得できます。

## <a name="see-also"></a>関連項目
- [使用可能なサービスの一覧](../extensibility/internals/list-of-available-services.md)
- [サービスを使用および提供する](../extensibility/using-and-providing-services.md)
- [サービスの基本情報](../extensibility/internals/service-essentials.md)
- [Visual Studio トラブルシューティング](/troubleshoot/visualstudio/welcome-visual-studio/)