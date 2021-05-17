---
title: 従来の言語サービスの登録 2 | Microsoft Docs
description: この記事では、Visual Studio で使用できるさまざまな言語サービス オプションのレジストリ エントリを一覧表示します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- registration, language services
- language services, registry information
- registry, language services
ms.assetid: ca312aa3-f9f1-4572-8553-89bf3a724deb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fbad469b28c0b8a6aab070d47cf12c326beb92d8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062786"
---
# <a name="registering-a-legacy-language-service-2"></a>従来の言語サービスの登録 2
以下のセクションでは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] で使用できるさまざまな言語サービス オプションのレジストリ エントリのリストを示します。

 次のレジストリ エントリのリストでは、*VS Reg Root* は HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\*X.Y* と等しくなります。ここで、*X.Y* は [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] バージョン番号です。

## <a name="registry-entries-for-language-service-options"></a>言語サービス オプションのレジストリ エントリ
 *VS Reg Root*\Languages\Language Services\\*Language Name* キーには、次の値を含められます。

|名前|Type|Range|説明|
|----------|----------|-----------|-----------------|
|(既定値)。|REG_SZ|*\<GUID>*|言語サービスの GUID。|
|LangResID|REG_DWORD|0x0 - 0xffff|言語のローカライズされたテキスト名の文字列リソース識別子 (ResID)。|
|パッケージ|REG_SZ|*\<GUID>*|VSPackage の GUID。|
|ShowCompletion|REG_DWORD|0-1|**[オプション]** ダイアログ ボックスの **[ステートメント入力候補]** オプションを有効にするかどうかを指定します。|
|ShowSmartIndent|REG_DWORD|0-1|**[オプション**] ダイアログ ボックスで **[スマート]** インデントを選択するオプションを有効にするかどうかを指定します。|
|RequestStockColors|REG_DWORD|0-1|キーワードに色を付けるために、カスタム色と既定の色のどちらを使用するかを指定します。|
|ShowHotURLs|REG_DWORD|0-1|ユーザーが URL をクリックできるかどうかを指定します。|
|Default to Non Hot URLs|REG_DWORD|0-1|**[オプション]** ダイアログ ボックスの **[シングル クリックでの URL ナビゲーションを有効にする]** オプションの初期設定を指定します。|
|DefaultToInsertSpaces|REG_DWORD|0-1|言語サービスの既定のタブ オプションとして "空白の挿入" があるかどうかを指定します。|
|ShowDropdownBarOption|REG_DWORD|0-1|**ナビゲーション バー** を表示または非表示にする **[オプション]** ダイアログ ボックスの **[ナビゲーション バー]** オプションを有効または無効にします。|
|Single Code Window Only|REG_DWORD|0-1|言語サービスの **[ウィンドウ]** メニューの **[新しいウィンドウ]** の選択肢を有効または無効にします。|
|EnableAdvancedMembersOption|REG_DWORD|0-1|**[メンバーの詳細を非表示]** の **[オプション]** ダイアログ ボックスの設定を有効または無効にします。|
|Support CF_HTML|REG_DWORD|0-1|エディターで HTML データのコピーと貼り付けを有効にするかどうかを指定します。|
|EnableLineNumbersOption|REG_DWORD|0-1|言語サービスで **[オプション]** ダイアログ ボックスの **[行番号]** オプションを有効にするかどうかを指定します。|
|HideAdvancedMembersByDefault|REG_DWORD|0-1|プライベート フィールドなどの高度なメンバーを入力候補リストで非表示にするかどうかを指定します。|
|ShowBraceCompletion|REG_DWORD|0-1|**[オプション]** ダイアログ ボックスの **[かっこの入力補完]** オプションを有効にするかどうかを指定します。|

