---
title: 安全基础概念
date: 2020-07-11 10:00:00
categories: Security
tags:
  - security
---

安全基础概念

<!--more-->

## 安全的本质

任何应用最本质的东西其实都是数据。用户使用产品的过程，就是在和企业进行数据交换的过程。比如，用户在使用微博时，或是将数据写入到微博（发博、评论、点赞等）中，或是从微博中获取数据（刷 feed、热门流）；用户在使用支付宝进行交易时，则是将资产以数据的形式进行转移。

安全的本质就是保护数据被合法地使用。怎么才叫“被合法地使用”呢？我们可以从机密性、完整性、可用性这 3 个方面具体来看。这也是在安全领域内最为基础的 3 个安全原则。

**安全原则**

机密性（Confidentiality）、完整性（Integrity）、可用性（Availability），我们可以简称为 CIA 三元组，是安全的基本原则。理论上来说，一个完整的安全保障体系，应该充分考虑到所有的 CIA 原则。当然，实际情况中，我们会根据企业需求，对安全在这三个方向上的投入做取舍。我们平时在评判一个企业的安全水平时，也会分别从这三个方向进行考量。

![1][1]

### 机密性

机密性用一句话来说就是，确保数据只被授权的主体访问，不被任何未授权的主体访问。 简单用一个词总结就是“不可见”。

举个例子，你不会允许陌生人查看你的个人隐私信息，但你可能会允许父母、朋友查看部分信息。同样的，对于应用中的数据，比如微信的朋友圈，你可以允许好友查看三天内的数据，但不允许好友查看三天前的数据。这些都是机密性在日常生活中的表现。

机密性强调的是数据的“不可见”，但这并不代表数据是正确的。比如，将一个“True”存成了“False”，这就不是机密性要考虑的事了，而这种错误的存储，则是完整性需要考虑的事情。

### 完整性

完整性就是确保数据只被授权的主体进行授权的修改，简单来说，就是“不可改”。

所谓“授权的修改”，就是对主体可进行的操作进行进一步的限制。比如，只能追加数据的主体无法执行删除的操作。以个人隐私信息为例，法律允许学校或者公司在个人档案内追加信息，但不能做任何修改。又或者说，你自己发的朋友圈，不希望被其他人进行修改。这些都是完整性的典型表现。

### 可用性

可用性应该是你最熟悉的原则。因为它不仅仅是安全方向上的问题，也是工程上面临的主要挑战。用一句话来说就是，可用性就是确保数据能够被授权的主体访问到， 简单来说，就是“可读”。

举个典型的例子，面对高峰期的集中用户访问，如何保障用户能够正常地获取数据（“双 11”购物或者 DDoS 攻击等），你可以看到大量的研发人员对这个问题进行探讨和分享，但这其实都属于安全在可用性上的考量范围。

在安全机制上，我们要确保授权机制能够正确运行，使得拥有访问数据的主体能够及时地被授权，这是可用性的基本。那具体来说，可用性会面临哪些挑战呢？

- 在运维层面上，有很多技术在为可用性提供支撑，比如，在基础建设上的机房建设（如何在断电、高温、火灾等情况下保护设备）、多地冗余，以及在服务中的备份、资源冗余等。
- 在研发层面上，如何降低响应延迟、如何处理海量数据、如何在峰值进行扩容等，这些问题其实都是在可用性上的挑战。
- 在攻击的角度上，黑客也会对可用性发起攻击，也就是我们常说的 DoS（Denial of Service，拒绝服务）攻击。比如，通过发送大量的流量来占满带宽资源。

**小结**

- 安全的基本原则：机密性，完整性，可用性。简称CIA。
- 机密性强调的是不可见性，数据只能被授权的主体访问。
- 完整性强调的是不可改，数据只能最追加操作，对数据的修改过程进行日志记录。
- 可用性强调的是可读，数据的可达性。

## 安全原则

不同的应用、不同的模块会受到不同的安全威胁，当然，我们面对这些威胁也会有不同的解决方案。万变不离其宗。正如安全威胁都是针对 CIA 三元组产生的攻击一样，安全解决方案在根本思路上也都是相通的。

### 什么是“黄金法则”？

