---
title: 分離シェル エントリ ポイントのパラメーター (C++) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Shell [Visual Studio], isolated mode%2C Start entry point
- Visual Studio shell, isolated mode%2C Start entry point
ms.assetid: 18f4b18b-2173-4afa-ba0a-42fe33e61118
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6089c4ef32ef0d0b0bce081cef6d16bd569c0901
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "60041952"
---
# <a name="isolated-shell-entry-point-parameters-c"></a>分離シェル エントリ ポイントのパラメーター (C++)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio シェルベースのアプリケーションの起動時には、Visual Studio シェルの開始のエントリ ポイントを呼び出します。 シェルの開始のエントリ ポイントへの呼び出しでは、次の設定をオーバーライドできます。 各設定の説明は、次を参照してください。[します。Pkgdef ファイル](../extensibility/modifying-the-isolated-shell-by-using-the-dot-pkgdef-file.md)します。  
  
- AddinsAllowed  
  
- AllowsDroppedFilesOnMainWindow  
  
- アプリ名  
  
- CommandLineLogo  
  
- DefaultHomePage  
  
- DefaultProjectsLocation  
  
- DefaultSearchPage  
  
- DefaultUserFilesFolderRoot  
  
- DisableOutputWindow  
  
- HideMiscellaneousFilesByDefault  
  
- HideSolutionConcept  
  
- NewProjDlgInstalledTemplatesHdr  
  
- NewProjDlgSlnTreeNodeTitle  
  
- SolutionFileCreatorIdentifier  
  
- SolutionFileExt  
  
- UserFilesSubFolderName  
  
- UserOptsFileExt  
  
  Visual Studio 分離シェルのテンプレートは、ソース ファイルを作成します*solutionName*.cpp、場所*solutionName*は、アプリケーションのソリューションの名前です。 このファイルは、アプリケーション、_tWinMain 関数のメイン エントリ ポイントを定義します。 この関数は、シェルの開始のエントリ ポイントを呼び出します。  
  
  アプリケーションの起動時に、これらの設定を変更することで、アプリケーションの動作を変更できます。  
  
## <a name="parameters"></a>パラメーター  
 Visual Studio シェルの開始のエントリ ポイントは、5 つのパラメーターを定義します。 最初の 4 つのパラメーターは変更しないでください。 5 番目のパラメーターは、設定の上書きの一覧を取得します。 シェルの開始のエントリ ポイントは、アプリケーションのメイン エントリ ポイントから呼び出されます。  
  
 シェルの開始のエントリ ポイントは、次のシグネチャを持ちます。  
  
```  
typedef int (__cdecl *STARTFCN)(LPSTR, LPWSTR, int, GUID *, WCHAR *pszSettings);  
```  
  
 アプリケーション設定を上書き、設定の値をそのままにしたくない場合は、null ポインターとしてパラメーターをオーバーライドします。  
  
 1 つまたは複数の設定を無効にするには、オーバーライドする設定を含む Unicode 文字列を渡します。 文字列は、名前/値ペアのセミコロンで区切られた一覧を示します。 各ペアは、後に等号 (=) の後に、設定を適用する値を無効にすると、設定の名前を表します。  
  
> [!NOTE]
>  Unicode 文字列に空白文字を含めないでください。  
  
 次の文字列が値 true を表すブール値の設定その他のすべての文字列は、値 false を表します。 これらの文字列が、区別されます。  
  
- \+  
  
- 1  
  
- -1  
  
- 日付  
  
- true  
  
- 可  
  
## <a name="example"></a>例  
 アドインを無効にして、アプリケーションの既定のプロジェクトの場所を変更、最後の"AddinsAllowed=false;DefaultProjectsLocation=%USERPROFILE%\temp"パラメーターを設定できます。  
  
## <a name="see-also"></a>関連項目  
 [分離シェルのカスタマイズ](../extensibility/customizing-the-isolated-shell.md)   
 [.pkgdef ファイル](../extensibility/modifying-the-isolated-shell-by-using-the-dot-pkgdef-file.md)
