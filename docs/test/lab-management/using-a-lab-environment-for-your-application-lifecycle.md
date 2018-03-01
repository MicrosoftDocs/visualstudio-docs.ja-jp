---
title: "DevOps でラボ環境を使用する |Microsoft ドキュメント"
ms.custom: 
ms.date: 05/02/2017
ms.reviewer: 
ms.suite: 
ms.technology: vs-devops-test
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- lab environment, test lab
ms.author: gewarren
manager: ghogen
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: 227068197de1d953ae6f3729888a1b6d2dfc164c
ms.sourcegitcommit: 7ae502c5767a34dc35e760ff02032f4902c7c02b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/09/2018
---
# <a name="use-a-lab-environment-for-your-devops"></a>DevOps でラボ環境を使用する

ラボ環境は、アプリケーションの開発およびテストに使用できる仮想マシンと物理マシンのコレクションです。 ラボ環境には、ワークステーション、Web サーバー、データベース サーバーなど、多層アプリケーションのテストに必要な複数のロールを含めることができます。 さらに、ラボ環境でビルド、配置、テストのワークフローを使用して、アプリケーションでの自動テストのビルド、配置、および実行のプロセスを自動化できます。

* **テスト計画を使用して自動テストを実行する** - *テスト計画*と呼ばれる自動テストのコレクションを実行し、進行状況を確認できます。  
  
* **ビルド、配置、テストのワークフローを使用する**- ビルド、配置、テストのワークフローを使用して、多層アプリケーションを自動的にテストできます。 代表的な例としては、ビルドを開始し、ビルド ファイルをラボ環境内の適切なコンピューター上に配置して、自動テストを実行するというワークフローがあります。 また、特定の間隔で実行するようワークフローをスケジュールできます。  
  
* **手動のテスト中でも、すべてのコンピューターから診断データを収集する** - 複数のコンピューターから同時に診断データを収集できます。 たとえば 1 回のテスト実行で、IntelliTrace、テストの影響、および Web サーバー、データベース サーバー、クライアントの他の形式のデータを収集できます。  
  
次に、ラボ環境の一般的なタイプの例を示します。  
  
