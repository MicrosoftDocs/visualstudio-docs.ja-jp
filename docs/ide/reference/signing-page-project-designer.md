---
title: "[署名] ページ (プロジェクト デザイナー) | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vs.AddNewStrongNameKey
- ResolveKeySource.KeyFileForSignAssemblyNotImported
- vb.ProjectPropertiesSigning.ChangePasswordDialog
- ResolveKeySource.KeyFileForManifestNotImported
- vb.ProjectPropertiesSigning
- vb.ProjectPropertiesSigning.PasswordNeededDialog
- vb.ProjectPropertiesSigning.PfxPasswordDialog
helpviewer_keywords:
- Project Designer, Signing page
- Signing page in Project Designer
ms.assetid: dab3ba13-2f92-4827-92bd-1be3c35bc48b
caps.latest.revision: 34
author: kempb
ms.author: kempb
manager: ghogen
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Human Translation
ms.sourcegitcommit: 3d32d11a430227800cb3ed53831a9565eb6adeb3
ms.openlocfilehash: e4abacb0286de16c148076572e73043daed4d567
ms.contentlocale: ja-jp
ms.lasthandoff: 05/30/2017

---
# <a name="signing-page-project-designer"></a>[署名] ページ (プロジェクト デザイナー)
**プロジェクト デザイナー**の [**署名**] ページを使用して、アプリケーション マニフェストと配置マニフェストに署名し、アセンブリに署名します (厳密な名前の署名)。  
  
 アプリケーション マニフェストと配置マニフェストの署名は、アセンブリの署名と同じく [**署名**] ページで実行されますが、異なるプロセスであることに注意してください。  
  
 また、キー ファイル情報のストレージは、マニフェストの署名とアセンブリの署名とは異なります。 マニフェストの署名では、キー情報はコンピューターの暗号化ストレージ データベースと現在のユーザーの Windows 証明書ストアに格納されます。 アセンブリの署名では、キー情報はコンピューターの暗号化ストレージ データベースだけに格納されます。  
  
 この [**署名**] ページにアクセスするには、**ソリューション エクスプローラー**でプロジェクト ノードを選択し、[**プロジェクト**] メニューの [**プロパティ**] をクリックします。 **プロジェクト デザイナー**が表示されたら、[**署名**] タブをクリックします。  
  
## <a name="application-and-deployment-manifest-signing"></a>アプリケーション マニフェストと配置マニフェストの署名  
 [**ClickOnce マニフェストに署名する**] チェック ボックス  
 公開キーと秘密キーのペアを使用して、アプリケーション マニフェストと配置マニフェストに署名するには、このチェック ボックスを選択します。 この方法の詳細については、「[方法: アプリケーション マニフェストおよび配置マニフェストに署名する](../../ide/how-to-sign-application-and-deployment-manifests.md)」を参照してください。  
  
 [**ストアから選択**] ボタン  
 現在のユーザーの個人証明書ストアから既存の証明書を選択できます。 アプリケーション マニフェストと配置マニフェストの署名にこれらの証明書のいずれかを選択することができます。  
  
 [**ストアから選択**] をクリックすると、[**証明書の選択**] ダイアログ ボックスが開きます。ここには、現在有効で (期限が切れていない)、秘密キーを持つ個人証明書ストア内の証明書が一覧表示されます。 選択した証明書の目的には、コード署名を含める必要があります。  
  
 [**証明書のプロパティを表示します**] をクリックすると、[**証明書の詳細**] ダイアログ ボックスが表示されます。 このダイアログ ボックスには、証明書の詳細情報、および追加オプションが含まれています。 追加のヘルプ情報を表示するには [**証明書の詳細情報**] をクリックします。  
  
 [**ファイルから選択**] ボタン  
 既存のキー ファイルから証明書を選択できます。  
  
 [**ファイルから選択**] をクリックすると、[**ファイルの選択**] ダイアログ ボックスが開きます。ここで証明書のキー (.pfx) ファイルを選択することができます。 ファイルはパスワードで保護する必要があり、個人証明書ストアに格納しておくことはできません。  
  
 [**ファイルを開くためのパスワードを入力してください**] ダイアログ ボックスで、証明書のキー (.pfx) ファイルを開くためのパスワードを入力します。 パスワード情報は、個人のキー コンテナー一覧と個人用証明書ストアに格納されます。  
  
 [**テスト証明書の作成**] ボタン  
 テスト用の証明書を作成できます。 テスト証明書は、ClickOnce アプリケーション マニフェストと配置マニフェストの署名に使用されます。  
  
 [**テスト証明書の作成**] をクリックすると、[**テスト証明書の作成**] ダイアログ ボックスが開きます。ここでテスト証明書の厳密な名前のキー ファイルのパスワードを入力することができます。 このファイルの名前は *projectname*_TemporaryKey.pfx です。 パスワードを入力せずに [**OK**] をクリックすると、.pfx ファイルはパスワードで暗号化されません。  
  
 [**タイムスタンプ サーバーの URL**] ボックス  
 署名にタイムスタンプを記録するサーバーのアドレスを指定します。 証明書を提供すると、この外部サイトによってアプリケーションが署名された時間が確認されます。  
  
