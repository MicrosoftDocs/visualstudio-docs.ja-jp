---
title: "Office ソリューション開発の概要 (VSTO) |Microsoft ドキュメント"
ms.custom: 
ms.date: 02/02/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- office-development
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- primary interop assemblies, Office
- Office development in Visual Studio, about developing solutions
author: TerryGLee
ms.author: tglee
manager: ghogen
ms.workload:
- office
ms.openlocfilehash: 53ff49eb204eda28174344b44d58e236bde24c64
ms.sourcegitcommit: f9fbf1f55f9ac14e4e5c6ae58c30dc1800ca6cda
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2018
---
# <a name="office-solutions-development-overview-vsto"></a>Office ソリューションの開発の概要 (VSTO)
  ソリューションのフロント エンドとして Microsoft Office を使用すると、Word のワープロ機能、Excel のデータの分析機能、および Outlook の電子メール管理機能などの使い慣れた Microsoft Office のユーザー インターフェイスとツールを活用することができます。 Office アプリケーションのカスタマイズおよびビジネス プロセスに必要な特定の機能の追加を行うために、Visual Studio でソリューションを開発することができます。 たとえば、Word を既存のパーツからコントラクトを組み合わせるコントラクト ジェネレーターにすることができます。既存のパーツは編集可能または編集可能でない場合があります。 Excel では、さまざまなプロジェクト用にカスタマイズされた自動予算のワークシートを作成できます。 ユーザーはオフラインで Office ソリューションを取得することもできます。これは、Web ベースのアーキテクチャを使用する場合に、複雑なソリューションをより実用的なものにします。  
  
 ここでは、Visual Studio の Office Developer Tools で使用可能な Visual Studio Tools for Office (VSTO) テンプレートを使用して作成できる、Office ソリューションの種類の概要について説明します。 Office での開発方法に関する一般的な情報については、「 [Office デベロッパー センター](https://dev.office.com/)」を参照してください。  
  
## <a name="choosing-an-office-project-type"></a>Office プロジェクトの種類の選択  
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] では、VSTO ベースの Office 開発のために、次の種類のプロジェクト テンプレートを提供します。  
  
-   **ドキュメント レベルのカスタマイズ** は、特定のドキュメントに関連付けられます。  
  
-   **VSTO Add-ins** は、アプリケーション自体に関連付けられます。  
  
 これらのプロジェクトの中でソリューションに最適な種類を決定するには、特定のドキュメントを開いたときにのみ実行するコードが必要かどうか、また、アプリケーションの実行時に使用できるコードが必要かどうかについて考えます。 プロジェクト テンプレートの詳細については、次を参照してください。 [Office プロジェクト テンプレートの概要](../vsto/office-project-templates-overview.md)です。  
  
 作成できるプロジェクトの種類は、開発用コンピューターにインストールした Office アプリケーションによって異なります。 詳細については、「[Office アプリケーションおよびプロジェクトの種類別の使用可能な機能](../vsto/features-available-by-office-application-and-project-type.md)」を参照してください。  
  
### <a name="document-level-customizations"></a>ドキュメント レベルのカスタマイズ  
 ドキュメント レベルのカスタマイズは、Microsoft Office Word または Microsoft Office Excel 内の単一のドキュメント、ブック、またはテンプレートに関連付けられているアセンブリで構成されます。 このアセンブリは、関連付けられたドキュメントを開いたときに読み込まれます。 作成するカスタマイズの機能は、関連付けられたドキュメントが開いている場合にのみ使用できます。 カスタマイズでは、任意のドキュメントが開いている場合の新しいメニュー項目やリボン タブの表示など、アプリケーション全体に変更を加えることはできません。  
  
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] には、ドキュメント レベルのカスタマイズを作成するのに役立つツールが含まれています。 カスタマイズするドキュメントは、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]のデザイン サーフェイスとしてホストされます。これにより、コントロールをドキュメントにドラッグ アンド ドロップして、ドキュメントをデザインすることができます。 その他の多くの [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 機能は、Windows フォーム コントロール、ドラッグ アンド ドロップのデータ バインディング、および統合デバッガーなど、ドキュメント レベルのプロジェクトで利用可能です。  
  
 カスタマイズの詳細については、次のトピックを参照してください。  
  
-   [Excel のドキュメント レベルのカスタマイズのプログラミングの概要](../vsto/getting-started-programming-document-level-customizations-for-excel.md)  
  
-   [Word 用のドキュメント レベルのカスタマイズのプログラミングについて](../vsto/getting-started-programming-document-level-customizations-for-word.md)  
  
-   [ドキュメント レベルのカスタマイズのアーキテクチャ](../vsto/architecture-of-document-level-customizations.md)  
  
### <a name="vsto-add-ins"></a>VSTO Add-ins  
 VSTO アドインは、Microsoft Office アプリケーションに関連付けられているアセンブリで構成されます。 アプリケーションが既に実行されている場合に VSTO アドインを読み込むこともできますが、通常、VSTO アドインは関連付けられたアプリケーションが開始されたときに実行されます。 作成した VSTO アドインの機能は、どのドキュメントが開いているかにかかわらず、アプリケーション自体に対して使用できます。  
  
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] には、VSTO アドインの作成に役立つツールが含まれています。アドイン プロジェクトには、VSTO アドインを表す自動的に生成されたクラスが含まれます。 このクラスは、ホスト アプリケーションのオブジェクト モデルへのアクセス、および VSTO アドインの読み込みとシャット ダウン時のコードの実行に使用できる、プロパティとイベントを提供します。 その他の多くの [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 機能は、Windows フォームや統合デバッガーなどの VSTO アドイン プロジェクトで利用可能です。  
  
 VSTO アドインの詳細については、次のトピックを参照してください。  
  
-   [VSTO アドインのプログラミングについて](../vsto/getting-started-programming-vsto-add-ins.md)  
  
-   [VSTO アドインのアーキテクチャ](../vsto/architecture-of-vsto-add-ins.md)  
  
## <a name="automating-office-applications-by-using-primary-interop-assemblies"></a>プライマリ相互運用機能アセンブリを使用して Office アプリケーションを自動化する  
 アプリケーションのオブジェクト モデルにアクセスするコードを記述して、Office アプリケーションの機能をソリューションにプログラムによって組み込むことができます。 オブジェクト モデルは、さまざまなプロパティとメソッドを介して機能を公開するクラスの配置です。 各 Office アプリケーションのオブジェクト モデルは異なります。  
  
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]の Office 開発者ツールを使用して作成されたソリューションから Office アプリケーションのオブジェクト モデルを使用するには、アプリケーションのプライマリ相互運用機能アセンブリ (PIA) を使用する必要があります。 PIA によって、Office アプリケーションの COM ベースのオブジェクト モデルと対話するソリューション内にマネージ コードを作成できるようになります。  
  
 ほとんどの開発タスクを実行するには、開発用コンピューターのグローバル アセンブリ キャッシュに Office PIA をインストールし、登録する必要があります。 詳細については、「 [Configuring a Computer to Develop Office Solutions](../vsto/configuring-a-computer-to-develop-office-solutions.md)」を参照してください。 エンド ユーザーのコンピューターで VSTO Office ソリューションを実行する場合には、Office PIA は必要ありません。 詳細については、「 [Designing and Creating Office Solutions](../vsto/designing-and-creating-office-solutions.md)」を参照してください。  
  
 VSTO Office ソリューションでの PIA の使用に関する詳細については、次のトピックを参照してください。  
  
