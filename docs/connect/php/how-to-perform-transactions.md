---
title: '方法: トランザクションを実行 |Microsoft ドキュメント'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transaction support
ms.assetid: f4643b85-f929-4919-8951-23394bc5bfa7
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fe11037ad2b7a5ae0f927a0880537adf67594899
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-perform-transactions"></a>方法: トランザクションを実行する
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] の SQLSRV ドライバーには、トランザクションを実行する 3 つの関数があります。  
  
-   [sqlsrv_begin_transaction](../../connect/php/sqlsrv-begin-transaction.md)  
  
-   [sqlsrv_commit](../../connect/php/sqlsrv-commit.md)  
  
-   [sqlsrv_rollback](../../connect/php/sqlsrv-rollback.md)  
  
PDO_SQLSRV ドライバーには、トランザクションを実行する 3 つの方法があります。  
  
-   [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md)  
  
-   [PDO::commit](../../connect/php/pdo-commit.md)  
  
-   [PDO::rollback](../../connect/php/pdo-rollback.md)  
  
例については、「 [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) 」を参照してください。  
  
このトピックの後半では、SQLSRV ドライバーを使用してトランザクションを実行する方法を説明し、例を示します。  
  
## <a name="remarks"></a>解説  
トランザクションを実行する手順の概要は次のとおりです。  
  
1.  使用してトランザクションを開始**sqlsrv_begin_transaction**です。  
  
2.  トランザクションに含まれる各クエリの成功または失敗を確認します。  
  
3.  必要に応じて、 **sqlsrv_commit**を使用してトランザクションを開始します。 コミットしない場合、 **sqlsrv_rollback**を使用してトランザクションを開始します。 呼び出した後**sqlsrv_commit**または**sqlsrv_rollback**ドライバーは自動コミット モードに返されます。  
  
    既定では、[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]自動コミット モードにします。 これは、すべてのクエリは、 **sqlsrv_begin_transaction**を使用してトランザクションを開始します。  
  
    場合は、明示的なトランザクションを使用してコミットは**sqlsrv_commit**、時、接続の終了またはスクリプトの終了時にロールバックされます。  
  
    トランザクションの実行に、埋め込みの Transact SQL を使用しないでください。 たとえば、トランザクションを開始するために、"BEGIN TRANSACTION" を Transact-SQL クエリとして使用してステートメントを実行しないでください。 埋め込みの Transact-SQL を使用してトランザクションを実行した場合、予測されるトランザクションの動作は保証できません。  
  
    トランザクションを実行するには、前述の **sqlsrv** 関数を使用する必要があります。  
  
## <a name="example"></a>例  
  
### <a name="description"></a>Description  
次の例では、トランザクションの一部としていくつかのクエリを実行します。 すべてのクエリが成功すると、トランザクションはコミットされます。 いずれかのクエリが失敗すると、トランザクションはロールバックされます。  
  
この例では、 *Sales.SalesOrderDetail* テーブルから販売注文を削除し、販売注文の各製品について *Product.ProductInventory* テーブルの製品インベントリ レベルを調整します。 データベースに注文および製品の入手の状態を正確に反映するには、これらのクエリすべてが成功する必要があるため、トランザクションに含まれています。  
  
この例の最初のクエリでは、指定された販売注文 ID の製品 ID と数量を取得します。 このクエリは、トランザクションの一部ではありません。 ただし、以降のトランザクションに含まれるクエリを完了するために製品 ID と数量が必要なので、このクエリが失敗すると、スクリプトは終了します。  
  
これらのクエリ (販売注文の削除と、製品在庫の数量の更新) の成功は、トランザクションの一部です。  
  
例では、SQL Server および[AdventureWorks](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works)データベースがローカル コンピューターにインストールされています。 コマンド ラインからこの例を実行すると、すべての出力はコンソールに書き込まれます。  
  
### <a name="code"></a>コード  
  
```  
<?php  
/* Connect to the local server using Windows Authentication and  
specify the AdventureWorks database as the database in use. */  
$serverName = "(local)";  
$connectionInfo = array( "Database"=>"AdventureWorks");  
$conn = sqlsrv_connect( $serverName, $connectionInfo);  
if( $conn === false )  
{  
     echo "Could not connect.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Begin transaction. */  
if( sqlsrv_begin_transaction($conn) === false )   
{   
     echo "Could not begin transaction.\n";  
     die( print_r( sqlsrv_errors(), true));  
}  
  
/* Set the Order ID.  */  
$orderId = 43667;  
  
/* Execute operations that are part of the transaction. Commit on  
success, roll back on failure. */  
if (perform_trans_ops($conn, $orderId))  
{  
     //If commit fails, roll back the transaction.  
     if(sqlsrv_commit($conn))  
     {  
         echo "Transaction committed.\n";  
     }  
     else  
     {  
         echo "Commit failed - rolling back.\n";  
         sqlsrv_rollback($conn);  
     }  
}  
else  
{  
     "Error in transaction operation - rolling back.\n";  
     sqlsrv_rollback($conn);  
}  
  
/*Free connection resources*/  
sqlsrv_close( $conn);  
  
/*----------------  FUNCTION: perform_trans_ops  -----------------*/  
function perform_trans_ops($conn, $orderId)  
{  
    /* Define query to update inventory based on sales order info. */  
    $tsql1 = "UPDATE Production.ProductInventory   
              SET Quantity = Quantity + s.OrderQty   
              FROM Production.ProductInventory p   
              JOIN Sales.SalesOrderDetail s   
              ON s.ProductID = p.ProductID   
              WHERE s.SalesOrderID = ?";  
  
    /* Define the parameters array. */  
    $params = array($orderId);  
  
    /* Execute the UPDATE statement. Return false on failure. */  
    if( sqlsrv_query( $conn, $tsql1, $params) === false ) return false;  
  
    /* Delete the sales order. Return false on failure */  
    $tsql2 = "DELETE FROM Sales.SalesOrderDetail   
              WHERE SalesOrderID = ?";  
    if(sqlsrv_query( $conn, $tsql2, $params) === false ) return false;  
  
    /* Return true because all operations were successful. */  
    return true;  
}  
?>  
```  
  
### <a name="comments"></a>コメント  
トランザクションの動作を重視するため、いくつかの推奨されるエラー処理は前の例には含まれていません。 実稼働アプリケーションでは、確認をお勧めへの呼び出し、 **sqlsrv**エラー機能し、それに応じて処理します。
  
## <a name="see-also"></a>参照  
[データの更新 &#40;Microsoft Drivers for PHP for SQL Server&#41;](../../connect/php/updating-data-microsoft-drivers-for-php-for-sql-server.md)

[トランザクション (データベース エンジン)](https://msdn.microsoft.com/library/ms190612.aspx)

[ドキュメントのコード例について](../../connect/php/about-code-examples-in-the-documentation.md)  
  
