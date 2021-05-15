---
title: '方法 : コード分析辞書をカスタマイズする'
ms.date: 11/04/2016
description: スペルと名前付け規則のエラーを識別するコード分析辞書について説明します。 カスタム辞書を作成し、プロジェクトに適用する方法を示します。
ms.custom: SEO-VS-2020
ms.topic: how-to
helpviewer_keywords:
- code analysis dictionary
- custom dictionary, code analysis
- dictionary, code analysis
ms.assetid: 667e3b4e-beff-48be-b3d1-376e1716a895
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 10466acedcd5c7f5fda835d66e654128a556d0a4
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99860101"
---
# <a name="how-to-customize-the-code-analysis-dictionary"></a>方法 : コード分析辞書をカスタマイズする

コード分析では、組み込みの辞書を使用してコード内の識別子をチェックし、スペル、文法上の大文字小文字、.NET デザイン ガイドラインのその他の名前付け規則のエラーがないかどうかを確認します。 カスタム辞書 XML ファイルを作成して、組み込みの辞書の用語、略語、頭字語を追加、削除、または変更できます。

たとえば、コードに **DoorKnokker** という名前のクラスが含まれているとします。 コード分析では、この名前は **door** と **knokker** という 2 つの単語の複合語として識別されます。 その後、**knokker** のスペルが正しくないことを示す警告が表示されます。 コード分析でこのスペルを認識させるには、**knokker** という用語をカスタム辞書に追加します。

## <a name="to-create-a-custom-dictionary"></a>カスタム辞書を作成するには

**CustomDictionary.xml** という名前のファイルを作成します。

次の XML 構造を使用して、カスタム単語を定義します。

```xml
<Dictionary>
      <Words>
         <Unrecognized>
            <Word>knokker</Word>
         </Unrecognized>
         <Recognized>
            <Word></Word>
         </Recognized>
         <Deprecated>
            <Term PreferredAlternate=""></Term>
         </Deprecated>
         <Compound>
            <Term CompoundAlternate=""></Term>
         </Compound>
         <DiscreteExceptions>
            <Term></Term>
         </DiscreteExceptions>
      </Words>
      <Acronyms>
         <CasingExceptions>
            <Acronym></Acronym>
         </CasingExceptions>
      </Acronyms>
   </Dictionary>
```

## <a name="custom-dictionary-elements"></a>カスタム辞書の要素

カスタム辞書の次の要素の内部テキストとして用語を追加することで、コード分析辞書の動作を変更できます。

- [Dictionary/Words/Recognized/Word](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsRecognizedWord)

- [Dictionary/Words/Unrecognized/Word](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsUnrecognizedWord)

- [Dictionary/Words/Deprecated/Term[@PreferredAlternate]](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsDeprecatedTermPreferredAlternate)

- [Dictionary/Words/Compound/Term[@CompoundAlternate]](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsCompoundTermCompoundAlternate)

- [Dictionary/Words/DiscreteExceptions/Term](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryWordsDiscreteExceptionsTerm)

