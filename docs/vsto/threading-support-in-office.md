---
title: Office でのスレッドのサポート
description: Microsoft Office オブジェクト モデルでは、スレッド処理がサポートされています。 Office オブジェクト モデルはスレッド セーフではありませんが、Office ソリューションで複数のスレッドを操作できます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- multiple threads [Office development in Visual Studio]
- threading [Office development in Visual Studio]
- Office applications [Office development in Visual Studio], threading support
- object models [Office development in Visual Studio], threading support
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: dce8bb0667cecbe073c734595d341f9c7b7ccac9
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826084"
---
# <a name="threading-support-in-office"></a>Office でのスレッドのサポート
  この記事では、Microsoft Office オブジェクト モデルでのスレッド処理のサポートについて説明します。 Office オブジェクト モデルはスレッド セーフではありませんが、Office ソリューションで複数のスレッドを操作できます。 Office アプリケーションは、コンポーネント オブジェクト モデル (COM) サーバーです。 COM では、クライアントが任意のスレッドで COM サーバーを呼び出すことができます。 スレッド セーフでない COM サーバーに対しては、COM には、同時呼び出しをシリアル化して、サーバー上で一度に 1 つの論理スレッドだけが実行されるようにするメカニズムが用意されています。 このメカニズムは、シングル スレッド アパートメント (STA) モデルと呼ばれています。 呼び出しがシリアル化されるため、サーバーがビジー状態であるかバックグラウンド スレッドで他の呼び出しを処理しているときに、呼び出し元が一定期間ブロックされることがあります。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="knowledge-required-when-using-multiple-threads"></a>複数のスレッドを使用する場合に必要な知識
 複数のスレッドを操作するには、マルチスレッドの次の側面について、少なくとも基本的な知識を持っている必要があります。

- Windows API

- COM マルチスレッドの概念

- コンカレンシー

- Synchronization

- マーシャリング

  マルチスレッドの一般的な情報については、「[マネージド スレッド処理](/dotnet/standard/threading/)」を参照してください。

  Office はメインの STA で実行されます。 これによる影響を理解することで、Office で複数のスレッドを使用する方法を理解できます。

## <a name="basic-multithreading-scenario"></a>基本的なマルチスレッドのシナリオ
 Office ソリューションのコードは、常にメイン UI スレッド上で実行されます。 別のタスクをバックグラウンド スレッドで実行することで、アプリケーションのパフォーマンスを向上させたいとします。 目標は、2 つのタスクが 1 つずつ順にではなく同時に完了するように見え、その結果、実行がよりスムーズになることです (複数のスレッドを使用する主な理由)。 たとえば、メインの Excel UI スレッドにイベント コードがあるとします。バックグラウンド スレッドでは別のタスクを実行して、サーバーからデータを収集し、そのデータで Excel UI のセルを更新することができます。

## <a name="background-threads-that-call-into-the-office-object-model"></a>Office オブジェクト モデルを呼び出すバックグラウンド スレッド
 バックグラウンド スレッドが Office アプリケーションの呼び出しを行うと、その呼び出しは STA の境界を越えて自動的にマーシャリングされます。 ただし、バックグラウンド スレッドによって呼び出しが行われたときに、それを Office アプリケーションで処理できる保証はありません。 いくつかのケースが考えられます。

1. 呼び出しが実行に入る機会を得られるように、Office アプリケーションでメッセージをポンプする必要があります。 大量の処理を中断なく実行している場合は、これには時間がかかることがあります。

2. 別の論理スレッドがアパートメント内に既に存在する場合、新しいスレッドは実行に入ることができません。 これは多くの場合、論理スレッドが Office アプリケーションに入ってから、呼び出し元のアパートメントに対する再入可能なコールバックを行うときに発生します。 アプリケーションは、その呼び出しが戻るのを待機してブロックされます。

3. Excel が、受け取った呼び出しをすぐに処理できない状態になっている可能性があります。 たとえば、Office アプリケーションがモーダル ダイアログ ボックスを表示している可能性があります。

   ケース 2 および 3 に対しては、COM には [IMessageFilter](/windows/desktop/api/objidl/nn-objidl-imessagefilter) インターフェイスが用意されています。 サーバーがそれを実装している場合は、すべての呼び出しが [HandleIncomingCall](/windows/desktop/api/objidl/nf-objidl-imessagefilter-handleincomingcall) メソッドを介して実行に入ります。 ケース 2 の場合、呼び出しは自動的に拒否されます。 ケース 3 の場合、サーバーは状況に応じて呼び出しを拒否できます。 呼び出しが拒否された場合は、呼び出し元で対処方法を決定する必要があります。 通常、呼び出し元は [IMessageFilter](/windows/desktop/api/objidl/nn-objidl-imessagefilter) を実装しています。その場合、[RetryRejectedCall](/windows/desktop/api/objidl/nf-objidl-imessagefilter-retryrejectedcall) メソッドによって拒否が通知されます。

   ただし、Visual Studio の Office 開発ツールを使用して作成されたソリューションの場合は、COM 相互運用機能によって、拒否されたすべての呼び出しが <xref:System.Runtime.InteropServices.COMException> に変換されます ("メッセージ フィルターはアプリケーションがビジーであることを示しています")。 バックグラウンド スレッドでオブジェクト モデルを呼び出す場合は常に、この例外を処理できるように準備する必要があります。 通常は、一定の時間だけ再試行してから、ダイアログを表示します。 ただし、バックグラウンド スレッドを STA として作成した後、そのスレッドでこのケースを処理するためのメッセージ フィルターを登録することもできます。

## <a name="start-the-thread-correctly"></a>スレッドを正しく開始する
 新しい STA スレッドを作成するときは、スレッドを開始する前にアパートメントの状態を STA に設定します。 これを実行する方法を次のコード例に示します。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreCreatingExcelCS/ThisWorkbook.cs" id="Snippet5":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreCreatingExcelVB/ThisWorkbook.vb" id="Snippet5":::

 詳細については、「[マネージド スレッド処理のベスト プラクティス](/dotnet/standard/threading/managed-threading-best-practices)」を参照してください。

## <a name="modeless-forms"></a>モードレス フォーム
 モードレス フォームを使用すると、フォームの表示中にアプリケーションとの間で一種の対話を行うことができます。 ユーザーはフォームと対話し、フォームは閉じることなくアプリケーションと対話します。 Office オブジェクト モデルでは、マネージド モードレス フォームがサポートされています。ただし、バックグラウンド スレッドでは使用しないでください。

## <a name="see-also"></a>関連項目
- [スレッド処理 (C#)](/dotnet/csharp/programming-guide/concepts/threading/index)
- [スレッド処理 (Visual Basic)](/dotnet/visual-basic/programming-guide/concepts/threading/index)
- [スレッドの使用とスレッド処理](/dotnet/standard/threading/using-threads-and-threading)
- [Office ソリューションを設計して作成する](../vsto/designing-and-creating-office-solutions.md)
