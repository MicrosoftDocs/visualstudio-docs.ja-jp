---
title: コンテキスト パラメーター | Microsoft Docs
description: ウィザードを追加または実装するときに、プロジェクトの状態を定義する Visual Studio 統合開発環境 (IDE) のコンテキスト パラメーターについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- wizards, context parameters
- context parameters
ms.assetid: 1a062dcb-8a8f-40dd-bea9-3d10f9448966
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 14d60aa31fb586651ea6e2b00a8f8038bfaa42b9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057079"
---
# <a name="context-parameters"></a>コンテキスト パラメーター
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE) では、 **[新しいプロジェクト]** 、 **[新しい項目の追加]** 、または **[サブプロジェクトの追加]** ダイアログ ボックスにウィザードを追加できます。 追加したウィザードは、 **[ファイル]** メニューで、または **ソリューション エクスプローラー** でプロジェクトを右クリックして表示できます。 IDE により、ウィザードの実装にコンテキスト パラメーターが渡されます。 IDE によりウィザードが呼び出されと、コンテキスト パラメーターによってプロジェクトの状態が定義されます。

 IDE では、プロジェクトの <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.AddItem%2A> メソッドに対する IDE による呼び出しの <xref:Microsoft.VisualStudio.Shell.Interop.VSADDITEMOPERATION> フラグを設定することにより、ウィザードが起動します。 設定された場合、プロジェクトは登録されているウィザードの名前または GUID、および IDE によって渡されるその他のコンテキスト パラメーターを使用して、`IVsExtensibility::RunWizardFile` メソッドが実行されるようにする必要があります。

## <a name="context-parameters-for-new-project"></a>新しいプロジェクトのコンテキスト パラメーター

| パラメーター | 説明 |
|-------------------------| - |
| `WizardType` | 登録されたウィザードの種類 (<xref:EnvDTE.Constants.vsWizardNewProject>)、またはウィザードの種類を示す GUID。 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] の実装では、ウィザードの GUID は {0F90E1D0-4999-11D1-B6D1-00A0C90F2744} です。 |
| `ProjectName` | 一意の [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] プロジェクト名を表す文字列。 |
| `LocalDirectory` | 作業プロジェクト ファイルのローカルの場所。 |
| `InstallationDirectory` | [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のインストールのディレクトリ パス。 |
| `FExclusive` | プロジェクトが開いているソリューションを閉じる必要があることを示すブール型のフラグ。 |
| `SolutionName` | ディレクトリ部分や *.sln* 拡張子を除いたソリューション ファイル名。 *.suo* ファイル名も、`SolutionName` を使用して作成されます。 この引数が空の文字列でない場合、ウィザードでは <xref:EnvDTE._Solution.AddFromTemplate%2A> をプロジェクトに追加する前に <xref:EnvDTE._Solution.Create%2A> が使用されます。 この名前が空の文字列の場合は、<xref:EnvDTE._Solution.Create%2A> を呼び出さずに <xref:EnvDTE._Solution.AddFromTemplate%2A> を使用します。 |
| `Silent` | **[完了]** がクリックされたかのようにサイレント モードで実行するかどうかを示すブール値です (`TRUE`)。 |

## <a name="context-parameters-for-add-new-item"></a>新しい項目の追加のコンテキスト パラメーター

| パラメーター | 説明 |
|-------------------------| - |
| `WizardType` | 登録されたウィザードの種類 (<xref:EnvDTE.Constants.vsWizardAddItem>)、またはウィザードの種類を示す GUID。 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] の実装では、ウィザードの GUID は {0F90E1D1-4999-11D1-B6D1-00A0C90F2744} です。 |
| `ProjectName` | 一意の [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] プロジェクト名を表す文字列。 |
| `ProjectItems` | 作業中のプロジェクト ファイルが格納されているローカルの場所。 |
| `ItemName` | 追加する項目の名前。 この名前は、既定のファイル名または **[項目の追加]** ダイアログ ボックスでユーザーが入力するファイル名のいずれかになります。 この名前は、 *.vsdir* ファイルで設定されているフラグに基づいています。 名前には null 値を指定できます。 |
| `InstallationDirectory` | [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のインストールのディレクトリ パス。 |
| `Silent` | **[完了]** がクリックされたかのようにサイレント モードで実行するかどうかを示すブール値です (`TRUE`)。 |

## <a name="context-parameters-for-add-sub-project"></a>サブ プロジェクトの追加のコンテキスト パラメーター

| パラメーター | 説明 |
|-------------------------| - |
| `WizardType` | 登録されたウィザードの種類 (<xref:EnvDTE.Constants.vsWizardAddSubProject>)、またはウィザードの種類を示す GUID。 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] の実装では、ウィザードの GUID は {0F90E1D2-4999-11D1-B6D1-00A0C90F2744} です。 |
| `ProjectName` | 一意の [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] プロジェクト名を表す文字列。 |
| `ProjectItems` | ウィザードで操作する `ProjectItems` コレクションへのポインター。 このポインターは、プロジェクト階層の選択に基づいてウィザードに渡されます。 ユーザーは、通常、項目を配置するフォルダーを選択してから、プロジェクトの **[項目の追加]** ダイアログ ボックスを呼び出します。 |
| `LocalDirectory` | 作業プロジェクト ファイルのローカルの場所。 |
| `ItemName` | 追加する項目の名前。 この名前は、既定のファイル名または **[項目の追加]** ダイアログ ボックスでユーザーが入力するファイル名のいずれかになります。 この名前は、 *.vsdir* ファイルで設定されているフラグに基づいています。 名前には null 値を指定できます。 |
| `InstallationDirectory` | [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のインストールのディレクトリ パス。 |
| `Silent` | **[完了]** がクリックされたかのようにサイレント モードで実行するかどうかを示すブール値です (`TRUE`)。 |

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject2>
- [カスタム パラメーター](../../extensibility/internals/custom-parameters.md)
- [ウィザード](../../extensibility/internals/wizards.md)
- [ウィザード (.vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)
- [ウィザード起動用のコンテキスト パラメーター](/previous-versions/tz690efs(v=vs.140))