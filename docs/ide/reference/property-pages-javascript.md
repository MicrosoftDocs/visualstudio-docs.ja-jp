---
title: "プロパティ ページ、JavaScript | Microsoft Docs"
ms.custom: 
ms.date: 06/21/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- javascript.project.property.debugging.debuggertype
- javascript.project.property.debugging.requireauthentication
- javascript.project.property.outputpath
- javascript.project.property.debugging.launchapplication
- javascript.project.property.defaultlanguage
- javascript.project.property.debugging.machinename
- javascript.project.property.debugging.allowlocalnetworkloopback
ms.assetid: a05ab01f-3d5d-4675-a845-eab51807d3a3
caps.latest.revision: 17
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
ms.sourcegitcommit: d2f4eba36e9069a35cf279ccf1c78f72a51d77a1
ms.openlocfilehash: 5d69e9d8d81ed36bb5933c42f3d8e9a499cd0b9d
ms.contentlocale: ja-jp
ms.lasthandoff: 06/23/2017

---
# <a name="property-pages-javascript"></a>プロパティ ページ、JavaScript
**[プロパティ ページ]** からプロジェクトの設定にアクセスできます。 **[プロパティ ページ]** に表示されるページを使用して、プロジェクトのプロパティを変更できます。  

 プロジェクトのプロパティを表示するには、**ソリューション エクスプローラー**でプロジェクト ノードを選択します。 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  

 [!INCLUDE[note_settings_general](../../data-tools/includes/note_settings_general_md.md)]  

 次に示すページとオプションが **[プロパティ ページ]** に表示されます。  

## <a name="configuration-and-platform-page"></a>[構成] ページと [プラットフォーム] ページ  
 次のオプションを使用して、表示または変更する構成とプラットフォームを選択します。  

 **構成**  
 表示または変更する構成設定を指定します。 この設定は **[デバッグ]** (既定)、**[リリース]**、**[すべての構成]**、またはユーザー定義の構成に指定できます。 詳細については、「[How to: Set debug and release configurations in Visual Studio](../../debugger/how-to-set-debug-and-release-configurations.md)」 (方法: Visual Studio でデバッグ構成とリリース構成を設定する) を参照してください。  

 **プラットフォーム**  
 表示または変更するプラットフォーム設定を指定します。 この設定は **[任意の CPU]** ([!INCLUDE[win8_appname_long](../../debugger/includes/win8_appname_long_md.md)] アプリの既定)、**[x64]**、**[ARM]**、**[x86]**、またはユーザー定義のプラットフォームに指定できます。 詳細については、「[How to: Set debug and release configurations in Visual Studio](../../debugger/how-to-set-debug-and-release-configurations.md)」 (方法: Visual Studio でデバッグ構成とリリース構成を設定する) を参照してください。  

## <a name="general-page"></a>[全般] ページ  
 次のオプションを使用して、プロジェクトの全般プロパティを設定します。  

> [!NOTE]
>  一部のオプションは、Windows ストア アプリでのみ使用できます。  

 **出力パス**  
 プロジェクト構成の出力ファイルの場所を指定します。 表示されているのは相対パスです。絶対パスを入力すると、その絶対パスがプロジェクトに保存されます。 既定の相対パスは bin\Debug です。  

 簡易ビルド構成を使用すると、デバッグ バージョンとリリース バージョンのどちらをビルドするかはプロジェクト システムによって決定されます。 **[デバッグ]**、**[デバッグ開始]** の順にクリックすると (または F5 キーを押すと)、指定した **[出力パス]** に関係なく、デバッグ用の場所にビルドが出力されます。 ただし、**[ビルド]** メニューの **[ソリューションのビルド]** コマンドでは、指定した場所にビルドが出力されます。 詳細ビルド構成を有効にするには、メニュー バーで **[ツール]**、**[オプション]** の順にクリックします。 **[オプション]** ダイアログ ボックスで、**[プロジェクトおよびソリューション]** を展開し、**[全般]** をクリックして、**[ビルド構成の詳細を表示]** チェック ボックスをオフにします。 これで、すべての構成値と、デバッグとリリース バージョンのいずれをビルドするかを手動で制御できます。  

 **既定の言語**  
 プロジェクトの既定の言語を指定します。 コントロール パネルの **[時計、言語、および地域]** で選択した言語オプションにより、ユーザーの優先する言語が指定されます。 プロジェクトの既定の言語を指定することで、ユーザーの優先する言語が、アプリケーションで指定した言語リソースと一致しない場合に、指定した既定の言語リソースが確実に使用されるようになります。  

## <a name="debug-page"></a>[デバッグ] ページ  
 次のオプションを使用して、プロジェクト内のデバッグ動作のプロパティを設定します。  

> [!NOTE]
>  一部のオプションは、Windows ストア アプリでのみ使用できます。  

 **[起動するデバッガー]**  
 デバッガーの既定のホストを指定します。  

-   Visual Studio ホスト コンピューターでアプリケーションを起動するには、**[ローカル マシン]** を選択します。 詳細については、「[ローカル コンピューターでのアプリの実行](http://go.microsoft.com/fwlink/?LinkId=234912)」を参照してください。  

-   シミュレーターでアプリケーションを起動するには、**[シミュレーター]** を選択します。 詳細については、「[シミュレーターでのアプリの実行](http://go.microsoft.com/fwlink/?LinkId=234913)」を参照してください。  

-   リモート コンピューターでアプリケーションを起動するには、**[リモート コンピューター]** を選択します。 リモート デバッグの詳細については、「[リモート コンピューターでのアプリの実行](http://go.microsoft.com/fwlink/?LinkId=234914)」を参照してください。  

 **[アプリケーションの起動]**  
 F5 キーを押すか、**[デバッグ]**、**[デバッグ開始]** の順にクリックすると、アプリケーションが起動されるかどうかを指定します。 アプリケーションが起動されるようにするには、**[はい]** を選択します。それ以外の場合は、**[いいえ]** を選択します。 **[いいえ]** を選択した場合でも、アプリケーションを別の方法で起動してデバッグできます。  

 **[デバッガーのタイプ]**  
 デバッグするコードの種類を指定します。 JavaScript コードをデバッグするには、**[スクリプトのみ]** を選択します。 共通言語ランタイムで管理されるコードをデバッグするには、**[マネージのみ]** を選択します。 C++ コードをデバッグするには、**[ネイティブのみ]** を選択します。 C++ と JavaScript をデバッグするには、**[スクリプトを使用したネイティブ コード]** を選択します。 マネージ コードと C++ コードの両方をデバッグするには、**[混合 (マネージとネイティブ)]** を選択します。  

 **[ローカル ネットワーク ループバックの許可]**  
 IP ループバック アドレスへのアクセスをアプリのテストに許可するかどうかを指定します。 クライアント アプリケーションとサーバー アプリケーションが同じコンピューターで実行されている場合に、ループバック アドレスの使用を許可するには、**[はい]** を選択します。それ以外の場合は、**[いいえ]** を選択します。 このプロパティを使用できるのは、**[起動するデバッガー]** プロパティが **[リモート コンピューター]** に設定されている場合のみです。  

 **[コンピューター名]**  
 デバッガーをホストするリモート コンピューターの名前を指定します。 このプロパティを使用できるのは、**[起動するデバッガー]** が **[リモート コンピューター]** に設定されている場合のみです。  

 **[認証が必要]**  
 リモート コンピューターで認証が必要かどうかを指定します。 このプロパティを使用できるのは、**[起動するデバッガー]** が **[リモート コンピューター]** に設定されている場合のみです。

