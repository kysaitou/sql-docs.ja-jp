---
title: SQL Server のメッセージ結果 |Microsoft ドキュメント
description: SQL Server のメッセージ結果
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: d9ab76565bac6a1fbf41dd5f8372776ea8625975
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="sql-server-message-results"></a>SQL Server のメッセージ結果
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  次[!INCLUDE[tsql](../../../includes/tsql-md.md)]ステートメントは SQL Server の行セットまたは実行時に影響を受けた行のカウントの OLE DB ドライバーを生成しません。  
  
-   PRINT  
  
-   重大度が 10 以下の RAISERROR  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 上記のステートメントでは、行セットや行数の結果が返されるのではなく、ステートメントから 1 つ以上の情報メッセージが返されるか、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] から情報メッセージが返されます。 正常に実行される、S_OK を返すと、OLE DB Driver for SQL Server と、メッセージは、OLE DB Driver for SQL Server コンシューマーを使用できます。  
  
 SQL Server の OLE DB Driver は、S_OK を返しますおり、1 つまたは複数の情報メッセージの多くの実行を次に利用可能な[!INCLUDE[tsql](../../../includes/tsql-md.md)]ステートメントや、OLE DB Driver for SQL Server メンバー関数のコンシューマー実行します。  
  
 クエリ テキストの動的な指定を許可する SQL Server コンシューマーの OLE DB Driver は各メンバー関数の実行後に、値に関係なく、リターン コードの有無、返されるエラー インターフェイスを確認する必要があります**IRowset**または**IMultipleResults**インターフェイスの参照、または影響を受けた行の数。  
  
## <a name="see-also"></a>参照  
 [エラー](../../oledb/ole-db-errors/errors.md)  
  
  
