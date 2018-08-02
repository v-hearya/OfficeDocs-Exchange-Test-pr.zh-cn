﻿---
title: '管理链接的邮箱: Exchange 2013 Help'
TOCTitle: 管理链接的邮箱
ms:assetid: 76e12d4a-1c3a-42e2-b64c-c09d36e81bd3
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ673532(v=EXCHG.150)
ms:contentKeyID: 50490862
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理链接的邮箱

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-11-27_

链接邮箱是由独立的受信任林中的用户访问的邮箱。 如果组织在资源林中部署 Exchange，则可能需要使用链接邮箱。 资源林方案使组织可以将 Exchange 集中在单个林中，同时允许使用位于一个或多个受信任林（称为*帐户林*）中的用户帐户访问 Exchange 组织。 在部署了 Exchange 的林中不存在要访问链接邮箱的用户帐户。 因此，创建与 Exchange 相同的林中存在的已禁用用户帐户并将其与对应链接邮箱关联。

下图说明了用于访问链接邮箱（位于帐户林中）的已链接用户帐户和与链接邮箱关联的 Exchange 资源林中已禁用用户帐户之间的关系。

**链接的邮箱**

![具有资源林的复杂 Exchange 组织](images/Aa998031.706725cf-e520-4b89-a275-acd8fb58943a(EXCHG.150).gif "具有资源林的复杂 Exchange 组织")

> [!NOTE]  
> 必须设置 Exchange 林与至少一个帐户林之间的信任，然后您才能创建链接邮箱。 您至少必须设置单向的传出信任，以便 Exchange 林信任帐户林。 有关详细信息，请参阅<a href="https://technet.microsoft.com/zh-cn/library/jj156983(v=exchg.150)">了解有关设置林信任以支持链接的邮箱的详细信息</a>。


## 在开始之前，您需要知道什么？

  - 估计完成时间： 2 至 5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“收件人设置权限”部分。

  - 帐户林中必须存在用户帐户（称为*链接主帐户*），然后您才能创建链接邮箱。 这是因为链接邮箱与帐户林中的用户相关联。

  - 如果您已配置 Exchange 林信任帐户林的单向传出信任，则您需要帐户林中的管理员凭据来创建链接邮箱。
    
    要在帐户林中创建链接的邮箱，而不提示输入管理员凭据，必须创建双向信任，或如果帐户林也信任 Exchange 林，则另外创建一个单向传出信任。 此步骤还需要帐户林中的管理员凭据。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 创建链接邮箱

## 使用 EAC 创建链接邮箱

1.  在 EAC 中，导航到“收件人”\>“邮箱”。

2.  单击“新建”\>“链接邮箱”。

3.  在“新建链接邮箱”页上的“受信任的林或域”框中，选择包含要为其创建链接邮箱的用户帐户的帐户林名称。 单击“下一步”。

4.  如果您的组织已配置 Exchange 林信任帐户林的单向传出信任，则系统会提示您提供帐户林中的管理员凭据，以便您可以获得对信任林中域控制器的访问权限。 键入帐户林中的管理员帐户的用户名和密码，然后单击“下一步”。
    
    > [!NOTE]  
    > 如果您已创建双向信任或已创建帐户林信任 Exchange 林的另一个单向传出信任，则系统将不会提示您提供管理员凭据。


5.  完成“选择链接主帐户”页上的以下框。
    
      - **链接域控制器**   在帐户林中选择域控制器。 Exchange 将连接到此域控制器以检索帐户林中的用户帐户列表，以便您可以选择链接主帐户。
    
      - **链接主帐户**   单击“浏览”，在帐户林中选择一个用户帐户，然后单击“确定”。 新的链接邮箱将与此帐户相关联。