## <a name="assembly-signing"></a>アセンブリの署名  
 [**アセンブリの署名**] チェック ボックス  
 アセンブリに署名し、厳密な名前のキー ファイルを作成するには、このチェック ボックスをオンにします。 **プロジェクト デザイナー**を使用してアセンブリに署名する詳細については、「[方法: アセンブリに署名する (Visual Studio)](http://msdn.microsoft.com/en-us/f468a7d3-234c-4353-924d-8e0ae5896564)」を参照してください。  
  
 このオプションは、[!INCLUDE[winsdklong](/dotnet/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name) で提供される Al.exe ツールを使用します。  
  
 [**厳密な名前のキー ファイルを選択してください**] 一覧  
 アセンブリに署名するために使用する新規または既存の厳密な名前のキー ファイルを指定できます。 [**\<参照...>**] を選択して、既存のキー ファイルを選択します。  
  
 [**\<新規...>**] を選択して、アセンブリの署名に使用する新しいキー ファイルを作成します。 [**厳密な名前キーの作成**] ダイアログ ボックスが表示されます。ここでキー ファイル名を指定し、パスワードを使用してキー ファイルを保護することができます。 パスワードの長さは 6 文字以上にする必要があります。 パスワードを指定すると、Personal Information Exchange (.pfx) ファイルが作成されます。パスワードを指定しない場合は、厳密な名前のキー (.snk) ファイルが作成されます。  
  
 [**パスワードの変更**] ボタン  
 アセンブリの署名に使用される、Personal Information Exchange (.pfx) キー ファイルのパスワードを変更します。  
  
 [**パスワードの変更**] をクリックすると、[**キー パスワードの変更**] ダイアログ ボックスが開きます。 このダイアログ ボックスでは、**古いパスワード**はキー ファイルの現在のパスワードです。 **新しいパスワード**の長さは 6 文字以上にする必要があります。 パスワード情報は、現在のユーザーの Windows 証明書ストアに格納されます。  
  
 [**遅延署名のみ**] チェック ボックス  
 遅延署名を有効にするには、このチェック ボックスを選択します。  
  
 遅延署名されたプロジェクトは実行されず、デバッグできないことに注意してください。 ただし、[Sn.exe (厳密名ツール)](/dotnet/framework/tools/sn-exe-strong-name-tool) と `-Vr` オプションを使用すると、開発時に検証をスキップできます。  
  
> [!NOTE]
>  アセンブリに署名するときに、秘密キーへのアクセス権がない場合があります。 たとえば、組織には、開発者が日常的にアクセスしない厳重に保護されたキーのペアがある場合があります。 公開キーは使用可能ですが、秘密キーへのアクセスは少数のユーザーに限定されます。 このような場合は、*遅延*または*部分署名*を使用して公開キーを提供し、アセンブリが引き渡されるまで、秘密キーの追加を遅らせることができます。  
  
## <a name="see-also"></a>関連項目  
 [プロジェクトのプロパティのリファレンス](../../ide/reference/project-properties-reference.md)   
 [アセンブリおよびマニフェストへの署名の管理](../../ide/managing-assembly-and-manifest-signing.md)   
 [マネージ アプリケーションの厳密な名前の署名](http://msdn.microsoft.com/en-us/5fef3490-c519-4363-94fd-8b1ad260dab5)   
 [方法 : アプリケーション マニフェストおよび配置マニフェストに署名する](../../ide/how-to-sign-application-and-deployment-manifests.md)   
 [方法: アセンブリに署名する (Visual Studio)](http://msdn.microsoft.com/en-us/f468a7d3-234c-4353-924d-8e0ae5896564)   
 [方法 : 厳密な名前でアセンブリに署名する](/dotnet/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name)   
 [厳密な名前付きアセンブリ](http://msdn.microsoft.com/Library/d4a80263-f3e0-4d81-9b61-f0cbeae3797b)
