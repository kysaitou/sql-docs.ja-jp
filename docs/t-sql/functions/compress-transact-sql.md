---
title: COMPRESS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- COMPRESS
- COMPRESS_TSQL
helpviewer_keywords:
- COMPRESS function
ms.assetid: c2bfe9b8-57a4-48b4-b028-e1a3ed5ece88
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 893790448524a844b488478230db0f5141173ffd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="compress-transact-sql"></a>COMPRESS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

この関数は GZIP アルゴリズムを使用して、入力式を圧縮します。 この関数は **varbinary (max)** 型のバイト配列を返します。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
COMPRESS ( expression )  
```  
  
## <a name="arguments"></a>引数  
*式 (expression)*  
A

* **binary(***n***)**
* **char(***n***)**
* **nchar(***n***)**
* **nvarchar(max)**
* **nvarchar(***n***)**
* **varbinary(max)**
* **varbinary(***n***)**
* **varchar(max)**

内の複数の

* **varchar(***n***)**

expression。 詳細については、「[式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)」を参照してください。
  
## <a name="return-types"></a>戻り値の型
圧縮された入力内容を表す **varbinary (max)**。
  
## <a name="remarks"></a>Remarks  
圧縮されたデータにインデックスを付けることはできません。
  
`COMPRESS` 関数は入力式のデータを圧縮します。 圧縮するデータ セクションごとに、この関数を呼び出す必要があります。 ストレージ中の行またはページ レベルでの自動データ圧縮の詳細については、「[データ圧縮](../../relational-databases/data-compression/data-compression.md)」を参照してください。
  
## <a name="examples"></a>使用例  
  
### <a name="a-compress-data-during-the-table-insert"></a>A. 表の挿入中にデータを圧縮する  
この例では、テーブルに挿入されるデータを圧縮する方法を示します。
  
```sql
INSERT INTO player (name, surname, info )  
VALUES (N'Ovidiu', N'Cracium',   
        COMPRESS(N'{"sport":"Tennis","age": 28,"rank":1,"points":15258, turn":17}'));  
  
INSERT INTO player (name, surname, info )  
VALUES (N'Michael', N'Raheem', compress(@info));  
```  
  
### <a name="b-archive-compressed-version-of-deleted-rows"></a>B. 削除された行の圧縮バージョンをアーカイブする  
次のステートメントは、まず `player` テーブルから古いプレーヤー レコードを削除します。 次に、領域を節約するために、レコードを圧縮形式で `inactivePlayer` テーブルに格納します。
  
```sql
DELETE player  
WHERE datemodified < @startOfYear  
OUTPUT id, name, surname datemodifier, COMPRESS(info)   
INTO dbo.inactivePlayers ;  
```  
  
## <a name="see-also"></a>参照
[文字列関数 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  
[DECOMPRESS &#40;Transact-SQL&#41;](../../t-sql/functions/decompress-transact-sql.md)
  
  
