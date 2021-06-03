---
title: SharePoint プロジェクト システムの拡張機能へのデータの保存 | Microsoft Docs
titleSuffix: ''
description: 拡張機能を含む SharePoint プロジェクトが閉じられた後も保持される文字列データを保存する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
helpviewer_keywords:
- SharePoint project items, saving string data
- project items [SharePoint development in Visual Studio], saving string data
- projects [SharePoint development in Visual Studio], saving string data
- SharePoint projects, saving string data
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 87e05ba763095a818cc5db6f92828e6259d30e73
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217438"
---
# <a name="save-data-in-extensions-of-the-sharepoint-project-system"></a>SharePoint プロジェクト システムの拡張機能にデータを保存する
  SharePoint プロジェクト システムを拡張すると、SharePoint プロジェクトが閉じられた後も保持される文字列データを保存できます。 これらのデータは通常、特定のプロジェクト項目またはプロジェクト自体に関連付けられています。

 保持する必要のないデータがある場合は、そのデータを、<xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject> インターフェイスを実装する SharePoint ツール オブジェクト モデル内の任意のオブジェクトに追加できます。 詳細については、「[カスタム データを SharePoint ツール拡張機能に関連付ける](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)」を参照してください。

## <a name="save-data-that-is-associated-with-a-project-item"></a>プロジェクト項目に関連付けられているデータを保存する
 特定の SharePoint プロジェクト項目に関連付けられているデータ (プロジェクト項目に追加するプロパティの値など) がある場合は、そのデータをプロジェクト項目の *.spdata* ファイルに保存できます。 これを行うには、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem> オブジェクトの <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> プロパティを使用します。 このプロパティに追加したデータは、プロジェクト項目の *.spdata* ファイル内の **ExtensionData** 要素に保存されます。 詳細については、「[ExtensionData 要素](../sharepoint/extensiondata-element.md)」を参照してください。

 次のコード例は、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> プロパティを使用して、カスタム SharePoint プロジェクト項目の種類で定義されている文字列プロパティの値を保存する方法を示しています。 この例をより大きな例のコンテキストで確認するには、「[方法: プロパティをカスタムの SharePoint プロジェクト項目の種類に追加する](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)」を参照してください。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemtypeproperty.vb" id="Snippet14":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemtypeproperty.cs" id="Snippet14":::

## <a name="save-data-that-is-associated-with-a-project"></a>プロジェクトに関連付けられているデータを保存する
 プロジェクト レベルのデータ (SharePoint プロジェクトに追加するプロパティの値など) がある場合は、そのデータをプロジェクト ファイル ( *.csproj* ファイルまたは *.vbproj* ファイル) またはプロジェクト ユーザー オプション ファイル ( *.csproj.user* ファイルまたは *.vbproj.user* ファイル) に保存できます。 データを保存するために選択するファイルは、そのデータをどのように使用するかによって異なります。

- SharePoint プロジェクトを開くすべての開発者がデータを使用できるようにする場合は、そのデータをプロジェクト ファイルに保存します。 このファイルは常にソース管理データベースにチェックインされるため、このファイル内のデータは、プロジェクトをチェックアウトする他の開発者が使用できます。

- Visual Studio で SharePoint プロジェクトを開いている現在の開発者のみがデータを使用できるようにする場合は、そのデータをプロジェクト ユーザー オプション ファイルに保存します。 このファイルは通常、ソース管理データベースにはチェックインされないため、このファイル内のデータは、プロジェクトをチェックアウトする他の開発者は使用できません。

### <a name="save-data-to-the-project-file"></a>プロジェクト ファイルにデータを保存する
 プロジェクト ファイルにデータを保存するに、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> オブジェクトを <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> オブジェクトに変換してから、<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetPropertyValue%2A> メソッドを使用します。 次のコード例は、このメソッドを使用して、プロジェクト プロパティの値をプロジェクト ファイルに保存する方法を示しています。 この例をより大きなサンプルのコンテキストで確認するには、「[方法: SharePoint プロジェクトにプロパティを追加する](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)」を参照してください。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/customspproperty/customproperty.vb" id="Snippet3":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/customspproperty/customproperty.cs" id="Snippet3":::

 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> オブジェクトの Visual Studio オートメーション オブジェクト モデルまたは統合オブジェクト モデル内のその他の種類への変換の詳細については、「[SharePoint プロジェクト システムの種類とその他の Visual Studio プロジェクトの種類の間で変換する](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md)」を参照してください。

### <a name="save-data-to-the-project-user-option-file"></a>プロジェクト ユーザー オプション ファイルにデータを保存する
 プロジェクト ユーザー オプション ファイルにデータを保存するに、<xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> オブジェクトの <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.ProjectUserFileData%2A> プロパティを使用します。 次のコード例は、このプロパティを使用して、プロジェクト プロパティの値をプロジェクト ユーザー オプション ファイルに保存する方法を示しています。 この例をより大きなサンプルのコンテキストで確認するには、「[方法: SharePoint プロジェクトにプロパティを追加する](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)」を参照してください。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/customspproperty/customproperty.vb" id="Snippet2":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/customspproperty/customproperty.cs" id="Snippet2":::

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクト システムを拡張する](../sharepoint/extending-the-sharepoint-project-system.md)
- [カスタム データを SharePoint ツール拡張機能に関連付ける](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)
- [SharePoint プロジェクト システムの種類とその他の Visual Studio プロジェクトの種類の間で変換する](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md)