黄金法则主要包含三部分：认证（Authentication）、授权（Authorization）、审计（Audit）。为什么称它为“黄金”呢？一方面是因为，它包含的这三部分重要且通用；另一方面是因为，这三个单词的前两个字母都是 Au，而 Au 在元素周期表中代表着“金”。

有的教材中，会给黄金法则加上问责（Accounting）这一部分，组成“4A 法则”；还有的会加上身份识别（Identification），组成“IAAAA 法则”。不管被划分为几个部分，这些法则的中心内容都是相似的，都是围绕着识别、认证、授权、审计、问责这五个部分展开的。因此，黄金法则其实就是 IAAAA 法则更高一层的概括，它将识别和认证、审计和问责归纳到了一起，更加强调了这两两之间的协同性质。

这三部分其实是一种串联的关系，它描述的其实是用户在使用应用过程中的生命周期：先进行登录、再进行操作、最后留下记录。

![2][2]

### 身份识别和认证

认证其实包括两个部分：身份识别和认证。身份识别其实就是在问“你是谁”，你会回答“你是你”。身份认证则会问“你是你吗”，那你要证明“你是你”这个回答是合法的。

身份识别和认证通常是同时出现的一个过程。身份识别强调的是主体如何声明自己的身份，而身份认证强调的是，主体如何证明自己所声明的身份是合法的。比如说，当你在使用用户名和密码登录的过程中，用户名起到身份识别的作用，而密码起到身份认证的作用；当你用指纹、人脸或者门卡等进行登入的过程中，这些过程其实同时包含了身份识别和认证。

依据具体的认证场景，对安全等级、易用性等的综合考量，认证形式可以大致分为三种。按照认证强度由弱到强排序，分别是：

- 你知道什么（密码、密保问题等）；
- 你拥有什么（门禁卡、安全令牌等）；
- 你是什么（生物特征，指纹、人脸、虹膜等）。

> 我们通过将多种类型的认证进行组合，可以形成多因素认证机制，进一步加强认证强度。常见的，在登录过程中，很多应用会在输入完账号密码后，让你进行手机验证，这其实就是结合了“你知道什么”和“你拥有什么”的双因素认证。

### 授权

在确认完“你是你”之后，下一个需要明确的问题就是“你能做什么”。毫无疑问，在系统或者应用中，我们的操作都会受到一定的限制。比如，某些文件不可读，某些数据不可修改。这就是授权机制。除了对“你能做什么”进行限制，授权机制还会对“你能做多少”进行限制。比如，手机流量授权了你能够使用多少的移动网络数据。

### 审计和问责

当你在授权下完成操作后，安全需要检查一下“你做了什么”，这个检查的过程就是审计。当发现你做了某些异常操作时，安全还会提供你做了这些操作的“证据”，让你无法抵赖，这个过程就是问责。

举一个生活中的例子，当你去银行办理业务时，工作人员会让你对一些单据签字。这些单据就是审计的信息来源，而签字则保证了你确认这是你进行的操作，这就是问责的体现。

审计和问责通常也是共同出现的一个过程，因为它们都需要共同的基础：日志。很容易理解，所谓审计，就是去通过日志还原出用户的操作历史，从而判断是否出现违规的操作。而问责则是通过日志的完整性，来确保日志还原出来的操作是可信的。

> 安全不存在“银弹”，不可能达到 100% 的安全。即使是 1% 的漏洞，也可能造成 100% 的损伤。

**小结**

黄金法则描述的是，在用户操作的各个环节中，我们所需要采取的安全策略。黄金法则的核心内容包括三部分：认证、授权、审计。大部分情况下，事前防御属于认证，事中防御属于授权，事后防御属于审计。

## 密码学基础

密码学是“黄金法则”的基础技术支撑。失去了密码学的保护，任何认证、授权、审计机制都是“可笑”的鸡肋。

首先，先来普及一个语文知识。密钥中的钥，发音为 yuè，不是 yào。(口语中多读mìyào)。

### 对称加密算法

所谓对称加密，代表加密和解密使用的是同一个密钥。概念很简单，但是也很不具体、直观。

![3][3]

