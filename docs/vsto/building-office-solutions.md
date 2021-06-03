---
title: Office ソリューションのビルド
description: Office プロジェクトのビルドとデバッグと、Visual Studio のその他の種類のプロジェクト (Windows フォームなど) のビルドおよびデバッグの違いについて説明します。
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- debugging [Office development in Visual Studio]
- debugging Office applications in Visual Studio
- solutions [Office development in Visual Studio], debugging
- Office applications [Office development in Visual Studio], debugging
- application development [Office development in Visual Studio], building
- Office applications [Office development in Visual Studio], building
- projects [Office development in Visual Studio], debugging
- Office solutions [Office development in Visual Studio], building
- solutions [Office development in Visual Studio], building
- Office projects [Office development in Visual Studio], debugging
- projects [Office development in Visual Studio], building
- builds [Office development in Visual Studio]
- Office projects [Office development in Visual Studio], building
- application development [Office development in Visual Studio], debugging
- Office solutions [Office development in Visual Studio], debugging
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 31cb28ad2c332d0afea9bef8cbe1c979b58536e6
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99896721"
---
# <a name="build-office-solutions"></a>Office ソリューションのビルド
  一般に、Office プロジェクトのビルドとデバッグは、Visual Studio のその他の種類のプロジェクト (Windows フォームなど) のビルドおよびデバッグとほとんど同じです。 このセクションのトピックでは、いくつかある相違点について説明します。 アプリケーションのビルド方法に関する一般的な情報については、「[Visual Studio でのコンパイルとビルド](../ide/compiling-and-building-in-visual-studio.md)」を参照してください。

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="project-output-for-office-projects"></a>Office プロジェクトのプロジェクト出力
 Office プロジェクトは、 *プロジェクト名*\bin\release または *プロジェクト名*\bin\debug に出力されます。 配置ディレクトリにはビルドできません。

### <a name="document-level-projects"></a>ドキュメントレベルのプロジェクト
 ドキュメント レベルのプロジェクトをビルドすると、プロジェクト出力には次の項目が含まれるようになります。

- プロジェクト ドキュメントのコピー。

- プロジェクト アセンブリと、 **［ローカル コピー］** プロパティが **true** に設定されているすべての参照先アセンブリ。

- アプリケーション マニフェスト。ファイル名には *.manifest* というファイル名拡張子が付けられます。 詳細については、「[Office ソリューションのアプリケーション マニフェスト](../vsto/application-manifests-for-office-solutions.md)」を参照してください。

- 配置マニフェスト。ファイル名には *.vsto* というファイル名拡張子が付けられます。 詳細については、「[Office ソリューションの配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)」を参照してください。

- プログラム データベース (*PDB*) ファイル。

> [!NOTE]
> ドキュメント レベルのソリューションを、ローカル コンピューターではなくリモートの場所に作成する場合は、アプリケーションのセキュリティ センターにある信頼できる場所のリストに完全修飾パスを追加します。 詳細については、「[Office ソリューションをセキュリティで保護する](../vsto/securing-office-solutions.md)」の「ドキュメントへの信頼の付与」セクションを参照してください。

### <a name="application-level-projects"></a>アプリケーション レベルのプロジェクト
 VSTO アドイン プロジェクトをビルドすると、次の項目がプロジェクト出力に含まれます。

- プロジェクト アセンブリと、 **［ローカル コピー］** プロパティが **true** に設定されているすべての参照先アセンブリ。

- アプリケーション マニフェスト。ファイル名には *.manifest* というファイル名拡張子が付けられます。 詳細については、「[Office ソリューションのアプリケーション マニフェスト](../vsto/application-manifests-for-office-solutions.md)」を参照してください。

- 配置マニフェスト。ファイル名には *.vsto* というファイル名拡張子が付けられます。 詳細については、「[Office ソリューションの配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)」を参照してください。

- プロジェクト アセンブリのプログラム データベース (*PDB*) ファイル。

  VSTO アドイン プロジェクトのビルド処理により、開発用コンピューターには、VSTO アドインの読み込みに必要な一連のレジストリ エントリも作成されます。 詳細については、「[VSTO アドインのレジストリ エントリ](../vsto/registry-entries-for-vsto-add-ins.md)」を参照してください。

  フォーム領域を含む Outlook VSTO アドイン プロジェクトをビルドすると、ビルド処理により、次に示す情報がレジストリに追加されます。

- 1 つ以上のフォーム領域に関連付けられている各メッセージ クラスのキー。

- 各フォーム領域のエントリと、Outlook VSTO アドインの名前を表す関連値。

  この情報は、Outlook がフォーム領域を読み込むために必要になります。

