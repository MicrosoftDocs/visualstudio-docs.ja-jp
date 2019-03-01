﻿---
title: -LCID (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- language default
- locale IDs, setting for IDE
- Devenv, /LCID switch
- locale IDs
- /l Devenv switch
- LCID devenv switch
- /lcid Devenv switch
ms.assetid: 3a3f4e70-ea66-4351-9d62-acb1dec30e8e
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: def8ce2a40e068c602b0182b4580f5e3b524d222
ms.sourcegitcommit: a83c60bb00bf95e6bea037f0e1b9696c64deda3c
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2019
ms.locfileid: "54782224"
---
# <a name="lcid-devenvexe"></a>/LCID (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
統合開発環境 (IDE) 内の文字列、通貨、およびその他の値に使用する既定の言語を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
devenv {/LCID|/l} LocaleID  
```  
  
## <a name="arguments"></a>引数  
 `LocaleID`  
 必須です。 指定する言語の LCID (ロケール ID)。  
  
## <a name="remarks"></a>解説  
 IDE を読み込み、環境用の既定の自然言語を設定します。 この変更はセッション間で保持され、IDE の **[オプション]** ダイアログ ボックスにある **[環境]** オプションの **[国際対応の設定]** ウィンドウに反映されます。  
  
 指定した言語がユーザーのシステムで使用できない場合、/LCID スイッチは無視されます。  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] でサポートされる言語の LCID の一覧を次の表に示します。  
  
|言語|LCID|  
|--------------|----------|  
|中国語 (簡体字、中国)|2052|  
|では |1028|  
|英語|1033|  
|フランス語|1036|  
|ドイツ語|1031|  
|イタリア語|1040|  
|日本語|1041|  
|韓国語|1042|  
|スペイン語|3082|  
  
## <a name="example"></a>例  
 この例では、英語のリソース文字列を使用して IDE を読み込みます。  
  
```  
devenv /LCID 1033  
```  
  
## <a name="see-also"></a>関連項目  
 [Devenv コマンド ライン スイッチ](../../ide/reference/devenv-command-line-switches.md)   
 [[国際対応の設定] \([オプション] ダイアログ ボックス - [環境])](../../ide/reference/international-settings-environment-options-dialog-box.md)   
 [ウィンドウ レイアウトをカスタマイズする](../../ide/customizing-window-layouts-in-visual-studio.md)