下面我来具体讲讲这个过程，如果我想给你发一段消息，又不想被其他人知道。那么我作为发送方，会使用加密算法和密钥，生成消息对应的密文；而你作为接收方，想要阅读消息，就需要使用解密算法和一个同样的密钥，来获得明文。

我们常见的经典对称加密算法有 DES、IDEA、AES、国密 SM1 和 SM4。

**第一种对称加密算法是 DES（数据加密标准，Data Encryption Standard）。**

DES 应该是最早的现代密码学算法之一。它由美国政府提出，密钥长度为 56 位。目前，它暴力破解 56 位密码的时间，已经能控制在 24 小时内了。

DES 实际上是一个过时的密码学算法，目前已经不推荐使用了。关于 DES，还有一点特别有意思。DES 包含一个关键模块：S 盒，其设计的原理一直没有公开。因此，很多人都相信，这个 S 盒中存在后门，只要美国政府需要，就能够解密任何 DES 密文。

**第二种对称加密算法是 IDEA（国际数据加密算法，International Data Encryption Algorithm）。**

IDEA 由瑞士研究人员设计，密钥长度为 128 位。对比于其他的密码学算法，IDEA 的优势在于没有专利的限制。相比于 DES 和 AES 的使用受到美国政府的控制，IDEA 的设计人员并没有对其设置太多的限制，这让 IDEA 在全世界范围内得到了广泛地使用和研究。

**第三种需要了解的对称加密算法是 AES（高级加密标准，Advanced  Encryption  Standard）。**

在 DES 被破解后，美国政府推出了 AES 算法，提供了 128 位、192 位和 256 位三种密钥长度。通常情况下，我们会使用 128 位的密钥，来获得足够的加密强度，同时保证性能不受影响。目前，AES 是国际上最认可的密码学算法。在算力没有突破性进展的前提下，AES 在可预期的未来都是安全的。

**最后一种是国密 SM1（SM1 Cryptographic Algorithm）和 SM4（SM4 Cryptographic Algorithm）。**

密码学作为安全的基础学科，如果全部依靠国外的技术，对于国家安全可能产生不利影响。因此，中国政府提出了一系列加密算法。其中，国密算法 SM1 和 SM4 都属于对称加密的范畴。SM1 算法不公开，属于国家机密，只能通过相关安全产品进行使用。而 SM4 属于国家标准，算法公开，可自行实现使用。国密算法的优点显而易见：受到国家的支持和认可。

![4][4]

在加密通信中（如 HTTPS、VPN、SSH 等），通信双方会协商出一个加密算法和密钥，对传输的数据进行加密，从而防止第三方窃取。在类似数据库加密这种存储加密技术中，通信双方也是将存储空间中的数据进行加密，这样即使硬盘被物理窃取，也不会导致信息丢失。在公司内部，为了避免用户的 Cookie 和隐私信息发生泄露，也需要对它们进行加密存储。

对于大部分公司来说，选取 AES128 进行加解密运算，就能获得较高的安全性和性能。如果是金融或政府行业，在涉及国家层面的对抗上，有一定的合规需求，则需要应用国密算法。

另外，在选取加密算法的时候，存在不同的分组计算模式：ECB/CBC/CFB/OFB/CTR。这些模式的具体细节不是我们学习的重点，在这里就不展开了。你需要知道的是：选取 CBC 和 CTR 这两种推荐使用的模式就可以满足大部分需求了，它们在性能和安全性上都有较好的保证。

### 非对称加密算法

非对称加密代表加密和解密使用不同的密钥。具体的加解密过程就是，发送方使用公钥对信息进行加密，接收方收到密文后，使用私钥进行解密。

![5][5]

当使用对称加密算法的时候，你不仅要跟每一个通信方协定一个密钥，还要担心协商过程中密钥泄露的可能性。比如，我当面告诉了你一个密码，怎么保证不被偷听呢？而在非对称加密算法中，公钥是公开信息，不需要保密，我们可以简单地将一个公钥分发给全部的通信方。也就是说，我现在就可以告诉你一个公钥密码，即使这意味着所有阅读这篇文章的人都知道了这个密码，那也没关系。因此，非对称密钥其实主要解决了密钥分发的难题。