## <a name="referenced-assemblies"></a>参照アセンブリ
 Office ソリューションのビルド プロジェクトからアセンブリ (クラス ライブラリ プロジェクトを含む) を参照できます。 各参照先アセンブリには、 **［ローカル コピー］** というプロパティがあります。 **［ローカル コピー］** では、アセンブリを出力ディレクトリにコピーするかどうかを指定します。 既定では **true** に設定されています。 **［ローカル コピー］** が **true** に設定されている参照先アセンブリは、すべて出力ディレクトリにコピーされます。

## <a name="security-during-the-build-process"></a>ビルド処理中のセキュリティ
 ビルド処理中、Visual Studio は、ソリューションに信頼を付与するように、開発用コンピューター上のセキュリティ設定を自動的に構成します。 これにより、デバッグしながらソリューションを実行できるようになります。

 Office プロジェクトでは、発行者を確認するために証明書が使用されます。 Visual Studio は、Office ソリューションを識別するための一時的な証明書を自動的に作成し、その一時的な証明書を信頼するように開発コンピューターを構成します。

 詳細については、「[Office ソリューションをセキュリティで保護する](../vsto/securing-office-solutions.md)」を参照してください。

### <a name="network-projects"></a>ネットワーク プロジェクト
 アセンブリまたはドキュメントの場所がネットワーク共有上に存在している場合は、ローカル (User レベル) セキュリティ ポリシーを更新するだけでは、ソリューションを実行できるようになりません。 管理者は、ソリューションの実行前に、コンピューター (Machine) レベルで、ネットワーク共有上のアセンブリとドキュメントに完全な信頼を付与する必要があります。 セキュリティ ポリシーの設定方法の詳細については、「[Office ソリューションをセキュリティで保護する](../vsto/securing-office-solutions.md)」を参照してください。

 ドキュメント レベルのプロジェクトでは、Office の信頼できるフォルダーのリストに、ドキュメントの完全修飾位置を追加する必要もあります。 詳細については、「[ドキュメントへの信頼の付与](../vsto/granting-trust-to-documents.md)」を参照してください。

## <a name="change-the-platform-target"></a>プラットフォーム ターゲットの変更
 既定では、Office プロジェクトのプラットフォーム ターゲットは **Any CPU** です。 通常、この設定を変更する必要はありません。 **Any CPU** プラットフォーム ターゲット設定でビルドされた Officeソリューションは、32 ビット バージョンと 64 ビット バージョンの Microsoft [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] または [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]で実行するようになります。

 64 ビット バージョンの Microsoft [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] または [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]でのみ実行するソリューションを作成していて、そのソリューションからネイティブの 64 ビット API を呼び出す場合は、プラットフォーム ターゲットを x64 に限定して設定する必要があります。 プラットフォームの対象設定変更の詳細については、「[方法: プロジェクトを構成して対象プラットフォームを設定する](../ide/how-to-configure-projects-to-target-platforms.md)」を参照してください。

 プラットフォーム ターゲットを x64 に設定すると、そのソリューションは 32 ビット バージョンの Windows または Office では実行できなくなります。 x64 プラットフォーム ターゲットには、64 ビット プロセスで実行するソリューションが必要になります。

## <a name="use-the-clean-command"></a>[クリーン] コマンドの使用
 開発用コンピューターからビルド済みのプロジェクト ファイルを削除する場合は、 **の** [ビルド] **メニューにある** [クリーン] [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]コマンドを使用できます。 **[クリーン]** コマンドにより、ビルドの出力場所にあるファイルがすべて削除されます。 アプリケーション レベルのプロジェクトの場合は、 **[クリーン]** コマンドによって、ビルド処理で作成されたレジストリ エントリも削除されます。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[Office プロジェクトのデバッグ](../vsto/debugging-office-projects.md)|Office プロジェクトのデバッグに関する問題について説明します。|
|[チュートリアル: Excel のドキュメント レベルのカスタマイズを初めて作成する](../vsto/walkthrough-creating-your-first-document-level-customization-for-excel.md)|Excel 用の基本的なドキュメント レベルのカスタマイズを作成する方法を示します。|
|[方法: 無効にされた VSTO アドインを再度有効にする](../vsto/how-to-re-enable-a-vsto-add-in-that-has-been-disabled.md)|ハードまたはソフトに無効化されている VSTO アドインを再度有効化する方法について説明します。|
|[Office ソリューションを設計して作成する](../vsto/designing-and-creating-office-solutions.md)|Office ソリューションの作成に関する情報と、ソリューション内のアセンブリの役割に関する情報へのリンクが掲載されています。|