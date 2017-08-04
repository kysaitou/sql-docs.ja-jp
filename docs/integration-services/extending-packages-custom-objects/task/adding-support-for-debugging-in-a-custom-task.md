---
title: "カスタム タスクでのデバッグのサポートの追加 |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BreakpointManager class
- breakpoints [Integration Services]
- custom tasks [Integration Services], debugging
- IDTSSuspend interface
- IDTSBreakpointSite interface
- SSIS custom tasks, debugging
- debugging [Integration Services], custom tasks
ms.assetid: 7f06e49b-0b60-4e81-97da-d32dc248264a
caps.latest.revision: 45
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: f6e3d95b834bf64cb4dd4201658e0905d3e3ed46
ms.contentlocale: ja-jp
ms.lasthandoff: 08/03/2017

---
# <a name="adding-support-for-debugging-in-a-custom-task"></a>カスタム タスクにおけるデバッグのサポートの追加
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] ランタイム エンジンでは、ブレークポイントを使用することにより、パッケージ、タスク、およびその他の種類のコンテナーを実行中に中断できます。 ブレークポイントを使用すると、アプリケーションまたはタスクの正しい動作を妨げるエラーを確認し、修正できます。 ブレークポイントのアーキテクチャにより、クライアントは、タスクの処理を中断している間にパッケージ内のオブジェクトのランタイム値を定義された実行地点で評価できます。  
  
 カスタム タスクの開発者はこのアーキテクチャを利用して、<xref:Microsoft.SqlServer.Dts.Runtime.IDTSBreakpointSite> インターフェイス、およびその親インターフェイスである <xref:Microsoft.SqlServer.Dts.Runtime.IDTSSuspend> を使用することにより、カスタム ブレークポイント ターゲットを作成できます。 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSBreakpointSite> インターフェイスは、ランタイム エンジンと、カスタム ブレークポイント サイトまたはターゲットを作成し管理するためのタスクとの間の対話を定義します。 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSSuspend> インターフェイスは、ランタイム エンジンによって呼び出され、タスクの実行の中断および再開を通知するメソッドおよびプロパティを提供します。  
  
 ブレークポイント サイトまたはターゲットは、処理を中断できるタスクの実行ポイントです。 使用できるブレークポイント サイトからユーザーを選択、**ブレークポイントの設定** ダイアログ ボックス。 たとえば、Foreach ループ コンテナーでは、既定のブレークポイント オプションだけでなく [ループの各繰り返しの開始点で停止します] オプションを使用できます。  
  
 タスクが実行中にブレークポイント ターゲットに達すると、タスクはブレークポイント ターゲットを評価して、そのブレークポイントが有効かどうかを判別します。 有効な場合は、そのブレークポイントで実行を停止することを示します。 ブレークポイントが有効な場合、タスクは、ランタイム エンジンに対して <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents.OnBreakpointHit%2A> イベントを発生させます。 ランタイム エンジンが呼び出すことによって、イベントに応答、 **Suspend**パッケージで現在実行されている各タスクのメソッドです。 ランタイムが呼び出すと、タスクの実行が再開されます、 **ResumeExecution**中断されたタスクのメソッドです。  
  
 ブレークポイントを使用していないタスクでも、<xref:Microsoft.SqlServer.Dts.Runtime.IDTSBreakpointSite> および <xref:Microsoft.SqlServer.Dts.Runtime.IDTSSuspend> インターフェイスを実装する必要があります。 これにより、パッケージ内の他のオブジェクトが <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents.OnBreakpointHit%2A> イベントを発生させた場合でも、タスクを正しく中断することができます。  
  
