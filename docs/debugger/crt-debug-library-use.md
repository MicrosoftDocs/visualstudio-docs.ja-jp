---
title: CRT デバッグ ライブラリの使用方法 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- c.debug.runtime
dev_langs:
- CSharp
- VB
- FSharp
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9434be46f357a97ad01f10ceec184ebe6c52eb43
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2019
ms.locfileid: "56624166"
---
# <a name="crt-debug-library-use"></a>CRT デバッグ ライブラリの使用方法
C ランタイム ライブラリには、広範なデバッグ支援機能が用意されています。 CRT デバッグ ライブラリのいずれかを使用するとリンクする必要があります[/debug](/cpp/build/reference/debug-generate-debug-info)を指定してコンパイル **/MDd**、 **/MTd**、または **/LDd**します。

## <a name="remarks"></a>解説
 CRT のデバッグに使用する主な定義とマクロは、CRTDBG.h ヘッダー ファイルに記述されています。

 CRT デバッグ ライブラリの関数は、デバッグ情報 ([/Z7、/Zd、/Zi、/ZI (デバッグ情報の形式)](/cpp/build/reference/z7-zi-zi-debug-information-format)) を含んだ状態で、最適化されずにコンパイルされています。 渡されるパラメーターを検証するためのアサート ステートメントを含む関数もあり、これらの関数のソース コードは公開されています。 このソース コードを利用すると、CRT 関数をステップ実行して、その関数が正常に動作しているかを確認したり、パラメーターやメモリ状態が不正でないかどうかを検証したりできます。 一部の CRT 技術については権利が保有されており、例外処理、浮動小数点数、その他いくつかのルーチンのソース コードは公開されていません。

 Visual C++ をインストールするときに、C ランタイム ライブラリのソース コードをハード ディスクにインストールするかどうかを選択できます。 ソース コードをインストールしない場合は、CRT 関数をステップ実行するときに CD-ROM が必要になります。

 使用できる各種ランタイム ライブラリの詳細については、[C ランタイム ライブラリ](/cpp/c-runtime-library/crt-library-features)に関するページを参照してください。

## <a name="see-also"></a>関連項目

- [CRT のデバッグ技術](../debugger/crt-debugging-techniques.md)
- [/MD、/MT、/LD (ランタイム ライブラリの使用)](/cpp/build/reference/md-mt-ld-use-run-time-library)
