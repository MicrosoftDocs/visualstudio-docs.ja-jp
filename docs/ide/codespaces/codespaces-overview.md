---
title: GitHub Codespaces の概要 (プレビュー)
description: Visual Studio での GitHub Codespaces の詳細と、これを使用して開発環境をクラウドに拡張する方法について説明します。
ms.topic: overview
ms.date: 09/04/2020
author: gregvanl
ms.author: gregvanl
manager: jmartens
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.workload:
- multiple
monikerRange: vs-2019
ms.openlocfilehash: ab50c3c2df2cfad6d489d800f47624503844dc9d
ms.sourcegitcommit: a667ce8394a800906d633737f4fcbc77f0fcba7b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2021
ms.locfileid: "108298744"
---
# <a name="what-is-github-codespaces-preview"></a>GitHub Codespaces とは (プレビュー)

> [!Important]
> 2021 年 4 月 12 日以後は、Visual Studio 2019 から GitHub Codespaces への接続はサポートされなくなります。このプライベート プレビューは終了しています。 Microsoft では、クラウドを利用した内部ループと、さまざまな Visual Studio ワークロードに合わせて最適化された VDI ソリューションの進化し続けるエクスペリエンスに焦点を合わせています。 今後のプレビューとロードマップの情報のために、Visual Studio の[開発者コミュニティ フォーラム](https://developercommunity.visualstudio.com/home)に参加することをお勧めします。

Codespaces へようこそ。 お待ちしておりました。

GitHub Codespaces は、クラウドを利用した開発環境をすべてのアクティビティに対して提供します。これは、長期のプロジェクトである場合も、pull request のレビューのような短期的なタスクである場合もあります。

さらに、GitHub Codespaces は、&mdash;一般的には運用ワークロード用に予約されている&mdash;再現性や信頼性のような多くの DevOps のベネフィットを開発環境にもたらします。 また、任意の必要なツール、プロセス、構成が存在するように、GitHub Codespaces を個人用に設定することもできます。

このドキュメントでは、主要な概念について説明し、Codespaces の機能を紹介します。 作業を開始する方法については、[codespace での Visual Studio の使用](use-visual-studio-with-codespaces.md)に関するページを参照してください。

## <a name="concepts-and-features"></a>概念と機能

GitHub Codespaces の機能は、いくつかの基本的な概念に基づいて構築されています。 このセクションでは、これらの概念について説明し、機能の概要を紹介します。

### <a name="remote-development"></a>リモート開発

最近、多くの開発者が、リモート セットアップまたは特定の開発およびランタイム スタックで構成された VM でコードを書こうとしています。 そのような開発環境をローカルに設定するのは非常に困難で、中断が多く、場合によってはほとんど不可能に近いためです。 また、ユーザーは、日常業務に必要なマシンを "台無しにする" 心配なしに、新しいテクノロジや新しいフレームワークを試したいと考えています。

リモート環境やリモート対応のツールを使用することは、開発者にとって便利ですが、マシン管理のオーバーヘッドが発生することが多くあります。 環境構成では、オンボードとコンテキスト切り替えが複雑になることがよくあります。 GitHub Codespaces は、多くの環境が同時に存在できるようにすることで、迅速なオンボードとコンテキスト切り替えの障壁を排除します。

GitHub Codespaces は、設定よりも生産性向上に専念できる管理ソリューションを提供します。 GitHub Codespaces は、リモート開発用に Visual Studio 2019 を概念的および技術的に拡張します。

### <a name="about-codespaces"></a>codespaces について

codespace は、GitHub Codespaces の "バックエンド" の半分です。 ここでは、ソフトウェア開発に関連するコンパイル、デバッグ、復元などのすべてのコンピューティングが行われます。codespace を作成すると、タスクの完了、pull request のレビュー、新しいプロジェクトの開始に必要なものすべてが準備されます。 codespaces ではプロジェクトでの作業に必要なランタイム、コンパイラ、デバッガー、エディター、カスタム ドットファイル、およびソース コードが構成されます。

クラウドでホストされる codespace には次のようなベネフィットがあります。

- 作成と破棄が高速になります。 必要な数 (アカウント制限まで) が作成され、完了したらそれらが破棄されます。
- 管理されているので、全体的なメンテナンスを削減できます。
- 価格が予測可能であり、料金は使用した分だけになります。 また、組み込みの autosuspend によって、ランナウェイ コストが排除されます。
- コンピューティング リソースが節約されます。 開発ワークロードをクラウドに移行すると、パーソナル マシン上の限られたリソースが解放されます。

## <a name="custom-configuration"></a>カスタム構成

GitHub Codespaces は、幅広いプロジェクトやタスクに対応するように構築されています。 一般的な既定値を提供するスマート構成機能を使用して開始することも、[カスタム構成](customize-codespaces.md)を使用して codespace を微調整することもできます。

柔軟な構成により、開発者は、ローカル コンピューターでは適用するのが困難な、独自の構成と要件を持つプロジェクトに迅速にオンボードできます。 また、再現可能な codespace によって "自分のマシンでは動作する" 問題が排除されます。

## <a name="personal-configuration"></a>個人用の構成

個人設定を維持することは、クラウドでホストされている codespace での開発を馴染みのある、自然なものにするために不可欠です。 GitHub Codespaces では、codespace 構成の上に個別のカスタマイズを行います。 GitHub Codespaces では、エディターとターミナルの個人用設定と構成がサポートされています。

codespace は、[カスタム ドットファイル](https://docs.github.com/github/developing-online-with-codespaces/personalizing-codespaces-for-your-account) (たとえば、`.bashrc`、`.gitconfig` など) のユーザー固有のコレクションを使用して作成できます。また、GitHub Codespaces ではプロジェクト固有の環境機能に関係なく、作成したすべての codespace の外観が希望どおりになるように、Git の ID、テーマ、設定が自動的に同期されます。

## <a name="see-also"></a>関連項目

* [codespace で Visual Studio を使用する方法](use-visual-studio-with-codespaces.md)
* [codespace をカスタマイズする方法](customize-codespaces.md)
* [サポートされている Visual Studio の機能](supported-features-codespaces.md)
