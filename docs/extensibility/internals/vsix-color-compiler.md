---
title: VSIX カラー コンパイラ | Microsoft Docs
description: Visual Studio 拡張機能のカラー コンパイラ ツールについて説明します。これは、Visual Studio のテーマの色を .pkgdef ファイルに変換するコンソール アプリケーションです。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 99395da7-ec34-491d-9baa-0590d23283ce
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2f7277299d3cedd2ea0db49a44109d8a0441ebd0
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901761"
---
# <a name="vsix-color-compiler"></a>VSIX カラー コンパイラ
Visual Studio 拡張機能のカラー コンパイラ ツールは、既存の Visual Studio テーマの色を表す .xml ファイルを取得し、それを .pkgdef ファイルに変換することで、それらの色を Visual Studio で使用できるようにするコンソール アプリケーションです。 .xml ファイル間の違いを簡単に比較できるため、このツールは、カスタム カラーをソース管理で管理するために役立ちます。 また、ビルド環境にフックして、ビルドの出力を有効な .pkgdef ファイルにすることもできます。

 **テーマ XML スキーマ**

 完全なテーマ .xml ファイルは次のようになります。

```xml
<Themes>
      <!—one or Theme elements -->
      <Theme>
        <!-- one or more Category elements -->
        <Category>
          <!-- one or more Color elements -->
          <Color>
            <!-- zero or one Background element -->
            <Background />
            <!-- zero or one Foreground element -->
            <Foreground />
          </Color>
        </Category>
      </Theme>
</Themes>
```

 **テーマ**

 \<Theme> 要素ではテーマ全体が定義されます。 1 つのテーマには少なくとも 1 つの \<Category> 要素が必要です。 テーマの要素は次のように定義されます。

```xml
<Theme Name="name" GUID="guid">
      <!-- one or more Category elements -->
</Theme>
```

|**属性**|**定義**|
|-|-|
|名前|[必須] テーマの名前|
|GUID|[必須] テーマの GUID (GUID 書式設定と一致する必要があります)|

 Visual Studio でカスタム カラーを作成するとき、次のテーマに対してそれらの色を定義する必要があります。 特定のテーマの色が存在しない場合、Visual Studio は、不足している色をライト テーマから読み込もうとします。

|**テーマ名**|**テーマ GUID**|
|-|-|
|白|{de3dbbcd-f642-433c-8353-8f1df4370aba}|
|黒|{1ded0138-47ce-435e-84ef-9ec1f439b749}|
|青|{a4d6a176-b948-4b29-8c66-53c97a1ed7d0}|
|ハイコントラスト|{a4d6a176-b948-4b29-8c66-53c97a1ed7d0}|

 **カテゴリ**

 \<Category> 要素では、テーマの色のコレクションが定義されます。 カテゴリ名によって論理的なグループ化が提供されます。できるだけ狭義に定義する必要があります。 1 つのカテゴリには少なくとも 1 つの \<Color> 要素を含める必要があります。 カテゴリの要素は次のように定義されます。

```xml
<Category Name="name" GUID="guid">
      <!-- one or more Color elements -->
 </Category>
```

|**属性**|**定義**|
|-|-|
|名前|[必須] カテゴリの名前|
|GUID|[必須] カテゴリの GUID (GUID 書式設定と一致する必要があります)|

 **色**

 \<Color> 要素では、コンポーネントの色すわなち UI の状態が定義されます。 お勧めする色の名前付けスキームは、[UI の種類] [状態] です。 冗長になるため "color" という語を使用しないでください。 色は、要素の種類と、その色が適用される状況 ("状態") を明確に示す必要があります。 色を空にすることはできません。\<Background> 要素と \<Foreground> 要素のいずれかまたは両方を含む必要があります。 色の要素は次のように定義されます。

```xml
<Color Name="name">
        <Background /> <!-- zero or one Background element -->
        <Foreground /> <!-- zero or one Foreground element -->
 </Color>
```

|**属性**|**定義**|
|-|-|
|名前|[必須] 色の名前|

 **背景または前景 (あるいは両方)**

 \<Background> 要素および \<Foreground> 要素では、UI 要素の背景または前景の色の値と種類が定義されます。 これらの要素には子はありません。

