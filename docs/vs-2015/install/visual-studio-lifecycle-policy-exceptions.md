---
title: Visual Studio のライフ サイクル ポリシーの例外 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-install
ms.topic: conceptual
ms.assetid: c238489d-6181-42c6-aa60-f75d0889dc68
caps.latest.revision: 3
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: b17693523c75dc434fdda258c07a9b17ecfda1b0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68180241"
---
# <a name="visual-studio-lifecycle-policy-exceptions"></a>Visual Studio のライフサイクル ポリシーの例外
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio には、多数のコンパイラ、言語、ランタイム、環境、およびその他のリソースが含まれているため、さまざまな Microsoft プラットフォームで開発できます。 Visual Studio のお客様の利便性のために、Visual Studio は、いくつかの Microsoft SDK と、Microsoft プラットフォームを対象としてサポートしているその他の Microsoft コンポーネントをインストールすることがあります。 これらのコンポーネントは、独自のライセンス条項とポリシーに基づいてライセンスされ、サポートされる可能性があります。  
  
## <a name="external-components-that-follow-a-lifecycle-policy-other-than-the-visual-studio-policy"></a>Visual Studio ポリシー以外のライフサイクル ポリシーに従う外部コンポーネント  
 次の表に、Visual Studio に含まれている可能性のある (Visual Studio ソフトウェアの特定のエディションに応じます) Microsoft プラットフォームのコンポーネントを示します。これらは、独自のサポート ポリシーとタイム フレームに従う必要があります。  
  
|製品ファミリ|外部名|  
|--------------------|-------------------|  
|[.NET 3.5](http://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=net%20framework%203.5&Filter=FilterNO)|.NET 3.5 SDK<br /><br /> Windows Identity Foundation|  
|[.NET 4.5](http://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=net%20framework%204.5&Filter=FilterNO)|.NET 4.5 SDK|  
|[.NET 4.5.1](http://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=.NET%20Framework%204.5.1&Filter=FilterNO)|.NET 4.5.1 MT パック (クラシック)<br /><br /> .NET 4.5.1 マルチ ターゲット パック (ストア)<br /><br /> .NET 4.5.1 OOB MSU<br /><br /> .NET 4.5.1 Redist<br /><br /> .NET 4.5.1 Redist 言語パック<br /><br /> .NET 4.5.1 SDK|  
|[ASP.NET Web スタック](http://go.microsoft.com/fwlink/?LinkId=328918)|ASP.NET MVC 4<br /><br /> ASP.NET MVC 5<br /><br /> ASP.NET Web API<br /><br /> ASP.NET Web API 2<br /><br /> ASP.NET Web ページ 2<br /><br /> ASP.NET Web ページ 3|  
|[Entity Framework 6](http://go.microsoft.com/fwlink/?LinkId=328950)|Entity Framework 6|  
|[Exchange 2013](http://go.microsoft.com/fwlink/?LinkId=328950)|Exchange Web サービス|  
|[Microsoft OWIN](http://go.microsoft.com/fwlink/?LinkId=328951)|Microsoft OWIN|  
|[Microsoft Web Developer Tools 2013](http://go.microsoft.com/fwlink/?LinkId=328952)|Microsoft Web Developer Tools 2013|  
|これらのコンポーネントの更新プログラムは NuGet 経由で配布され、標準的な Microsoft のライフサイクル ポリシーには従いません。  詳細については、「[http://docs.nuget.org/](http://docs.nuget.org/)」を参照してください。|Microsoft .NET Framework 4.5 用の JSON Web トークン ハンドラー<br /><br /> NuGet 2.7<br /><br /> SignalR<br /><br /> Web 最適化フレームワーク<br /><br /> WebGrease|  
|[ODataLib](http://go.microsoft.com/fwlink/?LinkId=328954)|ODataLib|  
|[Office 2013](http://support.microsoft.com/lifecycle/?p1=16674)|Open XML SDK|  
|[オンライン サービス ポリシー](http://support.microsoft.com/gp/OSSLpolicy)|Microsoft Ads SDK|  
|[SharePoint 2013](http://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=sharepoint%20server%202013&Filter=FilterNO)|SharePoint クライアント コンポーネント<br /><br /> SharePoint Foundation 2013<br /><br /> Windows Identity Foundation 拡張機能|  
|[Silverlight 5](http://support.microsoft.com/lifecycle/?p1=16278)<br /><br /> <br />> 参照: [http://support.microsoft.com/gp/lifean45](http://support.microsoft.com/gp/lifean45)|Silverlight 5 ランタイム<br /><br /> Silverlight 5 SDK|  
|[SQL Server 2008 R2](http://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=SQL%20Server%202008%20R2&Filter=FilterNO)|SQL システム CLR 型 (SQL Server 2008 R2)|  
|[SQL Server 2012](http://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=SQL%20Server%202012&Filter=FilterNO)|DACFx (DACFramework)<br /><br /> SMO (SharedManagementObjects)<br /><br /> SQL コマンド ライン ユーティリティ<br /><br /> SQL 言語サービス - IntelliSense (TSQLLanguageService)<br /><br /> SQL LocalDB<br /><br /> SQL ネイティブ クライアント (Sqlncli)<br /><br /> SQL Server Express 2012 SP1<br /><br /> SQL システム CLR 型 (SQL Server 2012)<br /><br /> SQLDOM|  
|[SQL Server 2014](https://support.microsoft.com/lifecycle/search?sort=PN&alpha=SQL%20Server%202014&Filter=FilterNO)|DACFx (DACFramework)<br /><br /> SMO (SharedManagementObjects)<br /><br /> SQL コマンド ライン ユーティリティ<br /><br /> SQL 言語サービス - IntelliSense (TSQLLanguageService)<br /><br /> SQL LocalDB<br /><br /> SQL ネイティブ クライアント (Sqlncli)<br /><br /> SQL Server Express 2014<br /><br /> SQL システム CLR 型 (SQL Server 2014)<br /><br /> SQLDOM|  
|[SQL Server Compact Edition 4.0](http://support.microsoft.com/lifecycle/?p1=16106)|SQL Server Compact Edition 4.0|  
|[WCF RIA Services v1.0 SP2](http://go.microsoft.com/fwlink/?LinkId=328955)|WCF RIA Services v1.0 SP2|  
|[Windows Server 2008](http://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=Windows%20Server%202008&Filter=FilterNO)|Windows Server 2008 用の Windows Web サービス (WWS)|  
|[Windows 7](http://support.microsoft.com/lifecycle/?c2=14019)|Windows 7 SDK|  
|[Windows 8](http://support.microsoft.com/lifecycle/?c2=16796)|Windows 8 SDK|  
|[Windows 8.1](http://support.microsoft.com/lifecycle/search/default.aspx?sort=PN&alpha=windows%208.1&Filter=FilterNO)|Windows 8.1 SDK<br /><br /> Windows Library for JavaScript (WinJS)|  
|[Microsoft Azure](http://support.microsoft.com/gp/azure-cloud-lifecycle-faq)<br /><br /> <br />> も参照してください。[オンライン ライフ サイクル ポリシー](http://support.microsoft.com/gp/OSSLpolicy)|Microsoft Azure Mobile Services SDK<br /><br /> Microsoft Azure Mobile Services Tools|