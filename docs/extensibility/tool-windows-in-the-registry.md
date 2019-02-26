---
title: Windows レジストリ内のツール |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- tool windows, registering
ms.assetid: c4bb8add-7148-49e4-a377-01d059fd5524
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: adb79fec233171a0d20e817f9675aaab8e7228f8
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2019
ms.locfileid: "56693166"
---
# <a name="tool-windows-in-the-registry"></a>ツールの Windows レジストリで
ツール ウィンドウを提供する Vspackage に登録する必要があります[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]同様のツール ウィンドウのプロバイダー。 Visual Studio パッケージ テンプレートを使用して作成されたツール ウィンドウは、既定でこれを実行します。 ツール ウィンドウのプロバイダーでは、既定のツール ウィンドウのサイズと場所、ツール ウィンドウのウィンドウとドッキング スタイルとして機能するウィンドウの GUID などの可視性属性を指定するシステムのレジストリ キーがあります。

 開発中は、管理されているツール ウィンドウのプロバイダーは、ソース コードに属性を追加し、生成されたアセンブリで RegPkg.exe ユーティリティを実行してツール ウィンドウを登録します。 詳細については、次を参照してください。[ツール ウィンドウの登録](../extensibility/registering-a-tool-window.md)します。

## <a name="registering-unmanaged-tool-window-providers"></a>管理されていないツール ウィンドウのプロバイダーを登録します。
 管理されていないツール ウィンドウのプロバイダーに登録する必要があります[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]システム レジストリの ToolWindows セクションでします。 次の .reg ファイル フラグメントは、動的なツール ウィンドウを登録する方法を示しています。

```
- [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\<version number>\ToolWindows\{f0e1e9a1-9860-484d-ad5d-367d79aabf55}]
@="{01069cdd-95ce-4620-ac21-ddff6c57f012}"
"Name"="Microsoft.Samples.VisualStudio.IDE.ToolWindow.DynamicWindowPane"
"Float"="250, 250, 410, 430"
"DontForceCreate"=dword:00000001

- [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\ToolWindows\{f0e1e9a1-9860-484d-ad5d-367d79aabf55}\Visibility]
"{f1536ef8-92ec-443c-9ed7-fdadf150da82}"=dword:00000000
```

 上記の例では、最初のキー、バージョン番号は、バージョンの[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]7.1 や 8.0、サブキー {f0e1e9a1-9860-484d-ad5d-367d79aabf55} は、ツール ウィンドウ ペイン (DynamicWindowPane) と既定値の {の GUID など、01069cdd-95ce-4620-ac21-ddff6c57f012} は、ツール ウィンドウを提供する VSPackage の GUID です。 Float 型および DontForceCreate サブキーの詳細については、次を参照してください。[ツール ウィンドウの表示構成](../extensibility/tool-window-display-configuration.md)します。

 2 番目の省略可能なキーである ToolWindows\Visibility には、表示するようにするツール ウィンドウを必要とするコマンドの Guid を指定します。 この場合、指定されたコマンドではありません。 詳細については、次を参照してください。[ツール ウィンドウの表示構成](../extensibility/tool-window-display-configuration.md)します。

## <a name="see-also"></a>関連項目
- [VSPackage](../extensibility/internals/vspackages.md)