---
title: ".NET Framework のメソッドによるファイル操作 (Visual Basic) | Microsoft Docs"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- I/O [Visual Basic], walkthroughs
- text files, writing to
- reading text files
- text, writing to files
- files, searching
- StreamReader class, walkthroughs
- files, accessing
- I/O [Visual Basic], writing text to files
- writing to files, walkthroughs
- StreamWriter class, walkthroughs
- text files, reading
- I/O [Visual Basic], reading text from files
ms.assetid: 7d2109eb-f98a-4389-b43d-30f384aaa7d5
caps.latest.revision: 18
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e8bf73f32dba51455542778ed91ef3bfd2898754
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-manipulating-files-by-using-net-framework-methods-visual-basic"></a>チュートリアル: .NET Framework のメソッドによるファイル操作 (Visual Basic)
このチュートリアルでは、<xref:System.IO.StreamReader> クラスを使用してファイルを開いて読み取り、ファイルがアクセスされているかどうかをチェックし、<xref:System.IO.StreamReader> クラスのインスタンスを使用したファイル読み取り内の文字列を検索し、<xref:System.IO.StreamWriter> クラスを使用してファイルにデータを書き込む方法について説明します。  
  
[!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
## <a name="creating-the-application"></a>アプリケーションの作成  
 [!INCLUDE[vsprvs](../../../../csharp/includes/vsprvs_md.md)] を起動し、ユーザーが指定のファイルへの書き込みに使用できるフォームを作成して、プロジェクトを開始します。  
  
#### <a name="to-create-the-project"></a>プロジェクトを作成するには  
  
1.  **[ファイル]** メニューの **[新しいプロジェクト]** を選択します。  
  
2.  **[新しいプロジェクト]** ペインで、**[Windows アプリケーション]** をクリックします。  
  
3.  **[名前]** ボックスに `MyDiary` と入力して、**[OK]** をクリックします。  
  
     [!INCLUDE[vsprvs](../../../../csharp/includes/vsprvs_md.md)] の**ソリューション エクスプローラー**にプロジェクトが追加され、**Windows フォーム デザイナー**が開きます。  
  
4.  次の表にあるコントロールをフォームに追加し、それらのプロパティに対応する値を設定します。  
  
|**オブジェクト**|**プロパティ**|**値**|  
|---|---|---|   
|<xref:System.Windows.Forms.Button>|**名前**<br /><br /> **テキスト**|`Submit`<br /><br /> **エントリの送信**|  
|<xref:System.Windows.Forms.Button>|**名前**<br /><br /> **テキスト**|`Clear`<br /><br /> **エントリのクリア**|  
|<xref:System.Windows.Forms.TextBox>|**名前**<br /><br /> **テキスト**<br /><br /> **Multiline**|`Entry`<br /><br /> **テキストを入力してください。**<br /><br /> `False`|  
  
## <a name="writing-to-the-file"></a>ファイルへの書き込み  
 アプリケーションを通じてファイルに書き込む機能を追加するには、<xref:System.IO.StreamWriter> クラスを使用します。 <xref:System.IO.StreamWriter> は、特定のエンコードでの文字出力用に設計されています。これに対し <xref:System.IO.Stream> クラスは、バイト入出力用に設計されています。 標準のテキスト ファイルに複数行の情報を書き込む場合には、<xref:System.IO.StreamWriter> を使用します。 <xref:System.IO.StreamWriter> クラスについて詳しくは、「<xref:System.IO.StreamWriter>」をご覧ください。  
  
#### <a name="to-add-writing-functionality"></a>書き込み機能を追加するには  
  
1.  **[表示]** メニューの **[コード]** を選択してコード エディターを開きます。  
  
2.  アプリケーションで <xref:System.IO> 名前空間を参照するので、コードの先頭、つまりフォームのクラス宣言 (`Public Class Form1` で始まるブロック) よりも前に、次のステートメントを追加します。  
  
     [!code-vb[VbVbcnMyFileSystem#35](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_1.vb)]  
  
     ファイルへの書き込みを行う前に、<xref:System.IO.StreamWriter> クラスのインスタンスを作成する必要があります。  
  
3.  **[表示]** メニューの **[デザイナー]** を選択して、**Windows フォーム デザイナー**に戻ります。 `Submit` ボタンをダブルクリックしてボタンの <xref:System.Windows.Forms.Control.Click> イベント ハンドラーを作成し、次のコードを追加します。  
  
     [!code-vb[VbVbcnMyFileSystem#36](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_2.vb)]  
  
> [!NOTE]
>  Visual Studio 統合開発環境 (IDE) の画面がコード エディターに戻り、コードを追加するイベント ハンドラー内にカーソルが配置されます。  
  
1.  ファイルへの書き込みを行うには、<xref:System.IO.StreamWriter> クラスの <xref:System.IO.StreamWriter.Write%2A> メソッドを使用します。 `Dim fw As StreamWriter` の直後に次のコードを追加します。 ファイルが見つからない場合に例外がスローされることを心配する必要はありません。ファイルまだ存在しない場合は、新規に作成されます。  
  
     [!code-vb[VbVbcnMyFileSystem#37](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_3.vb)]  
  
2.  ユーザーが空のエントリを送信しないよう、`Dim ReadString As String` の直後に次のコードを追加します。  
  
     [!code-vb[VbVbcnMyFileSystem#38](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_4.vb)]  
  
3.  これは日記なので、ユーザーが各エントリに日付を割り当てられようにする必要があります。 `fw = New StreamWriter("C:\MyDiary.txt", True)` の後に次のコードを挿入して、変数 `Today` を現在の日付に設定します。  
  
     [!code-vb[VbVbcnMyFileSystem#39](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_5.vb)]  
  
4.  最後に、<xref:System.Windows.Forms.TextBox> をクリアするためのコードをアタッチします。 `Clear` ボタンの <xref:System.Windows.Forms.Control.Click> イベントに次のコードを追加します。  
  
     [!code-vb[VbVbcnMyFileSystem#40](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_6.vb)]  
  
## <a name="adding-display-features-to-the-diary"></a>日記に表示機能を追加する  
 このセクションでは、`DisplayEntry`<xref:System.Windows.Forms.TextBox> に最新のエントリを表示する機能を追加します。 さまざまなエントリを表示したり、表示するエントリをユーザーが選択できるようにするための、`DisplayEntry`<xref:System.Windows.Forms.ComboBox> を追加することもできます。 <xref:System.IO.StreamReader> クラスのインスタンスは、`MyDiary.txt` からデータを読み取ります。 <xref:System.IO.StreamWriter> クラスと同様、<xref:System.IO.StreamReader> はテキスト ファイル用です。  
  
 チュートリアルのこのセクション用に、次の表にあるコントロールをフォームに追加し、それらのプロパティに対応する値を設定します。  
  
|コントロール|プロパティ|値|  
|-------------|----------------|------------|  
|<xref:System.Windows.Forms.TextBox>|**名前**<br /><br /> **Visible**<br /><br /> **Size**<br /><br /> **Multiline**|`DisplayEntry`<br /><br /> `False`<br /><br /> `120,60`<br /><br /> `True`|  
|<xref:System.Windows.Forms.Button>|**名前**<br /><br /> **テキスト**|`Display`<br /><br /> **表示**|  
|<xref:System.Windows.Forms.Button>|**名前**<br /><br /> **テキスト**|`GetEntries`<br /><br /> **エントリの取得**|  
|<xref:System.Windows.Forms.ComboBox>|**名前**<br /><br /> **テキスト**<br /><br /> **Enabled**|`PickEntries`<br /><br /> **エントリの選択**<br /><br /> `False`|  
  
#### <a name="to-populate-the-combo-box"></a>コンボ ボックスを設定するには  
  
1.  `PickEntries`<xref:System.Windows.Forms.ComboBox> は、ユーザーが各エントリを送信する日付を表示するために使用されます。これにより、ユーザーが特定の日付からエントリを選択できるようになります。 `GetEntries` ボタンの <xref:System.Windows.Forms.Control.Click> イベント ハンドラーを作成し、次のコードを追加します。  
  
     [!code-vb[VbVbcnMyFileSystem#41](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_7.vb)]  
  
2.  コードをテストするには、F5 キーを押してアプリケーションをコンパイルし、**[エントリの取得]** をクリックします。 <xref:System.Windows.Forms.ComboBox> でドロップダウンの矢印をクリックして、エントリの日付を表示します。  
  
#### <a name="to-choose-and-display-individual-entries"></a>個別のエントリを選択して表示するには  
  
1.  `Display` ボタンの <xref:System.Windows.Forms.Control.Click> イベント ハンドラーを作成し、次のコードを追加します。  
  
     [!code-vb[VbVbcnMyFileSystem#42](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_8.vb)]  
  
2.  コードをテストするには、F5 キーを押してアプリケーションをコンパイルし、エントリを送信をクリックします。 **[エントリの取得]** をクリックし、 <xref:System.Windows.Forms.ComboBox> からエントリを選択して、**[表示]** をクリックします。 選択したエントリのコンテンツが、`DisplayEntry`<xref:System.Windows.Forms.TextBox> に表示されます。  
  
## <a name="enabling-users-to-delete-or-modify-entries"></a>ユーザーがエントリの削除や変更を行えるようにする  
 ユーザーが `DeleteEntry` ボタンと `EditEntry` ボタンを使用してエントリを削除したり変更したりできる機能を追加できます。 どちらのボタンも、エントリが表示されているとき以外は無効になります。  
  
 次の表にあるコントロールをフォームに追加し、それらのプロパティに対応する値を設定します。  
  
|コントロール|プロパティ|値|  
|-------------|----------------|------------|  
|<xref:System.Windows.Forms.Button>|**名前**<br /><br /> **テキスト**<br /><br /> **Enabled**|`DeleteEntry`<br /><br /> **エントリの削除**<br /><br /> `False`|  
|<xref:System.Windows.Forms.Button>|**名前**<br /><br /> **テキスト**<br /><br /> **Enabled**|`EditEntry`<br /><br /> **エントリの編集**<br /><br /> `False`|  
|<xref:System.Windows.Forms.Button>|**名前**<br /><br /> **テキスト**<br /><br /> **Enabled**|`SubmitEdit`<br /><br /> **編集結果の送信**<br /><br /> `False`|  
  
#### <a name="to-enable-deletion-and-modification-of-entries"></a>エントリの削除と変更を有効にするには  
  
1.  `Display` ボタンの <xref:System.Windows.Forms.Control.Click> イベント (`DisplayEntry.Text = ReadString` の後) に、次のコードを追加します。  
  
     [!code-vb[VbVbcnMyFileSystem#43](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_9.vb)]  
  
2.  `DeleteEntry` ボタンの <xref:System.Windows.Forms.Control.Click> イベント ハンドラーを作成し、次のコードを追加します。  
  
     [!code-vb[VbVbcnMyFileSystem#44](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_10.vb)]  
  
3.  ユーザーがエントリが表示すると、`EditEntry` ボタンが有効になります。 `Display` ボタンの <xref:System.Windows.Forms.Control.Click> イベント (`DisplayEntry.Text = ReadString` の後) に、次のコードを追加します。  
  
     [!code-vb[VbVbcnMyFileSystem#45](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_11.vb)]  
  
4.  `EditEntry` ボタンの <xref:System.Windows.Forms.Control.Click> イベント ハンドラーを作成し、次のコードを追加します。  
  
     [!code-vb[VbVbcnMyFileSystem#46](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_12.vb)]  
  
5.  `SubmitEdit` ボタンの <xref:System.Windows.Forms.Control.Click> イベント ハンドラーを作成し、次のコードを追加します  
  
     [!code-vb[VbVbcnMyFileSystem#47](../../../../visual-basic/developing-apps/programming/drives-directories-files/codesnippet/VisualBasic/walkthrough-manipulating-files-by-using-net-framework-methods_13.vb)]  
  
 コードをテストするには、F5 キーを押してアプリケーションをコンパイルします。 **[エントリの取得]** をクリックし、エントリを選択して、**[表示]** をクリックします。 `DisplayEntry`<xref:System.Windows.Forms.TextBox> にエントリが表示されます。 **[エントリの編集]** をクリックします。 `Entry`<xref:System.Windows.Forms.TextBox> にエントリが表示されます。 `Entry`<xref:System.Windows.Forms.TextBox> でエントリを編集し、**[編集結果の送信]** をクリックします。 `MyDiary.txt` ファイルを開いて修正結果を確認します。 確認したら、エントリを選択し、**[エントリの削除]** をクリックします。 <xref:System.Windows.Forms.MessageBox> で確認を求められたら、**[OK]** をクリックします。 アプリケーションを閉じ、`MyDiary.txt` を開いて削除を確認します。  
  
## <a name="see-also"></a>関連項目  
 <xref:System.IO.StreamReader>   
 <xref:System.IO.StreamWriter>   
 [チュートリアル](../../../../visual-basic/walkthroughs.md)