### <a name="example"></a>例

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\
  Languages\
    Language Services\
      C/C++\
        (Default)             = reg_sz:{B2F072B0-ABC1-11D0-9D62-00C04FD9DFD9}
        LangResID             = reg_dword:0x00000000
        Package               = reg_sz:{8C2EA640-ABC1-11D0-9D62-00C04FD9DFD9}
        ShowCompletion        = reg_dword:0x00000001
        ShowSmartIndent       = reg_dword:0x00000001
        ShowDropdownBarOption = reg_dword:0x00000001
```

## <a name="registry-entries-for-debugger-languages-options"></a>デバッガー言語オプションのレジストリ エントリ
 The *VS Reg Root*\Languages\Language Services\\*Language Name*\Debugger Languages\\*GUID*\ キーには、次の値を含められます。

|名前|Type|Range|説明|
|----------|----------|-----------|-----------------|
|(既定値)。|REG_SZ|text|既定値を使用して、言語の名前を記録できます。 このキーの名前は、式エバリュエーターの GUID であり、 *\<VS Reg Root>* \AD7Metrics\Expression Evaluator に対応するエントリが含まれています。|

### <a name="example"></a>例

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\
  Languages\
    Language Services\
      C/C++\
        Debugger Languages\
          {3A12D0B7-C26C-11D0-B442-00A0244A1DD2}\
            (Default) = reg_sz:C++
```

## <a name="registry-entries-for-editor-tools-options"></a>エディター ツール オプションのレジストリ エントリ
 プロパティ ページとプロパティ ノードの EditorToolsOptions キーの下にレジストリ キーを追加できます。 これらのキーとその値により、言語サービスを構成するために使用される **[オプション]** ダイアログ ボックス ( **[ツール]** メニュー上) のプロパティ ページが識別されます。 次の例では、*Page Name* はプロパティ ページの名前であり、*Node Name* は **[オプション]** ダイアログ ボックスのツリー内のノードの名前です。 ページ エントリとノード エントリを別々に指定する必要があります。

|名前|Type|Range|説明|
|----------|----------|-----------|-----------------|
|(既定値)。|REG_SZ|ResID|このオプション ページのローカライズされた表示名。 名前には、リテラル テキストか # `nnn` を指定できます。ここで、`nnn` は、指定された VSPackage のサテライト DLL 内の文字列リソース ID です。|
|パッケージ|REG_SZ|*GUID*|このオプション ページを実装する VSPackage の GUID。|
|ページ|REG_SZ|*GUID*|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> メソッドを呼び出して VSPackage から要求するプロパティ ページの GUID。 このレジストリ エントリが存在しない場合、レジストリ キーにはページではなくノードが記述されます。|

### <a name="example"></a>例

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\
  Languages\
    Language Services\
      CSharp\
        EditorToolsOptions\
          Formatting\
            (Default) = reg_sz:#242
            Package   = reg_sz:{A066E284-DCAB-11D2-B551-00C04F68D4DB}
            General\
              (Default) = reg_sz:#255
              Package   = reg_sz:{A066E284-DCAB-11D2-B551-00C04F68D4DB}
              Page      = reg_sz:{3EB2CC0B-033E-4D75-B26A-B2362C25227E}
            Indentation\
              (Default) = reg_sz:#250
              Package   = reg_sz:{A066E284-DCAB-11D2-B551-00C04F68D4DB}
              Page      = reg_sz:{5E21D017-6D2A-4114-A1F1-C923F001CBBB}
            Newlines\
              (Default) = reg_sz:#253
              Package   = reg_sz:{A066E284-DCAB-11D2-B551-00C04F68D4DB}
              Page      = reg_sz:{607D8062-68D1-41E4-9A35-B5E7F14D0481}
```

## <a name="registry-entries-for-file-name-extension-options"></a>ファイル名拡張子オプションのレジストリ エントリ
 ファイル拡張子のエントリには、".myext" のように先頭のピリオド を含める必要があります。

|名前|Type|Range|説明|
|----------|----------|-----------|-----------------|
|(既定値)。|REG_SZ|*GUID*|このファイル名拡張子の種類に対する既定の言語サービスのサービス GUID。|

### <a name="example"></a>例

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\
  Languages\
    File Extensions\
      .cpp\
        (Default) = {B2F072B0-ABC1-11D0-9D62-00C04FD9DFD9}
```

