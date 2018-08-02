﻿---
title: '就地保留和诉讼保留: Exchange 2013 Help'
TOCTitle: 就地保留和诉讼保留
ms:assetid: 71031c06-852d-44d8-b558-dff444eaef8c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff637980(v=EXCHG.150)
ms:contentKeyID: 50490817
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 就地保留和诉讼保留

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2017-11-15_

> [!NOTE]  
> 在 Exchange Online（Office 365 和 Exchange Online 独立计划）中新建就地保留的截止时间为 2017 年 7 月 1 日，我们已推迟了这一最后期限。不过，今年晚些时候或明年初，将无法在 Exchange Online 中新建就地保留。作为就地保留的备选方法，可以在 Office 365 安全与合规中心使用<a href="https://go.microsoft.com/fwlink/?linkid=780738">电子数据展示服务案例</a>或<a href="https://go.microsoft.com/fwlink/?linkid=827811">保留策略</a>。在我们取消新建就地保留后，仍可以修改现有就地保留，并且在 Exchange Server 2013 和 Exchange 混合部署中新建就地保留也仍将受支持。此外，也仍可以将邮箱置于诉讼保留。


当存在诉讼的合理预期时，需要组织保留与事实相关的以电子方式存储的信息 (ESI)，包括电子邮件。这种预期通常会在知道事实的细节之前发生，并且保留内容通常很广泛。组织可能需要保留与特定主题相关的所有电子邮件，或特定个人的所有电子邮件。可能会采用以下度量标准来保留电子邮件，具体取决于组织的电子发现（电子数据展示）实践：

  - 可能会要求最终用户通过不删除任何邮件来保留电子邮件。但是，用户仍然可能会有意或无意地删除电子邮件。

  - 自动删除机制（如邮件记录管理 (MRM)）可能被挂起。这可能导致用户邮箱因有大量电子邮件而变得杂乱，因而影响用户的工作效率。挂起自动删除也不能防止用户手动删除电子邮件。

  - 一些组织会将电子邮件复制或移动到存档中以确保它不被删除、更改或篡改。由于将电子邮件复制或移动到存档需要手动操作，或使用第三方产品在 Exchange 外部收集和存储电子邮件，这将增加成本。

如果未能保留电子邮件，则可能会使组织面临法律和财务风险，例如组织的记录保留和发现过程的审查、不利的法律判决、制裁或罚款等。

您可以使用就地保留或诉讼保留来完成以下目标：

  - 保留用户邮箱并永久保留邮箱项目。

  - 保留由用户或自动删除过程删除的邮箱项目，例如 MRM。

  - 使用基于查询的就地保留搜索并保留与指定条件匹配的项目。

  - 无限期保留项目或保留特定的持续时间。

  - 将用户置于多个保留中用于不同的事例或调查。

  - 通过不必挂起 MRM 使保留对用户是透明的。

  - 启用置于保留状态的项目的就地电子数据展示搜索。

**目录**

就地保留方案

就地保留和诉讼保留

将邮箱置于就地保留中

将公用文件夹置于保留状态

保留和“可恢复的项目”文件夹

保留和邮箱配额

保留项和电子邮件转发

保留存档的 Lync 内容

删除处于保留状态的邮箱

将处于保留状态的邮箱从 Exchange 2013 迁移到 Office 365

## 就地保留方案

在 Exchange Server 2010 中，合法保留的概念是无限期保留某个用户的所有邮箱数据，或一直保留到删除保留。在 Exchange 2013 中，就地保留引入一种新的保留模型，允许您指定以下参数：

  - **要保留的内容**   您可以通过使用诸如关键字、发件人和收件人、开始日期和结束日期等查询参数指定要保留的项目，也可以指定要置于保留状态的诸如电子邮件或日历项目等邮件类型。

  - **保留时间**   可以指定保留项目的持续时间。

