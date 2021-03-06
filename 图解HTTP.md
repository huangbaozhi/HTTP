# 图解HTTP

## 第一章：了解Web及网络基础

### 使用HTTP协议访问Web

- 客户端（client）：通过发送请求获取服务器资源的Web浏览器等。
- 子主题 2

### HTTP的诞生

- 万维网：WWW （World Wide Web)
- 统一资源定位符：指定文档所在地址的URL（uniform Resource Locator）
- Web：WWW名称，是Web浏览当年用来浏览超文本的客户端应用程时的名称。现在则用来表示这一系列的集合，也可简称为Web。

### 网络基础TCP/IP

- TCP/IP协议族

	- 协议（protocol）：计算机与网络设备要相互通信，双方就必须基于相同的方法。
	- TCP/IP：把与互联网相关连的协议集合起来。

- TCP/IP的分层管理

	- 应用层

		- 决定向用户提供应用服务时通信的活动。
		- 应用服务：FTP（文件传输协议）和DNS（域名系统）
		- HTTP协议也处在该层

	- 传输层

		- 传输层对上层应用层，提供处于网络连接中的两台计算机之间的数据传输。
		- TCP（传输控制协议）和UDP（用户数据报协议）在该层。

	- 网络层（又名网络互连层）

		- 用来处理在网络上流的数据报。数据报时网络传输的最小数据单位。

	- 链路层（又名数据链路层，网络接口层）

		- 用来处理连接网络的硬件部分。

			- 控制操作系统
			- 硬件的设备驱动
			- NIC（网络适配器，即网卡）

- TCP/IP通信传输流

	- TCP/IP通信传输流

### 与HTTP关系密切的协议：IP、TCP和DNS

- 负责传输的IP协议

	- 按层次分，IP（Internet Protocol）网际协议位于网络层。
	- IP协议作用时把各种数据报传送给对方。
	- IP地址指明了节点被分配到的地址，MAC地址（Media Access Control Address）指网卡所属的固定地址。
	- 局域网（LAN）
	- ARP协议（Address Resolution Protocol）:ARP是一种用以解析地址的协议，根据通信方的IP地址就可以反查出对应的MAC地址。

- TCP协议

	- TCP位于传输层，提供可靠的字节流服务。

		- 字节流服务（Byte Stream Service)，是指为了方便传输，将大块数据分割成以报文段（segment）为单位的数据包进行管理。

	- TCP协议采用三次握手（three-way handshaking）策略。

### 负责域名解析的DNS服务

- DNS（Domain Name System)服务是和HTTP协议一样位于应用层的协议。它们提供域名到IP地址之间的解析服务。
- DNS协议提供通过域名查找IP地址，或逆向从IP地址饭查域名的服务。

### URI和URL

- URI（Uniform Resource Identifier，统一资源标识符）
- URL（Uniform Resource Locator，统一资源定位符。URL正是使用Web浏览器等访问Web页面时需要输入的网页地址。
- 服务器地址：使用绝对URI必须指定待访问的服务器地址。
- 服务器端口号：指定服务器连接的网络端口号
- 带层次的文件路径：指定服务器上的文件路径来定位待指的资源。
- 查询字符串：针对已制定的文件路径内的资源，可以使用查询字符串传入任意参数。
- 片段表示符：使用片段表示符通常可标记出以获取资源中的子资源（文档内的某个位置）

## 第二章：简单的HTTP协议

### HTTP协议用于客户端和服务器之间的通信

- HTTP协议用于客户端和服务器之间的通信。
- 客户端：请求访问文本或图像等资源的一端。
- 服务端：提供资源响应的一端。

### HTTP是不保存状态的协议（即无状态协议）

### 请求URI定位资源

### 告知服务器意图的HTTP方法

- GET：获取资源

	- GET方法用来请求访问已被URI识别的资源。

- POST：传输实体主体

	- 目的:不是获取响应的主体内容。

- PUT：传输文件
- HEAD：获得报文首部
- DELETE：删除文件
- OPTIONS：询问支持的方法

	- 用来查询针对请求URI指定的资源。

- TRACE：追踪路径

	- TRACE方法是让Web服务器端将之前的请求通信环回给客户端的方法。

		- XST（Cross-Site Tracing，跨站追踪）

- CONNECT：要求用隧道协议连接代理

	- CONNECT方法要求在与代理服务器通信时建立隧道，实现用隧道协议进行TCP通信。主要使用SSL（Secure Sockets Layer，安全套接层）和TLS（Transport Layer Swcurity，传输层安全）协议把通信内容加密后经网络隧道传输。

		- CONNECT方法的格式

			- CONNECT代理服务器名：端口号HTTP版本