-   [Writing Code in Office Solutions](../vsto/writing-code-in-office-solutions.md)  
  
-   [Office プライマリ相互運用機能アセンブリ](../vsto/office-primary-interop-assemblies.md)  
  
## <a name="running-microsoft-vsto-office-solutions-on-end-user-computers"></a>エンド ユーザーのコンピューターでの Microsoft VSTO Office ソリューションの実行  
 VSTO Office ソリューションを作成する場合、配置要件が開発方法に与える可能性のある影響について考慮します。  
  
### <a name="deployment-options"></a>配置オプション  
 ClickOnce または Windows インストーラーを使用して、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]の Office 開発者ツールを使用して作成したソリューションを配置します。 ClickOnce の配置では、インストールできる自己更新ソリューションを作成し、最小限のユーザー操作で実行することができます。 Windows インストーラー (.msi) ファイルは、エンドユーザーのコンピューターに簡単に配布したり、Systems Management Server (SMS) を使用して配布したりすることができます。 VSTO Office ソリューションの配置の詳細については、次を参照してください。 [Office ソリューションの配置](../vsto/deploying-an-office-solution.md)です。  
  
### <a name="installing-prerequisites"></a>必要条件のインストール  
 エンド ユーザーが [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]の Office 開発者ツールを使用して作成したソリューションを実行できるようにするには、ユーザーのコンピューターに特定の必須コンポーネントがインストールされている必要があります。 ClickOnce を使用するか、Windows インストーラー ファイルを作成して、ソリューションを配置する場合は、ソリューションと共にこれらの必須コンポーネントをインストールできます。 詳細については、「 [Office ソリューションを配置するための必須コンポーネント](http://msdn.microsoft.com/en-us/9f672809-43a3-40a1-9057-397ce3b5126e) 」と「 [方法: Office ソリューションを実行するために、エンド ユーザーのコンピューターに必須コンポーネントをインストールする](http://msdn.microsoft.com/en-us/74dd2c52-838f-4abf-b2b4-4d7b0c2a0a98)」を参照してください。  
  
### <a name="security"></a>セキュリティ  
 VSTO Office ソリューションのセキュリティは、 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] がソリューションのインストールおよび読み込み時に作成する一連のチェックによって強制されます。 これらのチェックには、配置マニフェストの場所が信頼されているかどうか、または配置マニフェストの署名に使用される証明書が信頼されているかどうかの検証が含まれます。 詳細については、「 [Securing Office Solutions](../vsto/securing-office-solutions.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [作業の開始 (&) #40 です。 Visual Studio &#41; での Office 開発](../vsto/getting-started-office-development-in-visual-studio.md)   
 [ドキュメント レベルのカスタマイズのアーキテクチャ](../vsto/architecture-of-document-level-customizations.md)   
 [VSTO アドインのアーキテクチャ](../vsto/architecture-of-vsto-add-ins.md)   
 [Excel 用ドキュメント レベル カスタマイズのプログラミング](../vsto/getting-started-programming-document-level-customizations-for-excel.md)   
 [Word 用ドキュメント レベル カスタマイズのプログラミング](../vsto/getting-started-programming-document-level-customizations-for-word.md)   
 [VSTO アドインのプログラミングについて](../vsto/getting-started-programming-vsto-add-ins.md)  
  
  