通过使用此新模型，就地保留允许您创建精细的保留策略以便在以下方案中保留邮箱项目：

  - **无限期保留**   无限期保留方案类似于诉讼保留。它旨在保留邮箱项目以便您可以满足电子数据展示要求。在诉讼或调查期间，从不删除项目。由于预先不知道持续时间，因此不配置结束日期。要无限期保留所有邮件项目，请不要在创建就地保留时指定任何查询参数或持续时间。

  - **基于查询的保留**   如果您的组织根据特定的查询参数保留项目，则可以使用基于查询的就地保留。您可以指定诸如关键字、开始日期和结束日期、发件人和收件人地址以及邮件类型这样的查询参数。创建基于查询的就地保留之后，会保留与查询参数匹配的所有现有邮箱项目和将来项目（包括在以后日期接收的邮件）。
    
    > [!IMPORTANT]  
    > 通常由于无法索引附件，标记为不可搜索的项目也会被保留，因为无法确定它们是否与查询参数相匹配。有关不可搜索项目的详细信息，请参阅 <a href="unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md">Exchange 电子数据展示中不可搜索的项目</a>。


  - **基于时间的保留**   就地保留和诉讼保留都允许您指定保留项目的持续时间。持续时间从接收或创建邮箱项目的日期计算得到。
    
    如果您的组织要求将所有邮箱项目保留特定的时间段（例如 7 年），则可以创建基于时间的保留。在 Exchange 2013 中，您可以指定保留项目的期间。保留项目的期限基于其接收日期。例如，分析基于时间进行就地保留并且将保留期间设置为 365 天的邮箱。如果自收到某个项目开始计算，300 天后删除了此邮箱中的某个项目，则在永久删除该项目之前还需要再保留 65 天。您可以将基于时间的就地保留与保留策略一起使用，以确保这些项目保留指定的持续时间并在该期间过后永久删除。

你可以使用就地保留将用户置于多个保留中。将用户放在多个保留中时，来自任何基于查询的搜索查询将合并（使用 **OR** 运算符）。在这种情况下，放在一个邮箱中的所有基于查询的保留中关键字的最大数量为 500。如果超过 500 个关键字，则邮箱中的所有内容都将置于保留状态（而不只是符合搜索条件的内容）。将保留所有内容，直到关键字总数减少到 500 或更少。

返回顶部

## 就地保留和诉讼保留

诉讼保留是 Exchange 2010 中引入的用于保留电子数据展示数据的保留功能，在 Exchange 2013 中仍然可用。诉讼保留使用邮箱的 **LitigationHoldEnabled** 属性。就地保留基于查询参数和放置多个保留的功能提供精细的保留功能，而诉讼保留仅允许您将所有项目都置于保留状态。当邮箱处于诉讼保留状态时，您还可以指定保留项目的持续时间。持续时间从接收或创建邮箱项目的日期开始计算。如果未设置持续时间，项目会无限期保留或一直保留到删除保留。

同时将邮箱置于一个或多个就地保留和诉讼保留（无持续时间）中时，将无限期保留所有项目或一直保留到删除保留。如果删除诉讼保留而用户仍置于一个或多个就地保留中，则将匹配就地保留条件的项目在保留设置中保留指定的时间段。将 Exchange 2010 中诉讼保留的邮箱移到 Exchange 2013 邮箱服务器时，将继续应用诉讼保留设置，从而确保在移动期间和之后继续满足合规性要求。

> [!NOTE]  
> 当您将邮箱置于就地保留或诉讼保留中时，该保留将置于主邮箱和存档邮箱中。如果将 Exchange 混合部署中的内部部署主邮箱置于保留状态，则也会将基于云的存档邮箱（如果已启用）置于保留状态。


有关详细信息，请参阅：

  - [将邮箱放到诉讼保留中](place-a-mailbox-on-litigation-hold-exchange-2013-help.md)

  - [保留所有邮箱](place-all-mailboxes-on-hold-exchange-2013-help.md)

## 将邮箱置于就地保留中

已添加到基于[发现管理](discovery-management-exchange-2013-help.md)角色的访问控制 (RBAC) 角色组或分配了合法保留和邮箱搜索管理角色的已获授权的用户可以将邮箱用户置于就地保留中。可以将该任务委派给组织的法律部门中的记录管理员、遵从性管理者或律师，同时分配最低特权。有关分配 发现管理 角色组的详细信息，请参阅[在 Exchange 中分配电子数据展示权限](assign-ediscovery-permissions-in-exchange-exchange-2013-help.md)。

> [!IMPORTANT]  
> 在 Exchange 2010 中，合法保留角色向用户提供了足以将邮箱置于诉讼保留中的权限。在 Exchange 2013 中，您可以使用相同的权限来将邮箱置于无限保留或基于时间的就地保留中。但是，要创建基于查询的就地保留，必须向用户分配邮箱搜索角色。发现管理 角色组已分配有这两个角色。