## 第三章：HTTP报文内的HTTP信息

### HTTP报文

- HTTP报文：用于HTTP协议交互的信息。
- 请求报文：请求端（客户端）的HTTP报文
- 响应报文：响应端（服务器端）

### 请求报文及响应报文的结构

- 请求行
- 状态行
- 首部字段
- 其他：可能包含HTTP的RFC里未定义的首部（Cookie等）。

### 编码提升传输速率

- HTTP在传输数据时可以按照数据原貌直接传输，但也可以在传输过程中通过编码提升传输速率。通过传输时编码，能有效的处理大量的访问请求。
- 报文主体和实体主体的差异

	- 报文（message)：是HTTP通信中的基本单位，由8位字节流（octet sequence，其中octet为8个比特）组成，通过HTTP通信传输。
	- 实体（entity)：作为请求或响应的有效载荷数据（补充项）被传输，其内容由实体首部和实体主体组成。

		- HTTP报文的主体用于传输请求或响应的实体主题。

	- 压缩传输的内容编码

		- 内容编码指明应用在实体内容上的编码格式，并保持信息原样压缩。内容编码后的实体由客户端接收并负责解码，

			- 常用的内容编码

				- gzip(GNU zip)
				- compress(UNIX系列的标准压缩）
				- deflate（zlib)
				- identity(不进行编码）

	- 分割发送的分块传输编码

		- 分块传输编码（Chunked Transfer Coding）

### 发送多种数据的多部份对象集合

- MIME（Multipurpose Internet Mail Extendions，多种途因特网邮件扩展）机制，它允许右键处理文本、图片、视频等多个不同类型的数据。
- 在MIME扩展中会使用一种称为多部分对象集合（Multipart）的方法，来容纳多份不同类型的数据。
- 内容协商（Content Negotiation）：当浏览器的默认语言为英语或中文，访问相同URI的Web页面时，则会显示对应的英语拌和中文版的Web页面。

	- 内容协商机制：是指客户端和服务器端就响应的资源内容进行交涉，然后提供给客户端最为适合的资源。内容协商会以响应资源的语言、字符集、编码方式等作为判断的基准。

		- Accept
		- Accept-Charset
		- Accept-Encoding
		- Accept-Language
		- Content-Language

- multiparty/form-data：在Web表单文件上传时使用。
- multipart/byteranges：状态码206（Partial Content，部分内容）响应报文包含了多个范围的内容时使用。

### 获取部分内容的范围请求

- 范围请求（Range Request)：指定范围发送的请求。

### 内容协商返回最合适的内容

- 内容协商技术的三种类型

	- 服务器驱动协商（Server-driven Negotiation）
	- 客户端驱动协商（Agent-driven Negotiation)
	- 透明协商（Transparent Negotiation）

## 第四章：返回结果的HTTP状态码

### 状态码告知从服务器端返回的请求结果

- WebDAV（Web-based Distributed Authoting and Versioning,基于万维网的分布式创作和版本控制）

### 2XX成功

- 2XX的响应结果表明请求被正常处理了。
- 200 OK

	- 表示从客户端发来的请求在服务器端被正常处理了。

- 206 Partial Content

	- 该状态码表示客户端进行了范围请求，而服务器成功执行了这部分的GET请求。

### 3XX重定向

- 3XX响应结果表明浏览器需要执行某些特殊的处理以正确处理请求。
- 301 Moved Permanently

	- 永久性重定向
	- 该状态码表示请求的资源已被分配了新的URI，以后应使用资源现在所指的URI。

- 302 Found

	- 临时性重定向
	- 该状态码表示请求的资源已被分配了新的URI，希望用户（本次）能使用新的URI访问。

- 303 See Other

	- 该状态码表示由于请求对应的资源存在着另一个URI，应使用GET方法定向获取请求的资源。

- 304 Not Modified

	- 该状态码表示客户端发送附带条件的请求时，服务器端允许请求访问资源，但因发生请求未满足条件的情况后，直接返回304 Not Modified（服务器端资源为改变，可直接使用客户端未过期的缓存）。

- 307 Temporary Redirect

	- 临时重定向

### 4XX客户端错误

- 4XX的响应结果表明客户端是发生错误的原因所在。
- 400 Bad Request

	- 该状态码表示请求报文中存在语法错误。当错误发生时，需修改请求的内容后再次发送请求。

