---
title: "配置した Web アプリケーションのデバッグ | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "vs-ide-debug"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "FSharp"
  - "VB"
  - "CSharp"
  - "C++"
helpviewer_keywords: 
  - "ASP.NET Web アプリケーション"
  - "ASP.NET, デバッグ (Web アプリケーションを)"
  - "デバッグ (Web サービスを)"
  - "Web サービス, デバッグ"
  - " XML Web サービス, デバッグ"
  - "XML, デバッグ (Web サービスを)"
ms.assetid: b938a91b-be96-416f-83bc-4177e7f3929a
caps.latest.revision: 31
caps.handback.revision: 31
author: "mikejo5000"
ms.author: "mikejo"
manager: "ghogen"
---
# 配置した Web アプリケーションのデバッグ
[!INCLUDE[vs2017banner](../code-quality/includes/vs2017banner.md)]

運用サーバーで実行されている Web アプリケーションをデバッグする場合は、慎重に行う必要があります。  たとえば、[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ワーカー プロセスにアタッチしてデバッグを行い、ブレークポイントにヒットした場合、そのワーカー プロセス内のすべてのマネージ コードが停止します。  ワーカー プロセス内のすべてのマネージ コードが停止すると、サーバーのすべてのユーザーの業務が停止する可能性があります。  運用サーバーでデバッグする場合は、事前に、実際の業務への影響について検討する必要があります。  
  
 配置されたアプリケーションを [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] を使用してデバッグするには、[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ワーカー プロセスにアタッチし、デバッガーからアプリケーションのシンボルにアクセスできるようにする必要があります。  また、アプリケーションのソース ファイルを見つけて開く必要があります。  詳細については、「[シンボルとソース コードの管理](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)」、「[方法 : ASP.NET プロセスの名前を見つける](../debugger/how-to-find-the-name-of-the-aspnet-process.md)」、および「[システム要件](../debugger/aspnet-debugging-system-requirements.md)」を参照してください。  
  
> [!NOTE]
>  多くの [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーションは、ビジネス ロジックまたはその他の有用なコードが格納されている DLL を参照します。  このような参照では、ローカル コンピューターにある DLL が自動的に Web アプリケーションの仮想ディレクトリの \\bin フォルダーにコピーされます。  デバッグ時には、Web アプリケーションが、ローカル コンピューターの DLL ではなく、仮想ディレクトリにある DLL のコピーを参照している点に注意してください。  
  
 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] ワーカー プロセスにアタッチする方法は、他のリモート プロセスにアタッチする場合と同じです。  アタッチしたときに正しいプロジェクトが開いていない場合、アプリケーションがブレークするとダイアログ ボックスが表示されます。  このダイアログ ボックスでは、アプリケーションのソース ファイルの場所を指定するように求められます。  このダイアログ ボックスに指定するファイル名は、Web サーバー上のデバッグ シンボルで指定されているファイル名と一致する必要があります。  詳細については、「[実行中のプロセスへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)」を参照してください。  
  
## 参照  
 [ASP.NET アプリケーションおよび AJAX アプリケーションのデバッグ](../debugger/debugging-aspnet-and-ajax-applications.md)   
 [Web アプリケーションとスクリプトのデバッグ](../debugger/debugging-web-applications-and-script.md)   
 [方法 : .NET アプリケーションのデバッグを有効にする](../debugger/how-to-enable-debugging-for-aspnet-applications.md)   
 [方法 : ASP.NET プロセスの名前を見つける](../debugger/how-to-find-the-name-of-the-aspnet-process.md)   
 [シンボルとソース コードの管理](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)