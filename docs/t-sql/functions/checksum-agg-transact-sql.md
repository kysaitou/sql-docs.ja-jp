---
title: CHECKSUM_AGG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CHECKSUM_AGG
- CHECKSUM_AGG_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- checksum values
- CHECKSUM_AGG function
- groups [SQL Server], checksum values
ms.assetid: cdede70c-4eb5-4c92-98ab-b07787ab7222
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 54e82e66d2f5ba49291cadf0cef198733cb7e0e0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="checksumagg-transact-sql"></a>CHECKSUM_AGG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

この関数はグループ内の値のチェックサムを返します。 `CHECKSUM_AGG` は null 値を無視します。 [OVER 句](../../t-sql/queries/select-over-clause-transact-sql.md)は `CHECKSUM_AGG` に続けることができます。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
CHECKSUM_AGG ( [ ALL | DISTINCT ] expression )  
```  
  
## <a name="arguments"></a>引数  
**ALL**  
すべての値にこの集計関数を適用します。 ALL が既定の引数です。
  
DISTINCT  
`CHECKSUM_AGG` で、一意な値のチェックサムを返します。
  
*式 (expression)*  
整数[式](../../t-sql/language-elements/expressions-transact-sql.md)です。 `CHECKSUM_AGG` では、サブクエリまたは集計関数の使用は許可されません。
  
## <a name="return-types"></a>戻り値の型
すべてのチェックサムを返します *式* 値としての **int**です。
  
## <a name="remarks"></a>Remarks  
`CHECKSUM_AGG` は、テーブルの変更を検出できます。
  
`CHECKSUM_AGG` の結果は、テーブル内の行の順序に依存しません。 また、`CHECKSUM_AGG` 関数では、DISTINCT キーワードおよび GROUP BY 句の使用が許可されます。
  
式リストの値が変更された場合、リストのチェックサム値リストも変更される可能性があります。 ただし、まれには、計算されたチェックサムが変更されない可能性があります。
  
`CHECKSUM_AGG` には、他の集計関数と同様の機能があります。 詳細については、を参照してください。 [集計関数 (&) #40 です。TRANSACT-SQL と #41;](../../t-sql/functions/aggregate-functions-transact-sql.md).
  
## <a name="examples"></a>使用例  
次の例では、`CHECKSUM_AGG` を使用して、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースの `ProductInventory` テーブルの `Quantity` 列の変更を検出します。
  
```sql
--Get the checksum value before the column value is changed.  
SELECT CHECKSUM_AGG(CAST(Quantity AS int))  
FROM Production.ProductInventory;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
------------------------  
262  
```  
  
```sql
UPDATE Production.ProductInventory   
SET Quantity=125  
WHERE Quantity=100;  
GO  
--Get the checksum of the modified column.  
SELECT CHECKSUM_AGG(CAST(Quantity AS int))  
FROM Production.ProductInventory;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
------------------------  
287  
```  
  
## <a name="see-also"></a>参照
[チェックサム (&) #40 です。TRANSACT-SQL と #41 です。](../../t-sql/functions/checksum-transact-sql.md)  
[句 (&) #40 です。TRANSACT-SQL と #41 です。](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  