6.  单击“下一步”并完成“输入常规信息”页上的以下框。
    
      - “\* 姓名”   使用此框可以键入用户的姓名。 这是在 EAC 和组织的通讯簿中用作显示名称以及在 Active Directory 中列出的名称。 此名称是必需的。
    
      - “组织单位”   可选择非默认的组织单位 (OU)（属于收件人作用域）。 如果将收件人作用域设置为林，则默认值设置为 Active Directory 域中的“用户”容器，该域包含运行 EAC 的计算机。 如果将收件人作用域设置为特定域，则将默认选择该域中的“用户”容器。 如果将收件人范围设置为某个特定 OU，则默认情况下，将选择该 OU。
        
        若要选择一个不同的 OU，请单击“浏览”。 该对话框显示 Exchange 林中的指定作用域内的所有 OU。 选择所需的 OU，然后单击“确定”。
    
      - **\* 用户登录名**   使用此框可以键入创建链接邮箱所需的用户登录名。 在此处键入用户名。 如果未指定别名，则此名称将用在链接邮箱的电子邮件地址的左侧部分。
        
        > [!NOTE]  
        > 因为在您创建链接邮箱时会禁用在 Exchange 林中创建的用户帐户，所以用户不使用用户登录名来登录到链接邮箱。 他们使用其帐户林中的凭据登录。


7.  单击“更多选项”配置下面的框。 否则，请跳到步骤 8 以保存新的链接邮箱。
    
      - **别名**   键入指定链接邮箱的电子邮件别名的别名。 用户的别名是电子邮件地址中 (@) 符号左侧的部分。 它在林中必须是唯一的。
        
        > [!NOTE]  
        > 如果您将此框保留为空，则会对电子邮件别名使用“用户登录名称”的用户名部分中的值。
    
      - **名字**、**姓名缩写**、**姓氏**
    
      - **邮箱数据库**   使用此选项可指定邮箱数据库，而不是让 Exchange 为您选择数据库。 单击“浏览”打开“选择邮箱数据库”对话框。 此对话框列出 Exchange 组织中的所有邮箱数据库。 默认情况下，按名称对邮箱数据库进行排序。 还可以单击相应列标题，按服务器名称或版本对数据库进行排序。 选择要使用的邮箱数据库，然后单击“确定”。
    
      - **通讯簿策略**   使用此选项可为链接邮箱指定通讯簿策略 (ABP)。 ABP 包含一个全局地址列表 (GAL)、一个脱机通讯簿 (OAB)、一个会议室列表以及一组地址列表。 在分配给用户时，ABP 使这些用户可以访问 Outlook 和 Outlook Web App 中的自定义 GAL。 若要了解更多信息，请参阅[通讯簿策略](address-book-policies-exchange-2013-help.md)。
        
        在下拉列表中，选择要与此邮箱关联的策略。

8.  完成后，请单击“保存”创建新的链接邮箱。

## 使用命令行管理程序创建链接邮箱

此示例为 CONTOSO Exchange 资源林中的 Ayla Kol 创建链接邮箱。 FABRIKAM 域位于帐户林中。 管理员帐户 FABRIKAM \\administrator 用于访问链接域控制器。

    New-Mailbox -Name "Ayla Kol" -LinkedDomainController "DC1_FABRIKAM" -LinkedMasterAccount " FABRIKAM\aylak" -OrganizationalUnit Users -UserPrincipalName aylak@contoso.com -LinkedCredential:(Get-Credential FABRIKAM\administrator)

