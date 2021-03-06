---
title: XSL 変換 (SQLXMLOLEDB プロバイダー) の適用 |Microsoft ドキュメント
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLXMLOLEDB Provider, applying XSL transformations
- applying XSL transformations [SQLXML]
- xsl property
- Base Path property
- XSL Transformations [SQLXML]
ms.assetid: cb5e41ab-dd20-4873-af20-f417bd1bbf6d
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e4b71d22ddc26dc72f2cbb203178f416fbe3d28c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
ms.locfileid: "32969563"
---
# <a name="applying-an-xsl-transformation-sqlxmloledb-provider"></a>XSL 変換の適用 (SQLXMLOLEDB プロバイダー)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  このサンプル ADO アプリケーションでは、SQL クエリが実行され、結果に XSL 変換が適用されます。 ClientSideXML プロパティを True に設定すると、クライアント側で行セットの処理が適用されます。 SQL クエリをテンプレートで指定する場合は、テンプレート実行時にコマンド言語を指定する必要があるため、コマンド言語 {5d531cb2-e6ed-11d2-b252-00c04f681b71} を設定します。 Xsl プロパティでは、変換の適用に使用する XSL ファイルを指定します。 Base Path プロパティの値は、XSL ファイルの検索に使用されます。 Xsl プロパティの値にパスを指定する場合、パス Base Path プロパティで指定されているパスの相対パスです。  
  
 この例では、次の SQLXMLOLEDB プロバイダー固有のプロパティについて、使用法を示します。  
  
-   ClientSideXML  
  
-   xsl  
  
 このクライアント側の ADO サンプル アプリケーションでは、SQL クエリで構成される XML テンプレートがサーバーで実行されます。  
  
 ClientSideXML プロパティが True に設定されているために、FOR XML 句のない SELECT ステートメントは、サーバーに送信されます。 サーバーではクエリが実行され、クライアントに行セットが返されます。 クライアントは、行セットに FOR XML 変換を適用し、XML ドキュメントを生成します。  
  
 Xsl プロパティは、アプリケーションで指定されました。そのため、クライアントでは、生成される XML ドキュメントに XSL 変換を適用し、結果は 2 列のテーブルです。  
  
 テンプレート コマンドを実行するには、XML テンプレート言語 {5d531cb2-e6ed-11d2-b252-00c04f681b71} を指定する必要があります。  
  
> [!NOTE]  
>  コードでは、接続文字列に Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス名を含める必要があります。 また、この例ではデータ プロバイダーとして [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client を使用するよう指定していますが、これには追加ネットワーク クライアントがインストールされていることが必要です。 詳細については、次を参照してください。 [SQL Server Native Client のシステム要件](../../../relational-databases/native-client/system-requirements-for-sql-server-native-client.md)です。  
  
```  
Option Explicit  
Sub main()  
Dim oTestStream As New ADODB.Stream  
Dim oTestConnection As New ADODB.Connection  
Dim oTestCommand As New ADODB.Command  
oTestConnection.Open "provider=SQLXMLOLEDB.4.0;data provider=SQLNCLI11;data source=SqlServerName;initial catalog=AdventureWorks;Integrated Security=SSPI;"  
Set oTestCommand.ActiveConnection = oTestConnection  
oTestCommand.Properties("ClientSideXML") = True  
oTestCommand.CommandText = _  
        "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql' >" & _  
       " <sql:query> " & _  
        "   SELECT TOP 25 FirstName, LastName FROM Person.Contact FOR XML AUTO " & _  
        "   </sql:query> " & _  
        " </ROOT> "  
oTestStream.Open  
' You need the dialect if you are executing a template.  
oTestCommand.Dialect = "{5d531cb2-e6ed-11d2-b252-00c04f681b71}"  
oTestCommand.Properties("Output Stream").Value = oTestStream  
oTestCommand.Properties("Base Path").Value = "c:\Schemas\SQLXML4\ExecuteTemplateWithXSL\"  
oTestCommand.Properties("xsl").Value = "myxsl.xsl"  
oTestCommand.Execute , , adExecuteStream  
  
oTestStream.Position = 0  
oTestStream.Charset = "utf-8"  
Debug.Print oTestStream.ReadText(adReadAll)  
End Sub  
Sub Form_Load()  
 main  
End Sub  
```  
  
 次は XSL テンプレートです。 この XSL テンプレートを適用すると、2 列のテーブルが生成されます。  
  
```  
<?xml version='1.0' encoding='UTF-8'?>            
 <xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">   
  
    <xsl:template match = 'Person.Contact'>  
       <TR>  
         <TD><xsl:value-of select = '@FirstName' /></TD>  
         <TD><B><xsl:value-of select = '@LastName' /></B></TD>  
       </TR>  
    </xsl:template>  
    <xsl:template match = '/'>  
      <HTML>  
        <HEAD>  
           <STYLE>th { background-color: #CCCCCC }</STYLE>  
        </HEAD>  
        <BODY>  
         <TABLE border='1' style='width:300;'>  
           <TR><TH colspan='2'>Contacts</TH></TR>  
           <TR>  
              <TH >First name</TH>  
              <TH>Last name</TH>  
           </TR>  
           <xsl:apply-templates select = 'ROOT' />  
         </TABLE>  
        </BODY>  
      </HTML>  
    </xsl:template>  
</xsl:stylesheet>  
```  
  
  
