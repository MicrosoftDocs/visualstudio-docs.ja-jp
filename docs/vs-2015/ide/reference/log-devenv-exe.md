﻿---
title: -Log (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Devenv, /Log switch
- Log switch [devenv.exe]
- /Log Devenv switch
ms.assetid: ae23c4ae-2376-4fe3-b8d2-81d34e61c8ba
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 18b455d3da5693e5a82dbf45e52d04b18edaef5d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68199095"
---
# <a name="log-devenvexe"></a>/Log (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

すべてのアクティビティをトラブルシューティング用のログ ファイルに記録します。 このファイルは、`devenv /log` を少なくとも 1 回呼び出した後に表示されます。 ログ ファイルは既定で次のものになります。  
  
 *%APPDATA%* \Microsoft\VisualStudio\\<*バージョン*>\ActivityLog.xml  
  
 ここで、<*バージョン*> は Visual Studio のバージョンです。 ただし、別のパスとファイル名を指定することもできます。  
  
## <a name="syntax"></a>構文  
  
```  
Devenv /log Path\NameOfLogFile  
```  
  
## <a name="remarks"></a>解説  
 このスイッチは、その他すべてのスイッチの後、コマンド ラインの末尾に指定する必要があります。  
  
 ログは、/log スイッチで呼び出した Visual Studio のすべてのインスタンスを対象として記録されます。 スイッチなしで呼び出した Visual Studio のインスタンスについてはログ記録の対象外です。  
  
## <a name="see-also"></a>関連項目  
 [Devenv コマンド ライン スイッチ](../../ide/reference/devenv-command-line-switches.md)