## <a name="registry-entries-for-editor-options"></a>エディター オプションのレジストリ エントリ
 *VS Reg Root*\Editors キーには、次の値を含めることができます。

|名前|Type|Range|説明|
|----------|----------|-----------|-----------------|
|(既定値)。|REG_SZ|""|未使用。ドキュメント用にここに名前を入力できます。|
|DefaultToolboxTab|REG_SZ|""|エディターがアクティブであるときに既定にするツールボックス タブの名前。|
|DisplayName|REG_SZ|ResID|**[プログラムから開く]** ダイアログ ボックスに表示する名前。 名前は、文字列リソース ID または標準形式の名前です。|
|ExcludeDefTextEditor|REG_DWORD|0-1|**[プログラムから開く]** コマンドで使用します。 特定のファイルの種類で使用可能なエディターのリストに、既定のテキスト エディターを一覧表示させない場合は、この値を 1 に設定します。|
|LinkedEditorGUID|REG_SZ|*\<GUID>*|コードページをサポートするファイルを開くことができるすべての言語サービスに使用されます。 たとえば、 **[プログラムから開く]** コマンドを使用して .txt ファイルを開くと、エンコードを使用した場合と使用しない場合でソース コード エディターを使用するためのオプションが表示されます。<br /><br /> サブキーの名前に指定された GUID は、コードページ エディター ファクトリ用です。この特定のレジストリ エントリで指定されているリンクされた GUID は、通常のエディター ファクトリ用です。 このエントリの目的は、IDE で既定のエディターを使用してファイルが開かれていない場合、IDE では、リストの次のエディターが使用されます。 この次のエディターはコードページ エディター ファクトリにしないでください。このエディター ファクトリは、基本的には失敗したエディター ファクトリと同じであるためです。|
|パッケージ|REG_SZ|*\<GUID>*|表示名の ResID の VSPackage GUID。|

### <a name="example"></a>例

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\
  \Editors\
    {8281C572-2171-45AA-A642-7D8BC1662F1C}\
      (Default)            = reg_sz:Html Editor with Encoding
      DefaultToolboxTab    = reg_sz:HTML
      DisplayName          = reg_sz:#20101
      LinkedEditorGUID     = reg_sz:{C76D83F8-A489-11D0-8195-00A0C91BBEE3}
      Package              = reg_sz:{1B437D20-F8FE-11D2-A6AE-00104BCC7269}
```

## <a name="registry-entries-for-logical-view-options"></a>論理ビュー オプションのレジストリ エントリ
 *VS Reg Root*\Editors\\*Editor GUI>* \LogicalViews キーには、次の値を含めることができます。

|名前|Type|Range|説明|
|----------|----------|-----------|-----------------|
|(既定値)。|REG_SZ||未使用。|
|*\<GUID>*|REG_SZ|""|サポートされている論理ビューのキー。 必要な数だけこれらを保有できます。 レジストリ エントリの名前は重要なものですが、値ではありません。これは常に空の文字列になります。|

### <a name="example"></a>例

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\
  \Editors\
    {8281C572-2171-45AA-A642-7D8BC1662F1C}\
      LogicalViews\
       (Default) = reg_sz:
       {7651a700-06e5-11d1-8ebd-00a0c90f26ea} = reg_sz:
       {7651a701-06e5-11d1-8ebd-00a0c90f26ea} = reg_sz:
       {7651a702-06e5-11d1-8ebd-00a0c90f26ea} = reg_sz:
       {7651a703-06e5-11d1-8ebd-00a0c90f26ea} = reg_sz:
```

## <a name="registry-entries-for-editor-extension-options"></a>エディター拡張機能オプションのレジストリ エントリ
 *VS Reg Root*\Editors\\*Editor GUID*\Extensions キーには、次の値を含めることができます。 ファイル名の拡張子には、先頭のピリオドは含まれません。