- 401 Unauthorized

	- 该状态码表示发送的请求需要由通过HTTP认证（BASIC认证、DIGEST认证）的认证信息。

- 403 Forbidden

	- 该状态码表明对请求资源的访问被服务器拒绝了。

- 404 Not Found

	- 该状态码表明服务器上无法找到请求的资源。

### 5XX服务器错误

- 5XX的响应结果表明服务器本身发生错误。
- 500 Internal Server Errot

	- 该状态码表明服务器端在执行请求时发生了错误。

- 503 Service Unavailable

	- 该状态码表明服务器暂时处于超负荷或正在进行停机维护，现在无法处理请求。

## 第五章：与HTTP协作的Web服务器

### 用单台虚拟主机实现多个域名

- HTTP/1.1规范允许一台HTTP服务器搭建多个Web站点。
- 虚拟主机（Virtual Host，又称虚拟服务器）
- 在互联网上，域名通过DNS服务映射到IP地址（域名解析）之后访问目标网站。
- 在相同的IP地址下，由虚拟主机可以寄存多个不同主机名和域名的Web网站，因此在发生HTTP请求时，必须在Host首部内完整指定主机或域名的URI。

### 通信数据转发程序：代理、网关、隧道

- 代理

	- 代理是一种有转发功能的应用程序，它扮演了位于服务器和客户端“中间人”的角色，接受由客户端发送的请求并转发给服务器，同时也接受服务器返回的响应并转发给客户端。
	- 代理服务器的基本行为：接受客户端发送的请求后转发给其他服务器。
	- 源服务器：持有资源实体的服务器。
	- 使用代理服务器的理由

		- 利用缓存技术减少网络带宽的流量，组织内部针对特定网站的访问控制，以获取访问日志为主要目的。
		- 缓存代理（Caching Proxy)

			- 代理转发响应时，缓存代理会预先将资源的副本（缓存）保存在代理服务器上。
			- 当代理再次接受到对相同资源的请求时，就可以不从源服务器哪里获取资源，二十将之前缓存的资源作为响应返回。

		- 透明代理（Transparent Proxy)

			- 转发请求或响应时，不对报文做任何加工的代理类型被称为透明代理。反之，对报文内容进行加工的代理被称为非透明代理。

- 网关

	- 网关时转发其他服务器通信数据的服务器，结束从客户端发送来的请求时，它就像自己拥有资源的源服务器一样对请求进行处理。
	- 网关能使同行线路上的服务器提供非HTTP协议服务。

- 隧道

	- 隧道时在相隔甚远的客户端和服务器两者之间进行中转，并保持双方通信连接的应用程序。
	- 目的：确保客户端能与服务器进行安全的通信。

### 保存资源的缓存

- 缓存时指代理服务器或客户端本地磁盘内保存的资源副本。利用缓存可减少对源服务器的访问，因此也就节省了同行流的和通信时间。
- 缓存的有效期限
- 客户端的缓存

	- 把客户端缓存称为临时网络文件（Temporary Internet File）。

### 在HTTP出现之前的协议

- FTP（File Transfer Protocol)

	- 传输文件时使用的协议。

- NNTP（Network News Transfer Protocol)

	- 用于NetNews电子会议室内传送消息的协议。

- Archie

	- 搜索anonymous FTP公开的文件信息的协议。

- WAIS（Wide Area Information Servers）

	- 以关键词检索多个数据库使用的协议。

- Gopher

	- 查找与互联网连接的计算机内信息的协议。

## 第六章：HTTP首部

### HTTP报文首部

- HTTP协议的请求和响应报文中必定包含HTTP首部。

	- 首部内容为客户端和服务器分别处理请求和响应剔红所需要的信息。

- HTTP请求报文

	- 在请求中，HTTP报文有方法、URI、HTTP版本、HTTP首部字段等部分构成。

- HTTP响应报文

	- 在响应中，HTTP报文由HTTP版本、状态码（数字和原因短语）、HTTP首部字段3部分构成。

### HTTP首部字段

- HTTP首部字段传递重要信息
- HTTP首部字段结构

	- HTTP首部字段是由首部字段名和字段值构成的。

- HTTP首部中以Content-Type这个字段来表示报文主题的对象类型。
- 4中HTTP首部字段类型

	- 通用首部字段（General Header Fields）
	- 请求首部字段（Request Header Fields）
	- 响应首部字段（Response Header Fields）
	- 实体首部字段（Entity Header Fields）

