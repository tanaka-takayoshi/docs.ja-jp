---
title: 正規表現での置換
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- regular expressions, substitutions
- replacement patterns
- metacharacters, substitutions
- .NET Framework regular expressions, substitutions
- constructs, substitutions
- substitutions
ms.assetid: d1f52431-1c7d-4dc6-8792-6b988256892e
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 53fd4ee63d49b3943fa0b1164591aaddaa764abc
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/04/2018
ms.locfileid: "33579419"
---
# <a name="substitutions-in-regular-expressions"></a>正規表現での置換
<a name="Top"></a> 置換は、置換パターン内でのみ認識される言語要素です。 置換では、正規表現パターンを使用して、入力文字列内の一致するテキストを置換するテキストの全体または一部を定義します。 置換パターンは、1 個以上の置換と、リテラル文字で構成されます。 置換パターンは、<xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=nameWithType> パラメーターを持つ `replacement` メソッドのオーバーロードおよび <xref:System.Text.RegularExpressions.Match.Result%2A?displayProperty=nameWithType> メソッドに対して用意されています。 メソッドは、一致するパターンを、 `replacement` パラメーターで定義されているパターンで置換します。  
  
 .NET Framework では、次の表に示す置換要素が定義されています。  
  
|代入|説明|  
|------------------|-----------------|  
|`$` *number*|*number*で識別されるキャプチャ グループに一致する最後の部分文字列を置換文字列に含めます。 *number* は 10 進値です。 詳細については、「 [番号付きグループの置換](#Numbered)」を参照してください。|  
|`${` *name* `}`|`(?<`*name*`> )` で指定された名前付きグループに一致する最後の部分文字列を置換文字列に含めます。 詳細については、「 [名前付きグループの置換](#Named)」を参照してください。|  
|`$$`|置換文字列に 1 つの "$" リテラルを含めます。 詳細については、「 ["$" 文字の置換](#DollarSign)」を参照してください。|  
|`$&`|一致した文字列全体のコピーを置換文字列に含めます。 詳細については、「 [一致した文字列全体の置換](#EntireMatch)」を参照してください。|  
|<code>$\`</code>|一致した場所より前にある入力文字列のテキストすべてを置換文字列に含めます。 詳細については、「 [一致した文字列より前にあるテキストの置換](#BeforeMatch)」を参照してください。|  
|`$'`|一致した場所より後にある入力文字列のテキストすべてを置換文字列に含めます。 詳細については、「 [一致した文字列より後にあるテキストの置換](#AfterMatch)」を参照してください。|  
|`$+`|最後にキャプチャされたグループを置換文字列に含めます。 詳細については、「 [キャプチャされた最後のグループの置換](#LastGroup)」を参照してください。|  
|`$_`|入力文字列全体を置換文字列に含めます。 詳細については、「 [入力文字列全体の置換](#EntireString)」を参照してください。|  
  
## <a name="substitution-elements-and-replacement-patterns"></a>置換要素と置換パターン  
 置換構成体は、置換パターンで認識される特殊な構成体です。 文字エスケープやピリオド (`.`) など、任意の文字に一致する他の正規表現言語要素はいずれもサポートされていません。 同様に、置換言語要素は置換パターン内でのみ認識され、正規表現パターン内では有効ではありません。  
  
 正規表現パターンと置換の両方に使用できる文字は `$` 文字だけですが、この文字の意味はコンテキストによって異なります。 正規表現パターンでは、 `$` は文字列の末尾に一致するアンカーです。 置換パターンでは、 `$` は置換の先頭を示します。  
  
> [!NOTE]
>  正規表現の中で置換パターンに似た機能を利用するには、前方参照を使用します。 前方参照の詳細については、「 [前方参照構成体](../../../docs/standard/base-types/backreference-constructs-in-regular-expressions.md)」を参照してください。  
  
<a name="Numbered"></a>   
## <a name="substituting-a-numbered-group"></a>番号付きグループの置換  
 `$`*number* 言語要素は、 *number* キャプチャ グループに一致する最後の部分文字列を置換文字列に含めます。 *number* は、キャプチャ グループのインデックスです。 たとえば、置換パターン `$1` は、一致した部分文字列がキャプチャされた最初のグループに置き換えられることを示します。 番号付きキャプチャ グループの詳細については、「 [Grouping Constructs](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md)」を参照してください。  
  
 `$` 以降のすべての数字が、 *number* グループに所属すると解釈されます。 そうしたくない場合は、代わりに名前付きグループを使用できます。 たとえば、 `$11` の代わりに、置換文字列 `${1}1` を使用して、最初のキャプチャ グループの値と数字 "1" を置換文字列として定義できます。 詳細については、「 [名前付きグループの置換](#Named)」を参照してください。  
  
 `(?<`*name*`>)` 構文を使用して名前が明示的に割り当てられていないキャプチャ グループには、1 から開始する番号が左から右の順に割り当てられます。 名前付きグループにも、最後の名前のないグループのインデックスよりも 1 つ大きい数値から開始する番号が、左から右へと順に割り当てられます。 たとえば、正規表現 `(\w)(?<digit>\d)`では、 `digit` という名前付きグループのインデックスは 2 です。  
  
 *number* が、正規表現パターンで定義される有効なキャプチャ グループを指定していない場合は、 `$`*number* が、一致した各文字列の置換に使用されるリテラル文字列シーケンスとして解釈されます。  
  
 次の例では、 `$`*number* の置換を使用して、10 進値から通貨記号を削除しています。 通貨値の先頭または末尾に見つかった通貨記号を削除し、最も一般的な 2 つの桁区切り記号 ("." および ",") を認識します。  
  
 [!code-csharp[Conceptual.RegEx.Language.Substitutions#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.substitutions/cs/numberedgroup1.cs#1)]
 [!code-vb[Conceptual.RegEx.Language.Substitutions#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.substitutions/vb/numberedgroup1.vb#1)]  
  
 正規表現パターン `\p{Sc}*(\s?\d+[.,]?\d*)\p{Sc}*` は、次の表に示すように定義されています。  
  
|パターン|説明|  
|-------------|-----------------|  
|`\p{Sc}*`|0 個以上の通貨記号文字と一致します。|  
|`\s?`|0 個または 1 個の空白文字と一致します。|  
|`\d+`|1 個以上の 10 進数と一致します。|  
|`[.,]?`|0 個または 1 個のピリオドまたはコンマと一致します。|  
|`\d*`|0 個以上の 10 進数と一致します。|  
|`(\s?\d+[.,]?\d*)`|空白の後に 1 つ以上の 10 進数、0 個または 1 個のピリオドまたはコンマ、さらに 0 個以上の 10 進数が続くパターンに一致します。 これが最初のキャプチャ グループです。 置換パターンは `$1` であるため、<xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=nameWithType> メソッドを呼び出すと、一致する部分文字列全体がこのキャプチャされたグループに置き換えられます。|  
  
 [ページのトップへ](#Top)  
  
<a name="Named"></a>   
## <a name="substituting-a-named-group"></a>名前付きグループの置換  
 `${`*name*`}` 言語要素は、 *name* キャプチャ グループに一致する最後の部分文字列を置換します。ここで、 *name* は `(?<`*name*`>)` 言語要素で定義されているキャプチャ グループの名前です。 名前付きキャプチャ グループの詳細については、「 [Grouping Constructs](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md)」を参照してください。  
  
 *name* が正規表現パターンで定義されている有効な名前付きキャプチャ グループを指定していないものの、数字で構成されている場合、 `${`*name*`}` は番号付きグループとして解釈されます。  
  
 *name* が、正規表現パターンで定義されている有効な名前付きキャプチャ グループも有効な番号付きキャプチャ グループも指定していない場合、 `${`*name*`}` は、一致した各文字列の置換に使用されるリテラル文字列シーケンスとして解釈されます。  
  
 次の例では、 `${`*name*`}` の置換を使用して、10 進値から通貨記号を削除しています。 通貨値の先頭または末尾に見つかった通貨記号を削除し、最も一般的な 2 つの桁区切り記号 ("." および ",") を認識します。  
  
 [!code-csharp[Conceptual.RegEx.Language.Substitutions#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.substitutions/cs/namedgroup1.cs#2)]
 [!code-vb[Conceptual.RegEx.Language.Substitutions#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.substitutions/vb/namedgroup1.vb#2)]  
  
 正規表現パターン `\p{Sc}*(?<amount>\s?\d[.,]?\d*)\p{Sc}*` は、次の表に示すように定義されています。  
  
|パターン|説明|  
|-------------|-----------------|  
|`\p{Sc}*`|0 個以上の通貨記号文字と一致します。|  
|`\s?`|0 個または 1 個の空白文字と一致します。|  
|`\d+`|1 個以上の 10 進数と一致します。|  
|`[.,]?`|0 個または 1 個のピリオドまたはコンマと一致します。|  
|`\d*`|0 個以上の 10 進数と一致します。|  
|`(?<amount>\s?\d[.,]?\d*)`|空白の後に 1 つ以上の 10 進数、0 個または 1 個のピリオドまたはコンマ、さらに 0 個以上の 10 進数が続くパターンに一致します。 これは、 `amount`という名前のキャプチャ グループです。 置換パターンは `${amount}` であるため、<xref:System.Text.RegularExpressions.Regex.Replace%2A?displayProperty=nameWithType> メソッドを呼び出すと、一致する部分文字列全体がこのキャプチャされたグループに置き換えられます。|  
  
 [ページのトップへ](#Top)  
  
<a name="DollarSign"></a>   
## <a name="substituting-a--character"></a>"$" 文字の置換  
 `$$` の置換は、リテラル文字 "$" を置換文字列に挿入します。  
  
 次の例では、 <xref:System.Globalization.NumberFormatInfo> オブジェクトを使用して、現在のカルチャの通貨記号と、通貨文字列内でのその配置を決定します。 次に、正規表現パターンと置換パターンの両方を動的に構築します。 現在 en-US カルチャが使用されているコンピューターでこの例を実行すると、 `\b(\d+)(\.(\d+))?` という正規表現パターンと `$$ $1$2`という置換パターンが生成されます。 置換パターンは、一致するテキストを、通貨記号と空白に続いて、キャプチャされた最初および 2 番目のグループで置換します。  
  
 [!code-csharp[Conceptual.Regex.Language.Substitutions#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.substitutions/cs/dollarsign1.cs#8)]
 [!code-vb[Conceptual.Regex.Language.Substitutions#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.substitutions/vb/dollarsign1.vb#8)]  
  
 正規表現パターン `\b(\d+)(\.(\d+))?` は、次の表に示すように定義されています。  
  
|パターン|説明|  
|-------------|-----------------|  
|`\b`|ワード境界の先頭から照合を開始します。|  
|`(\d+)`|1 個以上の 10 進数と一致します。 これが最初のキャプチャ グループです。|  
|`\.`|ピリオド (桁区切り記号) と一致します。|  
|`(\d+)`|1 個以上の 10 進数と一致します。 これが 3 番目のキャプチャ グループです。|  
|`(\.(\d+))?`|ピリオドの後に 1 つ以上の 10 進数が続くパターンの 0 回または 1 回の出現と一致します。 これが 2 番目のキャプチャ グループです。|  
  
<a name="EntireMatch"></a>   
## <a name="substituting-the-entire-match"></a>一致した文字列全体の置換  
 `$&` の置換は、一致した文字列全体を置換文字列に含めます。 通常は、一致した文字列の先頭または末尾に部分文字列を追加するために使用されます。 たとえば、 `($&)` という置換パターンは、一致した各文字列の先頭と末尾にかっこを追加します。 一致する文字列がない場合、 `$&` の置換は無効です。  
  
 `$&` の置換を使用して、文字列配列に格納されている書籍タイトルの先頭と末尾に引用符を追加する例を次に示します。  
  
 [!code-csharp[Conceptual.RegEx.Language.Substitutions#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.substitutions/cs/entirematch1.cs#3)]
 [!code-vb[Conceptual.RegEx.Language.Substitutions#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.substitutions/vb/entirematch1.vb#3)]  
  
 正規表現パターン `^(\w+\s?)+$` は、次の表に示すように定義されています。  
  
|パターン|説明|  
|-------------|-----------------|  
|`^`|入力文字列の先頭から照合を開始します。|  
|`(\w+\s?)+`|1 つ以上の単語文字の後に 0 個または 1 個の空白文字が 1 回以上続くパターンに一致します。|  
|`$`|入力文字列の末尾と一致します。|  
  
 `"$&"` という置換パターンは、各一致文字列の先頭と末尾にリテラルの一重引用符を追加します。  
  
 [ページのトップへ](#Top)  
  
<a name="BeforeMatch"></a>   
## <a name="substituting-the-text-before-the-match"></a>一致した文字列より前にあるテキストの置換  
 <code>$\`</code> の置換は、一致した場所より前にある入力文字列全体で一致した文字列を置換します。 つまり、一致した場所までの入力文字列を複製し、一致したテキストを削除します。 結果文字列では、一致したテキストに続くテキストは変更されません。 入力文字列に複数の一致文字列がある場合、置換テキストは、テキストが前の一致で置換された文字列からではなく、元の入力文字列から派生します  \(具体的な例を次に示します。\)一致する文字列がない場合、<code>$\`</code> の置換は無効です。  
  
 次の例では、正規表現パターン `\d+` を使用して、入力文字列内の 1 つ以上の 10 進数のシーケンスを照合します。 置換文字列 <code>$`</code> は、これらの数字を、一致文字列より前にあるテキストで置換します。  
  
 [!code-csharp[Conceptual.Regex.Language.Substitutions#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.substitutions/cs/before1.cs#4)]
 [!code-vb[Conceptual.Regex.Language.Substitutions#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.substitutions/vb/before1.vb#4)]  
  
 この例では、入力文字列 `"aa1bb2cc3dd4ee5"` に 5 つの一致が含まれています。 <code>$`</code> の置換によって、正規表現エンジンが入力文字列の各一致文字列をどのように置換するかを、次の表に示します。 挿入されたテキストは結果列に太字で示されています。  
  
|一致したもの|位置|一致した場所より前にある文字列|結果文字列|  
|-----------|--------------|-------------------------|-------------------|  
|1|2|aa|aa**aa**bb2cc3dd4ee5|  
|2|5|aa1bb|aaaabb**aa1bb**cc3dd4ee5|  
|3|8|aa1bb2cc|aaaabbaa1bbcc**aa1bb2cc**dd4ee5|  
|4|11|aa1bb2cc3dd|aaaabbaa1bbccaa1bb2ccdd**aa1bb2cc3dd**ee5|  
|5|14|aa1bb2cc3dd4ee|aaaabbaa1bbccaa1bb2ccddaa1bb2cc3ddee**aa1bb2cc3dd4ee**|  
  
 [ページのトップへ](#Top)  
  
<a name="AfterMatch"></a>   
## <a name="substituting-the-text-after-the-match"></a>一致した文字列より後にあるテキストの置換  
 `$'` の置換は、一致した場所より後にある入力文字列全体で一致した文字列を置換します。 つまり、一致した場所より後にある入力文字列を複製し、一致したテキストを削除します。 結果文字列では、一致したテキストより前にあるテキストは変更されません。 一致する文字列がない場合、  `$'` の置換は無効です。  
  
 次の例では、正規表現パターン `\d+` を使用して、入力文字列内の 1 つ以上の 10 進数のシーケンスを照合します。 置換文字列 `$'` は、これらの数字を、一致文字列に続くテキストで置換します。  
  
 [!code-csharp[Conceptual.Regex.Language.Substitutions#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.substitutions/cs/after1.cs#5)]
 [!code-vb[Conceptual.Regex.Language.Substitutions#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.substitutions/vb/after1.vb#5)]  
  
 この例では、入力文字列 `"aa1bb2cc3dd4ee5"` に 5 つの一致が含まれています。 `$'` の置換によって、正規表現エンジンが入力文字列の各一致文字列をどのように置換するかを、次の表に示します。 挿入されたテキストは結果列に太字で示されています。  
  
|一致したもの|位置|一致した場所より後にある文字列|結果文字列|  
|-----------|--------------|------------------------|-------------------|  
|1|2|bb2cc3dd4ee5|aa**bb2cc3dd4ee5**bb2cc3dd4ee5|  
|2|5|cc3dd4ee5|aabb2cc3dd4ee5bb**cc3dd4ee5**cc3dd4ee5|  
|3|8|dd4ee5|aabb2cc3dd4ee5bbcc3dd4ee5cc**dd4ee5**dd4ee5|  
|4|11|ee5|aabb2cc3dd4ee5bbcc3dd4ee5ccdd4ee5dd**ee5**ee5|  
|5|14|<xref:System.String.Empty?displayProperty=nameWithType>|aabb2cc3dd4ee5bbcc3dd4ee5ccdd4ee5ddee5ee|  
  
 [ページのトップへ](#Top)  
  
<a name="LastGroup"></a>   
## <a name="substituting-the-last-captured-group"></a>キャプチャされた最後のグループの置換  
 `$+` の置換は、キャプチャされた最後のグループで一致した文字列を置換します。 キャプチャされたグループがない場合、またはキャプチャされた最後のグループの値が <xref:System.String.Empty?displayProperty=nameWithType> の場合、`$+` の置換は無効です。  
  
 次の例では、文字列内の重複する単語を識別し、`$+` の置換を使用して、これらの単語をその単語 1 つに置換します。 <xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase?displayProperty=nameWithType> オプションを使用すると、大文字と小文字の違いを除いて同一である単語が重複と見なされるようになります。  
  
 [!code-csharp[Conceptual.Regex.Language.Substitutions#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.substitutions/cs/lastmatch1.cs#6)]
 [!code-vb[Conceptual.Regex.Language.Substitutions#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.substitutions/vb/lastmatch1.vb#6)]  
  
 正規表現パターン `\b(\w+)\s\1\b` は、次の表に示すように定義されています。  
  
|パターン|説明|  
|-------------|-----------------|  
|`\b`|ワード境界から照合を開始します。|  
|`(\w+)`|1 つ以上の単語文字に一致します。 これが最初のキャプチャ グループです。|  
|`\s`|空白文字と一致します。|  
|`\1`|キャプチャされた最初のグループと一致します。|  
|`\b`|ワード境界で照合を終了します。|  
  
 [ページのトップへ](#Top)  
  
<a name="EntireString"></a>   
## <a name="substituting-the-entire-input-string"></a>入力文字列全体の置換  
 `$_` の置換は、一致した文字列を入力文字列全体で置換します。 つまり、一致したテキストを削除し、一致したテキストを含む文字列全体でそのテキストを置換します。  
  
 次の例では、入力文字列の 1 つ以上の 10 進数を照合します。 `$_` の置換を使用して、これらを入力文字列全体で置換します。  
  
 [!code-csharp[Conceptual.Regex.Language.Substitutions#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.regex.language.substitutions/cs/entire1.cs#7)]
 [!code-vb[Conceptual.Regex.Language.Substitutions#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.regex.language.substitutions/vb/entire1.vb#7)]  
  
 この例では、入力文字列 `"ABC123DEF456"` に 2 つの一致が含まれています。 `$_` の置換によって、正規表現エンジンが入力文字列の各一致文字列をどのように置換するかを、次の表に示します。 挿入されたテキストは結果列に太字で示されています。  
  
|一致したもの|位置|一致したもの|結果文字列|  
|-----------|--------------|-----------|-------------------|  
|1|3|123|ABC**ABC123DEF456**DEF456|  
|2|5|456|ABCABC123DEF456DEF**ABC123DEF456**|  
  
## <a name="see-also"></a>参照  
 [正規表現言語 - クイック リファレンス](../../../docs/standard/base-types/regular-expression-language-quick-reference.md)
