---
title: JavaScript および TypeScript
description: Visual Studio for Mac の JavaScript サポートに関する情報
author: heiligerdankgesang
ms.author: dominicn
ms.date: 05/03/2018
ms.technology: vs-ide-general
ms.assetid: 61432695-5B12-4257-B250-48D37EED106D
ms.openlocfilehash: 5f1a400506f7766ba22ffbc1debde687b1709a21
ms.sourcegitcommit: 01a411cd7ae3488b7b979a947bca92fd296a98e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760927"
---
# <a name="javascript-and-typescript-support"></a>JavaScript および TypeScript のサポート

Visual Studio for Mac では、構文の強調表示、コードの書式設定、IntelliSense で JavaScript と TypeScript を利用できます。

![TypeScript エディター サポート](/visualstudio/mac/media/tsjseditor-2019.gif)

JavaScript のコード記述に関する詳細については、[JavaScript でのコードの記述](/scripting/javascript/writing-javascript-code)に関するガイドを参照してください。

## <a name="adding-a-javascript-file"></a>JavaScript ファイルの追加

JavaScript ファイルはほとんどの場合、**[新しいファイル]** ダイアログから ASP.NET Core プロジェクトに追加されます。 JavaScript ファイルを追加するには、プロジェクトを右クリックし、**[追加]、[新しいファイル]** の順に進みます。

![プロジェクトに新しいファイルを追加する](media/javascript-image1.png)

**[新しいファイル]** ダイアログから、**[Web]、[Empty JS file]\(空の JS ファイル\)** の順に選択するか、**[Web]、[TypeScript ファイル]** の順に選択します。 名前を付けて **[新規]** を選択します。

![テンプレートから新しい TypeScript ファイルを作成する](media/javascript-image2.png)

## <a name="intellisense"></a>IntelliSense

Visual Studio for Mac は [JavaScript Language Service](/visualstudio/ide/javascript-intellisense) を使用して Intellisense を提供しています。これにより、コードの記述時に、インテリジェントなコード補完、パラメーター情報、メンバー リストが提供されます。

Visual Studio for Mac の JavaScript IntelliSense は、型の推定、JSDoc、または TypeScript 宣言に基づくことができます。

- **型の推定** - コードの前後関係からオブジェクトの型を割り出します。 詳細については、「[型推論に基づく IntelliSense](/visualstudio/ide/javascript-intellisense#intellisense-based-on-type-inference)」の Visual Studio セクションを参照してください。
- **JSDoc** - 型の推定では正しい型情報が与えられないことがあります。 そのような場合、型情報は [JSDoc](https://jsdoc.app/about-getting-started.html) 注釈によって明示的に指定できます。 詳細については、Visual Studio の [JSDoc に基づいた IntelliSense](/visualstudio/ide/javascript-intellisense#intellisense-based-on-jsdoc) に関するセクションを参照してください。
- **TypeScript 宣言ファイル** - `.d.ts` ファイルを利用し、JavaScript IntelliSense の値が与えられます。 そのファイルに宣言されている型を JSDoc コメントで型として使用できます。 詳細については、「[TypeScript 宣言ファイルに基づく IntelliSense](/visualstudio/ide/javascript-intellisense#intellisense-based-on-typescript-declaration-files)」の Visual Studio のセクションを参照してください。

    ![TypeScript 定義ファイルの追加](media/javascript-image3.png)

## <a name="see-also"></a>関連項目

- [JavaScript IntelliSense (Windows の Visual Studio)](/visualstudio/ide/javascript-intellisense)
