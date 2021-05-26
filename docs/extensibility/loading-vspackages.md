---
title: VSPackage の読み込み | Microsoft Docs
description: パフォーマンスを向上させるために可能な限り使用される遅延読み込みなど、Visual Studio での VSPackage の読み込みについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, autoloading
- VSPackages, loading
ms.assetid: f4c3dcea-5051-4065-898f-601269649d92
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 39a58bcbad79191f54a7b4eeb2aa12e90d8a6e44
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073288"
---
# <a name="load-vspackages"></a>VSPackage を読み込む
VSPackage は、機能が必要な場合にのみ Visual Studio に読み込まれます。 たとえば、VSPackage は、VSPackage で実装されるプロジェクト ファクトリまたはサービスが Visual Studio で使用されるときに読み込まれます。 この機能は遅延読み込みと呼ばれ、パフォーマンス向上のために可能な場合は常に使用されます。

> [!NOTE]
> Visual Studio では、VSPackage で提供されるコマンドなどの特定の VSPackage 情報を、VSPackage を読み込まずに確認できます。

 VSPackage は、ソリューションを開いたときなど、特定のユーザー インターフェイス (UI) コンテキストで自動読み込みするように設定できます。 このコンテキストは <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> 属性で設定されます。

### <a name="autoload-a-vspackage-in-a-specific-context"></a>特定のコンテキストで VSPackage を自動読み込みする

- VSPackage 属性に `ProvideAutoLoad` 属性を追加します。

    ```csharp
    [DefaultRegistryRoot(@"Software\Microsoft\VisualStudio\14.0")]
    [PackageRegistration(UseManagedResourcesOnly = true)]
    [ProvideAutoLoad(UIContextGuids80.SolutionExists)]
    [Guid("00000000-0000-0000-0000-000000000000")] // your specific package GUID
    public class MyAutoloadedPackage : Package
    {. . .}
    ```

     UI コンテキストとその GUID 値の一覧については、<xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80> の列挙型フィールドを参照してください。

- <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> メソッドにブレークポイントを設定します。

- VSPackage をビルドし、デバッグを開始します。

- ソリューションを読み込むか、作成します。

     VSPackage が読み込まれ、ブレークポイントで停止します。

## <a name="force-a-vspackage-to-load"></a>VSPackage を強制的に読み込む
 状況によっては、VSPackage で別の VSPackage を強制的に読み込むことが必要な場合もあります。 たとえば、CMDUIContext として使用できないコンテキストで、軽量な VSPackage がより大きな VSPackage を読み込む場合があります。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsShell.LoadPackage%2A> メソッドを使用して、VSPackage を強制的に読み込むことができます。

- 別の VSPackage を強制的に読み込む VSPackage の <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> メソッドに、次のコードを挿入します。

    ```csharp
    IVsShell shell = GetService(typeof(SVsShell)) as IVsShell;
    if (shell == null) return;

    IVsPackage package = null;
    Guid PackageToBeLoadedGuid =
        new Guid(Microsoft.PackageToBeLoaded.GuidList.guidPackageToBeLoadedPkgString);
    shell.LoadPackage(ref PackageToBeLoadedGuid, out package);

    ```

     VSPackage が初期化されるとき、`PackageToBeLoaded` を強制的に読み込みます。

     VSPackage 通信には強制読み込みを使用しないでください。 代わりに、[サービスの使用および提供](../extensibility/using-and-providing-services.md)を使用してください。

## <a name="see-also"></a>関連項目
- [VSPackages](../extensibility/internals/vspackages.md)
