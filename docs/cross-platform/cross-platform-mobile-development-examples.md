---
title: クロス プラットフォーム モバイル開発の例 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-mobile
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: bc384c12-fccc-45d7-9fb9-b90d536aa663
author: corob-msft
ms.author: corob
manager: jillfra
ms.workload:
- xplat-cplusplus
ms.openlocfilehash: b3980273e746b5f6dacd2d8d612a5e5e7dfe2a8e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62819420"
---
# <a name="cross-platform-mobile-development-examples"></a>クロス プラットフォーム モバイル開発の例
Visual C++ for Cross-Platform Mobile Development でインストールされるテンプレートの中には、学習に利用できる完全なサンプルを生成できるものがあります。 さらに、Windows デベロッパー センターにはダウンロードして Visual Studio で試用できる複数のサンプル アプリケーションがあります。

- [hello-jni Android アプリケーションのサンプル](https://code.msdn.microsoft.com/hello-jni-Android-790ab73d)

   このサンプルは Android NDK hello-jni アプリケーションの移植版です。 このサンプルではエンドツーエンドの Java ネイティブ インターフェイス「Hello World」アプリのデモを実行します。 共有ライブラリで実装されたネイティブ メソッドから文字列を読み込み、それをアプリで表示します。

- [hello-gl2 Android アプリケーションのサンプル](https://code.msdn.microsoft.com/hello-gl2-Android-3b61896c)

   このサンプルは、Android NDK hello-gl2 アプリケーションの移植版です。 このサンプルでは、エンド ツー エンドの Java ネイティブ インターフェイス Android OpenGL アプリのデモを実行します。 OpenGL ES 2.0 シェーダー API を使用して、三角形を表示します。

- [ビットマップ プラズマ Android アプリケーションのサンプル](https://code.msdn.microsoft.com/Bitmap-Plasma-Android-77ae296a)

   このサンプルは Android NDK ビットマップ プラズマ アプリケーションの移植版です。 このサンプルでは、エンド ツー エンドの Java ネイティブ インターフェイス Android OpenGL ES 2.0 アプリケーションのデモを実行します。 プラズマ効果を生成する Android ビットマップ ピクセル バッファーへの直接の操作のデモを実行します。

- [TwoLibs Android ライブラリのサンプル](https://code.msdn.microsoft.com/TwoLibs-Android-Library-6396e5c4)

   このサンプルは、Android NDK TwoLibs サンプルの移植版です。 動的に読み込まれる共有ライブラリと、Java ネイティブ インターフェイス アプリから呼び出されるメソッドを実装する、静的な C++ Android ネイティブ ライブラリの両方が使用されています。 このサンプルは、開発者が Visual Studio 2015 で静的/動的共有ライブラリを使用して、エンド ツー エンドの JNI Android アプリケーションを構築する方法を理解するのに適した開始点です。

- [Tea Pot Android アプリケーションのサンプル](https://code.msdn.microsoft.com/Tea-Pot-Android-Application-e7c05d73)

   このサンプルは、Android NDK TeaPot アプリケーションの移植版です。 このサンプルでは、エンド ツー エンドの Java ネイティブ インターフェイス Android OpenGL ES 2.0 アプリケーションのデモを実行します。

- [MoreTeaPots Android アプリケーションのサンプル](https://code.msdn.microsoft.com/MoreTeaPots-Android-a9bd8549)

   このサンプルは Android NDK MoreTeaPots アプリケーションの移植版です。 このサンプルでは、エンド ツー エンドの Java ネイティブ インターフェイス Android OpenGL アプリケーションのデモを実行します。

- [test-libstdcpp Android ライブラリのサンプル](https://code.msdn.microsoft.com/test-libstdcpp-Android-00b548f5)

   このサンプルは、Android NDK test-libstdc++ のサンプルの Visual Studio 2015 専用の移植版です。 このサンプルは、開発者が標準ライブラリの使用法を理解するのに適した開始点です。

  いずれかのサンプルを Visual Studio で開くには、zip ファイルをダウンロードし、ダウンロードしたファイルの **[プロパティ]** ページをエクスプローラーで開きます。 **[ブロックの解除]** ボタンを選び、次に **[OK]** を選びます。 zip ファイルの内容を任意の場所に解凍し、解凍したサンプルの C++ フォルダーを開いてからソリューション ファイルを開きます。

  サンプルをビルドするには、**F7** キーを押すか、または、メニュー バーの **[ビルド]**、**[ソリューションのビルド]** の順に選びます。