除了加密功能外，大部分的非对称算法还提供签名的功能。这也就是说，我们可以使用私钥加密，公钥解密。一旦接收方通过公钥成功解密，我们就能够证明发送方拥有对应的私钥，也就能证实发送方的身份，也就是说，私钥加密就是我们说的签名。

所有的非对称加密算法，都是基于各种数学难题来设计的，这些数学难题的特点是：正向计算很容易，反向推倒则无解。经典的非对称加密算法包括：RSA、ECC 和国密 SM2。

**第一种非对称加密算法 RSA（RSA 加密算法，RSA Algorithm）。**

RSA 的数学难题是：两个大质数 p、q 相乘的结果 n 很容易计算，但是根据 n 去做质因数分解得到 p、q，则需要很大的计算量。RSA 是比较经典的非对称加密算法，它的主要优势就是性能比较快，但想获得较高的加密强度，需要使用很长的密钥。

**第二种 ECC（椭圆加密算法，Elliptic Curve Cryptography）。**

ECC 是基于椭圆曲线的一个数学难题设计的。目前学术界普遍认为，椭圆曲线的难度高于大质数难题，160 位密钥的 ECC 加密强度，相当于 1088 位密钥的 RSA。因此，ECC 是目前国际上加密强度最高的非对称加密算法。

**最后一种是国密 SM2（SM2 Cryptographic Algorithm）。**

国密算法 SM2 也是基于椭圆曲线问题设计的，属于国家标准，算法公开，加密强度和国际标准的 ECC 相当。而国密的优势在于国家的支持和认可。

![6][6]

对比于对称加密算法，非对称加密算法最大的优势就是解决密钥分发的问题。因此，现在大部分的认证和签名场景，其实使用的都是非对称加密算法。比如，在 SSH 登录、Git 上传等场景中，我们都可以将自己的公钥上传到服务端，然后由客户端保存私钥。如果你遇到需要使用非对称加密的场景（比如多对一认证），我推荐你使用 ECC 算法。

### 散列算法

散列算法应该是最常见到的密码学算法了。大量的应用都在使用 MD5 或者 SHA 算法计算一个唯一的 id。比如 Git 中的提交记录、文件的完整性校验、各种语言中字典或者 Map 的实现等等。很多场景下，我们使用散列算法并不是为了满足什么加密需求，而是利用它可以对任意长度的输入，计算出一个定长的 id。

作为密码学的算法，散列算法除了提供唯一的 id，其更大的利用价值还在于它的不可逆性。除了不可逆性，在密码学上，我们对散列算法的要求还有：鲁棒性（同样的消息生成同样的摘要）、唯一性（不存在两个不同的消息，能生成同样的摘要）。

经典的散列算法包括 MD5、SHA、国密 SM3。

**MD5（消息摘要算法，Message-Digest Algorithm 5）。**

MD5 可以用来生成一个 128 位的消息摘要，它是目前应用比较普遍的散列算法。虽然，因为算法的缺陷，它的唯一性已经被破解了，但是大部分场景下，这并不会构成安全问题。但是，如果不是长度受限（32 个字符），我还是不推荐你继续使用 MD5 的。

**SHA（安全散列算法，Secure Hash Algorithm）。**

SHA 是美国开发的政府标准散列算法，分为 SHA-1 和 SHA-2 两个版本，SHA-2 细分的版本我们就不介绍了。和 MD5 相同，虽然 SHA 的唯一性也被破解了，但是这也不会构成大的安全问题。目前，SHA-256 普遍被认为是相对安全的散列算法，也是我最推荐你使用的散列算法。

**国密 SM3（SM3 Cryptographic Algorithm）。**

国密算法 SM3 是一种散列算法。其属于国家标准，算法公开，加密强度和国际标准的 SHA-256 相当。和国密 SM2 一样，它的优势也在于国家的支持和认可。

![7][7]

