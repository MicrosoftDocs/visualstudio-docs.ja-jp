---
layout: LandingPage
title: アプリのデバッグ | Microsoft Docs
description: Visual Studio を使用して、ご使用のプラットフォームとデバイス向けに任意の言語でアプリケーション、サービス、ツールをデバッグする方法について説明します。
ms.custom: seodec18
ms.topic: landing-page
ms.author: mikejo
author: mikejo5000
manager: jillfra
ms.openlocfilehash: f3bf5cc1dd11e0062ca849f16fb806fa756e2203
ms.sourcegitcommit: 3d37c2460584f6c61769be70ef29c1a67397cf14
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2019
ms.locfileid: "58322078"
---
# <a name="debugging-in-visual-studio"></a>Visual Studio でのデバッグ

Visual Studio デバッガーを使用すると、プログラムの実行時の動作を確認し、問題を見つけることができます。 デバッガーは、すべての Visual Studio のプログラミング言語と関連ライブラリと連携します。 デバッガーを使ってプログラムの実行を中断し、コードのチェック、変数のチェックと編集、レジスタの確認、ソース コードで作成された命令の表示、アプリケーションで使用するメモリ空間の確認などができます。

<!-- markdownlint-disable MD033 -->

<ul class="panelContent cardsFTitle">
    <li>
        <a href="https://docs.microsoft.com/visualstudio/debugger/what-is-debugging">
            <div class="cardSize">
                <div class="cardPadding">
                    <div class="card">
                        <div class="cardImageOuter">
                            <div class="cardImage">
                                <img src="https://docs.microsoft.com/media/common/i_categorize.svg" alt="What is debugging?">
                            </div>
                        </div>
                        <div class="cardText">
                            <h3>デバッグとは</h3>
                        </div>
                    </div>
                </div>
            </div>
        </a>
    </li>
    <li>
        <a href="https://docs.microsoft.com/visualstudio/debugger/write-better-code-with-visual-studio">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="https://docs.microsoft.com/media/common/i_code-quality.svg" alt="Write better code">
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>デバッグの技術とツール</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
</ul>

<h2>デバッガーの使用開始</h2>

<ul class="panelContent cardsFTitle">
    <li>
        <a href="https://docs.microsoft.com/visualstudio/debugger/debugger-feature-tour">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="https://docs.microsoft.com/media/common/i_road-map.svg" alt="Road map">
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>デバッガーの機能を確認する</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="https://docs.microsoft.com/visualstudio/debugger/debugging-absolute-beginners">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="https://docs.microsoft.com/media/common/i_get-started.svg" alt="Absolute beginners">
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>初心者向けガイド</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="https://docs.microsoft.com/visualstudio/get-started/csharp/tutorial-debugger?toc=/visualstudio/debugger/toc.json">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="https://docs.microsoft.com/media/logos/logo_csharp.svg" alt="C#">
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>C# アプリをデバッグする</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="https://docs.microsoft.com/visualstudio/debugger/getting-started-with-the-debugger-cpp">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="https://docs.microsoft.com/media/logos/logo_Cplusplus.svg" alt="C++">
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>C++ アプリをデバッグする</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="https://docs.microsoft.com/visualstudio/get-started/visual-basic/tutorial-debugger?toc=/visualstudio/debugger/toc.json">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="https://docs.microsoft.com/media/logos/logo_vb.svg" alt="VB">
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Visual Basic アプリをデバッグする</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
</ul>

<h2>デバッガーを詳しく理解する</h2>

<ul class="panelContent cardsFTitle">
    <li>
        <a href="https://docs.microsoft.com/visualstudio/debugger/using-breakpoints">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="https://docs.microsoft.com/media/common/i_investigate.svg" alt="Use breakpoints">
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>ブレークポイントについて詳しく学ぶ</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="https://docs.microsoft.com/visualstudio/debugger/debugger-tips-and-tricks">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="https://docs.microsoft.com/media/common/i_debug.svg" alt="Tips and tricks">
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>デバッガーのヒントと秘訣</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="https://docs.microsoft.com/visualstudio/debugger/view-historical-application-state">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="https://docs.microsoft.com/media/common/i_investigate.svg" alt="View historical app state">
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>以前のアプリの状態を検査する (Visual Studio Enterprise)</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="https://docs.microsoft.com/visualstudio/debugger/debug-live-azure-applications">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="https://docs.microsoft.com/media/logos/logo_azure.svg" alt="Azure">
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Azure App Service アプリケーションのライブ デバッグ</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
</ul>

<hr>
<h2>参照</h2>

<ul class="panelContent cardsW">
    <li>
        <a href="/visualstudio/debugger/api-reference-for-intellitrace-extensibility">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardText">
                        <h3>IntelliTrace リファレンス</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="https://docs.microsoft.com/visualstudio/debugger/debug-interface-access/debug-interface-access-sdk">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardText">
                        <h3>Debug Interface Access SDK</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="https://docs.microsoft.com/visualstudio/debugger/spy-increment-help">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardText">
                        <h3>Spy++</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
    <li>
        <a href="https://docs.microsoft.com/visualstudio/mac/debugging">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardText">
                        <h3>デバッグ (Visual Studio for Mac)</h3>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li>
</ul>

---