- [Dictionary/Acronyms/CasingExceptions/Acronym](../code-quality/how-to-customize-the-code-analysis-dictionary.md#BKMK_DictionaryAcronymsCasingExceptionsAcronym)

### <a name="dictionarywordsrecognizedword"></a><a name="BKMK_DictionaryWordsRecognizedWord"></a> Dictionary/Words/Recognized/Word

コード分析で正しいスペルとして識別される用語のリストに用語を含めるには、その用語を Dictionary/Words/Recognized/Word 要素の内部テキストとして追加します。 Dictionary/Words/Recognized/Word 要素内の用語では、大文字と小文字は区別されません。

**例**

```xml
<Dictionary>
      <Words>
         <Recognized>
            <Word>knokker</Word>
            ...
         </Recognized>
         ...
      </Words>
      ...
</Dictionary>
```

Dictionary/Words/Recognized ノードの用語には、次のコード分析規則が適用されます。

- [CA1701:リソース文字列の複合語は、大文字と小文字を正しく区別しなければなりません](../code-quality/ca1701.md)

- [CA1702:複合語では、大文字と小文字が正しく区別されなければなりません](../code-quality/ca1702.md)

- [CA1703:リソース文字列は正しく入力されなければなりません](../code-quality/ca1703.md)

- [CA1704:識別子は正しく入力されなければなりません](../code-quality/ca1704.md)

- [CA1709:識別子では、大文字と小文字が正しく区別されなければなりません](../code-quality/ca1709.md)

- [CA1726:適切な用語を使用します](../code-quality/ca1726.md)

- [CA2204:リテラルに正しいスペルを要求](../code-quality/ca2204.md)

### <a name="dictionarywordsunrecognizedword"></a><a name="BKMK_DictionaryWordsUnrecognizedWord"></a> Dictionary/Words/Unrecognized/Word

コード分析で正しいスペルとして識別される用語のリストから用語を除外するには、除外する用語を Dictionary/Words/Unrecognized/Word 要素の内部テキストとして追加します。 Dictionary/Words/Unrecognized/Word 要素内の用語では、大文字と小文字は区別されません。

**例**

```xml
<Dictionary>
      <Words>
         <Unrecognized>
            <Word>meth</Word>
            ...
         </Unrecognized>
         ...
      </Words>
      ...
</Dictionary>
```

Dictionary/Words/Unrecognized ノードの用語には、次のコード分析規則が適用されます。

- [CA1701:リソース文字列の複合語は、大文字と小文字を正しく区別しなければなりません](../code-quality/ca1701.md)

- [CA1702:複合語では、大文字と小文字が正しく区別されなければなりません](../code-quality/ca1702.md)

- [CA1703:リソース文字列は正しく入力されなければなりません](../code-quality/ca1703.md)

- [CA1704:識別子は正しく入力されなければなりません](../code-quality/ca1704.md)

- [CA1709:識別子では、大文字と小文字が正しく区別されなければなりません](../code-quality/ca1709.md)

- [CA1726:適切な用語を使用します](../code-quality/ca1726.md)

- [CA2204:リテラルに正しいスペルを要求](../code-quality/ca2204.md)

### <a name="dictionarywordsdeprecatedtermpreferredalternate"></a><a name="BKMK_DictionaryWordsDeprecatedTermPreferredAlternate"></a> Dictionary/Words/Deprecated/Term[@PreferredAlternate]

コード分析で非推奨として識別される用語のリストに用語を含めるには、その用語を Dictionary/Words/Deprecated/Term 要素の内部テキストとして追加します。 非推奨の用語とは、スペルは正しくても使用すべきではない単語です。

代替用語の候補を警告に含めるには、Term 要素の PreferredAlternate 属性で代替用語を指定します。 代替用語を提案しない場合は、この属性値を空のままにしておいてかまいません。

- Dictionary/Words/Deprecated/Term 要素内の非推奨の用語では、大文字と小文字は区別されません。

- PreferredAlternate 属性値では、大文字と小文字が区別されます。 複合代替用語には、パスカル ケースを使用します。

**例**

```xml
<Dictionary>
      <Words>
         <Deprecated>
            <Term PreferredAlternate="LogOn">login</Term>
            ...
         </Deprecated>
         ...
      </Words>
      ...
</Dictionary>
```

Dictionary/Words/Deprecated ノードの用語には、次のコード分析規則が適用されます。

- [CA1701:リソース文字列の複合語は、大文字と小文字を正しく区別しなければなりません](../code-quality/ca1701.md)

- [CA1702:複合語では、大文字と小文字が正しく区別されなければなりません](../code-quality/ca1702.md)

- [CA1703:リソース文字列は正しく入力されなければなりません](../code-quality/ca1703.md)

- [CA1704:識別子は正しく入力されなければなりません](../code-quality/ca1704.md)

- [CA1726:適切な用語を使用します](../code-quality/ca1726.md)

### <a name="dictionarywordscompoundtermcompoundalternate"></a><a name="BKMK_DictionaryWordsCompoundTermCompoundAlternate"></a> Dictionary/Words/Compound/Term[@CompoundAlternate]

組み込みの辞書には、複合語ではなく、単一の個別の用語として識別される用語があります。 コード分析で複合語として識別される用語のリストに用語を含め、用語の正しい大文字小文字の区別を指定するには、その用語を Dictionary/Words/Compound/Term 要素の内部テキストとして追加します。 Term 要素の CompoundAlternate 属性で、個々の単語の最初の文字を大文字にして (パスカル ケース)、複合語を構成する個々の単語を指定します。 内部テキストで指定された用語は、Dictionary/Words/DiscreteExceptions リストに自動的に追加されることに注意してください。

- Dictionary/Words/Compound/Term 要素内の複合語では、大文字と小文字は区別されません。

- CompoundAlternate 属性値では、大文字と小文字が区別されます。 複合代替用語には、パスカル ケースを使用します。

**例**

```xml
<Dictionary>
      <Words>
         <Compound>
            <Term CompoundAlternate="CheckBox">checkbox</Term>
            ...
         </Compound>
         ...
      </Words>
      ...
</Dictionary>
```

Dictionary/Words/Compound ノードの用語には、次のコード分析規則が適用されます。

- [CA1701:リソース文字列の複合語は、大文字と小文字を正しく区別しなければなりません](../code-quality/ca1701.md)

- [CA1702:複合語では、大文字と小文字が正しく区別されなければなりません](../code-quality/ca1702.md)

- [CA1703:リソース文字列は正しく入力されなければなりません](../code-quality/ca1703.md)

- [CA1704:識別子は正しく入力されなければなりません](../code-quality/ca1704.md)

### <a name="dictionarywordsdiscreteexceptionsterm"></a><a name="BKMK_DictionaryWordsDiscreteExceptionsTerm"></a> Dictionary/Words/DiscreteExceptions/Term

コード分析で、複合語の大文字小文字の規則によって用語がチェックされるときに、単一の個別の単語として識別される用語のリストから用語を除外するには、その用語を Dictionary/Words/DiscreteExceptions/Term 要素の内部テキストとして追加します。 Dictionary/Words/DiscreteExceptions/Term 要素内の用語では、大文字と小文字は区別されません。

**例**

```xml
<Dictionary>
      <Words>
         <DiscreteExceptions>
            <Term>checkbox</Term>
            ...
         </DiscreteExceptions>
         ...
      </Words>
      ...
</Dictionary>
```

Dictionary/Words/DiscreteExceptions ノードの用語には、次のコード分析規則が適用されます。

- [CA1701:リソース文字列の複合語は、大文字と小文字を正しく区別しなければなりません](../code-quality/ca1701.md)

- [CA1702:複合語では、大文字と小文字が正しく区別されなければなりません](../code-quality/ca1702.md)

### <a name="dictionaryacronymscasingexceptionsacronym"></a><a name="BKMK_DictionaryAcronymsCasingExceptionsAcronym"></a> Dictionary/Acronyms/CasingExceptions/Acronym

コード分析で正しいスペルとして識別される用語のリストに頭字語を含めて、複合語の大文字小文字の規則によって用語がチェックされるときにその頭字語をどのようにチェックするのかを示すには、その用語を Dictionary/Acronyms/CasingExceptions/Acronym 要素の内部テキストとして追加します。 Dictionary/Acronyms/CasingExceptions/Acronym 要素内の頭字語では、大文字と小文字が区別されます。

**例**

```xml
<Dictionary>
      <Acronyms>
         <CasingExceptions>
            <Acronym>NESW</Acronym>   <!-- North East South West -->
            ...
         </CasingExceptions>
         ...
      </Acronyms>
      ...
</Dictionary>
```

Dictionary/Acronyms/CasingExceptions ノードの用語には、次のコード分析規則が適用されます。

- [CA1709:識別子では、大文字と小文字が正しく区別されなければなりません](../code-quality/ca1709.md)

## <a name="to-apply-a-custom-dictionary-to-a-project"></a><a name="BKMK_ToApplyACustomDictionaryToAProject"></a> カスタム辞書をプロジェクトに適用するには

1. **ソリューション エクスプローラー** で、次のいずれかの手順を使用します。

    - 1 つのプロジェクトに辞書を追加するには、プロジェクト名を右クリックし、 **[既存項目の追加]** をクリックします。 **[既存項目の追加]** ダイアログ ボックスでファイルを指定します。
  
    - 複数のプロジェクト間で共有される辞書を追加するには、 **[既存項目の追加]** ダイアログ ボックスで共有するファイルを見つけ、 **[追加]** ボタンの下矢印をクリックして、 **[リンクとして追加]** をクリックします。

2. **ソリューション エクスプローラー** で、**CustomDictionary.xml** のファイル名を右クリックし、 **[プロパティ]** をクリックします。

3. **[ビルド アクション]** の一覧で、 **[CodeAnalysisDictionary]** を選択します。

4. **[出力ディレクトリにコピー]** の一覧で、 **[コピーしない]** を選択します。