另外，我们在使用散列算法的时候，有一点需要注意一下，一定要注意加“盐”。所谓“盐”，就是一串随机的字符，是可以公开的。将用户的密码“盐”进行拼接后，再进行散列计算，这样，即使两个用户设置了相同的密码，也会拥有不同的散列值。同时，黑客往往会提前计算一个彩虹表来提升暴力破解散列值的效率，而我们能够通过加“盐”进行对抗，黑客需要为每个盐值计算一个彩虹表(为每一个用户建立一张彩虹表，而建表的过程，其实就和暴力破解的效果一样了)。“盐”值越长，安全性就越高。

**小结**

总的来说，在使用的时候，你要记住下面这些内容：对称加密具备较高的安全性和性能，要优先考虑。在一对多的场景中（如多人登录服务器），存在密钥分发难题的时候，我们要使用非对称加密；不需要可逆计算的时候（如存储密码），我们就使用散列算法。

在具体算法的选取上，你只需要记住：对称加密用 AES-CTR、非对称加密用 ECC、散列算法用 SHA256 加盐。这些算法就能够满足大部分的使用场景了，并且在未来很长一段时间内，都可以保持一个较高的安全强度。

如果使用https协议，用户在密码输入时，是否还需要在前端（通过JS）进行散列加密？

https可以保证传输过程中不被窃听。但最好还是对密码作散列，因为你同样需要保证服务端的密码不被泄露。最简单的，明文传输的话，你如何保证开发人员不会监守自盗？

## 身份认证

### 身份认证包括哪些东西？

首先，身份认证不仅仅是一个输入账号密码的登录页面而已，应用的各个部分都需要涉及身份认证。身份认证可以分为两个部分：对外认证和对内认证。

对外认证，其实就是应用的登录注册模块，它面向用户进行认证。对外认证的入口比较集中，一个应用通常只有一个登录入口。因此，我们可以在登录这个功能上，实现很多种认证的方式。这就可以用到我们之前提到的“你知道什么、你拥有什么、你是什么”。

除了应用本身需要有登录注册的模块，应用的各种内部系统同样需要涉及登录认证的功能，比如：服务器的登录、数据库的登录、Git 的登录、各种内部管理后台的登录等等。这也就是我所说的对内认证。

对外认证是单一场景下的认证，对内认证是多场景下的认证。

![8][8]

### 身份认证主要面临哪些威胁？

首先，没有认证环节是所有应用和公司存在的最普遍的问题。尤其是在对内认证的部分，我们经常会看到，很多公司的数据库、接口、管理后台在使用的时候，并不需要经过认证这个环节。

除了没有认证环节的直接“裸奔”，弱密码也是一个普遍存在的问题。我常常觉得，安全最大的敌人是人类的惰性。设计一个好记的强密码并不是一件简单的事情，这也是弱密码屡禁不止的原因。

说完了无认证和弱密码，接下来我们来聊一聊认证信息泄露。所谓认证信息泄露，就是指黑客通过各种手段，拿到了用户的密码信息和身份凭证这样的认证信息。常见的手段包括钓鱼、拖库等等。更可怕的是，很多攻击对于用户来说都是无感知的。