在 Exchange 2013 中，就地保留功能与就地电子数据展示搜索集成。可以使用 Exchange 管理中心 (EAC) 的“就地电子数据展示和保留”向导或 Exchange 命令行管理程序中的 **New-MailboxSearch** 和相关 cmdlet 将邮箱置于就地保留中。要了解有关将邮箱置于就地保留中的更多信息，请参阅[创建或删除就地保留](create-or-remove-an-in-place-hold-exchange-2013-help.md)。

> [!NOTE]  
> 如果使用 Exchange Online Archiving 为本地邮箱设置基于云的存档，则必须从本地 Exchange 2013 组织管理就地保留。使用 DirSync 自动将保留设置传播到基于云的存档。如前面所述，当将本地邮箱置于保留状态时，相应的基于云的存档也被置于保留状态。


许多组织都需要用户在置于保留时得到通知。此外，当邮箱置于保留时，不需要挂起适用于邮箱用户的任何保留策略。由于邮件继续按预期方式进行删除，因此用户可能不会注意到他们置于保留中。如果您的组织需要保留中的用户得到通知，则可以将通知邮件添加到邮箱用户的 **Retention Comment** 属性中，并使用 **RetentionUrl** 属性链接到提供详细信息的网页。Outlook 2010 及更高版本在 Backstage 区域显示通知和 URL。必须使用命令行管理程序来添加和管理邮箱的这些属性。

返回顶部

## 将公用文件夹置于保留状态

在 Exchange Online 中，可以通过使用就地保留将公用文件夹置于保留状态。不支持将诉讼保留用于公用文件夹。创建就地保留时，唯一的选项是将组织中的所有公用文件夹置于保留状态。其结果是，所有公用文件夹邮箱都被置于就地保留状态。

此外，将公用文件夹置于就地保留状态时，还保留了与公用文件夹层次结构同步过程相关的电子邮件。这可能会导致保存数千个与层次结构同步相关的电子邮件项。这些邮件可能会填满公用文件夹邮箱上可恢复项目文件夹的存储配额。为了防止发生此状况，可以创建一个基于查询的就地保留，并将下列 `property:value` 对添加到搜索查询：

    NOT(subject:HierarchySync*)

其结果是，主题行中包含短语“HierarchySync”的任何邮件（与公用文件夹层次结构的同步相关）都不会置于保留状态。

## 保留和“可恢复的项目”文件夹

就地保留和诉讼保留使用“可恢复的项目”文件夹来保留项目。“可恢复的项目”文件夹替换在早期版本的 Exchange 中非正式称为“转储程序”的功能。“可恢复的项目”文件夹在 Outlook、Outlook Web App 和其他电子邮件客户端的默认视图中处于隐藏状态。有关“可恢复的项目”文件夹的详细信息，请参阅[“可恢复的项目”文件夹](recoverable-items-folder-exchange-2013-help.md)。

默认情况下，当用户从“已删除的项目”文件夹之外的文件夹中删除邮件时，该邮件将移动到“已删除的项目”文件夹中。这称为“移动”。当用户对某个项目执行“软删除”操作（通过按 Shift 和 Delete 键来实现）或从“已删除的项目”文件夹中删除某个项目，该邮件将移动到“可恢复的项目”文件夹，因而将从用户视图中消失。

“可恢复的项目”文件夹中的项目按照在用户邮箱数据库中配置的已删除项目保留期进行保留。默认情况下，邮箱数据库的已删除项目保留期设置为 14 天。还可以为“可恢复的项目”文件夹配置存储配额。这样可保护组织免受潜在的拒绝服务 (DoS) 攻击，这种攻击源于“可恢复的项目”文件夹的快速增长以及因此导致的邮箱数据库增长。如果邮箱未置于就地保留或诉讼保留中，当超出“可恢复的项目”文件夹警告配额，或项目在该文件夹中的保留持续时间超过已删除项目保留期间时，将按照先进先出的原则从“可恢复的项目”文件夹永久清除项目。

