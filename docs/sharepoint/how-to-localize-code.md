---
title: '方法: コードをローカライズする | Microsoft Docs'
description: SharePoint で、ハードコーディングされた文字列を、ローカライズされたリソースを参照するメソッドである GetGlobalResourceObject の呼び出しに置き換えることにより、コードをローカライズする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- localizing code [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, localizing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: e76b8cfb2e9fcb513905918bd4ae87524078f6c6
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99931644"
---
# <a name="how-to-localize-code"></a>方法: コードをローカライズする
  ローカライズされていないコードでは、ハードコーディングされた文字列値が使用されています。 コードの文字列をローカライズするには、それらを <xref:System.Web.HttpContext.GetGlobalResourceObject%2A> の呼び出しに置き換えます。このメソッドは、ローカライズされたリソースを参照します。

## <a name="localize-code"></a>コードをローカライズする

#### <a name="to-localize-code"></a>コードをローカライズするには

1. **ソリューション エクスプローラー** で、プロジェクト項目のショートカット メニューを開き、 **[追加]**  >  **[モジュール]** を選択します。

     **[リソース ファイル]** テンプレートを選択します。

    > [!NOTE]
    > Deployment Type プロパティを使用できるように、SharePoint プロジェクト項目にリソース ファイルを必ず追加します。 このプロパティは、後で必要になります。

2. 既定の言語のリソース ファイルには、 *.resx* 拡張子が付いた任意の名前を付けます (*MyAppResources.resx* など)。

3. ローカライズ言語ごとに手順 1. と 2. を繰り返して、SharePoint プロジェクト項目にそれぞれのリソース ファイルを追加します。

     ローカライズされた各リソース ファイルに対しては、同じ基本名にカルチャ ID を加えた名前を使用します  (ドイツ語の場合は *MyAppResources.de-DE.resx* など)。

4. 各リソース ファイルを開いて、ローカライズされた文字列を追加します。 各ファイルで同じ文字列 ID を使用します。

5. 各リソース ファイルの **[配置タイプ]** プロパティの値を **[AppGlobalResource]** に変更して、サーバーの App_GlobalResources フォルダーに配置されるようにします。

6. 各ファイルの **[ビルド アクション]** プロパティの値は **[埋め込まれたリソース]** のままにします。

     埋め込みリソースはプロジェクトの DLL にコンパイルされます。

7. プロジェクトをビルドして、リソースのサテライト DLL を作成します。

8. **パッケージ デザイナー** で、 **[詳細設定]** タブをクリックし、サテライト アセンブリを追加します。

9. **[場所]** ボックスで、場所のパスの先頭にカルチャ ID のフォルダーを追加します (*de-DE\\\<Project Item Name>.resources.dll* など)。

10. ソリューションで System.Web アセンブリがまだ参照されていない場合は System.Web アセンブリへの参照を追加し、<xref:System.Web> に対するディレクティブをコードに追加します。

11. UI テキスト、エラー、メッセージ テキストなど、ユーザーへの表示用にコード内でハードコーディングされている文字列をすべて見つけます。 それらの文字列を、次の構文を使用する <xref:System.Web.HttpContext.GetGlobalResourceObject%2A> メソッドの呼び出しに置き換えます。

    ```csharp
    HttpContext.GetGlobalResourceObject("Resource File Name", "String ID")
    ```

12. **F5** キーを押してアプリケーションをビルドし、実行します。

13. SharePoint で、表示言語を既定の言語から変更します。

     ローカライズされた文字列がアプリケーションに表示されます。 ローカライズされたリソースを表示するには、リソース ファイルのカルチャに対応する Language Pack が SharePoint サーバーにインストールされている必要があります。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションをローカライズする](../sharepoint/localizing-sharepoint-solutions.md)
- [方法: フィーチャーをローカライズする](../sharepoint/how-to-localize-a-feature.md)
- [方法: ASPX マークアップをローカライズする](../sharepoint/how-to-localize-aspx-markup.md)
- [方法: リソース ファイルを追加する](../sharepoint/how-to-add-a-resource-file.md)
