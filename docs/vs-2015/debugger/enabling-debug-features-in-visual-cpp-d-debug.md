---
title: Visual C でのデバッグ機能 (-/d_debug) |Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.debug
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- /D_DEBUG compiler option [C++]
- debugging [C++], enabling debug features
- debugging [MFC], enabling debug features
- assertions, enabling debug features
- D_DEBUG compiler option
- MFC libraries, debug version
- debug builds, MFC
- _DEBUG macro
ms.assetid: 276e2254-7274-435e-ba4d-67fcef4f33bc
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: bf560bcde09b9d2e3c2bee689c92c9900c6e2af5
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2018
ms.locfileid: "51760596"
---
# <a name="enabling-debug-features-in-visual-c-ddebug"></a>Visual C++ でのデバッグ機能の使用 (/D_DEBUG)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vcprvc](../includes/vcprvc-md.md)]、記号でプログラムをコンパイルするときに、アサーションが有効になっているなどのデバッグ機能 **_DEBUG**定義します。 定義できます **_DEBUG** 2 つの方法のいずれかで。  
  
- 指定 **#define _DEBUG**でソース コード、または  
  
- 指定、 **/D_DEBUG**コンパイラ オプション。 (ウィザードを使って Visual Studio でプロジェクトを作成する場合 **/D_DEBUG**デバッグ構成で自動的に定義されます)。  
  
  ときに **_DEBUG**が定義されている場合、コンパイラはコンパイルで囲まれたコードのセクション **#ifdef _DEBUG**と`#endif`します。  
  
  MFC プログラムのデバッグ構成は、MFC ライブラリのデバッグ バージョンとリンクする必要があります。 MFC ヘッダー ファイルを決定など、定義済みのシンボルに基づいて正しいバージョンとリンクする MFC ライブラリの **_DEBUG**と **_UNICODE**します。 詳細については、[MFC ライブラリのバージョン](http://msdn.microsoft.com/library/3d7a8ae1-e276-4cf8-ba63-360c2f85ad0e)を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [ネイティブ コードのデバッグ](../debugger/debugging-native-code.md)   
 [C++ デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-cpp-debug-configuration.md)