| トポロジ | 説明 |  
|---|---|  
|![サーバーのみのトポロジ](../media/topology_backend.png)| このラボ環境は*サーバー トポロジ*を備えています。これは、サーバー アプリケーションで手動テストを実行するためによく使用されます。また、これにより、テスト担当者は自身のクライアント コンピューターを使用して環境内のバグを検証することができます。 バックエンド トポロジでは、ラボ環境にはサーバーのみが含まれています。 このタイプのトポロジを使用するば場合、一般的には、環境に含まれていないクライアント コンピューターを使用してラボ環境内のサーバーに接続します。|  
|![クラウドのラボ環境](../media/topology_cloud.png)| このラボ環境は、_サーバー トポロジ_と同様に機能します。ローカルで物理または仮想マシンを実行する必要がないため、設定に費やす時間を減らせ、メンテナンスが簡単になり、コストを抑えことができます。 Microsoft Azure などのクラウド環境には、複数の Web サイトや仮想マシンをカスタム ネットワークで早く簡単に構成できます。 詳細については、[こちら](#usebandrm)を参照してください。|  
|![クライアント サーバーのラボ環境](../media/topology_clientserver.png)| このラボ環境は、*クライアント/サーバー トポロジ*を備えています。これはサーバーとクライアントのコンポーネントを備えたアプリケーションをテストするために、よく使用されます。 クライアント/サーバー トポロジでは、アプリケーションのテストに使用されるクライアントとサーバーのすべてのコンピューターはラボ環境内にあります。 このトポロジを使用すると、テストに影響を与える各コンピューターからテスト データを収集することができます。|  
  
「[ビデオ: テスト用のラボ環境の管理](http://go.microsoft.com/fwlink/?LinkID=252614)」を参照してください。  
  
ラボ環境を設定する標準的な方法は次のとおりです。 
  
* **[Team Services や Team Foundation Server ビルドとリリース](#usebandrm)をクラウドと共に使用する**

* **[Microsoft Test Manager の Visual Studio Lab Management 機能を使用する](#usemtmlm)**

<a name="usebandrm"></a>
## <a name="use-the-cloud-with-team-services-or-team-foundation-server-build-amp-release"></a>Team Services や Team Foundation Server ビルドとリリースをクラウドと共に使用する

Team Foundation Server (TFS) および Visual Studio Team Services の[ビルドとリリース](https://www.visualstudio.com/team-services/continuous-integration/)機能を使用すると、自動テストと、ビルド、配置、テストの自動化を実行できます。 いくつかの利点を次に示します。

* ビルド コントローラーまたはテスト コントローラーが不要です。
* テスト エージェントはビルドまたはリリースの一部としてタスクでインストールされます。
* 配置の手順を簡単にカスタマイズできます。 1 つのスクリプトの使用のみに限定されなくなります。 この製品および Visual Studio Marketplace で使用可能な多数のタスクも利用できます。
* テスト スイートを維持する必要がありません。 バイナリから直接テストを実行できます。
* 各ビルドまたはリリース内で実行されたテストのより充実したインライン レポートを得ることができます。
* 各環境に現在配置され、テストされている資産 (リリース、ビルド、作業項目、コミット) を追跡できます。
* 自動化をカスタマイズして拡張し、複数のテスト環境や運用環境にも簡単に展開できるようになります。
* 自動化は、チェックインやコミットがあった場合、または特定の時刻に毎日行われるようスケジュールできます。

詳細については、[こちら](use-build-or-rm-instead-of-lab-management.md)を参照してください。

<a name="usemtmlm"></a>
## <a name="use-the-visual-studio-lab-management-features-of-microsoft-test-manager"></a>Microsoft Test Manager の Visual Studio Lab Management 機能を使用する

Visual Studio Enterprise または Visual Studio Test Professional を使用するとき、Microsoft Test Manager の Visual Studio Lab Management 機能を使用してラボ環境を作成および管理できます。

Lab Management は、環境内のすべてのコンピューターにテスト エージェントを自動的にインストールします。  
  
Lab Management を System Center Virtual Machine Manager (SCVMM) と共に使用すると、ラボ環境を使用したときに次のような利点も得られます。  
  
* **コンピューターの構成を迅速に再現する** - 一般的な稼動環境を再作成するために構成されている仮想マシンのコレクションを格納することができます。 格納済み環境の新しいコピーで、各テスト実行を行うことができます。  
  
* **バグの正確な状況を再現する** - テスト実行が失敗した場合、ラボ環境の状態のコピーを格納し、ビルドの結果または作業項目からアクセスすることができます。  
  
* **ラボ環境の複数のコピーを同時に実行する** - ラボ環境の複数のコピーを同時に実行することができます。  
  
### <a name="standard-environments-and-scvmm-environments"></a>標準の環境および SCVMM 環境

Visual Studio Lab Management で作成できるラボ環境には、**標準環境**と **SCVMM 環境**の 2 つのタイプがあります。
ただし、それぞれのタイプの環境の機能は異なります。  
  
> **注**: Lab Management では、SCVMM 2016 はサポート**していません**。 SCVMM の詳細については、「[Virtual Machine Manager](http://go.microsoft.com/fwlink/?LinkId=226332)」を参照してください。 
  
**標準環境:** 標準環境には、仮想マシンと物理マシンを混在させることができます。 また、サードパーティの仮想フレームワークで管理されている標準環境に、仮想マシンを追加することもできます。 標準環境では、SCVMM サーバーなどの追加のサーバー リソースは必要ありません。  
  
**SCVMM 環境:** SCVMM 環境には、SCVMM (System Center Virtual Machine Manager) で管理されている仮想マシンのみ含めることができるため、SCVMM 環境内の仮想マシンは、Hyper-V の仮想フレームワークでのみ実行できます。 ただし SCVMM 環境には、標準環境では使用できない、次の自動機能および管理機能が用意されています。  
  
- **環境スナップショット:** 環境スナップショットには、ラボ環境の状態が含まれているため、クリーンな環境へすぐに復元したり、変更した環境の状態を保存したりできます。 また、ビルド、配置、テストのワークフローを使用して、環境スナップショットの保存および復元のプロセスを自動化することもできます。  
  
- **格納された環境:** SCVMM 環境のコピーを格納して、環境の複数のコピーを配置することができます。  
  
- **ネットワークの分離:** ネットワークの分離により、1 つの SCVMM 環境の同一のコピーを、コンピューター名が競合することなく複数同時に実行することができます。  
  
- **仮想マシンのテンプレート:** 仮想マシンのテンプレートは、名前とその他の識別子を削除した仮想マシン テンプレートです。 VM テンプレートが SCVMM 環境に配置されると、Microsoft Test Manager は新しい識別子を生成します。 これにより、同じ環境、または複数の環境内に仮想マシンの複数のコピーを配置し、それらの仮想マシンを同時に実行することができます。  
  
- **格納された仮想マシン:** Team Project ライブラリに格納され、一意の識別子を持っている仮想マシン。  
  
これらの機能の詳細については、「[SCVMM 環境の作成および管理に関するガイダンス](https://msdn.microsoft.com/en-gb/library/ee830480.aspx)」を参照してください。  
  
標準環境および SCVMM 環境は、多数の同じ機能をサポートしています。 ただし、考慮すべき重要な違いがいくつかあります。 以下の表では、標準環境と SCVMM 環境で使用できる機能について比較しています。  
  
|機能|SCVMM 環境|標準環境|  
|----------------|------------------------|---------------------------|  
|**テスト**|||  
|手動テストの実行|サポート状況|サポート状況|  
|コード化された UI およびその他の自動テストの実行|サポート状況|サポート状況|  
|診断アダプターを使用してリッチ バグをファイルする|サポート状況|サポート状況|  
|**ビルドの配置**|||  
|自動化されているビルド、配置、テストのワークフロー|サポート状況|サポート状況|  
|**環境の作成と管理**|||  
|仮想マシンの他に物理マシンを使用する|サポートなし|サポート状況|  
|サードパーティの仮想マシンを使用する|サポートなし|サポート状況|  
|ラボ環境内のコンピューターにテスト エージェントを自動的にインストールする|サポート状況|サポート状況|  
|環境スナップショットを使用してラボ環境の状態を保存および配置する|サポート状況|サポートなし|  
|VM テンプレートからラボ環境を作成する|サポート状況|サポートなし|  
|環境の開始/停止/スナップショット作成を実行する|サポート状況|サポートなし|  
|環境ビューアーを使用して環境に接続する|サポート状況|サポート状況|  
|ネットワークの分離を使用して環境の複数のコピーを同時に実行する|サポート状況|サポートなし|  
  
### <a name="lab-management-concepts"></a>ラボ管理の概念

ここから先へ進む前に、次の概念についても理解しておく必要があります。  
  
|用語|説明|  
|----------|-----------------|  
|ラボ センター|ラボ環境を作成および管理する Microsoft Test Manager の領域。|  
|チーム プロジェクト ラボ|セットアップされたラボ環境のコレクションで、これらの環境に対して仮想マシンを接続して実行することができます。|  
|チーム プロジェクト ライブラリ|格納された仮想マシン、テンプレート、および格納されたラボ環境のアーカイブで、チーム プロジェクトのホスト グループにインポートされています。 SCVMM 環境でライブラリ内のアイテムを使用できますが、これらのアイテムを標準環境へ直接追加することはできません。 ライブラリ内のアイテムは実行できません。代わりに、新しい環境へアイテムを配置して使用します。|  
|配置されている環境|チーム プロジェクト ラボに配置されているラボ環境。この環境に接続してコンピューターを実行することができます。|  

#### <a name="related-topics"></a>関連トピック

* [ラボを計画する](https://msdn.microsoft.com/library/ff756575%28v=vs.140%29.aspx) 
* [ラボを管理する](https://msdn.microsoft.com/library/dd936084%28v=vs.140%29.aspx) 
* [SCVMM 環境用の設定を行う](https://msdn.microsoft.com/library/dd380687%28v=vs.140%29.aspx) 
* [SCVMM 2008 R2 から SCVMM 2012 へのアップグレード](upgrade-scvmm-2008-r2-scvmm-2012.md) 
* [アクセス許可を管理する](https://msdn.microsoft.com/library/dd380760%28v=vs.140%29.aspx) 
* [構成を変更する](https://msdn.microsoft.com/library/ee704508%28v=vs.140%29.aspx) 
* [トラブルシューティング](https://msdn.microsoft.com/library/ee853230%28v=vs.140%29.aspx)
  
### <a name="set-up-environments"></a>環境を設定する

* [ビルドとリリース クラウド環境](use-build-or-rm-instead-of-lab-management.md)
* [標準ラボ環境](https://msdn.microsoft.com/en-gb/library/ee390842.aspx)
* [SCVMM (仮想) 環境](https://msdn.microsoft.com/en-gb/library/ee943322.aspx)
* [ネットワーク分離環境の作成および使用](https://msdn.microsoft.com/en-gb/library/ee518924.aspx)
  
## <a name="see-also"></a>関連項目
  
* [テスト エージェントをインストールして構成する](install-configure-test-agents.md)
* [Visual Studio Lab Management Guide (Visual Studio ラボ管理ガイド)](http://go.microsoft.com/fwlink/?LinkID=230951)  
* [テスト用のラボ環境の管理](http://go.microsoft.com/fwlink/?LinkID=252614)  
* [Visual Studio devops + Team Foundation Server のブログ](http://go.microsoft.com/fwlink/?LinkID=254496)  
