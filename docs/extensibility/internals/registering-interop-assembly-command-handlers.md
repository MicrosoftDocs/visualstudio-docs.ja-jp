---
title: 相互運用機能アセンブリ コマンド ハンドラーの登録 | Microsoft Docs
description: 相互運用機能アセンブリを使用してコマンドを実装するすべての VSpackage で使用される基本的なコマンド コントラクトについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- interop assemblies, command handlers
- command handling with interop assemblies, registering
ms.assetid: 303cd399-e29d-4ea1-8abe-5e0b59c12a0c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 641a21658e490f94a27cbd9120d044539a7ec284
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062760"
---
# <a name="registering-interop-assembly-command-handlers"></a>相互運用機能アセンブリ コマンド ハンドラーの登録
統合開発環境 (IDE) によってコマンドが適切にルーティングされるように、VSPackage を [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に登録する必要があります。

 レジストリを更新するには、手動で編集するか、レジストラー (.rgs) ファイルを使用します。 詳細については、「 [Creating Registrar Scripts](/cpp/atl/creating-registrar-scripts)」を参照してください。

 Managed Package Framework (MPF) では、<xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute> クラスを通じてこの機能を提供します。

- [[コマンド テーブル形式のリファレンス]](/previous-versions/bb164647(v=vs.100)) リソースは、アンマネージド サテライト UI dll にあります。

## <a name="command-handler-registration-of-a-vspackage"></a>VSPackage のコマンド ハンドラーの登録
 ユーザー インターフェイス (UI) ベースのコマンドのハンドラーとして機能する VSPackage には、VSPackage `GUID` に基づいた名前が付けられたレジストリ エントリが必要です。 このレジストリ エントリは、VSPackage の UI リソース ファイルとそのファイル内のメニュー リソースの場所を指定します。 レジストリ エントリ自体は HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\\ *\<Version>* \Menus の下にあります。ここで、 *\<Version>* は 9.0 などの [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のバージョンです。

> [!NOTE]
> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\ *\<Version>* のルート パスは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] シェルが初期化されるときは代替ルートを使用してオーバーライドできます。 ルート パスの詳細については、「[Windows インストーラーによる VSPackage のインストール](../../extensibility/internals/installing-vspackages-with-windows-installer.md)」を参照してください。

### <a name="the-ctmenu-resource-registry-entry"></a>CTMENU リソース レジストリ エントリ
 このレジストリ エントリの構造は次のとおりです。

```
HKEY_LOCAL_MACHINE\Software\VisualStudio\<Version>\
  Menus\
    <GUID> = <Resource Information>
```

 \<*GUID*> は、{XXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX} の形式の VSPackage の `GUID` です。

 *\<Resource Information>* は、コンマで区切られた 3 つの要素で構成されます。 これらの要素の順序は次のとおりです。

 \<*Path to Resource DLL*>, \<*Menu Resource ID*>, \<*Menu Version*>

 次の表に \<*Resource Information*> のフィールドを示します。

| 要素 | 説明 |
|---------------------------| - |
| \<*Path to Resource DLL*> | これは、メニュー リソースを含むリソース DLL への完全パスです。または、これは空白のままになっており、この場合は、VSPackage のリソース DLL が使用されることを示します (VSPackage 自体が登録されている Packages サブキーで指定されています)。<br /><br /> このフィールドを空白にしておくことが慣例です。 |
| \<*Menu Resource ID*> | これは、[.vsct](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md) ファイルからコンパイルされたときに、VSPackage の UI 要素すべてを含む `CTMENU` リソースのリソース ID です。 |
| \<*Menu Version*> | これは、`CTMENU` リソースのバージョンとして使用される数字です。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、この値を使用して、`CTMENU` リソースの内容をすべての `CTMENU` リソースのキャッシュと再マージする必要があるかどうかを判断します。 再マージをトリガーするには、devenv のセットアップ コマンドを実行します。<br /><br /> この値は、最初に 1 に設定し、`CTMENU` リソースのあらゆる変更の後と、再マージの発生前にインクリメントする必要があります。 |

### <a name="example"></a>例
 いくつかのリソース エントリの例を次に示します。

```
HKEY_LOCAL_MACHINE\Software\VisualStudio\9.0Exp\
  Menus\
    {019971D6-4685-11D2-B48A-0000F87572EB} = ,1, 10
    {1b027a40-8f43-11d0-8d11-00a0c91bc942} = , 10211, 3
```

## <a name="see-also"></a>関連項目
- [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [相互運用機能アセンブリを使用するコマンドとメニュー](../../extensibility/internals/commands-and-menus-that-use-interop-assemblies.md)