有关语法和参数的信息，请参阅 [New-Mailbox](https://technet.microsoft.com/zh-cn/library/aa997663\(v=exchg.150\))。

## 您如何知道这有效？

要检查是否成功创建了链接邮箱，请执行以下操作之一：

  - 在 EAC 中，导航到“收件人”\>“邮箱”。 邮箱列表中将显示新的链接邮箱。 在“邮箱类型”下，该类型是“链接”。

  - 在命令行管理程序中，运行以下命令可显示有关新链接邮箱的信息。
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,IsLinked,LinkedMasterAccount

## 更改链接邮箱属性

创建链接邮箱后，您可以使用 Exchange 管理中心 (EAC) 或 Exchange 命令行管理程序对其进行更改并设置其他属性。

您也可同时为多个链接邮箱更改属性。 有关详细信息，请参阅[管理用户邮箱](manage-user-mailboxes-exchange-2013-help.md)主题中的“批量编辑用户邮箱”部分。

> [!IMPORTANT]  
> 完成此任务的估计时间将会根据您要查看或更改的属性数量而异。


## 使用 EAC 更改链接邮箱属性

1.  在 EAC 中，导航到“收件人”\>“邮箱”。

2.  在邮箱列表中，单击要更改其属性的链接邮箱，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在“邮箱属性”页面上，单击以下部分之一以查看或更改属性。
    
      - 常规
    
      - 邮箱用量
    
      - 电子邮件地址
    
      - 邮箱功能
    
      - 成员属于
    
      - 邮件提示
    
      - 邮箱委派

## 常规

使用“常规”部分可以查看或更改有关用户的基本信息。

  - **\* 链接邮箱名称**   这是在 Active Directory 中列出的名称。 如果您要更改此姓名，则它不能超过 64 个字符。

  - **\* 显示姓名**   此姓名将会出现在组织通讯簿中、电子邮件中的“收件人:” 和“发件人：” 行上以及 EAC 的“邮箱”列表中。 此姓名不能在显示姓名之前或之后包含空格。

  - **\* 用户登录名**   对于用户邮箱，这是用户用于登录其邮箱和登录域的名称。 对于链接邮箱，禁用创建链接邮箱时在 Exchange 林中创建的相应用户帐户。 用户使用其帐户林中的凭据登录链接邮箱。
    
    如果更改此名称，则它必须在组织中是唯一的。

  - **链接主帐户**   这是一个只读字段，显示帐户林中与链接邮箱相关联的用户（采用“域\\用户名”格式）。 要更改与链接邮箱相关联的链接主帐户，您必须使用命令行管理程序中的 **Set-Mailbox** cmdlet。 如果更改链接主帐户，则用户必须使用新链接主帐户的凭据才能登录链接邮箱。 有关更改链接主帐户的常用语法，请参阅使用命令行管理程序更改链接邮箱属性。

  - **不显示在地址列表中**   选中此复选框可以防止链接邮箱显示在 Exchange 组织中定义的通讯簿和其他地址列表中。 选中此复选框后，用户仍可使用电子邮件地址向此用户发送邮件。

单击“更多选项”查看或更改以下这些额外的属性：

  - “组织单位”   此只读框显示包含用户帐户的组织单位 (OU)。 必须使用 Active Directory 用户和计算机才能将此用户帐户移动到不同的 OU。

  - “邮箱数据库”   此只读框显示托管此邮箱的邮箱数据库的名称。 要将邮箱移到不同的数据库中，请在邮箱列表中选择该邮箱，然后在“详细信息”窗格中单击“将邮箱移到不同的数据库”。

  - **\* 别名**：它指定链接邮箱的电子邮件别名。 别名是电子邮件地址中 (@) 符号左侧的部分。 它在林中必须是唯一的。

  - **名字**、**姓名缩写**、**姓氏**

  - **自定义属性**   此部分显示为链接邮箱定义的自定义属性。 要指定自定义属性值，请单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。 最多可为收件人指定 15 个自定义属性。

## 邮箱用量

使用“邮箱用量”部分可查看或更改邮箱存储配额和链接邮箱的已删除项目保留设置。 创建链接邮箱时，将默认配置这些设置。 它们使用为邮箱数据库配置且适用于该数据库中所有邮箱的值。 您可以为每个邮箱自定义这些设置，而不是使用邮箱数据库默认设置。

  - **最近登录**   这是一个只读字段，显示用户上次登录邮箱的时间。

  - “邮箱使用情况”   此区域显示邮箱的总体大小和已使用总体邮箱配额的百分比。

> [!NOTE]  
> 为了获取前两个框中显示的信息，EAC 将查询托管邮箱的邮箱数据库。 如果 EAC 无法与包含邮箱数据库的 Exchange 存储通信，这些框将为空。 如果用户还没有首次登录邮箱，则会显示警告消息。


单击“更多选项”以查看或更改邮箱存储配额和邮箱的已删除邮件保留设置。

  - **存储配额设置**   要自定义邮箱的这些设置而不使用邮箱数据库默认设置，则单击“自定义此邮箱的设置”，键入新值，然后单击“保存”。
    
    任何存储配额设置的值范围介于 0 到 2047 千兆字节 (GB) 之间。
    
      - “在达到该限度时发出警告(GB)”   此框显示在向用户发出警告之前的最大存储限制。 如果邮箱大小达到或超过指定值，Exchange 将向邮箱用户发送警告消息。
    
      - “在达到该限度时禁止发送(GB)”   此框显示邮箱的“禁止发送”限制。 如果邮箱大小达到或超过指定的限制，Exchange 将阻止邮箱用户发送新邮件，并显示一条描述性错误消息。
    
      - “在达到该限度时禁止发送和接收(GB)”   此框显示此邮箱的“禁止发送和接收”限制。 如果邮箱大小达到或超过指定的限制，Exchange 将阻止邮箱用户发送新邮件，并且不会将任何新邮件发送到邮箱中。 发送到邮箱的任何邮件将返回给收件人，并附带一条描述性错误消息。

  - **已删除项目保留设置**   要自定义邮箱的这些设置而不使用邮箱数据库默认设置，则单击“自定义此邮箱的设置”，键入新值，然后单击“保存”。
    
      - “保留已删除项目的期限(天)”   此框显示在用户永久删除并且无法恢复项目之前，已删除项目的保留时间长度。 在创建邮箱后，该时间长度基于为邮箱数据库配置的已删除项目保留设置。 默认情况下，邮箱数据库配置为将已删除项目保留 14 天。 此属性的值范围介于 0 到 24855 天之间。
    
      - **完成对数据库的备份之后才永久删除项目**   选中此复选框可避免在备份此邮箱所在的邮箱数据库之前永久删除邮箱和电子邮件。

## 电子邮件地址

使用“电子邮件地址”部分可以查看或更改与链接邮箱关联的电子邮件地址。 这包括用户的主 SMTP 地址和任何关联的代理地址。 主 SMTP 地址（也称为“默认答复地址”）在地址列表中以粗体显示，大写的 **SMTP** 值显示在“类型”列中。

  - “添加”   单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")可为该邮箱添加新的电子邮件地址。 选择以下地址类型之一：
    
      - “SMTP”   这是默认的地址类型。 单击此单选按钮，然后在“\* 电子邮件地址”框中键入新的 SMTP 地址。
    
      - **EUM** EUM（Exchange 统一消息）地址由 Microsoft Exchange 统一消息服务用于在 Exchange 组织中查找已启用 UM 的用户。 EUM 地址包含已启用 UM 的用户的分机号和 UM 拨号计划。 单击此单选按钮，并在“地址/扩展名”框中键入分机号。 然后单击“浏览”，选择用户的拨号计划。
    
      - “自定义地址类型”   单击此按钮，然后在“\* 电子邮件地址”框中键入一个支持的非 SMTP 电子邮件地址。
        
        > [!NOTE]  
        > 除 X.400 地址以外，Exchange 不验证自定义地址的格式是否正确。 您必须确保所指定的自定义地址符合该地址类型的格式要求。


  - **基于应用到此收件人的电子邮件地址策略自动更新电子邮件地址**   如果您希望在更改组织中的电子邮件地址策略时自动更新收件人的电子邮件地址，则选中此复选框。 此框在默认情况下处于选中状态。

## 邮箱功能

使用“邮箱功能”部分可查看或更改下列邮箱功能和设置：

  - “共享策略”   此框显示应用于邮箱的共享策略。 共享策略可以控制组织中的用户与 Exchange 组织外的用户共享日历和联系人信息的方式。 在创建邮箱时就为这些邮箱分配了“默认共享策略”。 要更改已分配给此用户的共享策略，请从下拉列表中选择一个不同的共享策略。

  - “角色分配策略”   此框显示已分配给邮箱的角色分配策略。 角色分配策略指定分配给用户的基于角色的访问控制 (RBAC) 角色并控制用户可以修改的邮箱和通讯组配置设置。 要更改已分配给此用户的角色分配策略，请从下拉列表中选择一个不同的角色分配策略。

  - “保留策略”   该框显示为邮箱分配的保留策略。 保留策略是一组应用至用户邮箱的保留标记。 这些标记使您可以控制用户邮箱中各项的保留期限，并定义如何操作已达到一定期限的项目。 在创建保留策略时，不会将其分配给邮箱。 要将保留策略分配至用户，可从下拉列表中选择一个策略。

  - **通讯簿策略**   此框显示应用于邮箱的通讯簿策略。 通过通讯簿策略可以将用户分为特定组以提供通讯簿的自定义视图。 要应用或更改应用于邮箱的通讯簿策略，请从下拉列表中选择一个通讯簿策略。

  - **统一消息** 默认情况下禁用此功能。 启用统一消息 (UM) 时，用户将能够使用组织的 UM 功能，并且向用户应用一组默认的 UM 属性。 单击“启用”为邮箱启用 UM。 有关如何启用 UM 的信息，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。
    
    > [!NOTE]  
    > 必须有 UM 拨号计划以及 UM 邮箱策略方可启用 UM。


  - **移动设备**   使用此部分可查看和更改 Exchange ActiveSync（默认情况下会启用）的设置。 Exchange ActiveSync 支持从移动设备访问 Exchange 邮箱。 单击“禁用 Exchange ActiveSync”可为邮箱禁用此功能。

  - **Outlook Web App** 默认情况下，已启用此功能。 使用 Outlook Web App 可以从 Web 浏览器访问 Exchange 邮箱。 单击“禁用”来禁用邮箱的 Outlook Web App。 单击“编辑详细信息”来添加或更改邮箱的 Outlook Web App 邮箱策略。

  - **IMAP**   默认情况下启用此功能。 单击“禁用”对邮箱禁用 IMAP。

  - **POP3**   默认情况下启用此功能。 单击“禁用”对邮箱禁用 POP3。

  - **MAPI** 默认情况下启用此功能。 MAPI 支持从 MAPI 客户端（如 Outlook）访问 Exchange 邮箱。 单击“禁用”来禁用邮箱的 MAPI。

  - **诉讼保留**   默认情况下禁用此功能。 诉讼保留可以保留已删除的邮箱项目并记录对邮箱项目所作的更改。 在发现搜索中可返回已删除的项目和已更改项目的所有实例。 单击“启用”将邮箱置于诉讼保留。 如果邮箱处于诉讼保留状态，可单击“禁用”删除诉讼保留。 如果邮箱处于诉讼保留状态，可单击“编辑详细信息”来查看并更改以下诉讼保留设置：
    
      - **保留日期**   此只读框指示将邮箱置于诉讼保留中的日期和时间。
    
      - “保留者”   该只读框指明将邮箱置于诉讼保留状态的用户是谁。
    
      - “注意”   使用此框可以通知用户有关诉讼保留的信息、解释将邮箱置于诉讼保留的原因，或者向用户提供其他指南，如通知用户诉讼保留不会影响他们对邮箱的日常使用。
    
      - “URL”   使用此框可以提供指向某网站的 URL，该网站提供有关邮箱上的诉讼保留的信息或指南。
        
        > [!NOTE]  
        > 只有在使用 Outlook 2010 或更高版本时，这些框的文本才会显示在用户的邮箱中。 但不会显示在 Outlook Web App 或其他电子邮件客户端中。 要在 Outlook 中查看“说明”和“URL”框中的文本，请单击“文件”选项卡，在“信息”页上的“帐户设置”下，您将会看到诉讼保留注释。


  - **存档**   如果用户没有存档邮箱，则禁用此功能。 要启用存档邮箱，请单击“启用”。 如果用户具有存档邮箱，则会显示存档邮箱的大小和使用情况统计信息。 单击“编辑详细信息”来查看和更改以下存档邮箱设置：
    
      - “状态”   此只读框指示是否存在存档邮箱。
    
      - **数据库**   此只读框显示托管存档邮箱的邮箱数据库的名称。
    
      - “名称”   在此框中键入存档邮箱的名称。 该名称显示在 Outlook 或 Outlook Web App 中的文件夹列表下。
    
      - **配额使用情况**   此只读区域显示存档邮箱的总大小以及已经使用的存档邮箱总配额的百分比。
    
      - “配额值 (GB)”   该框显示为邮箱分配的保留策略。 要更改该大小，可在框中键入新的值或从下拉列表中选择一个值。
    
      - “达到该限度时发出警告 (GB)”   该框显示在向用户发出警告之前存档邮箱的最大存储限制。 如果存档邮箱大小达到或超过指定值，Exchange 将向用户发送警告消息。 要更改该限制，可在框中键入新的值或从下拉列表中选择一个值。

  - **传递选项**   使用“传递选项”可将发送给用户的电子邮件转发给另一个收件人以及设置用户可将邮件发送到的收件人最大数目。 单击“编辑详细信息”可查看和更改这些设置。
    
      - “转发地址”   选择“启用转发”复选框，然后单击“浏览”来显示“选择邮箱用户和邮箱“页。 使用此页选择收件人，发送到此邮箱的所有电子邮件将转发给该收件人。 邮件将同时传递到链接邮箱和转发地址。
    
      - **收件人限制**   此设置控制用户可将邮件发送到的收件人最大数目。 选中“最大收件人数”复选框限制电子邮件的“收件人:”、“抄送:”和“密件抄送:”行上允许的收件人数， 然后指定最大收件人数。
        
        > [!NOTE]  
        > 对于内部部署 Exchange 组织，收件人数目不受限。 对于 Exchange 在线组织，限制是 500 个收件人。


  - **邮件大小限制**   这些设置控制用户可以发送和接收的邮件大小。 单击“编辑详细信息”可查看和更改发送和接收的邮件的最大大小。
    
      - “已发送消息”   要指定该用户发送的消息的最大大小，可选择“最大消息大小 (KB)”复选框并在框中键入值。 邮件大小必须介于 0 到 2,097,151 KB 之间。 如果用户发送大于该指定大小的邮件，则会将该邮件返回至用户，并向其显示一条描述性的错误消息。
    
      - “已收到消息”   要指定该用户接收的消息的最大大小，可选择“最大消息大小 (KB)”复选框并在框中键入值。邮件大小必须介于 0 到 2,097,151 KB 之间。 如果用户收到大于指定大小的邮件，则该邮件将返回至发件人，并向其显示一条描述性的错误消息。

  - **邮件传递限制**   这些设置控制可以向此用户发送电子邮件的人员。 单击“编辑详细信息”可查看和更改这些限制。
    
      - **接受来自下列发件人的邮件**   使用该部分指定谁可将邮件发送至该用户。
        
          - **所有发件人**   选择此选项可指定用户能够接受来自所有发件人的邮件。 这包括 Exchange 组织中的发件人和外部发件人。 此选项默认情况下处于选中状态。 仅当清除了“要求所有发件人均通过身份验证”复选框时，此选项才包括外部用户。 如果选中此复选框，则会拒绝来自外部用户的邮件。
        
          - “仅限以下列表中的发件人”   选择此选项可指定该用户只能接受来自 Exchange 组织中指定的一组发件人的邮件。 单击“添加”显示“选取收件人”页面，该页面显示您 Exchange 组织中所有收件人的列表。 选择所需的收件人，将其添加至列表，然后单击“确定”。 也可以通过在搜索框中键入该收件人的姓名，然后单击“搜索”，搜索特定的收件人。
        
          - “要求所有发件人均通过身份验证”   选中此选项可防止匿名用户向此用户发送邮件。
    
      - “拒绝来自下列发件人的邮件”   使用该部分来阻止某些人将邮件发送至该用户。
        
          - “无发件人”   选择此选项可指定邮箱不会拒绝来自 Exchange 组织中任何发件人的邮件。 此选项默认情况下处于选中状态。
        
          - **以下列表中的发件人**   选择此选项可指定该邮箱将拒绝来自 Exchange 组织中指定的一组发件人的邮件。 单击“添加”显示“选择收件人”页，该页显示 Exchange 组织中所有收件人的列表。 选择要拒绝其邮件的收件人，将这些收件人添加到该列表中，然后单击“确定”。 也可以通过在搜索框中键入该收件人的姓名，然后单击“搜索”，搜索特定的收件人。

## 成员属于

使用“隶属于”部分可查看该用户所属通讯组或安全组的列表。 您不能在此页上更改成员信息。 请注意，用户可能符合您组织中的一个或多个动态通讯组的条件。 但是，动态通讯组不会显示在此页面上，因为每次使用它们时都会计算其成员资格。

## 邮件提示

使用“邮件提示”部分可添加邮件提示，以便在用户向此收件人发送邮件时告知用户潜在问题。 邮件提示是在将收件人添加到新电子邮件的“收件人”、“抄送”或“密件抄送”行中时，信息栏中显示的文本。

> [!NOTE]  
> 邮件提示可包含 HTML 标记，但不允许包含脚本。 自定义邮件提示的长度不能超过 175 个显示的字符。 此字符限制不计入 HTML 标记。


## 邮箱委派

使用“邮箱委派”部分将权限分配至其他用户（也称为*代理*）让他们登录用户邮箱或代表用户发送邮件。 可以分配以下权限：

  - **发送为**   该权限可让邮箱所有者之外的用户使用邮箱来发送邮件。 在将该权限分配给某个代理后，代理通过该邮箱发送的所有邮件都将显示为由邮箱所有者发送。 但是该权限不会允许代理登录用户邮箱。

  - **代表发送**   该权限也允许代理使用该邮箱发送邮件。 但是，在将此权限分配给代理后，代理发送的任何邮件中的“发件人：” 地址将指明邮件由代理代表邮箱所有者发送。

  - **完全访问权限**   该权限允许代理登录用户邮箱并查看邮箱内容。 但是，在将该权限分配给代理后，代理不能从邮箱发送邮件。 为了让代理从用户邮箱发送电子邮件，您仍然必须为代理分配“发送为”或“代表发送”权限。

若要向代理分配权限，请单击相应权限下面的“添加”显示“选择收件人”页面，该页面将显示 Exchange 组织内可分配该权限的所有收件人的列表。 选择要将代理权限分配给的收件人，将这些收件人添加到该列表中，然后单击“确定”。 也可以通过在搜索框中键入该收件人的姓名，然后单击“搜索”，搜索特定的收件人。

## 使用命令行管理程序更改链接邮箱属性

使用 **Get-Mailbox** 和 **Set-Mailbox** cmdlet 可查看和更改链接邮箱的属性。 使用命令行管理程序的一个好处是可以更改多个链接邮箱的属性。 有关什么参数对应邮箱属性的信息，请参阅下列主题：

  - [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))

