---
title: 登録と選択 (ソース管理 VSPackage) | Microsoft Docs
description: ソース管理 VSPackage を Visual Studio に登録する方法と、登録されている複数のソース管理パッケージからどのパッケージを読み込むかを選択する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- registration, source control packages
- source control packages, registration
ms.assetid: 7d21fe48-489a-4f55-acb5-73da64c4e155
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ff23784bb833c6a68e368f5db5d3b6f1a7433bb0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069414"
---
# <a name="registration-and-selection-source-control-vspackage"></a>登録と選択 (ソース管理 VSPackage)
ソース管理 VSPackage を [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] に公開するためには、登録が必要です。 複数のソース管理 VSPackage が登録されている場合、ユーザーは適切なタイミングで、どの VSPackage を読み込むかを選択できます。 VSPackage の詳細とその登録方法については、「[VSPackage](../../extensibility/internals/vspackages.md)」を参照してください。

## <a name="registering-a-source-control-package"></a>ソース管理パッケージの登録
 ソース管理パッケージが登録されることにより、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 環境では、パッケージを検索したり、パッケージでサポートされている機能を照会したりできます。 これは、パッケージのインスタンスは、その機能またはコマンドが必要な場合、または明示的に要求された場合にのみ作成されるという遅延読み込みスキームに従っています。

 VSPackages は、バージョン固有のレジストリ キー HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\*X.Y* に情報を配置します。*X* はメジャー バージョン番号、*Y* はマイナー バージョン番号です。 このしくみにより、複数のバージョンの [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のサイドバイサイド インストールをサポートすることが可能になります。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ユーザー インターフェイス (UI) では、インストールされている複数のソース管理プラグイン (ソース管理アダプター パッケージ経由) およびソース管理 VSPackage からの選択をサポートしています。 アクティブなソース管理プラグインまたは VSPackage は一度に 1 つしか存在できません。 ただし、以下で説明するように、IDE では、ソリューションベースの自動パッケージ交換メカニズムによって、ソース管理プラグインと VSPackage を切り替えることができます。 ソース管理 VSPackage の一部には、この選択メカニズムを有効にするために、いくつかの要件があります。

### <a name="registry-entries"></a>レジストリ エントリ
 ソース管理パッケージには、次の 3 つのプライベート GUID が必要です。

- パッケージ GUID: これは、ソース管理の実装を含むパッケージのメイン GUID です (このセクションでは ID_Package)。

- ソース管理 GUID: これは、Visual Studio ソース管理スタブへの登録に使用されるソース管理 VSPackage の GUID であり、コマンド UI コンテキストの GUID としても使用されます。 ソース管理サービス GUID は、ソース管理 GUID の配下に登録されます。 この例では、ソース管理 GUID は ID_SccProvider です。

- ソース管理サービス GUID: これは、Visual Studio によって使用されるプライベート サービスの GUID です (このセクションでは SID_SccPkgService)。 これに加えて、ソース管理パッケージでは、VSPackage、ツール ウィンドウなどの他の GUID を定義する必要があります。

  次のレジストリ エントリは、ソース管理 VSPackage によって作成される必要があります。

| キー名 | エントリ |
| - | - |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\` | (default) = rg_sz:{ID_SccProvider} |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\             {ID_SccProvider}\` | (default) = rg_sz:\<Friendly name of Package><br /><br /> Service = rg_sz:{SID_SccPkgService} |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SourceControlProviders\             {ID_SccProvider}\               Name\` | (default) = rg_sz:#\<Resource ID for localized name><br /><br /> Package = rg_sz:{ID_Package} |
| `HKEY_LOCAL_MACHINE\   SOFTWARE\     Microsoft\       VisualStudio\         X.Y\           SolutionPersistence\             <PackageName>\`<br /><br /> (キー名 `SourceCodeControl` は [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] によって既に使用されており、\<PackageName> の選択肢としては使用できないことに注意してください。) | (default) = rg_sz:{ID_Package} |

## <a name="selecting-a-source-control-package"></a>ソース管理パッケージの選択
 ソース管理プラグイン API ベースのプラグインとソース管理 VSPackage は、複数を同時に登録できます。 ソース管理プラグインまたは VSPackage を選択するプロセスでは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] が適切なタイミングでプラグインまたは VSPackage を読み込んで、不要なコンポーネントの読み込みを必要時まで先送りできるようにする必要があります。 さらに、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、メニュー項目、ダイアログ ボックス、ツール バーなど、他のアクティブでない VSPackage の UI をすべて削除して、アクティブな VSPackage の UI を表示する必要があります。

 次のいずれかの操作が実行されると、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] でソース管理 VSPackage が読み込まれます。

- ソリューションが開かれる (ソリューションがソース管理下にある場合)。

   ソース管理下にあるソリューションまたはプロジェクトが開かれると、IDE によって、そのソリューション用に指定されたソース管理 VSPackage が読み込まれます。

- ソース管理 VSPackage のメニュー コマンドのいずれかが実行される。

  ソース管理 VSPackage では、必要なコンポーネントを、実際に使用されるときに初めて読み込むのが理想的です (これは遅延読み込みとも呼ばれます)。

### <a name="automatic-solution-based-vspackage-swapping"></a>ソリューションベース VSPackage の自動交換
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の **[オプション]** ダイアログ ボックスの **[ソース管理]** カテゴリから、ソース管理 VSPackages を手動で入れ替えることができます。 ソリューションベース パッケージの自動交換とは、特定のソリューション用に指定されているソース管理パッケージが、そのソリューションが開かれると自動的にアクティブに設定されることを意味します。 すべてのソース管理パッケージは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetActive%2A> と <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProvider.SetInactive%2A> を実装する必要があります。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、(ソース管理プラグイン API を実装する) ソース管理プラグインと、ソース管理 VSPackage の両方間の切り替えを処理します。

 ソース管理アダプター パッケージは、任意のソース管理プラグイン API ベースのプラグインに切り替えるために使用されます。 中間のソース管理アダプター パッケージに切り替えたり、どのソース管理プラグインをアクティブまたは非アクティブに設定する必要があるかを決定したりするプロセスは、ユーザーには透過的です。 アダプター パッケージは、ソース管理プラグインが 1 つでもアクティブなときは常にアクティブです。 2 つのソース管理プラグインの切り替えは、単にプラグイン DLL を読み込んでアンロードする処理に相当します。 ただし、ソース管理 VSPackage に切り替えるには、IDE を操作して適切な VSPackage を読み込む必要があります。

 ソース管理 VSPackage は、何らかのソリューションが開かれ、VSPackage のレジストリ キーがソリューション ファイルにあるときに呼び出されます。 ソリューションが開かれると、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] によってレジストリ値が検出され、適切なソース管理 VSPackage が読み込まれます。 すべてのソース管理 VSPackage には、上記で説明したレジストリ エントリが必要です。 ソース管理下にあるソリューションは、特定のソース管理 VSPackage に関連付けられているものとしてマークされます。 ソース管理 VSPackage では、ソリューションベースの VSPackage 自動交換を有効にするために、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> を実装する必要があります。

### <a name="visual-studio-ui-for-package-selection-and-switching"></a>パッケージの選択と切り替えのための Visual Studio UI
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の **[オプション]** ダイアログ ボックスの **[ソース管理]** カテゴリには、ソース管理 VSPackage とプラグインの選択のための UI が用意されています。 これにより、ユーザーはアクティブなソース管理プラグインまたは VSPackage を選択できます。 ドロップダウン リストには、次のものが含まれます。

- すべてのインストールされているソース管理パッケージ

- すべてのインストールされているソース管理プラグイン

- ソース コード管理を無効にする "なし" オプション

  アクティブなソース管理の選択肢の UI のみが表示されます。 VSPackage を選択すると、前の VSPackage の UI が非表示になり、新しい UI が表示されます。 アクティブな VSPackage は、ユーザーごとに選択されます。 ユーザーが [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の複数のコピーを同時に開いている場合、異なるアクティブ VSPackage をそれぞれが使用する可能性があります。 複数のユーザーが同じコンピューターにログオンしている場合、各ユーザーが [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の別々のインスタンスを開き、それぞれのインスタンスで異なるアクティブ VSPackage を使用する可能性があります。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の複数のインスタンスがユーザーによって閉じられると、最後に開いていたソリューションでアクティブだったソース管理 VSPackage が既定のソース管理 VSPackage になり、再起動時にアクティブに設定されます。

  [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] の以前のバージョンとは異なり、IDE の再起動は、ソース管理 VSPackage を切り替えるための唯一の方法ではなくなりました。 VSPackage の選択は自動的です。 パッケージの切り替えには、(Administrator でも Power User でもなく) Windows ユーザーの権限が必要です。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>
- [機能](../../extensibility/internals/source-control-vspackage-features.md)
- [ソース管理プラグインの作成](../../extensibility/internals/creating-a-source-control-plug-in.md)
- [VSPackages](../../extensibility/internals/vspackages.md)