### HTTP/1.1 通用首部字段

- 通用首部字段是指，请求报文的响应报文双方都会使用的首部。
- Cache-Control

	- 缓存请求指令
	- 缓存响应指令
	- public指令

		- 当指定public指令时，则明确表明其他用户也可以利用缓存。

	- private指令

		- 当指定private指令后，响应只以特定用户作为对象。

	- no-cache指令

		- 使用no-cache指令的目的是为了防止从缓存中返回过期的资源。

## 第七章：确保Web安全的HTTPS

### HTTP的缺点

- 通信使用明文（不加密），内容可能会被窃听
- 不验证通信方的身份，因此，有可能遭遇伪装
- 无法证明报文的完整性，所以有可能一早篡改
- 通信使用明文肯会被窃听

	- TCP/IP是肯被窃听的网络
	- 加密处理防止被窃听

		- 通信的加密

			- HTTP协议中没有加密机制，但可以通过和SSL（Secure Socket Layer，安全套阶层）或TLS（Transport Layer Security，安全传输层协议）的组合使用，加密HTTP的通信内容。
			- 与SSL组合使用的HTTO被称为HTTPS（HTTP Secure，超文本传输安全协议）或HTTP over SSL。

		- 内容加密

			- 对HTTP报文里所含的内容进行加密处理。

### HTTP+加密+认证+完整性保护=HTTPS

- 添加了加密及认证机制的HTTP称为HTTPS（HTTP Secure)。
- HTTPS是身被SSL外壳的HTTP

	- SSL是独立与HTTP的协议，处理HTTP协议，其他运行在英寸层的SMTP和Telnet等协议均可配合SSL的协议使用。

- 加密和解密同用一个密钥的方式称为共享密钥（Common key crypto system），也被叫做对称密钥加密。

## 第八章：确认访问用户身份的认证

### 何为认证

- 密码：只有本人才会知道的字符串信息。
- 动态令牌：仅限本人持有的设备内显示的一次性密码。
- 数字证书：仅限本人（终端）持有的信息。
- 生物认证：指纹和虹膜等本人的生理信息。
- IC卡等：仅限本人持有的信息。
- HTTP使用的认证方式

	- BASIC认证（基本认证）
	- DIGEST认证（摘要认证）
	- SSL客户端认证
	- FormBase认证（基于表单认证）

### BASIC认证

- Web服务器与通信客户端之间进行认证方式。

### DIGEST认证

### SSL客户端认证

- SSL客户端是借由HTTPS的客户端证书完成认证的方式。

### 基于表单认证

- 客户端回想服务器上的Web应用程序发送登录信息（Credential），按登录信息的验证结果认证。

## 第九章：基于HTTP的功能追加协议

## 第十章：构建Web内容计术

### HTML

- HTML（HyperText Markup Language，超文本标记语言）
- CSS（Casading Style Sheets，层叠样式表）

### 动态HTML(Dynamic HTML）：使用客户端脚本语言将静态的HTML内容编程动态的技术的总称。

### Web应用

- CGI（通过网关接口）：Web服务器在接受到客户端发送过来的请求后转发给程序的一组机制。

### XML（可扩展标记语言）：一种可按应用目标进行扩展的通用标记语言。

### JSON（javaScript Object Notation)：一种以javaScript（ECMAScript)的对象表示为基础的基础级数据标记语言。

## 第十一章：Web的攻击技术

### Web的攻击技术

- 攻击目标：应用HTTP协议的服务器和客户端，以及运行在服务器上的Web应用等资源。
- 主动攻击（active attack）是指攻击者通过直接访问Web应用，把攻击代码传入攻击模式。

	- 主动攻击模式具有代表性的攻击是SQL注入攻击和OS命令注入攻击。

- 以服务器为目标的被动攻击

	- 被动攻击（passive attack）是指利用圈套策略执行攻击代码的攻击模式。

### 应输出值转义不完全引发安全漏洞

- 客户验证
- Web应用端（服务器）的验证
- 跨站脚本攻击（Cross-Site Scripting,XSS)：通过存在安全露铜的Web网站注册用户的浏览器内运行非法的HTML标签或JavaScript进行的一种攻击。
- SQL注入攻击

### 应设置或设计上的缺陷引发的安全漏洞

- 强制浏览（Forced Browding）安全漏洞：从安置在Web服务器的公开目录下的文件中，浏览哪些原本非自愿公开的文件。



