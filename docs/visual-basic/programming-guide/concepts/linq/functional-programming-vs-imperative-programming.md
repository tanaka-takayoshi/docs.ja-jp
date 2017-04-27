---
title: "関数型プログラミングと命令型プログラミング (Visual Basic) |Microsoft ドキュメント"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 6a1f3b57-00e6-447d-9906-74c7c4d5d85c
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 7fd7a2defabe2d03b658977cc0106e3bbf985202
ms.lasthandoff: 03/13/2017


---
# <a name="functional-programming-vs-imperative-programming-visual-basic"></a>関数型プログラミングと命令型プログラミング (Visual Basic)
このトピックでは、関数型プログラミングを従来の命令型 (手続き型) プログラミングと比較対照します。  
  
## <a name="functional-programming-vs-imperative-programming"></a>関数型プログラミングと命令型プログラミング  
 *関数型プログラミング*パラダイムは、問題を解決するため、純粋関数型アプローチをサポートするために明示的に作成します。 関数型プログラミングは一種の*宣言型プログラミング*します。 これに対し、c#、Visual Basic、C++、および、Java などのプログラミング (OOP) 言語のオブジェクト指向を含め、ほとんどの主流言語に設計されています、主にサポートする*命令型*(手続き型) プログラミングします。  
  
 命令型の方法では、開発者はコードを記述して、目的を達成するためにコンピューターが実行するステップを詳細に示します。 これとも呼ば*アルゴリズム*プログラミングします。 一方、関数型の方法では、実行される一連の関数として問題が組み立てられ、 それぞれの関数に何が入力され、何が返されるのかが、慎重に定義されます。 この&2; つの方法の一般的な違いを次の表に示します。  
  
|特徴|命令型の方法|関数型の方法|  
|--------------------|-------------------------|-------------------------|  
|プログラミングの焦点|タスク (アルゴリズム) の実行方法と状態の変化の追跡方法。|目的となる情報と必要な変換。|  
|状態変更|重要。|存在しない。|  
|実行の順序|重要。|あまり重要ではない。|  
|主要なフロー制御|ループ、条件、および関数 (メソッド) 呼び出し。|関数呼び出し (再帰を含む)。|  
|主要な操作単位|構造体またはクラスのインスタンス。|ファーストクラス オブジェクトとしての関数とデータ コレクション。|  
  
 ほとんどの言語は特定のプログラミング パラダイムをサポートするために作成されていますが、汎用言語の多くは、複数のパラダイムをサポートできる柔軟性を備えています。 たとえば、関数ポインターを含むほとんどの言語で関数型プログラミングがサポートされます。 さらに、Visual Basic には、ラムダ式などの関数型プログラミングのサポートや型推論する明確な言語拡張が含まれています。 LINQ テクノロジは、宣言型 (関数型) プログラミングの一種です。  
  
## <a name="functional-programming-using-xslt"></a>XSLT による関数型プログラミング  
 純粋関数型の方法については、多くの XSLT 開発者が精通しています。 XSLT スタイル シートを開発するための最も効果的な方法では、各テンプレートが、分離された構成可能な変換として扱われ、 実行の順序はまったく重要ではなくなります。 また、XSLT では副作用も許可されません (例外として、手続き型のコードを実行するためのエスケープ メカニズムによって副作用が導入されることがあります。このため、純粋関数型ではなくなる場合があります)。 XSLT は有効なツールですが、その一方で、最適とは言えない特性もあります。 たとえば、プログラミング構成要素が XML で表現されるため、コードが比較的冗長になり、保守が困難になります。 また、フロー制御のために再帰に大きく依存しているため、コードが読みにくくなることがあります。 XSLT の詳細については、次を参照してください。 [XSLT 変換](http://msdn.microsoft.com/library/202f8820-224c-494f-b61e-cd127eac6e03)します。  
  
 ただし、XML の形式を変換する場合に純粋関数型の方法を使用する意味は、XSLT によって証明されます。 LINQ to XML による純粋関数型プログラミングは多くの点で XSLT に似ていますが、 ただし、LINQ to XML と Visual Basic によって導入されるプログラミング構成要素では、読みやすくなり、実装する XSLT よりもを純粋関数型変換を記述できます。  
  
## <a name="advantages-of-pure-functions"></a>純粋関数の利点  
 関数型変換を純粋関数として実装する最大の理由は、純粋関数が構成可能であること (自己完結していて、ステートレスなこと) です。 これらの特性は、以下に示すようなさまざまな利点をもたらします。  
  
-   読みやすさが向上し、保守が容易になる。 これは、それぞれの関数が、引数を渡されると特定のタスクを実行するように作られていて、 外部の状態に依存しないためです。  
  
-   反復開発が容易になる。 コードのリファクタリングが容易になるため、多くの場合、設計変更を実装しやすくなります。 たとえば、複雑な変換を記述していて、何度も繰り返されているコードがあることに気付いた場合、 純粋メソッドによるリファクタリングでは、副作用を考慮せずにその純粋メソッドを自由に呼び出すことができます。  
  
-   テストやデバッグが容易になる。 純粋関数は単独でのテストが容易なため、典型的な値、有効なエッジ ケース、および無効なエッジ ケースを使用して純粋関数を呼び出すテスト コードを作成できます。  
  
## <a name="transitioning-for-oop-developers"></a>OOP 開発者向けの移行  
 従来のオブジェクト指向プログラミング (OOP) では、ほとんどの開発者が命令型/手続き型スタイルのプログラミングに慣れています。 純粋関数型スタイルの開発に移行するには、考え方を切り替えて、開発に適用する方法を変える必要があります。  
  
 問題を解決する際、OOP 開発者は、クラス階層を設計し、適切なカプセル化に焦点を絞り、クラス コントラクトの観点から考えます。 何より重要なのはオブジェクト型の動作と状態であり、それに対処するために、クラス、インターフェイス、継承、ポリモーフィズムなどの言語機能が用意されています。  
  
 一方、関数型プログラミングでは、計算の問題を、データ コレクションの純粋関数型変換の&1; つの課題として捉えます。 関数型プログラミングでは、状態や変化するデータを避け、関数の適用を重視します。  
  
 さいわい、Visual Basic では、命令型と関数の両方のプログラミング方法をサポートするために、関数型プログラミングに完全に移行が必要としません。 開発者は、個々のシナリオに適した方法を選択できます。 実際、プログラムで両方の方法が組み合わされている場合もよくあります。  
  
## <a name="see-also"></a>関連項目  
 [純粋関数型変換 (Visual Basic) の概要](../../../../visual-basic/programming-guide/concepts/linq/introduction-to-pure-functional-transformations.md)   
 [XSLT 変換](http://msdn.microsoft.com/library/202f8820-224c-494f-b61e-cd127eac6e03)   
 [純粋関数 (Visual Basic) へのリファクタリング](../../../../visual-basic/programming-guide/concepts/linq/refactoring-into-pure-functions.md)