下面是使用命令行管理程序更改链接邮箱属性的一些示例。

此示例使用 **Get-Mailbox** 命令查找组织中的所有链接邮箱。

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'LinkedMailbox')}

此示例使用 **Set-Mailbox** 命令将电子邮件的“收件人:”、“抄送:”和“密件抄送:”行上允许的收件人数 限制为 500。此限制应用于组织中的所有链接邮箱。

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'LinkedMailbox')} | Set-Mailbox -RecipientLimits 500

此示例更改 fabrikam.com 帐户林中与 Exchange 林中的链接邮箱相关联的链接主帐户。

    Set-Mailbox -Identity "Ayla Kol" -LinkedDomainController DC1.fabrikam.com -LinkedMasterAccount "fabrikam\robinw" -LinkedCredential:(Get-Credential fabrikam\administrator)

## 您如何知道这有效？

要验证是否已成功更改链接邮箱的属性，请执行以下操作：

  - 在 EAC 中，选择链接邮箱，然后单击“编辑”查看您更改的属性或功能。 根据您更改的属性，它可能显示在所选邮箱的“详细信息”窗格中。

  - 在命令行管理程序中，使用 **Get-Mailbox** cmdlet 验证更改。 使用命令行管理程序的一个好处是，您可查看多个链接邮箱的多个属性。 在上面的示例中，收件人限制有所更改，运行以下命令将验证新值。
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'LinkedMailbox')} | fl Name,RecipientLimits
    
    对于上面的示例，链接主帐户有所更改，运行以下命令来验证新值。
    
        Get-Mailbox "Ayla Kol" | fl LinkedMasterAccount
