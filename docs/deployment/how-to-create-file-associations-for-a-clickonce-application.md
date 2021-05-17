---
title: ファイルの関連付けを作成する (ClickOnce アプリ)
description: ClickOnce アプリケーションを 1 つ以上のファイル名拡張子に関連付ける方法について説明します。これにより、ユーザーがファイルを開いたときにアプリケーションが起動するようになります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- file associations, ClickOnce applications
- ClickOnce deployment, file associations
ms.assetid: 835230c8-3177-440f-85e3-e40f1d8b4f9d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 4b74e20d21ad2c67eed36add90051119c7b8b56e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99861167"
---
# <a name="how-to-create-file-associations-for-a-clickonce-application"></a>方法: ClickOnce アプリケーションのファイルの関連付けを作成する
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを 1 つまたは複数のファイル名拡張子に関連付けることができるため、ユーザーがこれらの種類のファイルを開いたときに、アプリケーションが自動的に起動されます。 ファイル名拡張子のサポートを [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションに追加するのは簡単です。

### <a name="to-create-file-associations-for-a-clickonce-application"></a>ClickOnce アプリケーションのファイルの関連付けを作成するには

1. 通常どおりに [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを作成するか、既存の [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] アプリケーションを使用します。

2. メモ帳などのテキスト エディターまたは XML エディターを使用して、アプリケーション マニフェストを開きます。

3. `assembly` 要素を見つけます。 詳細については、「[ClickOnce アプリケーション マニフェスト](../deployment/clickonce-application-manifest.md)」を参照してください。

4. `assembly` 要素の子要素として `fileAssociation` 要素を追加します。 `fileAssociation` 要素には 4 つの属性があります。

   - `extension`: アプリケーションに関連付けるファイル名拡張子。

   - `description`: Windows シェルに表示されるファイルの種類の説明。

   - `progid`: ファイルの種類を一意に識別する文字列。レジストリでマークします。

   - `defaultIcon`: このファイルの種類に使用するアイコン。 このアイコンは、アプリケーション マニフェストでファイル リソースとして追加する必要があります。 詳細については、「[方法:ClickOnce アプリケーションにデータ ファイルを含める](../deployment/how-to-include-a-data-file-in-a-clickonce-application.md)」を参照してください。

     `file` 要素と `fileAssociation` 要素の例については、「[\<fileAssociation> 要素](../deployment/fileassociation-element-clickonce-application.md)」を参照してください。

5. 複数のファイルの種類をアプリケーションに関連付ける場合は、追加の `fileAssociation` 要素を追加します。 `progid` 属性は、それぞれで異なる必要があることに注意してください。

6. アプリケーションマニフェストの作成が完了したら、マニフェストに再署名します。 これは、*Mage.exe* を使用してコマンド ラインから行うことができます。

    `mage -Sign WindowsFormsApp1.exe.manifest -CertFile mycert.pfx`

    詳しくは、「[Mage.exe (マニフェストの生成および編集ツール)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)」をご覧ください。

## <a name="see-also"></a>関連項目
- [\<fileAssociation> 要素](../deployment/fileassociation-element-clickonce-application.md)
- [ClickOnce アプリケーション マニフェスト](../deployment/clickonce-application-manifest.md)
- [Mage.exe (マニフェストの生成および編集ツール)](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)