## <a name="idtsbreakpointsite-interface-and-breakpointmanager"></a>IDTSBreakpointSite インターフェイスおよび BreakpointManager  
 タスクは、<xref:Microsoft.SqlServer.Dts.Runtime.BreakpointManager.CreateBreakpointTarget%2A> の <xref:Microsoft.SqlServer.Dts.Runtime.BreakpointManager> メソッドを呼び出し、整数 ID と説明のための文字列を提供することによって、ブレークポイント ターゲットを作成します。 タスクが、ブレークポイント ターゲットを含むコード内の地点に達すると、タスクは <xref:Microsoft.SqlServer.Dts.Runtime.BreakpointManager.IsBreakpointTargetEnabled%2A> メソッドを使用してブレークポイント ターゲットを評価し、そのブレークポイントが有効かどうかを判別します。 場合**true**、タスクでは、ランタイム エンジンを通知発生させることによって、<xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents.OnBreakpointHit%2A>イベント。  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSBreakpointSite> インターフェイスは、タスクの作成中にランタイム エンジンによって呼び出される単一メソッド <xref:Microsoft.SqlServer.Dts.Runtime.IDTSBreakpointSite.AcceptBreakpointManager%2A> を定義します。 メソッドは、パラメーターとして <xref:Microsoft.SqlServer.Dts.Runtime.BreakpointManager> オブジェクトを提供し、このオブジェクトは各タスクでブレークポイントの作成や管理を行うために使用されます。 タスクを格納する必要があります、<xref:Microsoft.SqlServer.Dts.Runtime.BreakpointManager>中に使用するローカル、**検証**と**Execute**メソッドです。  
  
 次のサンプル コードでは、<xref:Microsoft.SqlServer.Dts.Runtime.BreakpointManager> を使用してブレークポイント ターゲットを作成する方法を示します。 このサンプルでは <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents.OnBreakpointHit%2A> メソッドを呼び出してイベントを起動します。  
  
```csharp  
public void AcceptBreakpointManager( BreakpointManager breakPointManager )  
{  
   //   Store the breakpoint manager locally.  
   this.bpm  = breakPointManager;  
}  
public override DTSExecResult Execute( Connections connections,  
  Variables variables, IDTSComponentEvents events,  
  IDTSLogging log, DtsTransaction txn)  
{  
   //   Create a breakpoint.  
   this.bpm.CreateBreakPointTarget( 1 , "A sample breakpoint target." );  
...  
   if( this.bpm.IsBreakpointTargetEnabled( 1 ) == true )  
      events.OnBreakpointHit( this.bpm.GetBreakpointTarget( 1 ) );  
}  
```  
  
```vb  
Public Sub AcceptBreakpointManager(ByVal breakPointManager As BreakpointManager)  
  
   ' Store the breakpoint manager locally.  
   Me.bpm  = breakPointManager  
  
End Sub  
  
Public Overrides Function Execute(ByVal connections As Connections, _  
  ByVal variables As Variables, ByVal events As IDTSComponentEvents, _  
  ByVal log As IDTSLogging, ByVal txn As DtsTransaction) As DTSExecResult  
  
   ' Create a breakpoint.  
   Me.bpm.CreateBreakPointTarget(1 , "A sample breakpoint target.")  
  
   If Me.bpm.IsBreakpointTargetEnabled(1) = True Then  
      events.OnBreakpointHit(Me.bpm.GetBreakpointTarget(1))  
   End If  
  
End Function  
```  
  
## <a name="idtssuspend-interface"></a>IDTSSuspend インターフェイス  
 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSSuspend> インターフェイスは、タスクの実行が一時停止または再開されるときに、ランタイム エンジンによって呼び出されるメソッドを定義します。 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSSuspend>インターフェイスによって実装、<xref:Microsoft.SqlServer.Dts.Runtime.IDTSBreakpointSite>インターフェイス、およびその**Suspend**と**ResumeExecution**メソッドは通常、カスタム タスクでオーバーライドします。 ランタイム エンジンが受信すると、 **OnBreakpointHit**タスクからイベントを呼び出す、 **Suspend**を一時停止するタスクを通知する、実行中の各タスクのメソッドです。 ランタイム エンジンが呼び出すクライアントが実行を再開するとき、 **ResumeExecution**中断されているタスクのメソッドです。  
  
 タスクの実行が中断および再開されると、タスクの実行スレッドも一時停止および再開されます。 マネージ コードでこれを行うを使用して、 **ManualResetEvent**クラス**System.Threading** .NET Framework の名前空間。  
  
 次のコード サンプルは、タスクの実行を中断および再開します。 注意して、 **Execute**メソッドが前のコード サンプルを変更し、ブレークポイントが発生する実行スレッドが一時停止します。  
  
