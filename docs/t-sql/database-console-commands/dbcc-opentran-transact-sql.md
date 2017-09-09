---
title: "DBCC OPENTRAN (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC_OPENTRAN_TSQL
- DBCC OPENTRAN
- OPENTRAN_TSQL
- OPENTRAN
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server], transactions
- transactions [SQL Server], status information
- DBCC OPENTRAN statement
- open transactions
- displaying transaction information
- checking open transactions
- oldest transactions [SQL Server]
ms.assetid: 63163843-226f-42d3-9e2c-b634fbf06943
caps.latest.revision: 40
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f3d3b47d9bc553edd49f6f401d1a1c7a857d0a7d
ms.contentlocale: ja-jp
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-opentran-transact-sql"></a>DBCC OPENTRAN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

DBCC OPENTRAN はアクティブなトランザクションを識別するのに役立ち、ログの切り捨てを防ぐ目的でも使用できます。 DBCC OPENTRAN によって、指定したデータベースのトランザクション ログ内に存在する最も古いアクティブ トランザクション、および (存在する場合は) 最も古い分散型と非分散型のレプリケートされたトランザクションに関する情報が表示されます。 ログ内にアクティブ トランザクションが存在する場合、またはデータベースにレプリケーション情報が存在する場合にのみ、結果が表示されます。 ログ内にアクティブ トランザクションがない場合は、情報メッセージが表示されます。
  
> [!NOTE]  
>  DBCC OPENTRAN はサポートされていません以外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パブリッシャーです。  
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
DBCC OPENTRAN   
[   
    ( [ database_name | database_id | 0 ] ) ]  
    { [ WITH TABLERESULTS ]  
      [ , [ NO_INFOMSGS ] ]  
    }  
]   
```  
  
## <a name="arguments"></a>引数  
 *database_name* | *database_id*| 0  
 最も古いトランザクションに関する情報を表示するデータベースの名前または ID を指定します。 値を指定しないか 0 を指定した場合は、現在のデータベースが使用されます。 データベース名は、規則に従う必要があります[識別子](../../relational-databases/databases/database-identifiers.md)です。  
  
 TABLERESULTS  
 テーブルに読み込める表形式で結果を返すように指定します。 比較用としてテーブルに挿入できる表形式の結果を得たいときは、このオプションを指定します。 このオプションを指定しない場合、結果は読みやすい形式で返されます。  
  
 NO_INFOMSGS  
 すべての情報メッセージを表示しないようにします。  
  
## <a name="remarks"></a>解説  
DBCC OPENTRAN は、開かれたトランザクションがトランザクション ログ内に存在するかどうかを調べるときに使用します。 BACKUP LOG ステートメントを使用した場合は、ログの使用されていない部分しか切り捨てることができないため、開かれたトランザクションが存在すると、ログを完全に切り捨てることができなくなります。 開かれたトランザクションを識別するには、sp_who を使用してシステム プロセス ID を取得します。
  
## <a name="result-sets"></a>結果セット  
開かれたトランザクションがない場合、DBCC OPENTRAN は次の結果セットを返します。
  
```sql
No active open transactions.  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissions  
**sysadmin** 固定サーバー ロールまたは **db_owner** 固定データベース ロールのメンバーシップが必要です。
  
## <a name="examples"></a>使用例  
### <a name="a-returning-the-oldest-active-transaction"></a>A. 最も古いアクティブなトランザクションを返す  
次の例では、現在のデータベースのトランザクション情報を取得します。 結果は異なる場合があります。
  
```sql  
CREATE TABLE T1(Col1 int, Col2 char(3));  
GO  
BEGIN TRAN  
INSERT INTO T1 VALUES (101, 'abc');  
GO  
DBCC OPENTRAN;  
ROLLBACK TRAN;  
GO  
DROP TABLE T1;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`Transaction information for database 'master'.`
  
`Oldest active transaction:`
  
`SPID (server process ID) : 52`
  
`UID (user ID) : -1`
  
`Name          : user_transaction`
  
`LSN           : (518:1576:1)`
  
`Start time    : Jun  1 2004  3:30:07:197PM`
  
`SID           : 0x010500000000000515000000a065cf7e784b9b5fe77c87709e611500`
  
`DBCC execution completed. If DBCC printed error messages, contact your system administrator.`
  
> [!NOTE]  
>  "UID (ユーザー ID)"の結果は無意味であり、将来のバージョンで削除される予定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]です。  
  
### <a name="b-specifying-the-with-tableresults-option"></a>B. WITH TABLERESULTS オプションを指定する  
次の例では、DBCC OPENTRAN コマンドの結果を一時テーブルに読み込みます。
  
```sql  
-- Create the temporary table to accept the results.  
CREATE TABLE #OpenTranStatus (  
   ActiveTransaction varchar(25),  
   Details sql_variant   
   );  
-- Execute the command, putting the results in the table.  
INSERT INTO #OpenTranStatus   
   EXEC ('DBCC OPENTRAN WITH TABLERESULTS, NO_INFOMSGS');  
  
-- Display the results.  
SELECT * FROM #OpenTranStatus;  
GO  
```  
  
## <a name="see-also"></a>参照  
[BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)  
[トランザクションをコミット & #40 です。TRANSACT-SQL と #41 です。](../../t-sql/language-elements/commit-transaction-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DB_ID と #40 です。TRANSACT-SQL と #41 です。](../../t-sql/functions/db-id-transact-sql.md)  
[ROLLBACK TRANSACTION & #40 です。TRANSACT-SQL と #41 です。](../../t-sql/language-elements/rollback-transaction-transact-sql.md)
  
  