“可恢复的项目”文件夹包含以下子文件夹，这些子文件夹用于存储各种站点中的已删除项目并可加速就地保留和诉讼保留：

  - **Deletions** 从“已删除的项目”文件夹中删除或从其他文件夹中软删除的项目将移动到“删除”子文件夹，并且当用户在 Outlook 和 Outlook Web App 中使用“恢复已删除邮件”功能时对用户可见。默认情况下，项目将一直位于此文件夹中，直到为邮箱数据库或邮箱配置的已删除项目保留期过期为止。

  - **Purges**   当用户从“可恢复的项目”文件夹删除某个项目（使用 Outlook 和 Outlook Web App 中的“恢复已删除邮件”工具）时，该项目将移动到“清除”文件夹中。超出在邮箱数据库或邮箱中配置的已删除项目保留期的项目也会移动到“清除”文件夹中。如果用户使用“恢复已删除邮件”工具，则此文件夹中的项目对这些用户不可见。当邮箱助理处理邮箱时，“清除”文件夹中的项目将从邮箱数据库中清除。将邮箱用户置于诉讼保留状态时，邮箱助理不会清除此文件夹中的项目。

  - **DiscoveryHold**   如果将用户置于就地保留中，则会将已删除项目移到此文件夹中。当邮箱助理处理邮箱时，它将评估此文件夹中的邮件。将匹配就地保留查询的项目保留在该查询中指定的保留期。如果未指定保留期，则无限期保留项目或一直保留到从保留中删除用户。

  - **Versions**   当用户置于就地保留或诉讼保留中时，必须保护邮箱项目不被该用户或被进程篡改或修改。此操作通过使用*写入时复制*进程来实现。当用户或进程更改邮箱项目的特定属性时，在提交更改之前，会将原始项目的副本保存到“版本”文件夹中。对后续更改重复此过程。还会在就地电子数据展示搜索中对“版本”文件夹中捕获的项目编制索引并返回。删除保留后，托管文件夹助理将删除“版本”文件夹中的副本。

### 触发“写入时复制”的属性

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>项目类型</th>
<th>触发“写入时复制”的属性</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>邮件 (IPM.Note*)</p>
<p>公告 (IPM.Post*)</p></td>
<td><ul>
<li><p>主题</p></li>
<li><p>Body</p></li>
<li><p>附件</p></li>
<li><p>发件人/收件人</p></li>
<li><p>发送/接收日期</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>非邮件和公告的项目</p></td>
<td><p>对可见属性的任何更改（以下项除外）：</p>
<ul>
<li><p>项目位置（当在文件夹之间移动项目时）</p></li>
<li><p>项目状态更改（已读或未读）</p></li>
<li><p>对保留标记进行的应用于项目的更改</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>默认文件夹“草稿”中的项目</p></td>
<td><p>无（“草稿”文件夹中的项目免于“写入时复制”）</p></td>
</tr>
</tbody>
</table>


> [!IMPORTANT]  
> 从与会者获得会议响应并且更新会议的跟踪信息时，组织者邮箱中的日历项目将禁用“写入时复制”功能。对于设置了提醒的日历项和项目，ReminderTime 和 ReminderSignalTime 属性的“写入时复制”功能禁用。对这些属性的更改并不是由“写入时复制”功能捕获的。对 RSS 源的更改并不是由“写入时复制”功能捕获的。


尽管“DiscoveryHold”、“清除”和“版本”文件夹对用户不可见，但“可恢复的项目”文件夹中的所有项目由 Exchange 搜索编制索引，并且可使用就地电子数据展示来发现。从就地保留或诉讼保留中删除邮箱用户后，“DiscoveryHold”、“Purges”和“Version”文件夹中的项目将被托管文件夹助理清除。

返回顶部

## 保留和邮箱配额

“可恢复的项目”文件夹中的项目不根据用户的邮箱配额进行计算。在 Exchange 中，“可恢复的项目”文件夹有其自己的配额。在 Exchange 中，*RecoverableItemsWarningQuota* 和 *RecoverableItemsQuota* 邮箱属性的默认值分别设置为 20 GB 和 30 GB。若要对 Exchange Server 2013 邮箱数据库修改这些值，请使用 [Set-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/bb123971\(v=exchg.150\)) cmdlet。若要对单个邮箱修改这些值，请使用 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\)) cmdlet。

当用户的“可恢复的项目”文件夹超出可恢复的项目的警告配额（由 *RecoverableItemsWarningQuota* 参数指定）时，将在邮箱服务器的应用程序事件日志中记录事件。当该文件夹超出可恢复的项目的配额（由 *RecoverableItemsQuota* 参数指定）时，用户将无法清空“已删除的项目”文件夹或永久删除邮箱项目。而且，“写入时复制”也将无法创建已修改项目的副本。因此，监视就地保留的邮箱用户的“可恢复的项目”配额很关键。