```csharp  
private ManualResetEvent m_suspended = new ManualResetEvent( true );  
private ManualResetEvent m_canExecute = new ManualResetEvent( true );  
private int   m_suspendRequired = 0;  
private int   m_debugMode = 0;  
  
public override DTSExecResult Execute( Connections connections, Variables variables, IDTSComponentEvents events, IDTSLogging log, DtsTransaction txn)  
{  
   // While a task is not executing, it is suspended.    
   // Now that we are executing,  
   // change to not suspended.  
   ChangeEvent(m_suspended, false);  
  
   // Check for a suspend before doing any work,   
   // in case the suspend and execute calls  
   // were initiated at virtually the same time.  
   CheckAndSuspend();  
   CheckAndFireBreakpoint( componentEvents, 1);  
}  
private void CheckAndSuspend()  
{  
   // Loop until we can execute.    
   // The loop is required rather than a simple If  
   // because there is a time between the return from WaitOne and the  
   // reset that we might receive another Suspend call.    
   // Suspend() will see that we are suspended  
   // and return.  So we need to rewait.  
   while (!m_canExecute.WaitOne(0, false))  
   {  
      ChangeEvent(m_suspended, true);  
      m_canExecute.WaitOne();  
      ChangeEvent(m_suspended, false);  
   }  
}  
private void CheckAndFireBreakpoint(IDTSComponentEvents events, int breakpointID)  
{  
   // If the breakpoint is enabled, fire it.  
   if (m_debugMode != 0 &&    this.bpm.IsBreakpointTargetEnabled(breakpointID))  
   {  
      //   Enter a suspend mode before firing the breakpoint.    
      //   Firing the breakpoint will cause the runtime   
      //   to call Suspend on this task.    
      //   Because we are blocked on the breakpoint,   
      //   we are suspended.  
      ChangeEvent(m_suspended, true);  
      events.OnBreakpointHit(this.bpm.GetBreakpointTarget(breakpointID));  
      ChangeEvent(m_suspended, false);  
   }  
   // Check for a suspension for two reasons:   
   //   1. If we are at a point where we could fire a breakpoint,   
   //      we are at a valid suspend point.  Even if we didn't hit a  
   //      breakpoint, the runtime may have called suspend,   
   //      so check for it.       
   //   2. Between the return from OnBreakpointHit   
   //      and the reset of the event, it is possible to have  
   //      received a suspend call from which we returned because   
   //      we were already suspended.  We need to be sure it is okay  
   //      to continue executing now.  
   CheckAndSuspend();  
}  
static void ChangeEvent(ManualResetEvent e, bool shouldSet)  
{  
   bool succeeded;  
   if (shouldSet)  
      succeeded = e.Set();  
   else  
      succeeded = e.Reset();  
  
   if (!succeeded)  
      throw new Exception("Synchronization object failed.");  
  
}  
public bool SuspendRequired  
{  
   get   {return m_suspendRequired != 0;}  
   set  
   {  
      // This lock is also taken by Suspend().    
      // Because it is possible for the package to be  
      // suspended and resumed in quick succession,   
      // this property might be set before  
      // the actual Suspend() call.    
      // Without the lock, the Suspend() might reset the canExecute  
      // event after we set it to abort the suspension.  
      lock (this)  
      {  
         Interlocked.Exchange(ref m_suspendRequired, value ? 1 : 0);  
         if (!value)  
            ResumeExecution();  
      }  
   }  
}  
public void ResumeExecution()  
{  
   ChangeEvent( m_canExecute,true );  
}  
public void Suspend()  
{  
   // This lock is also taken by the set SuspendRequired method.    
   // It prevents this call from overriding an   
   // aborted suspension.  See comments in set SuspendRequired.  
   lock (this)  
   {  
      // If a Suspend is required, do it.  
      if (m_suspendRequired != 0)  
         ChangeEvent(m_canExecute, false);  
   }  
   // We can't return from Suspend until the task is "suspended".  
   // This can happen one of two ways:   
   // the m_suspended event occurs, indicating that the execute thread  
   // has suspended, or the canExecute flag is set,   
   // indicating that a suspend is no longer required.  
   WaitHandle [] suspendOperationComplete = {m_suspended, m_canExecute};  
   WaitHandle.WaitAny(suspendOperationComplete);  
}  
```  
  
