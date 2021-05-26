---
title: ユーザー設定のサポート | Microsoft Docs
description: Visual Studio SDK の設定 API を使用して、設定カテゴリの永続化を有効にする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Custom Settings Points
- user settings [Visual Studio SDK], registering persistence support
- persistence, registering settings
ms.assetid: ad9beac3-4f8d-4093-ad0e-6fb00444a709
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e0128ce1f27674010d1b624457815ddb1016e016
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080646"
---
# <a name="support-for-user-settings"></a>ユーザー設定のサポート
VSPackage では、1 つまたは複数の設定カテゴリを定義できます。これは、ユーザーが **[ツール]** メニューの **[設定のインポート/エクスポート]** コマンドを選択したときに保持される状態変数のグループです。 この永続化を有効にするには、[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] の設定 API を使用します。

 カスタム設定ポイントと呼ばれるレジストリ エントリと GUID によって VSPackage の設定カテゴリが定義されます。 VSPackage では複数の設定カテゴリをサポートでき、各設定カテゴリはカスタム設定ポイントによって定義されます。

- (<xref:Microsoft.VisualStudio.Shell.Interop.IVsUserSettings> インターフェイスを使用して) 相互運用機能アセンブリに基づく設定を実装するには、レジストリを編集するか、レジストラー スクリプト (.rgs ファイル) を使用して、カスタム設定ポイントを作成する必要があります。 詳細については、「 [Creating Registrar Scripts](/cpp/atl/creating-registrar-scripts)」を参照してください。

- Managed Package Framework (MPF) を使用するコードでは、カスタム設定ポイントごとに <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> を VSPackage にアタッチすることによって、カスタム設定ポイントを作成する必要があります。

     1 つの VSPackage で複数のカスタム設定ポイントをサポートしている場合、カスタム設定ポイントはそれぞれ別のクラスによって実装され、<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> クラスの一意のインスタンスによって登録されます。 その結果、設定を実装するクラスでは、複数の設定カテゴリをサポートできます。

## <a name="custom-settings-point-registry-entry-details"></a>カスタム設定ポイントのレジストリ エントリの詳細
 カスタム設定ポイントは、次の場所にあるレジストリ エントリに作成されます: HKLM\Software\Microsoft\VisualStudio\\ *\<Version>* \UserSettings\\`<CSPName>`。ここで、`<CSPName>` は、VSPackage でサポートされているカスタム設定ポイントの名前です。 *\<Version>* は、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のバージョンです (たとえば、8.0)。

> [!NOTE]
> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\ *\<Version>* のルート パスは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]統合開発環境 (IDE) の初期化時に代替ルートでオーバーライドできます。 詳細については、[コマンド ライン スイッチ](../../extensibility/command-line-switches-visual-studio-sdk.md)に関するページを参照してください。

 レジストリ エントリの構造を次に示します。

 HKLM\Software\Microsoft\VisualStudio\\ *\<Version>* \UserSettings\

 `<CSPName`>= s '#12345'

 Package = '{XXXXXX XXXX XXXX XXXX XXXXXXXXX}'

 Category = '{YYYYYY YYYY YYYY YYYY YYYYYYYYY}'

 ResourcePackage = '{ZZZZZZ ZZZZ ZZZZ ZZZZ ZZZZZZZZZ}'

 AlternateParent = CategoryName

| 名前 | 種類 | データ | 説明 |
|-----------------|--------| - | - |
| (既定値)。 | REG_SZ | カスタム設定ポイントの名前 | キーの名前 (`<CSPName`>) は、カスタム設定ポイントのローカライズされていない名前です。<br /><br /> MPF に基づく実装では、<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> コンストラクターの `categoryName` 引数と `objectName` 引数を `categoryName_objectName` に組み合わせてキーの名前を取得します。<br /><br /> キーは空にすることも、サテライト DLL 内のローカライズされた文字列への参照 ID を含めることもできます。 この値は、<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> コンストラクターの `objectNameResourceID` 引数から取得されます。 |
| パッケージ | REG_SZ | GUID | カスタム設定ポイントを実装する VSPackage の GUID。<br /><br /> <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> クラスを使用する MPF に基づく実装では 、VSPackage の <xref:System.Type> およびリフレクションを含むコンストラクターの `objectType` 引数を使用して、この値を取得します。 |
| カテゴリ | REG_SZ | GUID | 設定カテゴリを識別する GUID。<br /><br /> 相互運用機能アセンブリに基づく実装では、この値を任意に選択した GUID にすることができます。この GUID は [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE によって <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserSettings.ExportSettings%2A> メソッドと <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserSettings.ImportSettings%2A> メソッドに渡されます。 これら 2 つのメソッドのすべての実装では、GUID 引数を検証する必要があります。<br /><br /> MPF に基づく実装では、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の設定メカニズムを実装するクラスの <xref:System.Type> によってこの GUID を取得します。 |
| ResourcePackage | REG_SZ | GUID | 省略可能。<br /><br /> 実装する VSPackage で指定されていない場合の、ローカライズされた文字列を含むサテライト DLL へのパス。<br /><br /> MPF では、リフレクションを使用して適切なリソース VSPackage を取得するため、<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> クラスはこの引数を設定しません。 |
| AlternateParent | REG_SZ | このカスタム設定ポイントを含むツール オプション ページの下にあるフォルダーの名前。 | 省略可能。<br /><br /> 設定の実装で、オートメーション モデルのメカニズムではなく、[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] の永続化メカニズムを使用して状態を保存する **ツール オプション** ページがサポートされている場合にのみ、この値を設定する必要があります。<br /><br /> このような場合、AlternateParent キーの値は、特定の **ToolsOptions** ページを識別するために使用される `topic.sub-topic` 文字列の `topic` セクションです。 たとえば、**ToolsOptions** ページ `"TextEditor.Basic"` の場合、AlternateParent の値は `"TextEditor"` になります。<br /><br /> <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> でカスタム設定ポイントが生成されるときは、カテゴリ名と同じになります。 |