在 Exchange Online 中，当将邮箱置于诉讼保留或就地保留状态时，“可恢复的项目”文件夹（在用户的主邮箱中）的配额会自动增加至 100 GB。当置于保留状态的邮箱的主邮箱“可恢复的项目”文件夹的存储配额接近其限额时，可以执行以下操作：

  - **启用存档邮箱并开启自动扩展存档**   只需启用存档邮箱，然后启用 ExchangeOnline 中的自动扩展存档功能，就可以为“可恢复的项目”文件夹开启无限制存储容量。这会使主邮箱中“可恢复的项目”文件夹的容量达到 100 GB，而用户存档中的“可恢复的项目”文件夹的存储容量不受限制。请参阅如何：[在 Office 365 安全与合规中心中启用存档邮箱](https://go.microsoft.com/fwlink/p/?linkid=863320)和[在 Office 365 中启用无限制的存档](https://go.microsoft.com/fwlink/p/?linkid=844569)。
    
    **注意：** 
    
      - 为“可恢复的项目”文件夹存储配额接近上限的邮箱启用存档功能后，可能需要运行托管文件夹助理以自动触发助理处理邮箱，以便将过期项目移至存档邮箱的“可恢复的项目”文件夹。请参阅[增加置于保留状态的邮箱可恢复项目的配额](https://go.microsoft.com/fwlink/p/?linkid=786479)中的步骤 4 了解相关说明。
    
      - 注意，用户邮箱中的其他项目可能会移至新的存档邮箱。请考虑告知用户启用存档邮箱后可能会出现此情况。

  - **创建置于保留状态的邮箱的自定义保留策略**    除了为置于诉讼保留或就地保留状态的邮箱启用存档邮箱和自动扩展存档以外，你还可能想要为置于保留状态的邮箱创建自定义保留策略。你可以将保留策略应用于保留的邮箱，此策略与应用到未保留邮箱的“默认 MRM 策略”有所不同。这样就可以应用专为置于保留状态的邮箱设计的保留标记。其中包括为“可恢复的项目”文件夹创建新的保留标记。

有关详细信息，请参阅[增加置于保留状态的邮箱可恢复项目的配额](https://go.microsoft.com/fwlink/p/?linkid=786479)。

## 保留项和电子邮件转发

用户可以使用 Outlook 和 Outlook Web App 为其邮箱设置电子邮件转发。利用电子邮件转发，用户可以将邮箱配置为将发送至其邮箱的电子邮件转发给其组织内部或外部的其他邮箱。可以配置电子邮件转发，以便发送到原始邮箱的所有邮件不会被复制到该邮箱，并且只会被发送到转发地址。

如果为邮箱设置了电子邮件转发，而且邮件无法被复制到原始邮箱，则如果该邮箱处于保留状态，将会发生什么？根据该邮箱在 Exchange 2013 或 Exchange Online 组织中的不同情况，会发生相应不同的行为。

  - **Exchange Online**   在传递过程中会对邮箱的保留设置进行检查。如果邮件符合邮箱的保留条件，则该邮件的副本会被保存到“可恢复的项目”文件夹中。这意味着您可以使用就地电子数据展示搜索原始邮箱，以查找被转发到另一个邮箱的邮件。

  - **Exchange 2013**   如果邮件被转发到另一个邮箱，而且未复制到原始邮箱，则不会将这些邮件捕获并复制到“可恢复的项目”文件夹。这意味着不会将转发的邮件返回到就地电子数据展示搜索中。若要解决此问题，Exchange 2013 组织可以考虑删除用户配置电子邮件转发的功能。

返回顶部

## 保留存档的 Lync 内容

Exchange 2013、Microsoft Lync 2013 和 Microsoft SharePoint 2013 提供集成的保留和电子数据展示体验，使您能够跨不同数据存储保留和搜索项目。Exchange 2013 允许您将 Lync Server 2013 内容存档在 Exchange 中，并消除要具备单独的 SQL Server 数据库才能存储存档 Lync 内容的要求。通过 SharePoint 2013 中集成的保留和电子数据展示功能，您可以从单个控制台跨所有存储保留和搜索数据。

将 Exchange 2013 邮箱置于就地保留或诉讼保留时，Microsoft Lync 2013 内容（如联机会议中共享的即时消息会话和文件）将存档在邮箱中。如果使用 Microsoft SharePoint 2013 中的电子数据展示中心或 Exchange 2013 中的就地电子数据展示搜索邮箱，则搜索结果中还会返回匹配搜索查询的所有存档的 Lync 内容。还可以将搜索限制为邮箱中存档的 Lync 内容。

要启用 Exchange 2013 邮箱中 Lync 内容的存档，必须配置 Lync 2013 与 Exchange 2013 的集成。有关详细信息，请参阅下列主题：

  - [规划存档](https://technet.microsoft.com/zh-cn/library/jj205069\(v=ocs.15\))

  - [部署存档](https://technet.microsoft.com/zh-cn/library/jj205147\(v=ocs.15\))

返回顶部

## 删除处于保留状态的邮箱

当您删除了已被置于诉讼保留或就地保留的邮箱时，根据该邮箱位于 Exchange 2013 或 Exchange Online 组织的不同，结果会有所不同。

  - **Exchange 2013**   如果管理员删除带有邮箱的用户帐户，Exchange 信息存储最终将检测到此邮箱不再连接到用户帐户，并将此邮箱标记为删除，即使邮箱处于保留状态也是如此。如果您想保留此邮箱，则必须执行以下操作：
    
    1.  禁用用户帐户，而不是删除用户帐户。
    
    2.  更改邮箱的属性以限制邮箱的使用和对它的访问。例如，将发送和接收配额设置为 1，阻止可以将邮件发送到邮箱的用户，限制可以访问邮箱的用户。
    
    3.  保留此邮箱，直到擦除所有数据或直到不再需要保留数据为止。

  - **Exchange Online**   如果用户的邮箱被置于就地保留或诉讼保留状态，而相应的 Office 365 帐户被删除，则该邮箱会被转换为*处于非活动状态的邮箱* - 这是一种软删除邮箱。当用户离开您的组织之后，非活动邮箱用于保留该用户的邮箱内容。由于您在邮箱变为非活动邮箱之前将其置于保留状态，因此非活动邮箱中的项目会在此保留期内保留。这使得管理员、合规部主管或记录管理员可以使用就地电子数据展示来访问非活动邮箱的内容。非活动邮箱无法接收电子邮件，也不显示在您组织的共享通讯簿或其他列表中。有关详细信息，请参阅[Exchange Online 中的非活动邮箱](https://technet.microsoft.com/zh-cn/library/dn798632\(v=exchg.150\))。

返回顶部

## 将处于保留状态的邮箱从 Exchange 2013 迁移到 Office 365

如果您有 Exchange 混合部署，当您将本地 Exchange 2013 邮箱移动（上载）到 Office 365 中的 Exchange Online 时，应满足以下条件：

  - 如果本地邮箱处于诉讼保留或就地保留状态，则在保存保留设置之前应先将邮箱移动到 Exchange Online。

  - 如果本地邮箱处于诉讼保留或就地保留状态，则“可恢复的项目”文件夹中的任何内容都会移动到 Exchange Online 邮箱。

> [!NOTE]  
> 当您将 Exchange Online 邮箱移动（分离）到本地 Exchange 2013 组织中时，也会对“可恢复的项目”文件夹中的保留设置和内容进行保存。


还有其他一些方法可以将本地电子邮件数据迁移到 Office 365，例如，使用暂存 Exchange 迁移或直接转换 Exchange 迁移。

  - 暂存迁移可用于将邮箱从 Exchange 2003 或 Exchange 2007 中迁移到 Office 365。 在这些版本的 Exchange 中，“可恢复的项目”文件夹（及其功能）不存在。 因此，当您将 Exchange 2003 或 Exchange 2007 邮箱迁移到 Office 365 时，没有任何要移动的“可恢复的项目”文件夹内容。

  - 直接转换迁移可用于将邮箱从 Exchange 2003、Exchange 2007 和 Exchange 2010 迁移到 Office 365。如上文所述，Exchange 2003 和 Exchange 2007 邮箱都没有可迁移的“可恢复的项目”文件夹。因为在 Exchange 2010 中引入了“可恢复的项目”文件夹，所以当您使用直接转换迁移来迁移 Exchange 2010 邮箱时，“可恢复的项目”文件夹中的内容就会被迁移到 Office 365。

> [!TIP]  
> 对于 Exchange 2013 和 Exchange 2010，推荐采用 Exchange 混合部署作为将本地邮箱迁移到 Office 365 的方法。


返回顶部