|名前|Type|Range|説明|
|----------|----------|-----------|-----------------|
|(既定値)。|REG_SZ||未使用。|
|*\<ext>*|REG_DWORD|0-0xffffffff|拡張機能の相対的な優先度。 複数の言語で同じ拡張機能が共有されている場合は、優先度の高い言語が選択されます。|

 また、エディターの現在のユーザーの既定の選択は、HKEY_Current_User\Software\Microsoft\VisualStudio\\*X.Y*\Default Editors\\*ext* に格納されます。選択された言語サービスの GUID は、カスタム エントリにあります。 これは、現在のユーザーの場合に優先されます。

### <a name="example"></a>例

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\9.0\
  \Editors\
    {8281C572-2171-45AA-A642-7D8BC1662F1C}\
      Extensions\
       (Default) = reg_sz:
       *         = reg_dword:0x00000018
       html      = reg_dword:0x00000027
       shtm      = reg_dword:0x00000027
       shtml     = reg_dword:0x00000027
```

## <a name="registry-entries-for-managed-package-framework-language-service-options"></a>Managed Package Framework 言語サービス オプションのレジストリ エントリ
 次のレジストリ エントリは、Managed Package Framework (MPF) 言語サービス クラスに固有のものです。 これらのレジストリ エントリは、さまざまな IntelliSense 機能や、その他の高度な編集機能の言語サービスでのサポートを示しています。

 これらのレジストリ エントリには、<xref:Microsoft.VisualStudio.Package.LanguagePreferences> クラスを通じてアクセスします。

|名前|Type|Range|説明|
|----------|----------|-----------|-----------------|
|CodeSense|REG_DWORD|0-1|IntelliSense 操作のサポート。|
|MatchBraces|REG_DWORD|0-1|中かっこ、かっこ、角かっこなどの一致する言語のペアのサポート。|
|QuickInfo|REG_DWORD|0-1|IntelliSense クイック ヒント操作のサポート。|
|ShowMatchingBrace|REG_DWORD|0-1|一致する言語ペアをステータス バーに表示するためのサポート。|
|MatchBracesAtCaret|REG_DWORD|0-1|一致する言語のペアを表示するためのサポート。通常は、2 つの要素を強調表示します。|
|MaxErrorMessages|REG_DWORD|0-n|**[エラー一覧]** ウィンドウに表示できるエラーの最大数。|
|CodeSenseDelay|REG_DWORD|0-n|IntelliSense 操作のバックグラウンド解析を開始するまで遅延できるミリ秒数。|
|EnableAsyncCompletion|REG_DWORD|0-1|バックグラウンド解析のサポート。|
|EnableCommenting|REG_DWORD|0-1|選択したテキスト ブロックのコメント アウトのサポート。また、選択したテキストのコメント解除のサポートも意味します。|
|EnableFormatSelection|REG_DWORD|0-1|自動インデントや中かっこの位置の調整などのテキストの書式設定をサポートします。|
|AutoOutlining|REG_DWORD|0-1|アウトライン (折りたたむことのできる領域) のサポート。|
|MaxRegions|REG_DWORD|0-n|ファイルあたりの非表示領域の最大数。|

```
ExampleHKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\
  Languages\
    Language Services\
      XML\
        (Default)             = reg_sz:{f6819a78-a205-47b5-be1c-675b3c7f0b8e}
        MatchBraces           = reg_dword:0x00000001
        QuickInfo             = reg_dword:0x00000001
        ShowMatchingBrace     = reg_dword:0x00000001
        MatchBracesAtCaret    = reg_dword:0x00000000
        MaxErrorMessages      = reg_dword:0x00000064
        CodeSenseDelay        = reg_dword:0x000001f4
        MaxRegions            = reg_dword:0x0000000a
```

## <a name="see-also"></a>関連項目
- [従来の言語サービスの開発](../../extensibility/internals/developing-a-legacy-language-service.md)
