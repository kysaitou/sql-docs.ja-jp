---
title: PERCENTILE_DISC (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/20/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- PERCENTILE_DISC
- PERCENTILE_DISC_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PERCENTILE_DISC function
- analytic functions,PERCENTILE_DISC
ms.assetid: b545413d-c4f7-4c8e-8617-607599a26680
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c15033e0d5efc0b418b5c16ca15ba895907d5b34
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="percentiledisc-transact-sql"></a>PERCENTILE_DISC (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の行セット全体または行セットの別個のパーティション内で並べ替えられた値の特定の百分位数を計算します。 特定の百分位数 *P* の場合、PERCENTILE_DISC は ORDER BY 句で式の値を並べ替え、CUME_DIST 値が最小となる *P* 以上の値を返します (並べ替え仕様は同じ)。たとえば、PERCENTILE_DISC (0.5) は式の 50 番目の百分位数 (つまり、中央値) を計算します。 PERCENTILE_DISC は、列値の離散型分布に基づく百分位数を計算します。結果は列の特定の値と等しくなります。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
PERCENTILE_DISC ( numeric_literal ) WITHIN GROUP ( ORDER BY order_by_expression [ ASC | DESC ] )  
    OVER ( [ <partition_by_clause> ] )  
```  
  
## <a name="arguments"></a>引数  
 *literal*  
 計算する百分位数です。 値は 0.0 ～ 1.0 で指定してください。  
  
 WITHIN GROUP **(** ORDER BY *order_by_expression* [ **ASC** | DESC ]**)**  
 並べ替える値のリストを指定し、百分位数を計算します。 *order_by_expression* は 1 つだけ許可されます。 既定の並べ替え順は昇順です。 値のリストは、並べ替え操作に対して有効な任意のデータ型を指定できます。  
  
 OVER **(** \<partition_by_clause> **)**  
 FROM 句で生成された結果セットをパーティションに分割します。このパーティションにパーセンタイル関数が適用されます。 詳細については、を参照してください。 [経由句 (&) #40 です。TRANSACT-SQL と #41;](../../t-sql/queries/select-over-clause-transact-sql.md). \<ORDER BY clause> と \<rows or range clause> は PERCENTILE_DISC 関数では指定できません。  
  
## <a name="return-types"></a>戻り値の型  
 戻り値の型は *order_by_expression* の型によって決まります。  
  
## <a name="compatibility-support"></a>互換性サポート  
 互換性レベル 110 以上では、WITHIN GROUP は予約されたキーワードです。 詳細については、「[ALTER DATABASE 互換性レベル &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)」を参照してください。  
  
## <a name="general-remarks"></a>全般的な解説  
 データセット内の NULL はすべて無視されます。  
  
 PERCENTILE_DISC は非決定的です。 詳細については、「 [決定的関数と非決定的関数](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)」を参照してください。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-basic-syntax-example"></a>A. 基本構文例  
 次の例では、PERCENTILE_CONT と PERCENTILE_DISC を使用して、各部門の従業員給与の中央値を検索します。 これらの関数は同じ値を返さない可能性があります。 これは、データセットに存在するかどうかに関係なく PERCENTILE_CONT では適切な値が挿入されるためですが、PERCENTILE_DISC では常にセットから実際の値を返します。  
  
```  
USE AdventureWorks2012;  
  
SELECT DISTINCT Name AS DepartmentName  
      ,PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY ph.Rate)   
                            OVER (PARTITION BY Name) AS MedianCont  
      ,PERCENTILE_DISC(0.5) WITHIN GROUP (ORDER BY ph.Rate)   
                            OVER (PARTITION BY Name) AS MedianDisc  
FROM HumanResources.Department AS d  
INNER JOIN HumanResources.EmployeeDepartmentHistory AS dh   
    ON dh.DepartmentID = d.DepartmentID  
INNER JOIN HumanResources.EmployeePayHistory AS ph  
    ON ph.BusinessEntityID = dh.BusinessEntityID  
WHERE dh.EndDate IS NULL;  
```  
  
 次に結果セットの一部を示します。  
  
 ```
DepartmentName        MedianCont    MedianDisc
--------------------   ----------   ----------
Document Control       16.8269      16.8269
Engineering            34.375       32.6923
Executive              54.32695     48.5577
Human Resources        17.427850    16.5865
```
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] および [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-basic-syntax-example"></a>B. 基本構文例  
 次の例では、PERCENTILE_CONT と PERCENTILE_DISC を使用して、各部門の従業員給与の中央値を検索します。 これらの関数は同じ値を返さない可能性があります。 これは、データセットに存在するかどうかに関係なく PERCENTILE_CONT では適切な値が挿入されるためですが、PERCENTILE_DISC では常にセットから実際の値を返します。  
  
```  
-- Uses AdventureWorks  
  
SELECT DISTINCT DepartmentName  
       ,PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY BaseRate)  
        OVER (PARTITION BY DepartmentName) AS MedianCont  
       ,PERCENTILE_DISC(0.5) WITHIN GROUP (ORDER BY BaseRate)  
        OVER (PARTITION BY DepartmentName) AS MedianDisc  
FROM dbo.DimEmployee;  
  
```  
  
 次に結果セットの一部を示します。  
  
 ```
DepartmentName        MedianCont    MedianDisc  
--------------------   ----------   ----------  
Document Control       16.826900    16.8269  
Engineering            34.375000    32.6923  
Human Resources        17.427850    16.5865  
Shipping and Receiving  9.250000     9.0000
```  
  
## <a name="see-also"></a>参照  
 [PERCENTILE_CONT と #40 です。TRANSACT-SQL と #41 です。](../../t-sql/functions/percentile-cont-transact-sql.md)  
  
  


