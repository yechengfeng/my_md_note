# JWT实战教程

## 1. 什么是JWT

JSON Web Token (JWT) is an open standard ([RFC 7519](https://tools.ietf.org/html/rfc7519)) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object. This information can be verified and trusted because it is digitally signed. JWTs can be signed using a secret (with the **HMAC** algorithm) or a public/private key pair using **RSA** or **ECDSA**.

​																																																												           ----摘自官网

```markdown
# 翻译
- 官网地址：https://jwt.io/introduction/
- 翻译：JSON Web Token(JWT)是一个开放标准(rfc7519),它定义了一种紧凑的、自包含的方式。用于在各方之间以JSON对象安全的传输信息。此信息可以验证和信任，因为它是数字签名的。JWT可以使用秘密（使用HWAC算法）或使用RSA或ECDSA的公钥/私钥对进行签名。

# 通俗解释
- JSON Web Token简称JWT,也就是通过JSON形式作为web应用中的令牌，用于在各方之间安全的将信息作为JSON对象传输。在数据传输过程中还可以完成数据加密、签名等相关处理。
```

## 2. JWT能做什么

```markdown
# 1.授权
- 这是使用JWT最常见的方案。一旦用户登录，每个后续请求都将包括JWT,从而允许用户访问该令牌允许的路由、服务和资源。单点登录是当今广泛使用JWT的一项功能，因为它的开销很小而且可以在不同的领域中轻松使用。

# 2. 信息交换
- JSON Web Token是在各方之间安全的传输信息的好方法。因为可以对JWT进行签名（例如使用公钥/私钥对），所以您可以确保发件人是他们所说的人。此外，由于签名是使用标头和有效负载计算的，因此您还可以验证内容是否遭到篡改。
```

## 3. 为什么是JWT

### 基于传统的session认证

```markdown
# 1.认证方式

- 我们知道，http协议本身是一种无状态协议，而这就意味着如果用户向我们的应用提供了用户名和密码来进行用户验证，那么下一次请求时，用户还要再一次进行用户认证才行。因为根据http协议请求，我们并不知道是哪个用户发出的请求，所以为了让我们的应用能识别是哪个用户发出的请求，我们只能在服务器存储一份用户登陆的信息，这份登录信息会在响应时传递给浏览器，告诉其保存为cookie，以便下次请求时发送给我们的应用，这样我们的应用就能识别请求来自哪个用户了，这就是传统的基于session认证。

# 暴露问题

- 1. 每个用户经过我们的应用认证之后，我们的应用都要在服务器端做一次记录，以便用户下次请求的鉴别，通常而言session都是保存在内存中，而随着认证用户的增多，服务端的开销明显会增大。

- 2. 用户认证之后，服务端做认证记录，如果认证的纪录被保存在内存中的话，这意味着用户下次请求还必须使用这台服务器，这样才能拿到授权的资源，这样在分布式的应用上，相应的限制了负载均衡的能力。这也意味着限制了应用的扩展能力。

- 3. 因为是基于cookie来进行用户识别的，cookie如果被截获，用户就会很容易收到跨站请求伪造的攻击。

- 4. 在前后端分离系统中更加头疼：
	前后端分离在应用解耦后增加了部署的复杂度，通常用户一次请求就要转发多次。如果用session每次携带sessionId到服务器，服务器还要查询用户携带信息。同时如果用户很多，这些用户信息都要存储下服务器的内存中，会给服务器增加负担。还有CSRF（跨站伪造请求攻击）攻击，session是基于cookie进行用户识别的，cookie如果被截获，用户很容易收到攻击。还有就是sessionId是一个特征值，表达的信息不够丰富，不易于扩展。如果服务端是多节点部署，那么就需要实现session共享机制，不方便集群应用。
```

### 基于JWT认证

```markdown
# 1. 认证流程

- 首先，前端通过Web表单将自己的用户名和密码发送到后端的接口。这一过程一般是HTTP POST请求。建议的方式是通过SSL加密的传输（https协议），从而避免敏感信息被嗅探。

- 后端核对用户名和密码成功后，将用户的id等其他信息作为JWT Payload(负载)，将其与头部分分别进行Base64编码拼接后签名，形成一个JWT(Token)。形成的JWT就是一个形同lll.zzz.xxx的字符串

- 后端将JWT字符串作为登录的返回结果返回给前端。前端可以将返回的结果保存在localStorage或sessionStorage上，退出登录时前端删除保存到JWT即可。

- 前端在每次请求时将JWT放入Http Header中的Authorization位置。（解决XSS和XSRF问题）

- 后端检查是否存在，如存在，验证JWT的有效性。例如：检查签名是否正确；检查token是否过期；检查token的接收方式是否是自己。

- 验证通过后后端使用JWT中包含的用户信息进行其他逻辑操作，返回结果。


# 2. JWT优势

- 简洁(Compact)：可以通过URL POST参数或者HTTP header发送，因为数据量小传输的速度也很快

- 自包含(self-contained)：负载中包含了所有用户所需要的信息，避免了多次查询数据库

- 因为Token是以JSON加密的形式保存在客户端的，所以JWT是跨语言的，原则上任何web形式都可以

- 不需要在服务器保存会话信息，特别适用于分布式微服务
```

## 4. JWT的结构是什么

```markdown
token   String   →   header.payload.signature
# 1.令牌组成
- 1> 标头（header）
- 2> 有效载荷（Payload）
- 3> 签名（Signature）
- 因此，JWT通常如下所示：xxxxx.yyyyy.zzzzz	header.payload.signature
```

```markdown
# 2.Header
- 标头通常由两部分组成：令牌的类型（即JWT）和所使用的签名算法，例如HMAC SHA256或RSA。它会使用Base64编码组成JWT结构的第一部分。

- 注意：Base64是一种编码，也就是说，它可以被翻译回原来的样子的。它并不是一种加密过程。
```

```json
{
    "alg": "HS256",
    "typ": "JWT"
}
```

```markdown
# 3.Payload
- 令牌的第二部分是有效负载，其中包含声明。声明是有关实体（通常是用户）和其他数据的声明。同样的，它会使用Base64编码组成JWT结构的第二部分
```

