---
title: "SET DATEFIRST (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET DATEFIRST
- SET_DATEFIRST_TSQL
- DATEFIRST_TSQL
- DATEFIRST
dev_langs:
- TSQL
helpviewer_keywords:
- first day of week [SQL Server]
- day of week [SQL Server]
- SET DATEFIRST option [SQL Server]
- DATEFIRST option [SQL Server]
- weekdays [SQL Server]
- options [SQL Server], date
ms.assetid: 6b0d0e52-8ac1-4f88-b091-f98d6fb8574a
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 193930e0050d50c8baee39aba4131cc7bf2dc6c4
ms.contentlocale: ja-jp
ms.lasthandoff: 09/01/2017

---
# <a name="set-datefirst-transact-sql"></a>SET DATEFIRST (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  週の最初の曜日を 1 ～ 7 の数値で設定します。  
  
 すべての概要については[!INCLUDE[tsql](../../includes/tsql-md.md)]日付と時刻のデータ型および関数を参照してください[日付と時刻のデータ型および関数 &#40;TRANSACT-SQL と #41 です。](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
SET DATEFIRST { number | @number_var }   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
SET DATEFIRST 7 ;  
```  
  
## <a name="arguments"></a>引数  
 *数* | **@***number_var*  
 週の最初の曜日を示す整数値を指定します。 値は次のいずれかを指定することができます。  
  
|値|週の最初の曜日|  
|-----------|------------------------------|  
|**1**|月曜日|  
|**2**|火曜日|  
|**3**|水曜日|  
|**4**|木曜日|  
|**5**|金曜日|  
|**6**|土曜日|  
|**7** (既定値、u. s.既定値)|日曜日|  
  
## <a name="remarks"></a>解説  
 SET DATEFIRST の現在の設定を表示するを使用して、 [@@DATEFIRST ](../../t-sql/functions/datefirst-transact-sql.md)関数。  
  
 SET DATEFIRST は、解析時ではなく実行時に設定されます。  
  
 SET DATEFIRST を指定しても DATEDIFF に影響はありません。 DATEDIFF では、週の最初の曜日として常に日曜日を使用し、関数が決定的であることを確認します。  
  
## <a name="permissions"></a>Permissions  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例は、日付の値の曜日を表示し、変更の効果を示しています、`DATEFIRST`設定します。  
  
```  
-- SET DATEFIRST to U.S. English default value of 7.  
SET DATEFIRST 7;  
  
SELECT CAST('1999-1-1' AS datetime2) AS SelectDate  
    ,DATEPART(dw, '1999-1-1') AS DayOfWeek;  
-- January 1, 1999 is a Friday. Because the U.S. English default   
-- specifies Sunday as the first day of the week, DATEPART of 1999-1-1  
-- (Friday) yields a value of 6, because Friday is the sixth day of the   
-- week when you start with Sunday as day 1.  
  
SET DATEFIRST 3;  
-- Because Wednesday is now considered the first day of the week,  
-- DATEPART now shows that 1999-1-1 (a Friday) is the third day of the   
-- week. The following DATEPART function should return a value of 3.  
SELECT CAST('1999-1-1' AS datetime2) AS SelectDate  
    ,DATEPART(dw, '1999-1-1') AS DayOfWeek;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>例:[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]と[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```  
-- SET DATEFIRST to U.S. English default value of 7.  
SET DATEFIRST 7;  
  
```  
  
## <a name="see-also"></a>参照  
 [SET ステートメント &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

