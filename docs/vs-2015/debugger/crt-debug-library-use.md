---
title: CRT デバッグ ライブラリの使用方法 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- c.debug.runtime
dev_langs:
- FSharp
- VB
- CSharp
- C++
- C++
helpviewer_keywords:
- /DEBUG linker option [C++]
- crtdbg.h file
- debug library
- MDd compiler option [C++]
- libraries, CRT debug library
- MTd compiler option [C++]
- LDd compiler function [C++]
- /MTd compiler option [C++]
- /MDd compiler option [C++]
- debugging [CRT], CRT debug library
- DEBUG linker option [C++]
- /LDd compiler function [C++]
ms.assetid: 464de16b-4215-4787-9bfa-921aaff9d9f4
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 51534d226f3ae0f8726bb818423bf0a9b788fd8c
ms.sourcegitcommit: c496a77add807ba4a29ee6a424b44a5de89025ea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2019
ms.locfileid: "58963953"
---
# <a name="crt-debug-library-use"></a>CRT デバッグ ライブラリの使用方法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

C ランタイム ライブラリには、広範なデバッグ支援機能が用意されています。 CRT デバッグ ライブラリのいずれかを使用するとリンクする必要があります[/debug](http://msdn.microsoft.com/library/1af389ae-3f8b-4d76-a087-1cdf861e9103)を指定してコンパイル **/MDd**、 **/MTd**、または **/LDd**します。  
  
## <a name="remarks"></a>Remarks  
 CRT のデバッグに使用する主な定義とマクロは、CRTDBG.h ヘッダー ファイルに記述されています。  
  
 CRT デバッグ ライブラリの関数は、デバッグ情報 ([/Z7、/Zd、/Zi、/ZI (デバッグ情報の形式)](http://msdn.microsoft.com/library/ce9fa7e1-0c9b-47e3-98ea-26d1a16257c8)) を含んだ状態で、最適化されずにコンパイルされています。 渡されるパラメーターを検証するためのアサート ステートメントを含む関数もあり、これらの関数のソース コードは公開されています。 このソース コードを利用すると、CRT 関数をステップ実行して、その関数が正常に動作しているかを確認したり、パラメーターやメモリ状態が不正でないかどうかを検証したりできます。 一部の CRT 技術については権利が保有されており、例外処理、浮動小数点数、その他いくつかのルーチンのソース コードは公開されていません。  
  
 Visual C++ をインストールするときに、C ランタイム ライブラリのソース コードをハード ディスクにインストールするかどうかを選択できます。 ソース コードをインストールしない場合は、CRT 関数をステップ実行するときに CD-ROM が必要になります。  
  
 使用できる各種ランタイム ライブラリの詳細については、[C ランタイム ライブラリ](http://msdn.microsoft.com/library/a889fd39-807d-48f2-807f-81492612463f)に関するページを参照してください。  
  
## <a name="see-also"></a>関連項目  
 [CRT のデバッグ技術](../debugger/crt-debugging-techniques.md)   
 [/MD、/MT、/LD (ランタイム ライブラリの使用)](http://msdn.microsoft.com/library/cf7ed652-dc3a-49b3-aab9-ad60e5395579)
