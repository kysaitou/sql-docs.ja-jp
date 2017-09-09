---
title: "(TRANSACT-SQL) のような |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ESCAPE
- LIKE
- ESCAPE_TSQL
- LIKE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ESCAPE keyword
- '% (wildcard - character(s) to match)'
- ASCII pattern matching
- pattern searching [SQL Server]
- wildcard characters [SQL Server]
- literals [SQL Server], using wildcards
- character strings [SQL Server], LIKE
- exact matches [SQL Server]
- Boolean functions
- LIKE comparisons
- matching patterns [SQL Server]
- NOT LIKE keyword
ms.assetid: 581fb289-29f9-412b-869c-18d33a9e93d5
caps.latest.revision: 50
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 643966017caf06959fef24177dd93d7254f30915
ms.contentlocale: ja-jp
ms.lasthandoff: 09/01/2017

---
# <a name="like-transact-sql"></a>LIKE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指定された文字列が指定されたパターンと一致するかどうかを判断します。 パターンは、標準の文字とワイルドカード文字を含むことができます。 パターン検索時に、標準の文字は文字列に指定された文字と正確に一致する必要があります。 しかし、ワイルドカード文字は文字列の任意の部分と一致することができます。 = や != などの文字列比較演算子を使用する場合と比べて、ワイルドカード文字を使用する方がより柔軟に LIKE 演算子を使用できます。 引数が文字列データ型でない場合、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]は可能であれば引数を文字列データ型に変換します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
match_expression [ NOT ] LIKE pattern [ ESCAPE escape_character ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
match_expression [ NOT ] LIKE pattern  
```  
  
## <a name="arguments"></a>引数  
 *match_expression*  
 有効な[式](../../t-sql/language-elements/expressions-transact-sql.md)の文字データ型。  
  
 *パターン*  
 特定の文字列内で検索する文字の*match_expression*、次の有効なワイルドカード文字を含めることができます。 *パターン*8,000 バイトの最大数を指定できます。  
  
|ワイルドカード文字|Description|例|  
|------------------------|-----------------|-------------|  
|%|0 個以上の文字で構成される任意の文字列です。|WHERE title LIKE '%computer%' と指定すると、書籍名に "computer" という単語が含まれるすべての書籍が検索されます。|  
|_ (アンダースコア)|任意の 1 文字です。|WHERE au_fname LIKE '_ean' と指定すると、ean で終わる 4 文字のすべての名 (Dean、Sean など) が検索されます。|  
|[ ]|指定した範囲 ([a-f]) またはセット ([abcdef]) 内にある任意の 1 文字です。|WHERE au_lname LIKE '[C-P]arsen' と指定すると、Carsen、Larsen、Karsen などのように、姓が C から P の間にある任意の 1 文字で始まり、arsen で終わる著者が検索されます。 範囲で検索する場合、照合順序の並べ替え規則に応じて範囲に含まれる文字が変わります。|  
|[^]|指定した範囲 ([^a-f]) またはセット ([^abcdef]) 内にない任意の 1 文字です。|WHERE au_lname LIKE 'de[^l]%' と指定すると、姓が de で始まり、次の文字が l ではないすべての著者が検索されます。|  
  
 *escape_character*  
 特定のワイルドカードがワイルドカードとしてではなく標準の文字として解釈されるようにするために、そのワイルドカードの前に配置する文字です。 *escape_character*既定されておらず、1 つだけの文字に評価される必要があります文字式です。  
  
## <a name="result-types"></a>戻り値の型  
 **ブール値**  
  
## <a name="result-value"></a>結果の値  
 ような場合に TRUE を返します、 *match_expression* 、指定された一致*パターン*です。  
  
## <a name="remarks"></a>解説  
 LIKE を使用して文字列の比較を行うときは、パターン文字列中のすべての文字が比較の対象になります。 これには、パターンの先頭の空白や後続する空白も含まれます。 クエリ内の比較で LIKE 'abc ' 文字列 (abc に空白が 1 つ続く) を含むすべての行が返される場合、列の値が"abc" (abc の後ろに空白がない) の行は返されません。 ただし、パターンが一致する式の中の後続する空白は無視されます。 クエリ内の比較で LIKE 'abc' 文字列 (abc の後ろに空白がない) を含むすべての行が返される場合、"abc" で始まり、0 または空白が後続するすべての行が返されます。  
  
 含むパターンを使用して、文字列比較**char**と**varchar**データは、データの格納方法により、LIKE 比較をパスできません可能性があります。 各データ型の格納方法や、LIKE 比較ができない場合について理解しておく必要があります。 次の例では、ローカル**char**ストアド プロシージャとし、使用パターンと一致するすべての従業員の最後で始まる指定された文字のセットを検索する変数。  
  
```tsql
-- Uses AdventureWorks  
  
CREATE PROCEDURE FindEmployee @EmpLName char(20)  
AS  
SELECT @EmpLName = RTRIM(@EmpLName) + '%';  
SELECT p.FirstName, p.LastName, a.City  
FROM Person.Person p JOIN Person.Address a ON p.BusinessEntityID = a.AddressID  
WHERE p.LastName LIKE @EmpLName;  
GO  
EXEC FindEmployee @EmpLName = 'Barb';  
GO  
```  
  
 `FindEmployee`プロシージャ、行が返されないため、 **char**変数 (`@EmpLName`) 名前には、20 文字未満が含まれている場合、後続する空白が含まれています。 `LastName`列は**varchar**、末尾の空白を入れません。 後続する空白が意味を持つため、このプロシージャは失敗します。  
  
 ただし、次の例は成功を後続の空白が追加されないので、 **varchar**変数。  
  
```tsql
-- Uses AdventureWorks  
  
CREATE PROCEDURE FindEmployee @EmpLName varchar(20)  
AS  
SELECT @EmpLName = RTRIM(@EmpLName) + '%';  
SELECT p.FirstName, p.LastName, a.City  
FROM Person.Person p JOIN Person.Address a ON p.BusinessEntityID = a.AddressID  
WHERE p.LastName LIKE @EmpLName;  
GO  
EXEC FindEmployee @EmpLName = 'Barb';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 FirstName      LastName            City
 ----------     -------------------- --------------- 
 Angela         Barbariol            Snohomish
 David          Barber               Snohomish
 (2 row(s) affected)  
 ``` 
 
## <a name="pattern-matching-by-using-like"></a>LIKE を使用するパターン検索  
 LIKE では、ASCII パターン検索と Unicode パターン検索を行えます。 ときにすべての引数 (*match_expression*、*パターン*、および*escape_character*がある場合)、ASCII 文字データ型は、ASCII パターン マッチが行わします。 引数のいずれかが Unicode データ型の場合は、すべての引数が Unicode に変換され、Unicode パターン検索が行われます。 Unicode データを使用する場合 (**nchar**または**nvarchar**データ型) と同様、後続する空白は重要です。 ただし、非 Unicode データの末尾の空白は意味を持ちません。 Unicode LIKE は、ISO 標準と互換性があります。 ASCII LIKE は、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と互換性があります。  
  
 次の一連の例では、ASCII LIKE パターン検索と Unicode LIKE パターン検索で返される行の違いを示します。  
  
```tsql  
-- ASCII pattern matching with char column  
CREATE TABLE t (col1 char(30));  
INSERT INTO t VALUES ('Robert King');  
SELECT *   
FROM t   
WHERE col1 LIKE '% King';   -- returns 1 row  
  
-- Unicode pattern matching with nchar column  
CREATE TABLE t (col1 nchar(30));  
INSERT INTO t VALUES ('Robert King');  
SELECT *   
FROM t   
WHERE col1 LIKE '% King';   -- no rows returned  
  
-- Unicode pattern matching with nchar column and RTRIM  
CREATE TABLE t (col1 nchar (30));  
INSERT INTO t VALUES ('Robert King');  
SELECT *   
FROM t   
WHERE RTRIM(col1) LIKE '% King';   -- returns 1 row  
```  
  
> [!NOTE]  
>  LIKE 比較は、照合順序の影響を受けます。 詳細については、「[COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)」を参照してください。  
  
## <a name="using-the--wildcard-character"></a>% ワイルドカード文字の使用  
 場合、LIKE '5%' 記号を指定すると、[!INCLUDE[ssDE](../../includes/ssde-md.md)]続く 0 個以上の文字の文字列を数字の 5 を検索します。  
  
 たとえば、次のクエリは、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベース内のすべての動的管理ビューを表示します。これらのすべての動的管理ビューは、文字 `dm` で始まるためです。  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT Name  
FROM sys.system_views  
WHERE Name LIKE 'dm%';  
GO  
```  
  
 動的管理ビューではないすべてのオブジェクトを表示する`NOT LIKE 'dm%'`です。 仮に、オブジェクトの総数が 32、LIKE パターンに一致する名前が 13 件発見されるとすると、NOT LIKE では、LIKE パターンに一致しないオブジェクトを 19 件発見します。  
  
 `LIKE '[^d][^m]%'` のようなパターンと一致する名前が検索されるとは限りません。 19 名は、代わりにのみ 14 で始まるすべての名前を見つけることがあります`d`も`m`結果、および動的管理ビューの名前から削除する 2 番目の文字として。 これは、否定ワイルドカード文字を使用した検索文字列は 1 文字ずつ順番に評価されるために生じます。 評価のいずれかの段階で一致しなければ、削除されます。  
  
## <a name="using-wildcard-characters-as-literals"></a>リテラルとしてのワイルドカード文字の使用  
 ワイルドカード パターン検索文字をリテラル文字として使用できます。 ワイルドカード文字をリテラル文字として使用するには、ワイルドカード文字をかっこで囲みます。 次の表は、LIKE キーワードと [ ] ワイルドカード文字の使用例を示しています。  
  
|記号|意味|  
|------------|-------------|  
|LIKE '5[%]'|5%|  
|LIKE '[_]n'|_n|  
|LIKE '[a-cdf]'|a、b、c、d、または f|  
|LIKE '[-acdf]'|-、a、c、d、または f|  
|LIKE '[ [ ]'|[|  
|LIKE ']'|]|  
|LIKE 'abc[_]d%'|abc_d および abc_de|  
|LIKE 'abc[def]'|abcd、abce、および abcf|  
  
## <a name="pattern-matching-with-the-escape-clause"></a>ESCAPE 句を使用するパターン検索  
 1 文字以上の特殊なワイルドカード文字を含む文字列を検索できます。 たとえば、customers データベース内の discounts テーブルには、パーセント記号 (%) を含む割引の値が格納されています。 ワイルドカード文字ではなく、文字としてパーセント記号を検索するには、ESCAPE キーワードとエスケープ文字を指定する必要があります。 たとえば、サンプル データベースには、"30%" というテキストを含んでいる comment という名前の列があります。 comment 列内の任意の場所で文字列 "30%" を含んでいる任意の行を検索するには、`WHERE comment LIKE '%30!%%' ESCAPE '!'` などの WHERE 句を指定します。 ESCAPE とエスケープ文字を指定していない場合、[!INCLUDE[ssDE](../../includes/ssde-md.md)]は文字列 "30" を含む行を返します。  
  
 LIKE パターンでエスケープ文字の後に文字がない場合、そのパターンは無効になり、LIKE は FALSE を返します。 エスケープ文字の後にある文字がワイルドカード文字ではない場合、このパターンの中ではエスケープ文字は破棄され、エスケープ文字の次の文字が通常の文字として扱われます。 これには、2 つの角かっこ ([ ]) に囲まれたパーセント記号 (%)、アンダースコア (_)、および左角かっこ ([) の各ワイルドカード文字が含まれます。 また、2 つの角かっこ ([ ]) で囲んだ場合は、エスケープ文字は使用することができ、キャレット (^)、ハイフン (-)、および右角かっこ (]) はエスケープできます。  
  
 0x0000 (**char (0)**) の Windows 照合順序で未定義の文字は、LIKE に含めることはできません。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-like-with-the--wildcard-character"></a>A. LIKE を % ワイルドカード文字と共に使用する  
 次の例では、`415` テーブルで市外局番 `PersonPhone` を持つすべての電話番号を検索します。  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName, ph.PhoneNumber  
FROM Person.PersonPhone AS ph  
INNER JOIN Person.Person AS p  
ON ph.BusinessEntityID = p.BusinessEntityID  
WHERE ph.PhoneNumber LIKE '415%'  
ORDER by p.LastName;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
 
 ```
 FirstName             LastName             Phone
 -----------------     -------------------  ------------
 Ruben                 Alonso               415-555-124  
 Shelby                Cook                 415-555-0121  
 Karen                 Hu                   415-555-0114  
 John                  Long                 415-555-0147  
 David                 Long                 415-555-0123  
 Gilbert               Ma                   415-555-0138  
 Meredith              Moreno               415-555-0131  
 Alexandra             Nelson               415-555-0174  
 Taylor                Patterson            415-555-0170  
 Gabrielle              Russell             415-555-0197  
 Dalton                 Simmons             415-555-0115  
 (11 row(s) affected)  
 ``` 
 
### <a name="b-using-not-like-with-the--wildcard-character"></a>B. NOT LIKE を % ワイルドカード文字と共に使用する  
 次の例では、`PersonPhone` テーブルで `415` 以外の市外局番を持つすべての電話番号を検索します。  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT p.FirstName, p.LastName, ph.PhoneNumber  
FROM Person.PersonPhone AS ph  
INNER JOIN Person.Person AS p  
ON ph.BusinessEntityID = p.BusinessEntityID  
WHERE ph.PhoneNumber NOT LIKE '415%' AND p.FirstName = 'Gail'  
ORDER BY p.LastName;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
 
 ```
FirstName              LastName            Phone
---------------------- -------------------- -------------------
Gail                  Alexander            1 (11) 500 555-0120  
Gail                  Butler               1 (11) 500 555-0191  
Gail                  Erickson             834-555-0132  
Gail                  Erickson             849-555-0139  
Gail                  Griffin              450-555-0171  
Gail                  Moore                155-555-0169  
Gail                  Russell              334-555-0170  
Gail                  Westover             305-555-0100  
(8 row(s) affected)  
```  

### <a name="c-using-the-escape-clause"></a>C. ESCAPE 句を使用する  
 次の例では、`ESCAPE`句とエスケープ文字を正確な文字の文字列を検索する`10-15%`列で`c1`の`mytbl2`テーブル。  
  
```tsql
USE tempdb;  
GO  
IF EXISTS(SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES  
      WHERE TABLE_NAME = 'mytbl2')  
   DROP TABLE mytbl2;  
GO  
USE tempdb;  
GO  
CREATE TABLE mytbl2  
(  
 c1 sysname  
);  
GO  
INSERT mytbl2 VALUES ('Discount is 10-15% off'), ('Discount is .10-.15 off');  
GO  
SELECT c1   
FROM mytbl2  
WHERE c1 LIKE '%10-15!% off%' ESCAPE '!';  
GO  
```  
  
### <a name="d-using-the---wildcard-characters"></a>D. [ ] ワイルドカード文字を使用する  
 次の例は、上の従業員を検索、`Person`の最初の名前を持つテーブル`Cheryl`または`Sheryl`です。  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT BusinessEntityID, FirstName, LastName   
FROM Person.Person   
WHERE FirstName LIKE '[CS]heryl';  
GO  
```  
  
 次の例では、内の従業員の行を検索、`Person`の最後の名前を持つテーブル`Zheng`または`Zhang`です。  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT LastName, FirstName  
FROM Person.Person  
WHERE LastName LIKE 'Zh[ae]ng'  
ORDER BY LastName ASC, FirstName ASC;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例:[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]と[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-like-with-the--wildcard-character"></a>E. LIKE を % ワイルドカード文字と共に使用する  
 次の例は、のすべての従業員を検索、`DimEmployee`で始まる電話番号を持つテーブル`612`です。  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, Phone  
FROM DimEmployee  
WHERE phone LIKE '612%'  
ORDER by LastName;  
```  
  
### <a name="f-using-not-like-with-the--wildcard-character"></a>F. NOT LIKE を % ワイルドカード文字と共に使用する  
 次の例は、内のすべての電話番号を検索、`DimEmployee`で始まらないテーブル`612`です。  のインスタンスにアクセスするたびに SQL Server ログインを指定する必要はありません。  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, Phone  
FROM DimEmployee  
WHERE phone NOT LIKE '612%'  
ORDER by LastName;  
```  
  
### <a name="g-using-like-with-the--wildcard-character"></a>G. 使用するようを _ のワイルドカード文字  
 次の例で始まる市外局番を持つすべての電話番号を検索する`6`と最終`2`で、`DimEmployee`テーブル。 市外局番、電話番号の最初の部分と追加の文字が、列の値の後に存在するためには、% ワイルドカード文字が、検索パターンの末尾に含まれてもことに注意してください。  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, Phone  
FROM DimEmployee  
WHERE phone LIKE '6_2%'  
ORDER by LastName;   
```  
  
### <a name="h-using-the---wildcard-characters"></a>H. [ ] ワイルドカード文字を使用する  
 次の例検索`DimEmployee`の姓を持つ行`Rob`または`Bob`です。  
  
```tsql  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, Phone  
FROM DimEmployee  
WHERE FirstName LIKE '[RB]ob'  
ORDER by LastName;  
```  
  
## <a name="see-also"></a>参照  
 [式 & #40 です。TRANSACT-SQL と #41 です。](../../t-sql/language-elements/expressions-transact-sql.md)   
 [組み込み関数 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [ここで & #40 です。TRANSACT-SQL と #41 です。](../../t-sql/queries/where-transact-sql.md)  
 