```vb  
Private m_suspended As ManualResetEvent = New ManualResetEvent(True)  
Private m_canExecute As ManualResetEvent = New ManualResetEvent(True)  
Private m_suspendRequired As Integer = 0  
Private m_debugMode As Integer = 0  
  
Public Overrides Function Execute(ByVal connections As Connections, _  
ByVal variables As Variables, ByVal events As IDTSComponentEvents, _  
ByVal log As IDTSLogging, ByVal txn As DtsTransaction) As DTSExecResult  
  
   ' While a task is not executing it is suspended.    
   ' Now that we are executing,  
   ' change to not suspended.  
   ChangeEvent(m_suspended, False)  
  
   ' Check for a suspend before doing any work,   
   ' in case the suspend and execute calls  
   ' were initiated at virtually the same time.  
   CheckAndSuspend()  
   CheckAndFireBreakpoint(componentEvents, 1)  
  
End Function  
  
Private Sub CheckAndSuspend()  
  
   ' Loop until we can execute.    
   ' The loop is required rather than a simple if  
   ' because there is a time between the return from WaitOne and the  
   ' reset that we might receive another Suspend call.    
   ' Suspend() will see that we are suspended  
   ' and return.  So we need to rewait.  
   Do While Not m_canExecute.WaitOne(0, False)  
              ChangeEvent(m_suspended, True)  
              m_canExecute.WaitOne()  
              ChangeEvent(m_suspended, False)  
   Loop  
  
End Sub  
  
Private Sub CheckAndFireBreakpoint(ByVal events As IDTSComponentEvents, _  
ByVal breakpointID As Integer)  
  
   ' If the breakpoint is enabled, fire it.  
   If m_debugMode <> 0 AndAlso Me.bpm.IsBreakpointTargetEnabled(breakpointID) Then  
              '   Enter a suspend mode before firing the breakpoint.    
              '   Firing the breakpoint will cause the runtime   
              '   to call Suspend on this task.    
              '   Because we are blocked on the breakpoint,   
              '   we are suspended.  
              ChangeEvent(m_suspended, True)  
              events.OnBreakpointHit(Me.bpm.GetBreakpointTarget(breakpointID))  
              ChangeEvent(m_suspended, False)  
   End If  
  
   ' Check for a suspension for two reasons:   
   '   1. If we are at a point where we could fire a breakpoint,   
   '         we are at a valid suspend point.  Even if we didn't hit a  
   '         breakpoint, the runtime may have called suspend,   
   '         so check for it.     
   '   2. Between the return from OnBreakpointHit   
   '         and the reset of the event, it is possible to have  
   '         received a suspend call from which we returned because   
   '         we were already suspended.  We need to be sure it is okay  
   '         to continue executing now.  
   CheckAndSuspend()  
  
End Sub  
  
Shared Sub ChangeEvent(ByVal e As ManualResetEvent, ByVal shouldSet As Boolean)  
  
   Dim succeeded As Boolean  
   If shouldSet Then  
              succeeded = e.Set()  
   Else  
              succeeded = e.Reset()  
   End If  
  
   If (Not succeeded) Then  
              Throw New Exception("Synchronization object failed.")  
   End If  
  
End Sub  
  
Public Property SuspendRequired() As Boolean  
   Get  
               Return m_suspendRequired <> 0  
  End Get  
  Set  
    ' This lock is also taken by Suspend().    
     '   Because it is possible for the package to be  
     '   suspended and resumed in quick succession,   
     '   this property might be set before  
     '   the actual Suspend() call.    
     '   Without the lock, the Suspend() might reset the canExecute  
     '   event after we set it to abort the suspension.  
              SyncLock Me  
                         Interlocked.Exchange(m_suspendRequired,IIf(Value, 1, 0))  
                         If (Not Value) Then  
                                    ResumeExecution()  
                         End If  
              End SyncLock  
   End Set  
End Property  
  
Public Sub ResumeExecution()  
   ChangeEvent(m_canExecute,True)  
End Sub  
  
Public Sub Suspend()  
  
   ' This lock is also taken by the set SuspendRequired method.    
   ' It prevents this call from overriding an   
   ' aborted suspension.  See comments in set SuspendRequired.  
   SyncLock Me  
   ' If a Suspend is required, do it.  
              If m_suspendRequired <> 0 Then  
                         ChangeEvent(m_canExecute, False)  
              End If  
   End SyncLock  
   ' We can't return from Suspend until the task is "suspended".  
   ' This can happen one of two ways:   
   ' the m_suspended event occurs, indicating that the execute thread  
   ' has suspended, or the canExecute flag is set,   
   ' indicating that a suspend is no longer required.  
   Dim suspendOperationComplete As WaitHandle() = {m_suspended, m_canExecute}  
   WaitHandle.WaitAny(suspendOperationComplete)  
  
End Sub  
```  
  
## <a name="see-also"></a>参照  
 [制御フローのデバッグ](../../../integration-services/troubleshooting/debugging-control-flow.md)  
  
  