---
description: Dia2dump サンプルでは、Microsoft Debug Interface Access ソフトウェア開発キット (DIA SDK) を使用して、PDB ファイルの情報を照会する方法を示します。
title: Dia2dump サンプル | Microsoft Docs
ms.date: 07/24/2018
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- sample applications [DIA SDK]
- Dia2dump sample [DIA SDK]
ms.assetid: 492c0893-7043-452f-a020-890a47230d20
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a94a16d8e9fd60b042ea7113304b6d14c649b6fa
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "108634522"
---
# <a name="dia2dump-sample"></a>Dia2dump サンプル

Dia2dump サンプルでは、Microsoft Debug Interface Access ソフトウェア開発キット (DIA SDK) を使用して、PDB ファイルの情報を照会する方法を示します。

Dia2dump サンプルは Visual Studio と共にインストールされ、ソリューションとソース ファイルが含まれています。 コンパイルされた実行可能ファイルは、コマンド ラインから実行されます。 プログラム データベース (.pdb) ファイル全体の内容を表示することも、目的のセクションだけを表示することもできます。

## <a name="install-the-sample"></a>サンプルをインストールする

このサンプルは、Visual Studio インストーラーで **[C++ によるデスクトップ開発]** ワークロードを選択したときにインストールされます。 Visual Studio をインストールし、特定のワークロードと個々のコンポーネントを選択する方法については、「[Visual Studio のインストール](../../install/install-visual-studio.md)」を参照してください。

インストールされると、このサンプルは Visual Studio のインストール ディレクトリの \DIA SDK\Samples\DIA2Dump というサブディレクトリにあります。

## <a name="build-the-sample"></a>サンプルをビルドする

既定では、インストール ディレクトリは保護されたディレクトリです。 つまり、この場所でサンプル ソリューションをビルドおよび編集するには、管理者特権で開発者コマンド プロンプトまたは Visual Studio のインスタンスを使用する必要があります。 ビルドを簡略化するには、最初にサンプル ディレクトリのファイルを別のディレクトリ ([ドキュメント] フォルダー内のフォルダーなど) にコピーしてから、サンプルをビルドすることをお勧めします。

### <a name="to-build-the-dia2dump-sample-in-visual-studio"></a>Visual Studio で Dia2Dump サンプルをビルドするには

1. Visual Studio で DIA2Dump.sln ファイルを開きます。 ソリューションを別のディレクトリにコピーしていない場合は、管理者特権で Visual Studio を再起動するように求められることがあります。

1. **ソリューション エクスプローラー** で、ソリューションではなく Dia2Dump プロジェクトを選択します。

1. プロジェクトの **[プロパティ ページ]** ダイアログ ボックスを開きます。 詳細については、「[プロジェクトのプロパティの操作](/cpp/build/working-with-project-properties)」を参照してください。

1. **[構成プロパティ]**  >  **[C/C++]**  >  **[全般]** プロパティ ページを開きます。

1. **[追加のインクルード ディレクトリ]** プロパティのドロップダウン コントロールを選択し、 **[編集]** を選択します。

1. **[追加のインクルード ディレクトリ]** ダイアログの [編集] フィールドに、`$(VSInstallDir)DIA SDK\include` ディレクトリを入力します。 このディレクトリを追加すると、コンパイラで確実に dia2.h ファイルを見つけることができます。 **[OK]** を選択して変更を保存します。

1. **[OK]** を選択して、プロジェクト プロパティへの変更を保存します。

1. **[ビルド]** メニューの **[ソリューションのリビルド]** をクリックします。 既定では、Visual Studio ではサンプルのデバッグ バージョンがビルドされます。これは、ソリューション ディレクトリの Debug サブディレクトリにあります。

1. Visual Studio を閉じます。

### <a name="to-build-the-dia2dump-sample-at-the-command-line"></a>コマンド ラインで Dia2Dump サンプルをビルドするには

1. 開発者コマンド プロンプト ウィンドウで、サンプル ファイルをコピーしたディレクトリに移動します。 サンプルを別のディレクトリにコピーしていない場合は、管理者特権で (管理者として実行) 開発者コマンド プロンプト ウィンドウを使用する必要があります。

1. コマンド `nmake makefile` を入力して、dia2dump.exe の既定のデバッグ構成をビルドします。

## <a name="run-the-dia2dump-sample"></a>Dia2Dump サンプルを実行する

Dia2Dump.exe では、サービスを提供するために msdia *version*.dll COM サーバーを利用します。 Visual Studio 2015 以降では、バージョンは msdia140.dll です。 msdia *version*.dll COM サーバーが初期化されていない場合、dia2dump.exe を機能させるには、まずサーバーを登録する必要があります。 DIA SDK ディレクトリには、x86 バージョンの DLL を格納する bin サブディレクトリがあります。 x64 アーキテクチャ コンピューター用のバージョンは bin\amd64 にあり、ARM 用のバージョンは bin\arm にあります。 dll を登録するには、管理者特権で開発者コマンド プロンプト ウィンドウを開き、コンピューター アーキテクチャに対応するバージョンが格納されているディレクトリに移動します。 コマンド `regsvr32 msdia140.dll` を入力して COM サーバーを登録します。

### <a name="to-run-the-sample"></a>サンプルを実行するには

1. コマンド プロンプトを開き、ビルドした dia2dump.exe が格納されているディレクトリに移動します。

1. コマンド `dia2dump filename` を入力します。ここで、*filename* は確認する PDB ファイルの名前です。 PDB ファイルが別のディレクトリにある場合は、*filename* としてファイルへの完全パスを使用します。 このコマンドは、PDB ファイル内のすべてのデータを一覧表示します。

1. Dia2Dump には、選択した情報のみを表示する他のオプションがあります。 使用可能なすべてのオプションを一覧表示するには、`dia2dump -?` コマンドを使用します。

## <a name="see-also"></a>関連項目

- [Visual Studio プロジェクトのポート、移行、アップグレード](../../porting/port-migrate-and-upgrade-visual-studio-projects.md)
