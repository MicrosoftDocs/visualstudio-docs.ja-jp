---
title: '方法: サービスを取得する | Microsoft Docs'
description: さまざまな機能にアクセスするために Visual Studio サービスを取得する方法について説明します。 ほとんどのサービスは、VSPackage を使用して取得できます。
ms.custom: SEO-VS-2020
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- services, consuming
ms.assetid: 1f000020-8fb7-4e39-8e1e-2e38c7fec3d4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9096250f72e6bf64b2c6b76eeaa313ee7769dd51
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070090"
---
# <a name="how-to-get-a-service"></a>方法: サービスを取得する

さまざまな機能にアクセスするために Visual Studio サービスの取得がしばしば必要になります。 一般に、Visual Studio サービスには、使用できる 1 つ以上のインターフェイスが用意されています。 ほとんどのサービスは VSPackage から取得できます。

<xref:Microsoft.VisualStudio.Shell.Package> から派生し、正しくサイト設定されているすべての VSPackage では、任意のグローバル サービスを要求できます。 `Package` クラスでは <xref:System.IServiceProvider> を実装するため、`Package` から派生するすべての VSPackage もサービス プロバイダーになります。

Visual Studio で <xref:Microsoft.VisualStudio.Shell.Package> を読み込むと、初期化中に <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> オブジェクトを <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> メソッドに渡します。 これを、VSPackage の *サイト設定* と呼びます。 `Package` クラスでは、このサービス プロバイダーをラップし、サービスを取得するための <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> メソッドを提供します。

## <a name="getting-a-service-from-an-initialized-vspackage"></a>初期化された VSPackage からのサービスの取得

1. すべての Visual Studio 拡張機能は、拡張機能アセットを格納する VSIX デプロイ プロジェクトから始まります。 `GetServiceExtension` という名前の [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] VSIX プロジェクトを作成します。 VSIX プロジェクト テンプレートは、 **[新しいプロジェクト]** ダイアログで「vsix」と検索すると見つかります。

2. 次に、**GetServiceCommand** という名前のカスタム コマンド項目テンプレートを追加します。 **[新しい項目の追加]** ダイアログで、 **[Visual C#]**  >  **[機能拡張]** の順にアクセスし、 **[カスタム コマンド]** を選択します。 ウィンドウの下部にある **[名前]** フィールドで、コマンド ファイル名を *GetServiceCommand.cs* に変更します。 カスタム コマンドを作成する方法の詳細については、「[メニュー コマンドを使用した拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)」を参照してください

3. *GetServiceCommand.cs* で、`MenuItemCommand` メソッドの本体を削除して次のコードを追加します。

   ```csharp
   IVsActivityLog activityLog = ServiceProvider.GetService(typeof(SVsActivityLog)) as IVsActivityLog;
   if (activityLog == null) return;
   System.Windows.Forms.MessageBox.Show("Found the activity log service.");

   ```

    このコードでは、SVsActivityLog サービスを取得し、アクティビティ ログに書き込むために使用できる <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog> インターフェイスにキャストします。 例については、「[方法: アクティビティ ログを使用する](../extensibility/how-to-use-the-activity-log.md)」を参照してください。

4. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。

5. 実験用インスタンスの **[ツール]** メニューで、 **[GetServiceCommand の呼び出し]** ボタンを探します。 このボタンをクリックすると、 **[アクティビティ ログ サービスが見つかりました]** というメッセージ ボックスが表示されます。

## <a name="getting-a-service-from-a-tool-window-or-control-container"></a>ツール ウィンドウまたはコントロール コンテナーからサービスを取得する

サイト設定されていないか、必要なサービスを認識していないサービス プロバイダーでサイト設定されているツール ウィンドウまたはコントロール コンテナーからサービスを取得する必要がある場合があります。 たとえば、コントロール内からアクティビティ ログに書き込みたい場合があります。

静的 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> メソッドは、<xref:Microsoft.VisualStudio.Shell.Package> から派生した VSPackage が最初にサイト設定されるときに初期化される、キャッシュされたサービス プロバイダーに依存します。

VSPackage コンストラクターは VSPackage がサイト設定される前に呼び出されるため、通常、グローバル サービスは VSPackage コンストラクター内からは使用できません。 回避策については、「[方法: サービスのトラブルシューティング](../extensibility/how-to-troubleshoot-services.md)」を参照してください。

ツール ウィンドウまたはその他の非 VSPackage 要素でサービスを取得する方法の例を次に示します。

```csharp
IVsActivityLog log = Package.GetGlobalService(typeof(SVsActivityLog)) as IVsActivityLog;
if (log == null) return;
```

## <a name="getting-a-service-from-the-dte-object"></a>DTE オブジェクトからサービスを取得する

<xref:EnvDTE.DTEClass> オブジェクトからサービスを取得することもできます。 ただし、VSPackage から、または静的 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> メソッドを呼び出すことによって、DTE オブジェクトをサービスとして取得する必要があります。

DTE オブジェクトでは <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> を実装します。これを使用すると、<xref:Microsoft.VisualStudio.Shell.ServiceProvider.GetService%2A> を使用してサービスのクエリを実行できます。

DTE オブジェクトからサービスを取得する方法を次に示します。

```csharp
// Start with the DTE object, for example: 
// using EnvDTE;
// DTE dte = (DTE)GetService(typeof(DTE));

ServiceProvider sp = new ServiceProvider((Microsoft.VisualStudio.OLE.Interop.IServiceProvider)dte);
if (sp != null)
{
    IVsActivityLog log = sp.GetService(typeof(SVsActivityLog)) as IVsActivityLog;
    if (log != null)
    {
        System.Windows.Forms.MessageBox.Show("Found the activity log service.");
    }
}
```

## <a name="see-also"></a>関連項目

- [方法: サービスを提供する](../extensibility/how-to-provide-a-service.md)
- [サービスを使用および提供する](../extensibility/using-and-providing-services.md)
- [サービスの基本情報](../extensibility/internals/service-essentials.md)
