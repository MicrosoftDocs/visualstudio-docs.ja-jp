---
title: キャッシュ データ
description: ドキュメント レベルのカスタマイズでデータ オブジェクトをキャッシュして、データにオフラインで、または Microsoft Office Word や Excel を開かずに、アクセスできるようにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data caching [Office development in Visual Studio], about caching data
- data [Office development in Visual Studio], caching
- data caching [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f31556e64ee93a73fb09c27edd095bcd2653dfdc
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99836164"
---
# <a name="cache-data"></a>キャッシュ データ
  ドキュメント レベルのカスタマイズでデータ オブジェクトをキャッシュすることで、データにオフラインで、または Microsoft Office Word や Microsoft Office Excel を開かずに、アクセスすることができます。 オブジェクトをキャッシュするには、オブジェクトのデータ型が特定の要件を満たしている必要があります。 <xref:System.String>、<xref:System.Data.DataSet>、<xref:System.Data.DataTable> など、.NET Framework の多くの一般的なデータ型はその要件を満たします。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 データ キャッシュにオブジェクトを追加するには、2 つの方法があります。

- ソリューションのビルド時にオブジェクトをデータ キャッシュに追加するには、<xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 属性をオブジェクト宣言に適用します。 詳細については、「[方法: オフラインで使用するデータまたはサーバー上で使用するデータをキャッシュする](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)」を参照してください。

- 実行時にプログラムでオブジェクトをデータ キャッシュに追加するには、`ThisDocument` や `ThisWorkbook` クラスなどのホスト項目の `StartCaching` メソッドを使います。 詳細については、「[方法: Office ドキュメント内のデータ ソースをプログラムでキャッシュする](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)」を参照してください。

  オブジェクトをデータ キャッシュに追加した後は、Word または Excel を起動しなくても、キャッシュされているデータにアクセスして変更することができます。 詳細については、「[サーバー上のドキュメントのデータにアクセスする](../vsto/accessing-data-in-documents-on-the-server.md)」を参照してください。

## <a name="requirements-for-data-objects-to-be-cached"></a>データ オブジェクトをキャッシュするための要件
 ソリューションでデータ オブジェクトをキャッシュするには、オブジェクトが次の要件を満たしている必要があります。

- `ThisDocument` や `ThisWorkbook` クラスなどのホスト項目の読み取り/書き込みパブリック フィールドまたはプロパティであること。

- インデクサーまたはその他のパラメーター化されたプロパティではないこと。

  さらに、データ オブジェクトは <xref:System.Xml.Serialization.XmlSerializer> クラスによってシリアル化可能である必要があります。つまり、オブジェクトの型には次の特性が必要です。

- パブリック型であること。

- パラメーターなしのパブリック コンストラクターがあること。

- 追加のセキュリティ特権を必要とするコードを実行しないこと。

- 読み取り/書き込みのパブリック プロパティのみを公開していること (他のプロパティは無視されます)。

- 多次元配列を公開していないこと (入れ子になった配列は受け入れられます)。

- プロパティやフィールドからインターフェイスを返さないこと。

- コレクションの場合、<xref:System.Collections.IDictionary> を実装していないこと。

  データ オブジェクトをキャッシュすると、[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]によって、ドキュメント内の "*カスタム XML パーツ*" に格納される XML 文字列に、オブジェクトがシリアル化されます。 詳細については、「[カスタム XML パーツの概要](../vsto/custom-xml-parts-overview.md)」を参照してください。

## <a name="cached-data-size-limits"></a>キャッシュされるデータのサイズの制限
 ドキュメント内のデータ キャッシュに追加できるデータの総量と、データ キャッシュ内の個々のオブジェクトのサイズには、いくつかの制限があります。 これらの制限を超えると、データがデータ キャッシュに保存されるときに、アプリケーションが予期せず終了する可能性があります。

 これらの制限を回避するには、次のガイドラインに従ってください。

- 10 MB を超えるオブジェクトを、データ キャッシュに追加しないでください。

- 1 つのドキュメントのデータ キャッシュに、合計で 100 MB を超えるデータを追加しないでください。

  これらはおおよその値です。 正確な制限は、使用可能な RAM や実行中のプロセスの数など、いくつかの要因によって異なります。

## <a name="control-the-behavior-of-cached-objects"></a>キャッシュされたオブジェクトの動作を制御する
 キャッシュされたオブジェクトの動作をより詳細に制御するには、キャッシュされるオブジェクトの型に <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.ICachedType> インターフェイスを実装できます。 たとえば、オブジェクトが変更されたときにユーザーに通知する方法を制御する場合は、このインターフェイスを実装できます。 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.ICachedType> の実装方法を示すコードの例については、「[Office 開発のサンプルとチュートリアル](../vsto/office-development-samples-and-walkthroughs.md)」の Excel ダイナミック コントロール サンプルと Word ダイナミック コントロール サンプルで `ControlCollection` クラスを参照してください。

## <a name="persist-changes-to-cached-data-in-password-protected-documents"></a>パスワードで保護されたドキュメント内のキャッシュされたデータに変更を保持する
 パスワードで保護されたドキュメント内のデータ オブジェクトをキャッシュする場合、キャッシュされたデータへの変更は保存されません。 2 つのメソッドをオーバーライドすることで、キャッシュされたデータへの変更を保存できます。 これらのメソッドをオーバーライドして、ドキュメントの保存時に保護を一時的に解除し、保存操作の完了後に保護を再適用します。

 詳細については、「[方法: パスワードで保護されたドキュメント内のデータをキャッシュする](../vsto/how-to-cache-data-in-a-password-protected-document.md)」を参照してください。

## <a name="prevent-data-loss-when-adding-null-values-to-the-data-cache"></a>データ キャッシュに null 値を追加するときにデータが失われないようにする
 オブジェクトをデータ キャッシュに追加するときは、ドキュメントを保存して閉じる前に、キャッシュされるすべてのオブジェクトを **null** 以外の値に初期化する必要があります。 ドキュメントが保存されて閉じられるときに、キャッシュされるいずれかのオブジェクトに **null** 値がある場合は、[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]によって、キャッシュされるすべてのオブジェクトがデータ キャッシュから自動的に削除されます。

 デザイン時に <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 属性を使用して、**null** 値が含まれるオブジェクトをデータ キャッシュに追加する場合は、<xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> クラスを使用して、ドキュメントが開かれる前にキャッシュされるデータ オブジェクトを初期化できます。 これは、ドキュメントがエンド ユーザーによって開かれる前に、Word または Excel がインストールされていないサーバーでキャッシュされるデータを初期化する場合に便利です。 詳細については、「[サーバー上のドキュメントのデータにアクセスする](../vsto/accessing-data-in-documents-on-the-server.md)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [方法: オフラインで使用するデータまたはサーバー上で使用するデータをキャッシュする](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)
- [方法: Office ドキュメント内のデータ ソースをプログラムでキャッシュする](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)
- [方法: パスワードで保護されたドキュメント内のデータをキャッシュする](../vsto/how-to-cache-data-in-a-password-protected-document.md)
- [チュートリアル: キャッシュされたデータセットを使用してマスター詳細関係を作成する](../vsto/walkthrough-creating-a-master-detail-relation-using-a-cached-dataset.md)
