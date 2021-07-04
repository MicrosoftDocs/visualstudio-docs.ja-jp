---
title: C++ のアクセス違反をデバッグする | Microsoft Docs
description: 複数のポインターが候補である場合にアクセス違反をトラブルシューティングするためのヒントについて説明します。 最近のバージョンの Visual Studio では、間違ったポインターに名前が指定されます。
ms.custom: SEO-VS-2020
ms.date: 02/05/2019
ms.topic: how-to
f1_keywords:
- vs.debug.access
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- access violation debugging
- debugging [Visual Studio], access violations
ms.assetid: 9311d754-0ce9-4145-b147-88b6ca77ba63
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- cplusplus
ms.openlocfilehash: 3689942c9db9fde3598590cf30100fc590c50753
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387035"
---
# <a name="how-can-i-debug-a-c-access-violation"></a>C++ のアクセス違反をデバッグする方法

## <a name="problem-description"></a>問題の説明

プログラムでアクセス違反が発生します。 どのようにデバッグしたらいいのでしょうか。

## <a name="solution"></a>ソリューション

複数のポインターを逆参照するコード行でアクセス違反が発生する場合、どのポインターがアクセス違反を引き起こしたかを見つけるのが困難な場合があります。 Visual Studio 2015 の Update 1 以降、例外ダイアログ ボックスにアクセス違反の原因となったポインターの名前が明示的に表示されるようになりました。

たとえば、次のコードではアクセス違反が発生します。

```C++
#include <iostream>
using namespace std;

class ClassC {
public:
  void printHello() {
    cout << "hello world";
  }
};

class ClassB {
public:
  ClassC* C;
  ClassB() {
    C = new ClassC();
  }
};

class ClassA {
public:
  ClassB* B;
  ClassA() {
    // Uncomment to fix
    // B = new ClassB();
  }
};

int main() {
  ClassA* A = new ClassA();
  A->B->C->printHello();

}
```

このコードを Visual Studio 2015 の Update 1 で実行する場合、次の例外ダイアログ ボックスが表示されます。

![Microsoft Visual Studio の例外ダイアログのスクリーンショット。"A->B が nullptr でした" の読み取りアクセス違反が示されています。 [中断] ボタンが選択されています。](../debugger/media/accessviolationcplus.png)

ポインターがアクセス違反を引き起こした理由を特定できない場合、コードをトレースして、問題の原因となったポインターが正しく割り当てられているかどうかを確認します。  パラメーターとして渡される場合は、正常に渡され、誤って[簡易コピー](https://stackoverflow.com/questions/184710/what-is-the-difference-between-a-deep-copy-and-a-shallow-copy)を作成していないことを確認します。 次に、問題のポインターに対してデータ ブレークポイントを作成し、プログラム内の別の場所で変更されていないことを確認することにより、値がプログラム内のどこかで意図せずに変更されていないことを検証します。 データ ブレークポイントの詳細については、 [Using Breakpoints](../debugger/using-breakpoints.md)のデータ ブレークポイントのセクションを参照してください。

## <a name="see-also"></a>関連項目
- [ネイティブ コードのデバッグに関する FAQ](../debugger/debugging-native-code-faqs.md)