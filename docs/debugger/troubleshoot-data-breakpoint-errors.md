---
title: データ ブレークポイントを設定できない | Microsoft Docs
description: '[値が変更されたときに中断] の使用時に発生する "データ ブレークポイントを設定できません" エラーの説明、解決策、および回避策を紹介します。'
ms.custom: SEO-VS-2020
ms.date: 5/19/2020
ms.topic: error-reference
f1_keywords:
- vs.debug.error.unable_to_set_data_breakpoint
dev_langs:
- CSharp
helpviewer_keywords:
- debugging [Visual Studio], managed
- debugging managed code, data breakpoint
ms.assetid: b06b5d65-424b-490f-bf58-97583cd7006a
author: wardengnaw
ms.author: waan
manager: caslan
ms.workload:
- multiple
ms.openlocfilehash: 73e7e02d90e2a89c81b5e690718c95fe7efe0fb3
ms.sourcegitcommit: 6e27b1238a8aa704b127eac34f4173e9d56690c5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2021
ms.locfileid: "110231966"
---
# <a name="troubleshooting-data-breakpoint-errors"></a>データ ブレークポイント エラーのトラブルシューティング
このページでは、[値が変更されたときに中断] の使用時に発生する一般的なエラーを解決する手順を説明します。

## <a name="diagnosing-unable-to-set-data-breakpoint-errors"></a>"データ ブレークポイントを設定できません" エラーを診断する
> [!IMPORTANT]
> マネージド データ ブレークポイントは .NET Core 3.0 以降と .NET 5.0.3 以降でサポートされています。 最新バージョンは[ここから](https://dotnet.microsoft.com/download)ダウンロードできます。

次に示すのは、マネージド データ ブレークポイントを使用するときに発生する可能性があるエラーの一覧です。 エラーが発生した理由と、エラーを解決する解決策または回避策について、追加の説明が含まれています。

- *"ターゲット プロセスで使用される .NET のバージョンが、データ ブレークポイントをサポートしていません。データ ブレークポイントには、x86 または x64 で実行される .NET Core 3.x または .NET 5.0.3 以降が必要です。"*

  - マネージド データ ブレークポイントがサポートされるのは .NET Core 3.0 以降です。 現在のところ、.NET Framework、3.0 より下のバージョンの .NET Core、5.0.3 より下のバージョンの .NET ではサポートされていません。 
    
  - **解決策**:これを解決するには、プロジェクトを .NET Core 3.0 にアップグレードします。

- "*この値がマネージ ヒープに見つからないため、追跡できません。* "
  - 変数がスタックで宣言されています。
    - スタックで作成された変数のデータ ブレークポイントの設定はサポートされません。関数が終了すると、変数が無効になるためです。
    - **対応策**: 変数が使用されている行にブレークポイントを設定します。

  - ドロップダウンから展開されない変数について "値が変更されたときに中断" します。
    - デバッガーは、追跡するフィールドを含むオブジェクトを内部的に認識している必要があります。ガベージ コレクターはオブジェクトをヒープ内で移動する場合があるため、デバッガーは、追跡する変数を保持しているオブジェクトを認識する必要があります。 
    - **対応策**: データ ブレークポイントを設定しようとするオブジェクト内のメソッドを表示している場合は、1 つ上のフレームに移動し、`locals/autos/watch` ウィンドウを使用して、オブジェクトを展開し、必要なフィールドにデータ ブレークポイントを設定します。

- "*静的フィールドまたは静的プロパティでは、データ ブレークポイントはサポートされていません。* "
    
  - 現時点では、静的フィールドと静的プロパティはサポートされていません。 この機能に関心がある場合は、[フィードバック](#provide-feedback)をお寄せください。

- "*構造体のフィールドおよびプロパティは追跡できません。* "

  - 現時点では、構造体のフィールドとプロパティはサポートされていません。 この機能に関心がある場合は、[フィードバック](#provide-feedback)をお寄せください。

- "*プロパティ値が変更されたため、追跡できません。* "

  - プロパティによって実行時の計算方法が変更されることがあります。その場合、プロパティが依存する変数の数が増えると、ハードウェア制限を超える可能性があります。 後述の `"The property is dependent on more memory than can be tracked by the hardware."` をご覧ください。

- "*このプロパティは、ハードウェアで追跡できないメモリに依存しています。* "
    
  - 各アーキテクチャには、サポートできるバイト数とハードウェア データ ブレークポイント数のセットがあります。データ ブレークポイントを設定しようとするプロパティが、この制限を超えました。 「[データ ブレークポイントのハードウェア制限](#data-breakpoint-hardware-limitations)」の表を参照して、使用しているアーキテクチャについて、ハードウェアでサポートされるブレークポイント数とバイト数を確認してください。 
  - **対応策**: プロパティ内で変化する可能性のある値にデータ ブレークポイントを設定します。

- "*レガシ C# 式エバリュエーターを使用している場合、データ ブレークポイントはサポートされていません。* "

  - データ ブレークポイントは、レガシ以外の C# 式エバリュエーターでしかサポートされません。 
  - **解決策**:レガシ C# 式エバリュエーターを無効にするには、[`Debug -> Options`] に移動し、[`Debugging -> General`] の下の [`"Use the legacy C# and VB expression evaluators"`] をオフにします。

- *"クラス **X** には、それに特有のデータに対するデータ ブレークポイントの使用を妨げるカスタム デバッガー ビューがあります。"*
  
  - データ ブレークポイントは、ターゲット プロセス (デバッグされているアプリケーション) で作成されたメモリでのみサポートされます。 データ ブレークポイントが設定されているメモリには、[DebuggerTypeProxy 属性](using-debuggertypeproxy-attribute.md)か、ターゲット プロセスに含まれない他の何かで作成されたオブジェクトによって所有されている可能性があるというフラグが設定されています。
  - **回避策**: オブジェクトの DebuggerTypeProxy ビューを展開する代わりにオブジェクトの "未加工ビュー" を展開し、データ ブレークポイントを設定します。 この操作により、DebuggerTypeProxy 属性によって作成されたオブジェクトに所有されているメモリ上にデータ ブレークポイントがないことが保証されます。

## <a name="data-breakpoint-hardware-limitations"></a>データ ブレークポイントのハードウェア制限

プログラムが実行するアーキテクチャ (プラットフォーム構成) では、使用できるハードウェア データ ブレークポイントの数が制限されています。 次の表は、アーキテクチャごとに使用できるレジスタの数を示しています。

| アーキテクチャ | ハードウェアでサポートされているデータ ブレークポイントの数 | 最大バイト サイズ|
| :-------------: |:-------------:| :-------------:|
| x86 | 4 | 4 |
| X64 | 4 | 8 |
| ARM | 1 | 4 |
| ARM64 | 2 | 8 |

## <a name="provide-feedback"></a>フィードバックの提供

この機能に関する問題や提案は、IDE の [ヘルプ] > [フィードバックの送信] > [[問題の報告]](../ide/how-to-report-a-problem-with-visual-studio.md)、または[開発者コミュニティ](https://aka.ms/feedback/suggest?space=8)でお知らせください。

## <a name="see-also"></a>関連項目

- [.NET Core 3.0 での [値が変更されたときに中断] の使用](using-breakpoints.md#BKMK_set_a_data_breakpoint_native_cplusplus)
- [DevBlog:値が変更されたときに中断:Visual Studio 2019 での .NET Core のデータ ブレークポイント](https://devblogs.microsoft.com/visualstudio/break-when-value-changes-data-breakpoints-for-net-core-in-visual-studio-2019/)