你可以在 [haveibeenpwned](https://haveibeenpwned.com) 中，输入自己的账号信息，测试一下它们是否被泄露了。如果显示“Oh no -powned!”，那就说明你的邮箱密码已经被泄露了，我建议你可以尽快修改你的密码了。

除了密码的直接泄露以外，大部分的登录系统都无法应对重放攻击。重放攻击简单来说就是，黑客在窃取到身份凭证（如 Cookie、Session ID）之后，就可以在无密码的情况下完成认证了。

总结来说，身份认证面临的威胁其实都是认证信息的泄露。这其中，既可能是应用本身就没有认证信息或者认证信息强度比较弱，使得黑客可以通过猜测的方式快速获取认证信息；也有可能是黑客通过一些攻击手段（如窃听等），从用户那获取了认证信息，从而冒充用户进行登录。

### 身份认证的安全怎么保证？

解决安全问题，不只是在解决一个技术问题，还要培养外部用户和内部员工的安全意识。

比如，对密码的强度进行限制（如强制使用字母、数字、特殊字符的组合密码，并达到一定长度），强制用户定期修改密码，对关键操作设置第二密码（如微信、支付宝的支付密码）等等。通过手机验证替代密码验证（因为丢失手机的几率比丢失密码的几率低）；通过人脸、指纹等生物特征替代密码。

除此之外，我们还可以通过加密信道（如 HTTPS）来防止窃听；也可以通过给下发的凭证设置一个有效期，来限制凭证在外暴露的时间，以此来减少重放攻击带来的影响。

这里面有一点你要注意，身份认证的最大的问题还是在于身份管理。随着公司业务的不断扩张，当账号体系变得越来越复杂时，如何对这些账号进行统一的管理，是解决身份认证问题的关键。而单点登录就是一个非常有效的解决方案。

### 单点登录如何解决身份认证问题？

单点登录（Single Sign On，SSO）到底是什么呢？单点登录的概念很简单：用户只需要进行一次认证，就可以访问所有的网页、应用和其他产品了。随着互联网产品形式的不断发展，单点登录的实现方式也经历了多次的升级革新。几种典型的单点登录方式：CAS 流程、JWT、OAuth 和 OpenID。

**CAS（Central Authentication Service，集中式认证服务）流程。**

CAS 是一个开源的单点登录框架，它不属于某一种单点登录的实现方式，而是提供了一整套完整的落地方案。

![9][9]

1. 假如用户现在要访问某个应用。比如极客时间 App。
2. 应用需要进行认证，但应用本身不具备认证功能。因此，应用将用户重定向至认证中心的页面。比如，你在登录一个应用的时候，它显示你可以选择微信、QQ、微博账号进行登录，你点击微信登录，就跳转至微信的登录页面了。
3. 用户在认证中心页面进行认证操作。如果用户之前已经在其他应用进行过认证了，那么认证中心可以直接识别用户身份，免去用户再次认证的过程。
4. 认证完成后，认证中心将认证的凭据，有时会加上用户的一些信息，一起返回给客户端。也就是你在微信登录完成后，回到了极客时间 App。
5. 客户端将凭据和其他信息发送给应用，也就是说，极客时间 App 将微信的登录凭据发送给了极客时间后端。
6. 应用收到凭据后，可以通过签名的方式，验证凭据的有效性。或者，应用也可以直接和认证中心通信，验证凭据并获取用户信息。这也就是为什么极客时间能够拿到你的微信头像了。
7. 用户完成认证。

**JWT（JSON Web Token）是一种非常轻量级的单点登录流程。**

它会在客户端保存一个凭证信息，之后在你每一次登录的请求中都带上这个凭证，将其作为登录状态的依据。JWT 的好处在于，不需要应用服务端去额外维护 Cookie 或者 Session 了。但是，正是因为它将登录状态落到了客户端，所以我们无法进行注销等操作了。

**OAuth（Open Authorization）的主要特点是授权。**

我们通常用 QQ、微信登录其他应用时所采用的协议。通过 OAuth，用户在完成了认证中心的登录之后，应用只能够验证用户确实在第三方登录了。但是，想要维持应用内的登录状态，应用还是得颁发自己的登录凭证。这也就是为什么 QQ 授权后，应用还需要绑定你的手机号码。这也就意味着，应用是基于 QQ 的信息创建了一个自身的账号。

**OpenID（Open Identity Document）和 OAuth 的功能基本一致。**

但是，OpenID 不提供授权的功能。最常见的，当我们需要在应用中使用微信支付的时候，应用只需要收集支付相关的信息即可，并不需要获取用户的微信头像。

在实际情况中，基于各种业务需求的考虑，很多公司都倾向于自己去实现一套 SSO 的认证体系，它的认证流程如下图所示：

![10][10]

在这个流程中，应用的服务器直接接收用户的认证信息，并转发给认证中心。对用户来说，这个认证中心是完全透明的。但是，这个流程给予了应用过多的信任，从安全性方面考量的话，是不合理的。在这个过程中，应用直接获取到了用户的认证信息，但应用能否保护好这些信息呢？我们并没有有效的办法去做确认。

因此，我的建议是，多花一些功夫去接入成熟的单点登录体系，而不是自己去实现一个简化版的。JWT 适用范围广，在单点登录的选取上面，如果想要将用户信息做统一管理，选择它最为简单；如果认证中心只是被用来维护账号密码，由业务去维护用户所绑定的其他手机等信息，那么，采用 OAuth 更合适。

## 访问控制

“授权”和“访问控制”其实是同一个概念，都是允许或者禁止某个用户做某件事情。现在行业内普遍用“访问控制”这个术语来讨论相关问题。

### 访问控制模型

![11][11]

如何具体的理解这个模型呢？你可以这样想：在用户去读取文件的过程中，用户是主体，读取这个操作是请求，文件是客体。

- 主体：请求的发起者。主体可以是用户，也可以是进程、应用、设备等任何发起访问请求的来源。
- 客体：请求的接收方，一般是某种资源。比如某个文件、数据库，也可以是进程、设备等接受指令的实体。
- 请求：主体对客体进行的操作。常规的是读、写和执行，也可以进一步细分为删除、追加等粒度更细的操作。

### 常见的访问控制机制

常见的访问控制机制有 4 种：DAC、role-BAC、rule-BAC、MAC。

**DAC（Discretionary Access Control，自主访问控制）。**

DAC 就是让客体的所有者来定义访问控制规则。想象一下，你想要从图书馆中拿走一本书。这个时候，管理员说，“你经过这本书的所有人同意了吗？”这个过程就是 DAC。

在 DAC 中，访问控制的规则维护完全下发到了所有者手上，管理员在理论上不需要对访问控制规则进行维护。因此，DAC 具备很高的灵活性，维护成本也很低。相对的，尽管 DAC 降低了管理员的工作难度，但是会增加整体访问控制监管的难度，以至于安全性完全取决于所有者的个人安全意识。

这么说来，DAC 的特性其实就是将安全交到了用户手中，因此，DAC 适合在面向用户的时候进行使用。当用户需要掌控自己的资源时，我们通常会采取 DAC，来完成访问控制。比方说，Linux 中采用的就是 DAC，用户可以控制自己的文件能够被谁访问。

**role-BAC（role  Based Access Control，基于角色的访问控制）。**

role-BAC 就是将主体划分为不同的角色，然后对每个角色的权限进行定义。我们还是以图书馆为例。当你想借书的时候，管理员说，“你是学生吗？”这个过程就是 role-BAC。管理员只需要定义好每一个角色所具备的功能权限，然后将用户划分到不同的角色中去，就完成了访问控制配置的过程。

role-BAC 是防止权限泛滥，实现最小特权原则的经典解决方案。试想一下，假如没有角色的概念，那么管理员需要给每一个用户都制定不同的权限方案。当用户的岗位或职责发生变更时，理论上管理员需要对这个用户的权限进行重新分配。但是，准确识别每一个用户需要哪些权限、不需要哪些权限，是一个很有挑战的工作。如果采用了 role-BAC，那么管理员只需要简单地将用户从一个角色转移到另一个角色，就可以完成权限的变更。

因此，role-BAC 更适合在管理员集中管理的时候进行使用。在这种情况下，所有的权限都由管理员进行分配和变更，所以，使用 role-BAC 可以大大降低管理员的工作难度，提高他们的工作效率。同样的原理也适用于应用，应用可以对不同的角色限定不同的操作权限，比如：运维人员给开发、产品、运维划分不同的机器操作权限。

**rule-BAC（rule Based Access Control，基于规则的访问控制）。**

rule-BAC 就是制定某种规则，将主体、请求和客体的信息结合起来进行判定。在 rule-BAC 的控制机制中，如果你想要在图书馆借书，管理员会说，“根据规定，持有阅览证就可以借书。”

相比较来说，DAC 是所有者对客体制定的访问控制策略，role-BAC 是管理员对主体制定的访问控制策略，而 rule-BAC 可以说是针对请求本身制定的访问控制策略。

在 rule-BAC 中，有一点需要我们注意。那就是，我们需要定义是“默认通过”还是“默认拒绝”，即当某次请求没有命中任何一条规则时，我们是应该让它“通过”还是“拒绝”呢？这需要根据安全的需求来进行综合考量。

比如，某个服务只提供了 80 和 443 端口的 Web 服务，那么防火墙配置的规则是允许这两个端口的请求通过。对于其他任何请求，因为没有命中规则，所以全部拒绝。这就是“默认拒绝”的策略。很多时候，为了保障更高的可用性，应用会采取“默认通过”的策略。

rule-BAC 适合在复杂场景下提供访问控制保护，因此，rule-BAC 相关的设备和技术在安全中最为常见。一个典型的例子就是防火墙。防火墙通过将请求的源 IP 和端口、目标 IP 和端口、协议等特征获取到后，根据定义好的规则，来判定是否允许主体访问。比如，限制 22 端口，以拒绝 SSH 的访问。同样地，应用也往往会采取风控系统，对用户异常行为进行判定。

**MAC（Mandatory Access Control，强制访问控制）。**

MAC 是一种基于安全级别标签的访问控制策略。只看这个定义你可能不太理解，我们还是用图书馆的例子来解释一下，当你在图书馆排队借书的时候，听到管理员说：“初中生不能借阅高中生的书籍。”这就是一种强制访问控制。在互联网中，主体和客体被划分为“秘密、私人、敏感、公开”这四个级别。MAC 要求对所有的主体和客体都打上对应的标签，然后根据标签来制定访问控制规则。

比如：为了保证机密性，MAC 不允许低级别的主体读取高级别的客体、不允许高级别的主体写入低级别的客体；为了保证完整性，MAC 不允许高级别的主体读取低级别的客体，不允许低级别的主体写入高级别的客体。这么说有些难以理解，我们可以这样来记：机密性不能低读、高写；完整性不能高读、低写。

MAC 是安全性最高的访问控制策略。但它对实施的要求也很高，需要对系统中的所有数据都进行标记。在实际工作中，想要做到这一点并不容易。每一个应用和系统，每时每刻都在不停地生产新的数据，数据也不停地在各个系统之间流转。你需要对这些行为进行全面的把控，才能将标签落地。因此，MAC 仅仅会出现在政府系统中，普通公司在没有过多的合规需求下，不会采取 MAC。

![12][12]

### 威胁评估的步骤

威胁评估主要有三个步骤：识别数据、识别攻击、识别漏洞。

我们先来看一下识别数据。我们知道，安全保护的核心资产就是数据。因此，威胁评估的第一步就是去识别数据。识别数据的最终目的是，当发生攻击，某一份数据的 CIA 受到影响时，会对公司造成多大的损失。这也是我们衡量安全投入高低的一个主要指标。

一般情况下，在识别完数据之后，我们就能推测出黑客会采取哪些方式进行攻击，这也就到了第二个步骤：识别攻击。识别攻击的核心就是，明确什么样的数据有价值被攻击。比如，对于公开的数据，没有被窃取的意义，所以黑客只会通过爬虫来抓站，而不会花费更大的成本去盗号。

在识别了数据和攻击之后，我们就需要根据应用去识别可能的漏洞了。这也就是第三个步骤：识别漏洞。比如，对于 Web 应用，它可能出现诸如 XSS、SQL 注入等 Web 漏洞。关于这一点，业内将常见的攻击和漏洞进行了总结。比如，近两年来由 MITRE 提出的ATTACK框架比较知名。在识别漏洞的时候，我们可以基于这些总结性框架去进行罗列。

通过对数据、攻击、漏洞的识别，你就能够知道，公司当前面临了哪些潜在的威胁，从而可以去思考解决方案，并推动它的落地。通常来说，我们需要定期（比如每年）对公司进行一次全面的威胁评估工作，并且随着公司的发展，不断调整安全方案。

## 脑图

![13][13]

## 参考

- 极客时间《安全攻防技能30讲》

[1]: /images/security/security-concepts/1.jpg
[2]: /images/security/security-concepts/2.jpg
[3]: /images/security/security-concepts/3.jpg
[4]: /images/security/security-concepts/4.jpg
[5]: /images/security/security-concepts/5.jpg
[6]: /images/security/security-concepts/6.jpg
[7]: /images/security/security-concepts/7.jpg
[8]: /images/security/security-concepts/8.jpg
[9]: /images/security/security-concepts/9.jpg
[10]: /images/security/security-concepts/10.jpg
[11]: /images/security/security-concepts/11.jpg
[12]: /images/security/security-concepts/12.jpg
[13]: /images/security/security-concepts/13.jpg