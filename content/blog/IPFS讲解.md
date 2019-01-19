+++
author = "Abser"
categories = ["IPFS"]
date = 2019-01-19T15:37:49+08:00
description = "关于IPFS的基础概念"
featured = "pic02.jpg"
featuredalt = "pic02"
featuredpath = "date"
linktitle = ""
title = "IPFS讲解"
type = "post"

+++

# IPFS普及知识

### 行星际文件系统任务
InterPlanetary文件系统（IPFS）的目标是创建分布式Web。一种点对点超媒体协议，使网络更快，更安全，更开放。<br /><br />
### 两个'中心'问题
集中化带来了几个主要问题。第一个是当你有一个控制大量数据的中央公司时，如果无法访问这些服务器会发生什么？控制存储大量有价值和有用数据的服务器的中央公司单点故障导致完全无法访问。这种失败可能是由于攻击造成的，也可能是因为服务器离线了。<br />将数据存储在中心位置的第二个问题是审查。当大多数数据托管在几个主要服务器上时，政府更容易阻止对它们的访问。2017年，土耳其居民无法访问Wikipedia.com。土耳其政府禁止该网站称其为“国家安全威胁”。这也发生在2011年1月的埃及，当时政府为95％以上的公民切断了互联网和手机接入。<br /><br />
### 为什么我们使用有缺陷的系统？
我们继续接受这种模式的真正原因是我们已经因为接入互联网而受到损害。我们希望网页以毫秒为单位加载，图像和视频无延迟地显示，当然，这一切都必须具有最高的HD或4K质量。集中服务器使公司可以完全控制他们提供此内容的速度，并相应地收取费用。我们继续这种方法的另一个原因是，确实没有一个好的选择。<br /><br />
### IPFS→好的选择
InterPlanetary文件系统（也称为IPFS）是一种使Internet完全分布的想法。该概念将传统的“HTTP”互联网转变为对等网络，类似于BitTorrent的工作方式。<br />Juan Benet是IPFS的创建者和Protocol Labs的创始人。Protocol Labs是一家负责IPFS的技术研发实验室，他们还开发了Filecoin和IPLD（以及其他）。Benet在斯坦福大学学习计算机科学，并且非常关注与知识，科学和技术有关的任何事情。<br />![](https://achainofblocks.com/wp-content/uploads/2018/10/interplanetary-file-system-ipfs-simply-explained-file-coin-bitcoin-juan-benet.png#align=left&display=inline&height=245&link=https%3A%2F%2Fachainofblocks.com%2Fwp-content%2Fuploads%2F2018%2F10%2Finterplanetary-file-system-ipfs-simply-explained-file-coin-bitcoin-juan-benet.png&linkTarget=_blank&originHeight=183&originWidth=160&width=214)<br />Juan Benets最初的目标并不是在制作这个概念时必然会创建IPFS。他想要做的是找到一种有效的方法来移动科学数据集，这意味着数据大小可能是10-100 + GB。IPFS的设计看起来像Git和BitTorrent一起生孩子时会发生什么。BitTorrent使您能够快速地在网络上移动大型文件，Git为您提供内置的数据版本。<br />![](https://achainofblocks.com/wp-content/uploads/2018/10/interplanetary-file-system-ipfs-simply-explained-file-coin-bitcoin-ipfs-300x147.png#align=left&display=inline&height=147&link=https%3A%2F%2Fachainofblocks.com%2Fwp-content%2Fuploads%2F2018%2F10%2Finterplanetary-file-system-ipfs-simply-explained-file-coin-bitcoin-ipfs.png&linkTarget=_blank&originHeight=147&originWidth=300&width=300)<br />在创建此协议之后，Benet很快意识到其影响远大于移动大型数据集。他实际上创建了一个协议，可以取代其他流行的协议，以便我们今天通过网络访问信息。<br /><br />
### InterPlanetary文件系统的名称来自哪里？
当他们提出行星际文件系统（IPFS）的命名时，其想法是向互联网如何命名致敬。JCR Licklider是Arpanet（互联网的前身）的创造者，其目标是建立一个星际网络。因此，互联网对于星际网络而言确实很短。InterPlanetary采用相同的命名约定，此外，IPFS旨在成为Internet协议（IP）的文件系统（FS）。当把它们放在一起时，便有了IPFS，即互联网文件系统。我将深入探讨IPFS如何作为文件系统。但首先，了解我们今天如何从网络访问文件非常重要。<br /><br /><br />当您想从互联网上下载图像时，您可以告诉您的计算机确切地找到您要求的图像的位置。此位置通常采用URL的形式，其中包含存储照片的公司的域名，后面跟着指定文件内容的扩展名。此博客文章的示例请求如下所示：https://achainofblocks.com/ipfs-simple-guide.jpg。这种访问资源的方法称为“基于位置的寻址”，您告诉计算机他们可以访问信息的位置，并且计算机检索信息。此方法的一个问题是，如果位置不可访问（可能服务器处于脱机状态），则用户的计算机无法检索所需的信息。<br />![](https://achainofblocks.com/wp-content/uploads/2018/10/InterPlanetary-File-System-IPFS-Location-Based-Addressing-HTTP-300x120.png#align=left&display=inline&height=156&link=https%3A%2F%2Fachainofblocks.com%2Fwp-content%2Fuploads%2F2018%2F10%2FInterPlanetary-File-System-IPFS-Location-Based-Addressing-HTTP.png&linkTarget=_blank&originHeight=120&originWidth=300&width=390)

### 服务器关闭，我们都倒闭了
使用服务器关闭时基于位置的寻址，无法通过Internet访问该服务器中包含的所有内容。但是，当服务器发生故障时，另一个用户很可能已下载该图像，并将其本地存储在其计算机上。但即使另一台计算机确实有此文件，您的计算机也无法与这些计算机连接以传输该文件。<br /><br />
### 关于内容
为了帮助解决这个问题，IPFS引入了“基于内容的寻址”的概念。在请求特定资源时使用基于内容的寻址时，您无需指定位置，只需指定所需内容即可。<br />每个文件都有一个唯一的哈希值，可以将其视为文件的指纹或标识。如果要访问特定文件，只需向网络询问具有指定哈希值的文件副本即可。请求完成后，IPFS网络上的某个人将提供您请求的资源。您将下载该资源，并将副本保存到您的IPFS缓存中。现在，当另一个人来并请求相同的文件时，您将能够提供给他们。这创建了一个系统，随着它的使用速度越来越快，因为共享的文件越多，它们就越容易获得，它们就是一组节点。<br /><br />
### 有改变是好事…
在这一点上，我和你有同样的问题：这个行为正确吗？我怎么知道提供给我文件的人或节点没有以某种方式篡改它？因为您使用哈希函数来检索文件，所以您可以验证收到的内容。更改文件的哈希值与更改区块链中的事务同样困难。请求具有特定散列的文件，因此在收到文件时，请确保散列与请求匹配。这与您用于验证亚马逊购买的方法相同。如果您订购了Green Socks，并且Red Socks出现，您将拒绝它们并等待您的Green Socks出现。<br />IPFS的另一个功能是重复数据删除，这意味着当多个用户发布同一文件时，它只在网络上创建一次。这有助于提高网络效率。<br /><br />
### IPFS如何真正起作用
现在您已经了解了IPFS与当今传统方法的比较基础，让我们更深入地了解IPFS如何实际存储数据并使其可供用户访问。<br />在IPFS中，文件存储在IPFS对象中，每个Object可以存储256 kb的数据。对象还可以包含指向另一个IPFS对象的链接，链接可以存储大于256 kb的数据。例如，如果您只上传一个小文本文件，那么一个256 kb的对象应该适合您的少量文本。<br />![](https://achainofblocks.com/wp-content/uploads/2018/10/InterPlanetary-File-System-IPFS-Content-Based-Addressing-Data-object-300x188.png#align=left&display=inline&height=188&link=https%3A%2F%2Fachainofblocks.com%2Fwp-content%2Fuploads%2F2018%2F10%2FInterPlanetary-File-System-IPFS-Content-Based-Addressing-Data-object.png&linkTarget=_blank&originHeight=188&originWidth=300&width=300)<br />但是，如果要存储图片，则会将其分解为多个对象，每个对象最大为256 kb。然后，IPFS系统将创建一个空对象，该对象将链接到构成该图片的所有对象。<br />![](https://achainofblocks.com/wp-content/uploads/2018/10/InterPlanetary-File-System-IPFS-Content-Based-Addressing-Data-object-JPG-300x193.png#align=left&display=inline&height=345&link=https%3A%2F%2Fachainofblocks.com%2Fwp-content%2Fuploads%2F2018%2F10%2FInterPlanetary-File-System-IPFS-Content-Based-Addressing-Data-object-JPG.png&linkTarget=_blank&originHeight=193&originWidth=300&width=536)<br />这种架构非常简单，但它也非常强大，该架构真正使IPFS能够用作文件系统。如果你看一下下面的简单文件目录结构，我将解释如何将其转换为IPFS结构：<br />![](https://achainofblocks.com/wp-content/uploads/2018/10/Interplanetary-File-System-IPFS-Simple-File-Structure-300x293.png#align=left&display=inline&height=352&link=https%3A%2F%2Fachainofblocks.com%2Fwp-content%2Fuploads%2F2018%2F10%2FInterplanetary-File-System-IPFS-Simple-File-Structure.png&linkTarget=_blank&originHeight=293&originWidth=300&width=360)<br />通过为每个文件和每个文件夹/目录创建1个对象，然后将文件链接到指定的目录，可以将其转换为IPFS。如果考虑到IPFS使用基于内容的寻址的话会变得更好。这意味着添加的文件是不可变的，它们永远不会被更改，非常像区块链。这意味着访问的资源是正确的数据，并且从未被更改过。<br />![](https://achainofblocks.com/wp-content/uploads/2018/10/InterPlanetary-File-System-IPFS-Content-Based-Addressing-Data-object-File-System-300x214.png#align=left&display=inline&height=335&link=https%3A%2F%2Fachainofblocks.com%2Fwp-content%2Fuploads%2F2018%2F10%2FInterPlanetary-File-System-IPFS-Content-Based-Addressing-Data-object-File-System.png&linkTarget=_blank&originHeight=214&originWidth=300&width=470)

### 我如何更新我的数据？
IPFS支持文件版本控制，这与Git如何作为开源代码库一样工作。例如，您正在处理名为“Important Document – v1.doc”的文本文件，并且您希望与使用IFPS的人共享此文档。当您将此文件添加到IPFS时，幕后发生的事情是，IPFS将创建一个新的Commit对象。这个Object是非常基本的，它只是告诉IPFS哪个Commit在此之前，它链接到与文件相关的IPFS对象，'Important Document – v1.doc'。<br />![](https://achainofblocks.com/wp-content/uploads/2018/10/InterPlanetary-File-System-IPFS-Content-Based-Addressing-Data-object-commit-object-207x300.png#align=left&display=inline&height=300&link=https%3A%2F%2Fachainofblocks.com%2Fwp-content%2Fuploads%2F2018%2F10%2FInterPlanetary-File-System-IPFS-Content-Based-Addressing-Data-object-commit-object.png&linkTarget=_blank&originHeight=300&originWidth=207&width=207)<br />现在让我们假设已经过了一段时间，你的'Important Document.doc'需要修改。只需将新文件添加到IPFS“Important Document – v2.doc”即可完成此操作，软件将为更新的文件创建新的提交对象（与原始进程相同）。此提交对象现在链接到先前的提交对象，第一个提交用作父对象。这个过程可以无休止地重复，创建一个链接的相同数据版本，所有这些都引用整个链。IPFS确保您的文件以及整个文件版本控制历史记录可供网络上的所有其他节点访问。<br />![](https://achainofblocks.com/wp-content/uploads/2018/10/InterPlanetary-File-System-IPFS-Content-Based-Addressing-Data-object-commit-object-versioning-300x163.png#align=left&display=inline&height=242&link=https%3A%2F%2Fachainofblocks.com%2Fwp-content%2Fuploads%2F2018%2F10%2FInterPlanetary-File-System-IPFS-Content-Based-Addressing-Data-object-commit-object-versioning.png&linkTarget=_blank&originHeight=163&originWidth=300&width=445)

### 没有系统是完美的
到目前为止，我们已经讨论了InterPlanetary文件系统的许多有用功能和关键概念。但是，所有协议都有局限性和缺点。正如您可能想象的那样，IPFS目前面临的最大问题是保持文件可用。网络上的每个节点都保留了已下载文件的缓存，并有助于使其可用，因为其他用户需要它们。但是，在一个简单的情况下，如果一个Document由4个节点托管，并且它们全部脱机，则该文档不再可访问。<br />有几种方法可以解决上述问题。一种方法是激励节点保持在线并使文件可供社区使用。对可以提交给网络的存储空间的奖励，这将确保文件很可能在需要时可用。另一种方法是主动在整个网络中分发文件，确保在任何给定时间总是有足够的在线副本。你可以把它想象成大规模的冗余。<br /><br />
### Filecoin
这个问题是Filecoin旨在解决的确切问题。Filecoin由创建IPFS的同一组创建。Filecoin是一个建立在IPFS之上的区块链，其目标是创建一个分散的存储市场。这意味着在硬盘上有额外存储空间的用户可以将其出租用作IPFS存储，并在此过程中从中赚取一些钱。您可以将Filecoin视为与Airbnb类似的服务，而不是租用您家中的可用空间，您可以租用计算机上的可用空间进行存储。Filecoin为节点创建了一种激励，使数据保持在线并尽可能长时间保留。除了保持节点在线的激励之外，它还可以跨多个节点复制数据，使其高度可用且易于访问（即使少数节点处于脱机状态）。Filecoin和IPFS具有相同的目标，即脱机优先，这意味着他们不断努力获得更好的体验，而无需调用服务器来访问资源。<br />这是Filecoin的一个非常高级的快速摘要。我将在未来的文章中深入研究Filecoin以及Protocol实验室中的一些其他伟大项目。<br />![](https://achainofblocks.com/wp-content/uploads/2018/10/interplanetary-file-system-ipfs-filecoin-300x200.png#align=left&display=inline&height=200&link=https%3A%2F%2Fachainofblocks.com%2Fwp-content%2Fuploads%2F2018%2F10%2Finterplanetary-file-system-ipfs-filecoin.png&linkTarget=_blank&originHeight=200&originWidth=300&width=300)

### 行星际关联数据（IPLD）
根据[https://ipld.io](https://ipld.io/)：<br />“IPLD是内容可寻址网络的数据模型。它允许我们将所有与哈希相关的数据结构视为统一信息空间的子集，统一所有将数据与哈希作为IPLD实例链接的数据模型。“<br />这意味着IPLD旨在成为可互操作协议的数据模型。这种技术有很多用例。这使得能够在IPFS上运行智能合约。关键是IPLD提供的库使底层数据可以跨工具和协议进行互操作。<br />IPLD和Fileco都是非常复杂的项目，需要他们自己的专门文章才能完全理解。<br /><br />
### 额外的想法
我希望通过阅读本文显而易见，IPFS是一个非常雄心勃勃的项目。以权力下放为重点的大多数早期项目主要涉及货币和财务方面。IPFS实际上是建立一种更好的共享数据的方式。之前有过HTTP的挑战。然而，IPFS显然是最成熟的，并且被视为可以在未来几年中大规模采用的系统。我绝不暗示HTTP正在消失，Juan Benet自己也承认HTTP是一个很棒的协议，它仍然非常有用。但是，它是一个超过25年的协议，随着IPFS在采用中的不断增长，用例将随着技术的发展而扩展。在IPFS最终接管之前，我们很有可能会同时使用这两种协议。


## Reference
[https://achainofblocks.com/2018/10/05/ipfs-interplanetary-file-system-simply-explained/](https://achainofblocks.com/2018/10/05/ipfs-interplanetary-file-system-simply-explained/)<br />翻译整理：abser