```xml
<Background Type="type" Source="int" />
<Foreground Type="type" Source="int" />
```

|**属性**|**定義**|
|-|-|
|Type|[必須] 色の種類。 次のいずれかを指定できます。<br /><br /> *CT_INVALID:* 色が無効か設定されていません。<br /><br /> *CT_RAW:* 未処理の ARGB 値。<br /><br /> *CT_COLORINDEX:* 使用しないでください。<br /><br /> *CT_SYSCOLOR:* SysColor の Windows システム色。<br /><br /> *CT_VSCOLOR:* __VSSYSCOLOREX の Visual Studio 色。<br /><br /> *CT_AUTOMATIC:* 自動色。<br /><br /> *CT_TRACK_FOREGROUND:* 使用しないでください。<br /><br /> *CT_TRACK_BACKGROUND:* 使用しないでください。|
|source|[必要] 16 進数で表される色の値|

 __VSCOLORTYPE 列挙でサポートされるすべての値は、スキーマによって Type 属性でサポートされます。 ただし、CT_RAW と CT_SYSCOLOR のみを使用することをお勧めします。

 **まとめ**

 有効なテーマ .xml ファイルの単純な例を次に示します。

```xml
<Themes>
  <Theme Name="Light" GUID="{de3dbbcd-f642-433c-8353-8f1df4370aba}">
    <Category Name="MyCategory" GUID="{0A96238B-70CE-4479-9170-EECEAA3FCD58}">
      <Color Name="MyActiveBorder">
        <Background Type="CT_RAW" Source="FFCCCEDB" />
      </Color>
    </Category>
  </Theme>
</Themes>
```

## <a name="how-to-use-the-tool"></a>ツールの使用方法
 **構文**

 VsixColorCompiler \<XML file> \<PkgDef file> \<Optional Args>

 **引数**

|**スイッチ名**|**ノート**|**必須または省略可能**|
|-|-|-|
|名前なし (.xml ファイル)|これは最初の名前のないパラメーターで、変換する XML ファイルへのパスです。|必須|
|名前なし (.pkgdef ファイル)|これは 2 番目の名前のないパラメーターで、生成される .pkgdef ファイルの出力パスです。<br /><br /> 既定値: \<XML Filename>.pkgdef|省略可能|
|/noLogo|このフラグを設定すると、製品および著作権情報は出力されなくなります。|オプション|
|/?|ヘルプ情報を出力します。|オプション|
|/help|ヘルプ情報を出力します。|オプション|

 **例**

- VsixColorCompiler D:\xml\colors.xml D:\pkgdef\colors.pkgdef

- VsixColorCompiler D:\xml\colors.xml /noLogo

## <a name="notes"></a>メモ

- このツールでは、最新バージョンの VC++ ランタイムがインストールされている必要があります。

- 単一のファイルのみがサポートされます。 フォルダー パスを使用した一括変換はサポートされていません。

- ツールは `<VS Install Path>\VSSDK\VisualStudioIntegration\Tools\Bin\` にあります

## <a name="sample-output"></a>サンプル出力
 ツールによって生成される .pkgdef ファイルは次のキーのようになります。

```
[$RootKey$\Themes\{de3dbbcd-f642-433c-8353-8f1df4370aba}\Environment]
"Data"=hex:3a,00,00,00,0b,00,00,00,01,00,00,00,c3,d9,4e,62,fd,bd,fa,41,96,c3,7c,82,4e,a3,2e,3d,01,00,00,00,0c,00,00,00,41,63,74,69,76,65,42,6f,72,64,65,72,01,cc,ce,db,ff,01,33,31,24,ff

[$RootKey$\Themes\{de3dbbcd-f642-433c-8353-8f1df4370aba}\TreeView]
"Data"=hex:38,00,00,00,0b,00,00,00,01,00,00,00,8e,f0,ec,92,13,8b,f4,4c,99,e9,ae,26,92,38,21,85,01,00,00,00,0a,00,00,00,42,61,63,6b,67,72,6f,75,6e,64,01,f5,f5,f5,ff,01,1e,1e,1e,ff
```
