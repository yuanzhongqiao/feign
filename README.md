<div class="Box-sc-g0xbh4-0 bJMeLZ js-snippet-clipboard-copy-unpositioned" data-hpc="true"><article class="markdown-body entry-content container-lg" itemprop="text"><div class="markdown-heading" dir="auto"><h1 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Feign 简化了编写 Java HTTP 客户端的过程</font></font></h1><a id="user-content-feign-simplifies-the-process-of-writing-java-http-clients" class="anchor" aria-label="永久链接：Feign 简化了编写 Java HTTP 客户端的过程" href="#feign-simplifies-the-process-of-writing-java-http-clients"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><a href="https://gitter.im/OpenFeign/feign?utm_source=badge&amp;utm_medium=badge&amp;utm_campaign=pr-badge&amp;utm_content=badge" rel="nofollow"><img src="https://camo.githubusercontent.com/2da7039d862cabe847953554272000b86e80b158a0723c9a832720b935df3f43/68747470733a2f2f6261646765732e6769747465722e696d2f4a6f696e253230436861742e737667" alt="加入聊天：https://gitter.im/OpenFeign/feign" data-canonical-src="https://badges.gitter.im/Join%20Chat.svg" style="max-width: 100%;"></a>
<a href="https://circleci.com/gh/OpenFeign/feign/tree/master" rel="nofollow"><img src="https://camo.githubusercontent.com/1e74038a186bedc8ced19bda3c36c7a2c0716c52f965de53b4773534bae82c41/68747470733a2f2f636972636c6563692e636f6d2f67682f4f70656e466569676e2f666569676e2f747265652f6d61737465722e7376673f7374796c653d737667" alt="循环CI" data-canonical-src="https://circleci.com/gh/OpenFeign/feign/tree/master.svg?style=svg" style="max-width: 100%;"></a>
<a href="https://search.maven.org/artifact/io.github.openfeign/feign-core/" rel="nofollow"><img src="https://camo.githubusercontent.com/c2a3a10442200e29c429836cadee089bceb0277bd9561ddaf49881cecafae77c/68747470733a2f2f6d6176656e2d6261646765732e6865726f6b756170702e636f6d2f6d6176656e2d63656e7472616c2f696f2e6769746875622e6f70656e666569676e2f666569676e2d636f72652f62616467652e706e67" alt="梅文中心" data-canonical-src="https://maven-badges.herokuapp.com/maven-central/io.github.openfeign/feign-core/badge.png" style="max-width: 100%;"></a></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Feign 是一个 Java 到 HTTP 客户端绑定器，其灵感来自于</font></font><a href="https://github.com/square/retrofit"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Retrofit</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">、</font></font><a href="https://jax-rs-spec.java.net/nonav/2.0/apidocs/index.html" rel="nofollow"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">JAXRS-2.0</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">和</font></font><a href="http://www.oracle.com/technetwork/articles/java/jsr356-1937161.html" rel="nofollow"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">WebSocket</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">。 Feign 的第一个目标是降低将</font></font><a href="https://github.com/Netflix/Denominator"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Denominator</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">统一绑定到 HTTP API 的复杂性，</font><font style="vertical-align: inherit;">而不管</font></font><a href="http://www.slideshare.net/adrianfcole/99problems" rel="nofollow"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">ReSTativity</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">如何。</font></font></p>
<hr>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">为什么是 Feign 而不是 X？</font></font></h3><a id="user-content-why-feign-and-not-x" class="anchor" aria-label="永久链接：为什么是 Feign 而不是 X？" href="#why-feign-and-not-x"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Feign 使用 Jersey 和 CXF 等工具为 ReST 或 SOAP 服务编写 Java 客户端。此外，Feign 允许您在 Apache HC 等 http 库之上编写自己的代码。 Feign 以最小的开销将您的代码连接到 http API，并且通过可自定义的解码器和错误处理来编写代码，这些代码可以写入任何基于文本的 http API。</font></font></p>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Feign 是如何工作的？</font></font></h3><a id="user-content-how-does-feign-work" class="anchor" aria-label="永久链接：Feign 是如何工作的？" href="#how-does-feign-work"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Feign 的工作原理是将注释处理为模板化请求。在输出之前，参数会以简单的方式应用于这些模板。尽管 Feign 仅限于支持基于文本的 API，但它极大地简化了系统方面，例如重放请求。此外，知道这一点后，Feign 可以轻松地对您的转换进行单元测试。</font></font></p>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Java版本兼容性</font></font></h3><a id="user-content-java-version-compatibility" class="anchor" aria-label="永久链接：Java 版本兼容性" href="#java-version-compatibility"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Feign 10.x 及更高版本基于 Java 8 构建，应该适用于 Java 9、10 和 11。对于需要 JDK 6 兼容性的用户，请使用 Feign 9.x</font></font></p>
<div class="markdown-heading" dir="auto"><h2 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">功能概述</font></font></h2><a id="user-content-feature-overview" class="anchor" aria-label="永久链接：功能概述" href="#feature-overview"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">这是 feign 提供的当前主要功能的地图：</font></font></p>
<p dir="auto"><a target="_blank" rel="noopener noreferrer nofollow" href="https://camo.githubusercontent.com/4922a4bb1cb17e62acdd037870cdf5f3c355f20adadc60fbd6f619b1a00cf0d9/687474703a2f2f7777772e706c616e74756d6c2e636f6d2f706c616e74756d6c2f70726f78793f63616368653d6e6f267372633d68747470733a2f2f7261772e67697468756275736572636f6e74656e742e636f6d2f4f70656e466569676e2f666569676e2f6d61737465722f7372632f646f63732f6f766572766965772d6d696e646d61702e69756d6c"><img src="https://camo.githubusercontent.com/4922a4bb1cb17e62acdd037870cdf5f3c355f20adadc60fbd6f619b1a00cf0d9/687474703a2f2f7777772e706c616e74756d6c2e636f6d2f706c616e74756d6c2f70726f78793f63616368653d6e6f267372633d68747470733a2f2f7261772e67697468756275736572636f6e74656e742e636f6d2f4f70656e466569676e2f666569676e2f6d61737465722f7372632f646f63732f6f766572766965772d6d696e646d61702e69756d6c" alt="思维导图概述" data-canonical-src="http://www.plantuml.com/plantuml/proxy?cache=no&amp;src=https://raw.githubusercontent.com/OpenFeign/feign/master/src/docs/overview-mindmap.iuml" style="max-width: 100%;"></a></p>
<div class="markdown-heading" dir="auto"><h1 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">路线图</font></font></h1><a id="user-content-roadmap" class="anchor" aria-label="永久链接：路线图" href="#roadmap"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<div class="markdown-heading" dir="auto"><h2 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Feign 11 及更高版本</font></font></h2><a id="user-content-feign-11-and-beyond" class="anchor" aria-label="永久链接：Feign 11 及更高版本" href="#feign-11-and-beyond"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">让</font></font><em><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">API</font></font></em><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">客户端更轻松</font></font></p>
<div class="markdown-heading" dir="auto"><h2 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">短期——我们现在正在做的事情。 ⏰</font></font></h2><a id="user-content-short-term---what-were-working-on-now-" class="anchor" aria-label="永久链接：短期 - 我们现在正在做的事情。 ⏰" href="#short-term---what-were-working-on-now-"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<ul dir="auto">
<li><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">响应缓存
</font></font><ul dir="auto">
<li><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">支持缓存 api 响应。允许用户定义在什么条件下响应适合缓存以及应使用什么类型的缓存机制。</font></font></li>
<li><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">支持内存缓存和外部缓存实现（EhCache、Google、Spring 等...）</font></font></li>
</ul>
</li>
<li><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">完整的 URI 模板表达式支持
</font></font><ul dir="auto">
<li><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">支持</font></font><a href="https://tools.ietf.org/html/rfc6570#section-1.2" rel="nofollow"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">级别 1 到级别 4</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;"> URI 模板表达式。</font></font></li>
<li><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">使用</font></font><a href="https://github.com/uri-templates/uritemplate-test"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">URI 模板 TCK</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">来验证合规性。</font></font></li>
</ul>
</li>
<li><code>Logger</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">API重构
</font></font><ul dir="auto">
<li><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">重构</font></font><code>Logger</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">API 以更接近 SLF4J 等框架，为 Feign 中的日志记录提供通用的思维模型。 Feign 本身将自始至终使用该模型，并为如何</font></font><code>Logger</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">使用提供更清晰的方向。</font></font></li>
</ul>
</li>
<li><code>Retry</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">API重构
</font></font><ul dir="auto">
<li><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">重构</font></font><code>Retry</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">API 以支持用户提供的条件并更好地控制回退策略。</font></font><strong><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">这可能会导致不向后兼容的重大更改</font></font></strong></li>
</ul>
</li>
</ul>
<div class="markdown-heading" dir="auto"><h2 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">中期 - 接下来会发生什么。 ⏲</font></font></h2><a id="user-content-medium-term---whats-up-next-" class="anchor" aria-label="永久链接：中期 - 接下来会发生什么。 ⏲" href="#medium-term---whats-up-next-"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<ul dir="auto">
<li><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">异步执行支持通过</font></font><code>CompletableFuture</code>
<ul dir="auto">
<li><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">允许</font></font><code>Future</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">请求/响应生命周期的链接和执行器管理。  </font></font><strong><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">实施将需要非向后兼容的重大更改</font></font></strong><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">。然而，在考虑响应式执行之前，需要此功能。</font></font></li>
</ul>
</li>
<li><font style="vertical-align: inherit;"><a href="https://www.reactive-streams.org/" rel="nofollow"><font style="vertical-align: inherit;">通过反应流的</font></a><font style="vertical-align: inherit;">反应执行支持</font></font><a href="https://www.reactive-streams.org/" rel="nofollow"><font style="vertical-align: inherit;"></font></a>
<ul dir="auto">
<li><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">对于 JDK 9+，请考虑使用</font></font><code>java.util.concurrent.Flow</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">.</font></font></li>
<li><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">支持</font><font style="vertical-align: inherit;">JDK 8 上的</font></font><a href="https://projectreactor.io/" rel="nofollow"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Project Reactor</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">和</font></font><a href="https://github.com/ReactiveX/RxJava"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">RxJava 2+实现。</font></font></a><font style="vertical-align: inherit;"></font></li>
</ul>
</li>
</ul>
<div class="markdown-heading" dir="auto"><h2 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">长期 - 未来☁️</font></font></h2><a id="user-content-long-term---the-future-️" class="anchor" aria-label="永久链接：长期 - 未来 ☁️" href="#long-term---the-future-️"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<ul dir="auto">
<li><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">额外的断路器支持。
</font></font><ul dir="auto">
<li><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">支持其他断路器实现，例如</font></font><a href="https://resilience4j.readme.io/" rel="nofollow"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Resilience4J</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">和 Spring Circuit Breaker</font></font></li>
</ul>
</li>
</ul>
<hr>
<div class="markdown-heading" dir="auto"><h1 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">用法</font></font></h1><a id="user-content-usage" class="anchor" aria-label="永久链接：用法" href="#usage"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">feign 库可从</font></font><a href="https://central.sonatype.com/artifact/io.github.openfeign/feign-core" rel="nofollow"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Maven Central</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">获取。</font></font></p>
<div class="highlight highlight-text-xml notranslate position-relative overflow-auto" dir="auto"><pre>&lt;<span class="pl-ent">dependency</span>&gt;
    &lt;<span class="pl-ent">groupId</span>&gt;io.github.openfeign&lt;/<span class="pl-ent">groupId</span>&gt;
    &lt;<span class="pl-ent">artifactId</span>&gt;feign-core&lt;/<span class="pl-ent">artifactId</span>&gt;
    &lt;<span class="pl-ent">version</span>&gt;??feign.version??&lt;/<span class="pl-ent">version</span>&gt;
&lt;/<span class="pl-ent">dependency</span>&gt;</pre><div class="zeroclipboard-container">
   
  </div></div>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">基本</font></font></h3><a id="user-content-basics" class="anchor" aria-label="永久链接：基础知识" href="#basics"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">用法通常如下所示，是</font></font><a href="https://github.com/square/retrofit/blob/master/samples/src/main/java/com/example/retrofit/SimpleService.java"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">规范 Retrofit 示例</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">的改编版。</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">interface</span> <span class="pl-smi">GitHub</span> {
  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"GET /repos/{owner}/{repo}/contributors"</span>)
  <span class="pl-smi">List</span>&lt;<span class="pl-smi">Contributor</span>&gt; <span class="pl-en">contributors</span>(<span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"owner"</span>) <span class="pl-smi">String</span> <span class="pl-s1">owner</span>, <span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"repo"</span>) <span class="pl-smi">String</span> <span class="pl-s1">repo</span>);

  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"POST /repos/{owner}/{repo}/issues"</span>)
  <span class="pl-smi">void</span> <span class="pl-en">createIssue</span>(<span class="pl-smi">Issue</span> <span class="pl-s1">issue</span>, <span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"owner"</span>) <span class="pl-smi">String</span> <span class="pl-s1">owner</span>, <span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"repo"</span>) <span class="pl-smi">String</span> <span class="pl-s1">repo</span>);

}

<span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-k">class</span> <span class="pl-smi">Contributor</span> {
  <span class="pl-smi">String</span> <span class="pl-s1">login</span>;
  <span class="pl-smi">int</span> <span class="pl-s1">contributions</span>;
}

<span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-k">class</span> <span class="pl-smi">Issue</span> {
  <span class="pl-smi">String</span> <span class="pl-s1">title</span>;
  <span class="pl-smi">String</span> <span class="pl-s1">body</span>;
  <span class="pl-smi">List</span>&lt;<span class="pl-smi">String</span>&gt; <span class="pl-s1">assignees</span>;
  <span class="pl-smi">int</span> <span class="pl-s1">milestone</span>;
  <span class="pl-smi">List</span>&lt;<span class="pl-smi">String</span>&gt; <span class="pl-s1">labels</span>;
}

<span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">MyApp</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>... <span class="pl-s1">args</span>) {
    <span class="pl-smi">GitHub</span> <span class="pl-s1">github</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                         .<span class="pl-en">decoder</span>(<span class="pl-k">new</span> <span class="pl-smi">GsonDecoder</span>())
                         .<span class="pl-en">target</span>(<span class="pl-smi">GitHub</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.github.com"</span>);

    <span class="pl-c">// Fetch and print a list of the contributors to this library.</span>
    <span class="pl-smi">List</span>&lt;<span class="pl-smi">Contributor</span>&gt; <span class="pl-s1">contributors</span> = <span class="pl-s1">github</span>.<span class="pl-en">contributors</span>(<span class="pl-s">"OpenFeign"</span>, <span class="pl-s">"feign"</span>);
    <span class="pl-k">for</span> (<span class="pl-smi">Contributor</span> <span class="pl-s1">contributor</span> : <span class="pl-s1">contributors</span>) {
      <span class="pl-smi">System</span>.<span class="pl-s1">out</span>.<span class="pl-en">println</span>(<span class="pl-s1">contributor</span>.<span class="pl-s1">login</span> + <span class="pl-s">" ("</span> + <span class="pl-s1">contributor</span>.<span class="pl-s1">contributions</span> + <span class="pl-s">")"</span>);
    }
  }
}</pre><div class="zeroclipboard-container">
   
  </div></div>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">接口注释</font></font></h3><a id="user-content-interface-annotations" class="anchor" aria-label="永久链接：接口注释" href="#interface-annotations"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Feign 注释定义了</font></font><code>Contract</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">接口和底层客户端应该如何工作之间的关系。 Feign的默认合约定义了以下注解：</font></font></p>
<table>
<thead>
<tr>
<th><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">注解</font></font></th>
<th><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">接口目标</font></font></th>
<th><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">用法</font></font></th>
</tr>
</thead>
<tbody>
<tr>
<td><code>@RequestLine</code></td>
<td><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">方法</font></font></td>
<td><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">定义请求的</font></font><code>HttpMethod</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">和</font></font><code>UriTemplate</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">。   </font></font><code>Expressions</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">，用大括号括起来的值</font></font><code>{expression}</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">使用相应的带注释的参数来解析</font></font><code>@Param</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">。</font></font></td>
</tr>
<tr>
<td><code>@Param</code></td>
<td><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">范围</font></font></td>
<td><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">定义一个模板变量，其值将用于解析相应的 template </font></font><code>Expression</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">，通过作为注释值提供的名称。如果值丢失，它将尝试从字节码方法参数名称中获取名称（如果代码是使用</font></font><code>-parameters</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">标志编译的）。</font></font></td>
</tr>
<tr>
<td><code>@Headers</code></td>
<td><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">方法、类型</font></font></td>
<td><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">定义一个</font></font><code>HeaderTemplate</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">; a 的变体</font></font><code>UriTemplate</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">。它使用</font></font><code>@Param</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">带注释的值来解析相应的</font></font><code>Expressions</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">.当在 上使用时</font></font><code>Type</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">，模板将应用于每个请求。当用于 a 时</font></font><code>Method</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">，模板将仅应用于带注释的方法。</font></font></td>
</tr>
<tr>
<td><code>@QueryMap</code></td>
<td><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">范围</font></font></td>
<td><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">定义一组</font></font><code>Map</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">名称-值对（或 POJO）以扩展为查询字符串。</font></font></td>
</tr>
<tr>
<td><code>@HeaderMap</code></td>
<td><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">范围</font></font></td>
<td><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">定义一系列</font></font><code>Map</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">名称-值对，以扩展为</font></font><code>Http Headers</code></td>
</tr>
<tr>
<td><code>@Body</code></td>
<td><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">方法</font></font></td>
<td><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">定义 a </font></font><code>Template</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">，类似于 a</font></font><code>UriTemplate</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">和</font></font><code>HeaderTemplate</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">，它使用</font></font><code>@Param</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">带注释的值来解析相应的</font></font><code>Expressions</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">.</font></font></td>
</tr>
</tbody>
</table>
<blockquote>
<p dir="auto"><strong><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">覆盖请求行</font></font></strong></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">如果需要将请求定位到不同的主机，然后是创建 Feign 客户端时提供的主机，或者您想为每个请求提供目标主机，请包含一个</font></font><code>java.net.URI</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">参数，Feign 将使用该值作为请求目标。</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"POST /repos/{owner}/{repo}/issues"</span>)
<span class="pl-smi">void</span> <span class="pl-s1">createIssue</span>(<span class="pl-smi">URI</span> <span class="pl-s1">host</span>, <span class="pl-smi">Issue</span> <span class="pl-s1">issue</span>, <span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"owner"</span>) <span class="pl-smi">String</span> <span class="pl-s1">owner</span>, <span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"repo"</span>) <span class="pl-smi">String</span> <span class="pl-s1">repo</span>);</pre><div class="zeroclipboard-container">
   
  </div></div>
</blockquote>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">模板和表达式</font></font></h3><a id="user-content-templates-and-expressions" class="anchor" aria-label="永久链接：模板和表达式" href="#templates-and-expressions"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Feign</font></font><code>Expressions</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">表示</font></font><a href="https://tools.ietf.org/html/rfc6570" rel="nofollow"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">URI 模板 - RFC 6570</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">定义的简单字符串表达式（级别 1） 。  使用相应的</font><font style="vertical-align: inherit;">带注释的方法参数</font></font><code>Expressions</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">进行扩展。</font></font><code>Param</code><font style="vertical-align: inherit;"></font></p>
<p dir="auto"><em><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">例子</font></font></em></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">interface</span> <span class="pl-smi">GitHub</span> {

  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"GET /repos/{owner}/{repo}/contributors"</span>)
  <span class="pl-smi">List</span>&lt;<span class="pl-smi">Contributor</span>&gt; <span class="pl-en">contributors</span>(<span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"owner"</span>) <span class="pl-smi">String</span> <span class="pl-s1">owner</span>, <span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"repo"</span>) <span class="pl-smi">String</span> <span class="pl-s1">repository</span>);

  <span class="pl-k">class</span> <span class="pl-smi">Contributor</span> {
    <span class="pl-smi">String</span> <span class="pl-s1">login</span>;
    <span class="pl-smi">int</span> <span class="pl-s1">contributions</span>;
  }
}

<span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">MyApp</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">GitHub</span> <span class="pl-s1">github</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                         .<span class="pl-en">decoder</span>(<span class="pl-k">new</span> <span class="pl-smi">GsonDecoder</span>())
                         .<span class="pl-en">target</span>(<span class="pl-smi">GitHub</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.github.com"</span>);

    <span class="pl-c">/* The owner and repository parameters will be used to expand the owner and repo expressions</span>
<span class="pl-c">     * defined in the RequestLine.</span>
<span class="pl-c">     *</span>
<span class="pl-c">     * the resulting uri will be https://api.github.com/repos/OpenFeign/feign/contributors</span>
<span class="pl-c">     */</span>
    <span class="pl-s1">github</span>.<span class="pl-en">contributors</span>(<span class="pl-s">"OpenFeign"</span>, <span class="pl-s">"feign"</span>);
  }
}</pre><div class="zeroclipboard-container">
    
  </div></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">表达式必须括在花括号中</font></font><code>{}</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">，并且可以包含正则表达式模式，并用冒号分隔</font></font><code>:</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">  以限制解析值。  </font></font><em><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">示例</font></font></em> <code>owner</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">必须按字母顺序排列。</font></font><code>{owner:[a-zA-Z]*}</code></p>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">请求参数扩展</font></font></h4><a id="user-content-request-parameter-expansion" class="anchor" aria-label="永久链接：请求参数扩展" href="#request-parameter-expansion"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><code>RequestLine</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">模板</font></font><code>QueryMap</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">遵循</font></font><a href="https://tools.ietf.org/html/rfc6570" rel="nofollow"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">URI 模板 - RFC 6570</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">级别 1 模板规范，该规范指定以下内容：</font></font></p>
<ul dir="auto">
<li><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">未解析的表达式被省略。</font></font></li>
<li><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">所有文字和变量值（如果尚未</font></font><code>encoded</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">通过</font></font><code>@Param</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">注释进行编码或标记）均经过 pct 编码。</font></font></li>
</ul>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">我们还对 3 级路径样式表达式提供有限支持，并具有以下限制：</font></font></p>
<ul dir="auto">
<li><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">地图和列表默认展开。</font></font></li>
<li><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">仅支持单变量模板。</font></font></li>
</ul>
<p dir="auto"><em><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">例子：</font></font></em></p>
<div class="snippet-clipboard-content notranslate position-relative overflow-auto"><pre class="notranslate"><code>{;who}             ;who=fred
{;half}            ;half=50%25
{;empty}           ;empty
{;list}            ;list=red;list=green;list=blue
{;map}             ;semi=%3B;dot=.;comma=%2C
</code></pre><div class="zeroclipboard-container">
   
  </div></div>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">interface</span> <span class="pl-smi">MatrixService</span> {

  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"GET /repos{;owners}"</span>)
  <span class="pl-smi">List</span>&lt;<span class="pl-smi">Contributor</span>&gt; <span class="pl-en">contributors</span>(<span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"owners"</span>) <span class="pl-smi">List</span>&lt;<span class="pl-smi">String</span>&gt; <span class="pl-s1">owners</span>);

  <span class="pl-k">class</span> <span class="pl-smi">Contributor</span> {
    <span class="pl-smi">String</span> <span class="pl-s1">login</span>;
    <span class="pl-smi">int</span> <span class="pl-s1">contributions</span>;
  }
}</pre><div class="zeroclipboard-container">
  
  </div></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">如果</font></font><code>owners</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">在上面的示例中定义为</font></font><code>Matt, Jeff, Susan</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">，则 uri 将扩展为</font></font><code>/repos;owners=Matt;owners=Jeff;owners=Susan</code></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">有关详细信息，请参阅</font></font><a href="https://datatracker.ietf.org/doc/html/rfc6570#section-3.2.7" rel="nofollow"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">RFC 6570，第 3.2.7 节</font></font></a></p>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">未定义与空值</font></font></h4><a id="user-content-undefined-vs-empty-values" class="anchor" aria-label="永久链接：未定义与空值" href="#undefined-vs-empty-values"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">未定义表达式是指表达式的值是显式的</font></font><code>null</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">或未提供值的表达式。根据</font></font><a href="https://tools.ietf.org/html/rfc6570" rel="nofollow"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">URI 模板 - RFC 6570</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">，可以为表达式提供空值。当 Feign 解析一个表达式时，它首先判断该值是否已定义，如果是则查询参数将保留。如果表达式未定义，则删除查询参数。请参阅下面的完整细分。</font></font></p>
<p dir="auto"><em><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">空字符串</font></font></em></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-smi">void</span> <span class="pl-s1">test</span>() {
   <span class="pl-smi">Map</span>&lt;<span class="pl-smi">String</span>, <span class="pl-smi">Object</span>&gt; <span class="pl-s1">parameters</span> = <span class="pl-k">new</span> <span class="pl-smi">LinkedHashMap</span>&lt;&gt;();
   <span class="pl-s1">parameters</span>.<span class="pl-en">put</span>(<span class="pl-s">"param"</span>, <span class="pl-s">""</span>);
   <span class="pl-smi">this</span>.<span class="pl-s1">demoClient</span>.<span class="pl-en">test</span>(<span class="pl-s1">parameters</span>);
}</pre><div class="zeroclipboard-container">
  
  </div></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">结果</font></font></p>
<div class="snippet-clipboard-content notranslate position-relative overflow-auto"><pre class="notranslate"><code>http://localhost:8080/test?param=
</code></pre><div class="zeroclipboard-container">
  
  </div></div>
<p dir="auto"><em><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">丢失的</font></font></em></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-smi">void</span> <span class="pl-s1">test</span>() {
   <span class="pl-smi">Map</span>&lt;<span class="pl-smi">String</span>, <span class="pl-smi">Object</span>&gt; <span class="pl-s1">parameters</span> = <span class="pl-k">new</span> <span class="pl-smi">LinkedHashMap</span>&lt;&gt;();
   <span class="pl-smi">this</span>.<span class="pl-s1">demoClient</span>.<span class="pl-en">test</span>(<span class="pl-s1">parameters</span>);
}</pre><div class="zeroclipboard-container">
   
  </div></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">结果</font></font></p>
<div class="snippet-clipboard-content notranslate position-relative overflow-auto"><pre class="notranslate"><code>http://localhost:8080/test
</code></pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="http://localhost:8080/test" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon">
    <path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none">
    <path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<p dir="auto"><em><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">不明确的</font></font></em></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-smi">void</span> <span class="pl-s1">test</span>() {
   <span class="pl-smi">Map</span>&lt;<span class="pl-smi">String</span>, <span class="pl-smi">Object</span>&gt; <span class="pl-s1">parameters</span> = <span class="pl-k">new</span> <span class="pl-smi">LinkedHashMap</span>&lt;&gt;();
   <span class="pl-s1">parameters</span>.<span class="pl-en">put</span>(<span class="pl-s">"param"</span>, <span class="pl-c1">null</span>);
   <span class="pl-smi">this</span>.<span class="pl-s1">demoClient</span>.<span class="pl-en">test</span>(<span class="pl-s1">parameters</span>);
}</pre><div class="zeroclipboard-container">
   
  </div></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">结果</font></font></p>
<div class="snippet-clipboard-content notranslate position-relative overflow-auto"><pre class="notranslate"><code>http://localhost:8080/test
</code></pre><div class="zeroclipboard-container">
    
  </div></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">有关更多示例，</font><font style="vertical-align: inherit;">请参阅</font></font><a href="#advanced-usage"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">高级用法。</font></font></a><font style="vertical-align: inherit;"></font></p>
<blockquote>
<p dir="auto"><strong><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">斜杠呢？</font></font><code>/</code></strong></p>
<p dir="auto"><font style="vertical-align: inherit;"></font><code>/</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">@RequestLine 模板默认</font><font style="vertical-align: inherit;">不编码斜杠字符。</font><font style="vertical-align: inherit;">要更改此行为，请将属性</font><font style="vertical-align: inherit;">设置</font></font><code>decodeSlash</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">为</font><font style="vertical-align: inherit;">。</font></font><code>@RequestLine</code><font style="vertical-align: inherit;"></font><code>false</code><font style="vertical-align: inherit;"></font></p>
</blockquote>
<blockquote>
<p dir="auto"><strong><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">加号呢？</font></font><code>+</code></strong></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">根据 URI 规范，</font></font><code>+</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">URI 的路径段和查询段中都允许使用符号，但是，查询中符号的处理可能不一致。在某些遗留系统中，</font></font><code>+</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">相当于空格。 Feign 采用现代系统的方法，其中
</font></font><code>+</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">符号不应代表空格，并且应按照</font></font><code>%2B</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">在查询字符串中找到时的方式进行显式编码。</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">如果您希望用作</font></font><code>+</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">空格，请使用文字</font></font><code> </code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">字符或直接将值编码为</font></font><code>%20</code></p>
</blockquote>
<div class="markdown-heading" dir="auto"><h5 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">定制扩展</font></font></h5><a id="user-content-custom-expansion" class="anchor" aria-label="永久链接：自定义扩展" href="#custom-expansion"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">该</font></font><code>@Param</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">注释有一个可选属性，</font></font><code>expander</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">允许完全控制单个参数的扩展。该</font></font><code>expander</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">属性必须引用实现该接口的类</font></font><code>Expander</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">：</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">interface</span> <span class="pl-smi">Expander</span> {
    <span class="pl-smi">String</span> <span class="pl-en">expand</span>(<span class="pl-smi">Object</span> <span class="pl-s1">value</span>);
}</pre><div class="zeroclipboard-container">
 
  </div></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">该方法的结果遵循上述相同的规则。如果结果是</font></font><code>null</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">空字符串，则省略该值。如果该值不是 pct 编码的，则它将是。</font><font style="vertical-align: inherit;">有关更多示例，</font><font style="vertical-align: inherit;">请参阅</font></font><a href="#custom-param-expansion"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">自定义 @Param 扩展。</font></font></a><font style="vertical-align: inherit;"></font></p>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">请求标头扩展</font></font></h4><a id="user-content-request-headers-expansion" class="anchor" aria-label="永久链接：请求标头扩展" href="#request-headers-expansion"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><code>Headers</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">和模板遵循与</font><a href="#request-parameter-expansion"><font style="vertical-align: inherit;">请求参数扩展</font></a></font><code>HeaderMap</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">相同的规则，</font><font style="vertical-align: inherit;">
但有以下更改：</font></font><a href="#request-parameter-expansion"><font style="vertical-align: inherit;"></font></a><font style="vertical-align: inherit;"></font></p>
<ul dir="auto">
<li><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">未解析的表达式被省略。如果结果是空标头值，则删除整个标头。</font></font></li>
<li><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">不执行 pct 编码。</font></font></li>
</ul>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">有关示例，</font><font style="vertical-align: inherit;">请参阅</font></font><a href="#headers"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">标头。</font></font></a><font style="vertical-align: inherit;"></font></p>
<blockquote>
<p dir="auto"><strong><font style="vertical-align: inherit;"></font><code>@Param</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">关于参数及其名称的</font><font style="vertical-align: inherit;">注释</font></font></strong><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">：</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">所有具有相同名称的表达式，无论它们在</font></font><code>@RequestLine</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">、</font></font><code>@QueryMap</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">、</font></font><code>@BodyTemplate</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">、 或上的位置如何，</font></font><code>@Headers</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">都将解析为相同的值。在以下示例中， , 的值</font></font><code>contentType</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">将用于解析标头和路径表达式：</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">interface</span> <span class="pl-smi">ContentService</span> {
  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"GET /api/documents/{contentType}"</span>)
  <span class="pl-c1">@</span><span class="pl-c1">Headers</span>(<span class="pl-s">"Accept: {contentType}"</span>)
  <span class="pl-smi">String</span> <span class="pl-en">getDocumentByType</span>(<span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"contentType"</span>) <span class="pl-smi">String</span> <span class="pl-s1">type</span>);
}</pre><div class="zeroclipboard-container">
  
  </div></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">设计界面时请记住这一点。</font></font></p>
</blockquote>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">请求正文扩展</font></font></h4><a id="user-content-request-body-expansion" class="anchor" aria-label="永久链接：请求正文扩展" href="#request-body-expansion"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><code>Body</code><font style="vertical-align: inherit;"></font><a href="#request-parameter-expansion"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">模板遵循与请求参数扩展</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">相同的规则，</font><font style="vertical-align: inherit;">
但有以下更改：</font></font></p>
<ul dir="auto">
<li><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">未解析的表达式被省略。</font></font></li>
<li><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">扩展值</font><font style="vertical-align: inherit;">在放置在请求正文之前</font></font><strong><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">不会</font></font></strong><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">经过 an 传递。</font></font><code>Encoder</code><font style="vertical-align: inherit;"></font></li>
<li><font style="vertical-align: inherit;"></font><code>Content-Type</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">必须指定标头</font><font style="vertical-align: inherit;">。</font><font style="vertical-align: inherit;">有关示例，</font><font style="vertical-align: inherit;">请参阅</font></font><a href="#body-templates"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">正文模板。</font></font></a><font style="vertical-align: inherit;"></font></li>
</ul>
<hr>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">定制化</font></font></h3><a id="user-content-customization" class="anchor" aria-label="固定链接：定制" href="#customization"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Feign 有几个方面可以定制。</font></font><br><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">
对于简单的情况，您可以使用</font></font><code>Feign.builder()</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">自定义组件构建 API 接口。</font></font><br><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">
对于请求设置，可以使用</font></font><code>options(Request.Options options)</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">on</font></font><code>target()</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">设置connectTimeout、connectTimeoutUnit、readTimeout、readTimeoutUnit、followRedirects。</font></font><br><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">
例如：</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">interface</span> <span class="pl-smi">Bank</span> {
  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"POST /account/{id}"</span>)
  <span class="pl-smi">Account</span> <span class="pl-en">getAccountInfo</span>(<span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"id"</span>) <span class="pl-smi">String</span> <span class="pl-s1">id</span>);
}

<span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">BankService</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">Bank</span> <span class="pl-s1">bank</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
        .<span class="pl-en">decoder</span>(<span class="pl-k">new</span> <span class="pl-smi">AccountDecoder</span>())
        .<span class="pl-en">options</span>(<span class="pl-k">new</span> <span class="pl-smi">Request</span>.<span class="pl-smi">Options</span>(<span class="pl-c1">10</span>, <span class="pl-smi">TimeUnit</span>.<span class="pl-c1">SECONDS</span>, <span class="pl-c1">60</span>, <span class="pl-smi">TimeUnit</span>.<span class="pl-c1">SECONDS</span>, <span class="pl-c1">true</span>))
        .<span class="pl-en">target</span>(<span class="pl-smi">Bank</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.examplebank.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
 
  </div></div>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">多种接口</font></font></h3><a id="user-content-multiple-interfaces" class="anchor" aria-label="永久链接：多个接口" href="#multiple-interfaces"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Feign可以产生多个api接口。这些被定义为</font></font><code>Target&lt;T&gt;</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">（默认</font></font><code>HardCodedTarget&lt;T&gt;</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">），允许在执行之前动态发现和装饰请求。</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">例如，以下模式可能会使用来自身份服务的当前 url 和身份验证令牌来装饰每个请求。</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">CloudService</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">CloudDNS</span> <span class="pl-s1">cloudDNS</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
      .<span class="pl-en">target</span>(<span class="pl-k">new</span> <span class="pl-smi">CloudIdentityTarget</span>&lt;<span class="pl-smi">CloudDNS</span>&gt;(<span class="pl-s1">user</span>, <span class="pl-s1">apiKey</span>));
  }

  <span class="pl-k">class</span> <span class="pl-smi">CloudIdentityTarget</span> <span class="pl-k">extends</span> <span class="pl-smi">Target</span>&lt;<span class="pl-smi">CloudDNS</span>&gt; {
    <span class="pl-c">/* implementation of a Target */</span>
  }
}</pre><div class="zeroclipboard-container">
    
  </div></div>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">例子</font></font></h3><a id="user-content-examples" class="anchor" aria-label="永久链接：示例" href="#examples"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Feign 包括示例</font></font><a href="/OpenFeign/feign/blob/master/example-github"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">GitHub</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">和</font></font><a href="/OpenFeign/feign/blob/master/example-wikipedia"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Wikipedia</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">客户端。实践中分母项目也可以为 Feign 刮取。特别是看看它的</font></font><a href="https://github.com/Netflix/denominator/tree/master/example-daemon"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">示例 daemon</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">。</font></font></p>
<hr>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">集成</font></font></h3><a id="user-content-integrations" class="anchor" aria-label="永久链接：集成" href="#integrations"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Feign 打算与其他开源工具很好地配合。欢迎模块与您喜欢的项目集成！</font></font></p>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">编码器/解码器</font></font></h3><a id="user-content-encoderdecoder" class="anchor" aria-label="永久链接：编码器/解码器" href="#encoderdecoder"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">格森</font></font></h4><a id="user-content-gson" class="anchor" aria-label="永久链接：Gson" href="#gson"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><a href="/OpenFeign/feign/blob/master/gson"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Gson</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">包含一个编码器和解码器，您可以将其与 JSON API 一起使用。</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">添加</font></font><code>GsonEncoder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">和/或</font></font><code>GsonDecoder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">到你</font></font><code>Feign.Builder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">喜欢的地方：</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">GsonCodec</span> <span class="pl-s1">codec</span> = <span class="pl-k">new</span> <span class="pl-smi">GsonCodec</span>();
    <span class="pl-smi">GitHub</span> <span class="pl-s1">github</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                         .<span class="pl-en">encoder</span>(<span class="pl-k">new</span> <span class="pl-smi">GsonEncoder</span>())
                         .<span class="pl-en">decoder</span>(<span class="pl-k">new</span> <span class="pl-smi">GsonDecoder</span>())
                         .<span class="pl-en">target</span>(<span class="pl-smi">GitHub</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.github.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
 
  </div></div>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">杰克逊</font></font></h4><a id="user-content-jackson" class="anchor" aria-label="永久链接：杰克逊" href="#jackson"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><a href="/OpenFeign/feign/blob/master/jackson"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Jackson</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">包含一个编码器和解码器，您可以将其与 JSON API 一起使用。</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">添加</font></font><code>JacksonEncoder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">和/或</font></font><code>JacksonDecoder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">到你</font></font><code>Feign.Builder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">喜欢的地方：</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
      <span class="pl-smi">GitHub</span> <span class="pl-s1">github</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                     .<span class="pl-en">encoder</span>(<span class="pl-k">new</span> <span class="pl-smi">JacksonEncoder</span>())
                     .<span class="pl-en">decoder</span>(<span class="pl-k">new</span> <span class="pl-smi">JacksonDecoder</span>())
                     .<span class="pl-en">target</span>(<span class="pl-smi">GitHub</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.github.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
  
  </div></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">对于重量较轻的 Jackson Jr，请使用</font><a href="/OpenFeign/feign/blob/master/jackson-jr"><font style="vertical-align: inherit;">Jackson Jr 模块</font></a><font style="vertical-align: inherit;">中的</font></font><code>JacksonJrEncoder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">和</font><font style="vertical-align: inherit;">。</font></font><code>JacksonJrDecoder</code><font style="vertical-align: inherit;"></font><a href="/OpenFeign/feign/blob/master/jackson-jr"><font style="vertical-align: inherit;"></font></a><font style="vertical-align: inherit;"></font></p>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">莫希</font></font></h4><a id="user-content-moshi" class="anchor" aria-label="永久链接：莫西" href="#moshi"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><a href="/OpenFeign/feign/blob/master/moshi"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Moshi</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">包含一个编码器和解码器，您可以将其与 JSON API 结合使用。添加</font></font><code>MoshiEncoder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">和/或</font></font><code>MoshiDecoder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">到你</font></font><code>Feign.Builder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">喜欢的地方：</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-smi">GitHub</span> <span class="pl-s1">github</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                     .<span class="pl-en">encoder</span>(<span class="pl-k">new</span> <span class="pl-smi">MoshiEncoder</span>())
                     .<span class="pl-en">decoder</span>(<span class="pl-k">new</span> <span class="pl-smi">MoshiDecoder</span>())
                     .<span class="pl-en">target</span>(<span class="pl-smi">GitHub</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.github.com"</span>);</pre><div class="zeroclipboard-container">
   
  </div></div>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">萨克斯管</font></font></h4><a id="user-content-sax" class="anchor" aria-label="永久链接：萨克斯" href="#sax"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><a href="/OpenFeign/feign/blob/master/sax"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">SaxDecoder</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">允许您以与普通 JVM 和 Android 环境兼容的方式解码 XML。</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">以下是如何配置 Sax 响应解析的示例：</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
      <span class="pl-smi">Api</span> <span class="pl-s1">api</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
         .<span class="pl-en">decoder</span>(<span class="pl-smi">SAXDecoder</span>.<span class="pl-en">builder</span>()
                            .<span class="pl-en">registerContentHandler</span>(<span class="pl-smi">UserIdHandler</span>.<span class="pl-k">class</span>)
                            .<span class="pl-en">build</span>())
         .<span class="pl-en">target</span>(<span class="pl-smi">Api</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://apihost"</span>);
    }
}</pre><div class="zeroclipboard-container">
  
  </div></div>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">联合航空航天局</font></font></h4><a id="user-content-jaxb" class="anchor" aria-label="永久链接：JAXB" href="#jaxb"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><a href="/OpenFeign/feign/blob/master/jaxb"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">JAXB</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">包含可与 XML API 一起使用的编码器和解码器。</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">添加</font></font><code>JAXBEncoder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">和/或</font></font><code>JAXBDecoder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">到你</font></font><code>Feign.Builder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">喜欢的地方：</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">Api</span> <span class="pl-s1">api</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
             .<span class="pl-en">encoder</span>(<span class="pl-k">new</span> <span class="pl-smi">JAXBEncoder</span>())
             .<span class="pl-en">decoder</span>(<span class="pl-k">new</span> <span class="pl-smi">JAXBDecoder</span>())
             .<span class="pl-en">target</span>(<span class="pl-smi">Api</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://apihost"</span>);
  }
}</pre><div class="zeroclipboard-container">
    
  </div></div>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">肥皂</font></font></h4><a id="user-content-soap" class="anchor" aria-label="永久链接： 肥皂" href="#soap"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><a href="/OpenFeign/feign/blob/master/soap"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">SOAP</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">包括可与 XML API 一起使用的编码器和解码器。</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">该模块添加了对通过 JAXB 和 SOAPMessage 编码和解码 SOAP Body 对象的支持。它还通过将 SOAPFault 包装到原始 SOAPFault 中来提供 SOAPFault 解码功能</font></font><code>javax.xml.ws.soap.SOAPFaultException</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">，这样您只需捕获</font></font><code>SOAPFaultException</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">即可处理 SOAPFault。</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">添加</font></font><code>SOAPEncoder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">和/或</font></font><code>SOAPDecoder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">到你</font></font><code>Feign.Builder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">喜欢的地方：</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">Api</span> <span class="pl-s1">api</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
	     .<span class="pl-en">encoder</span>(<span class="pl-k">new</span> <span class="pl-smi">SOAPEncoder</span>(<span class="pl-s1">jaxbFactory</span>))
	     .<span class="pl-en">decoder</span>(<span class="pl-k">new</span> <span class="pl-smi">SOAPDecoder</span>(<span class="pl-s1">jaxbFactory</span>))
	     .<span class="pl-en">errorDecoder</span>(<span class="pl-k">new</span> <span class="pl-smi">SOAPErrorDecoder</span>())
	     .<span class="pl-en">target</span>(<span class="pl-smi">MyApi</span>.<span class="pl-k">class</span>, <span class="pl-s">"http://api"</span>);
  }
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public class Example {
  public static void main(String[] args) {
    Api api = Feign.builder()
	     .encoder(new SOAPEncoder(jaxbFactory))
	     .decoder(new SOAPDecoder(jaxbFactory))
	     .errorDecoder(new SOAPErrorDecoder())
	     .target(MyApi.class, &quot;http://api&quot;);
  }
}" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon">
    <path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none">
    <path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<p dir="auto"><font style="vertical-align: inherit;"></font><code>SOAPErrorDecoder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">注意：如果响应中返回 SOAP 错误并带有错误 http 代码（4xx、5xx、...），</font><font style="vertical-align: inherit;">您可能还需要添加</font></font></p>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Fastjson2</font></font></h4><a id="user-content-fastjson2" class="anchor" aria-label="永久链接：Fastjson2" href="#fastjson2"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><a href="/OpenFeign/feign/blob/master/fastjson2"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">fastjson2</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">包含可与 JSON API 一起使用的编码器和解码器。</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">添加</font></font><code>Fastjson2Encoder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">和/或</font></font><code>Fastjson2Decoder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">到你</font></font><code>Feign.Builder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">喜欢的地方：</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
      <span class="pl-smi">GitHub</span> <span class="pl-s1">github</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                     .<span class="pl-en">encoder</span>(<span class="pl-k">new</span> <span class="pl-smi">Fastjson2Encoder</span>())
                     .<span class="pl-en">decoder</span>(<span class="pl-k">new</span> <span class="pl-smi">Fastjson2Decoder</span>())
                     .<span class="pl-en">target</span>(<span class="pl-smi">GitHub</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.github.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public class Example {
  public static void main(String[] args) {
      GitHub github = Feign.builder()
                     .encoder(new Fastjson2Encoder())
                     .decoder(new Fastjson2Decoder())
                     .target(GitHub.class, &quot;https://api.github.com&quot;);
  }
}" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon">
    <path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none">
    <path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">合同</font></font></h3><a id="user-content-contract" class="anchor" aria-label="永久链接：合同" href="#contract"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">JAX-RS</font></font></h4><a id="user-content-jax-rs" class="anchor" aria-label="永久链接：JAX-RS" href="#jax-rs"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><a href="/OpenFeign/feign/blob/master/jaxrs"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">JAXRSContract</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">会覆盖注释处理，转而使用 JAX-RS 规范提供的标准注释处理。当前针对的是 1.1 规范。</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">下面是使用 JAX-RS 重写的上面的示例：</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">interface</span> <span class="pl-smi">GitHub</span> {
  <span class="pl-c1">@</span><span class="pl-c1">GET</span> <span class="pl-c1">@</span><span class="pl-c1">Path</span>(<span class="pl-s">"/repos/{owner}/{repo}/contributors"</span>)
  <span class="pl-smi">List</span>&lt;<span class="pl-smi">Contributor</span>&gt; <span class="pl-en">contributors</span>(<span class="pl-c1">@</span><span class="pl-c1">PathParam</span>(<span class="pl-s">"owner"</span>) <span class="pl-smi">String</span> <span class="pl-s1">owner</span>, <span class="pl-c1">@</span><span class="pl-c1">PathParam</span>(<span class="pl-s">"repo"</span>) <span class="pl-smi">String</span> <span class="pl-s1">repo</span>);
}

<span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">GitHub</span> <span class="pl-s1">github</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                       .<span class="pl-en">contract</span>(<span class="pl-k">new</span> <span class="pl-smi">JAXRSContract</span>())
                       .<span class="pl-en">target</span>(<span class="pl-smi">GitHub</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.github.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="interface GitHub {
  @GET @Path(&quot;/repos/{owner}/{repo}/contributors&quot;)
  List<Contributor> contributors(@PathParam(&quot;owner&quot;) String owner, @PathParam(&quot;repo&quot;) String repo);
}

public class Example {
  public static void main(String[] args) {
    GitHub github = Feign.builder()
                       .contract(new JAXRSContract())
                       .target(GitHub.class, &quot;https://api.github.com&quot;);
  }
}" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon">
    <path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none">
    <path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">客户</font></font></h3><a id="user-content-client" class="anchor" aria-label="永久链接： 客户端" href="#client"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">好的http</font></font></h4><a id="user-content-okhttp" class="anchor" aria-label="永久链接：OkHttp" href="#okhttp"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><a href="/OpenFeign/feign/blob/master/okhttp"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">OkHttpClient</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">将 Feign 的 http 请求定向到</font></font><a href="http://square.github.io/okhttp/" rel="nofollow"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">OkHttp</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">，从而实现 SPDY 和更好的网络控制。</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">要将 OkHttp 与 Feign 一起使用，请将 OkHttp 模块添加到类路径中。然后，配置 Feign 以使用 OkHttpClient：</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">GitHub</span> <span class="pl-s1">github</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                     .<span class="pl-en">client</span>(<span class="pl-k">new</span> <span class="pl-smi">OkHttpClient</span>())
                     .<span class="pl-en">target</span>(<span class="pl-smi">GitHub</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.github.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public class Example {
  public static void main(String[] args) {
    GitHub github = Feign.builder()
                     .client(new OkHttpClient())
                     .target(GitHub.class, &quot;https://api.github.com&quot;);
  }
}" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon">
    <path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none">
    <path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">丝带</font></font></h4><a id="user-content-ribbon" class="anchor" aria-label="永久链接： 丝带" href="#ribbon"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><a href="/OpenFeign/feign/blob/master/ribbon"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">RibbonClient</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">覆盖 Feign 客户端的 URL 解析，添加</font></font><a href="https://github.com/Netflix/ribbon"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Ribbon</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">提供的智能路由和弹性功能。</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">集成要求您将功能区客户端名称作为 url 的主机部分传递，例如</font></font><code>myAppProd</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">。</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">MyService</span> <span class="pl-s1">api</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
          .<span class="pl-en">client</span>(<span class="pl-smi">RibbonClient</span>.<span class="pl-en">create</span>())
          .<span class="pl-en">target</span>(<span class="pl-smi">MyService</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://myAppProd"</span>);
  }
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public class Example {
  public static void main(String[] args) {
    MyService api = Feign.builder()
          .client(RibbonClient.create())
          .target(MyService.class, &quot;https://myAppProd&quot;);
  }
}" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon">
    <path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none">
    <path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Java 11 HTTP2</font></font></h4><a id="user-content-java-11-http2" class="anchor" aria-label="永久链接：Java 11 Http2" href="#java-11-http2"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><a href="/OpenFeign/feign/blob/master/java11"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Http2Client</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">将 Feign 的 http 请求定向到</font><font style="vertical-align: inherit;">实现 HTTP/2 的Java11 </font></font><a href="https://openjdk.java.net/jeps/321" rel="nofollow"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">New HTTP/2 Client 。</font></font></a><font style="vertical-align: inherit;"></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">要将 New HTTP/2 Client 与 Feign 结合使用，请使用 Java SDK 11。然后，配置 Feign 以使用 Http2Client：</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-smi">GitHub</span> <span class="pl-s1">github</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                     .<span class="pl-en">client</span>(<span class="pl-k">new</span> <span class="pl-smi">Http2Client</span>())
                     .<span class="pl-en">target</span>(<span class="pl-smi">GitHub</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.github.com"</span>);</pre><div class="zeroclipboard-container">
 
  </div></div>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">断路器</font></font></h3><a id="user-content-breaker" class="anchor" aria-label="永久链接：断路器" href="#breaker"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">海斯特里克斯</font></font></h4><a id="user-content-hystrix" class="anchor" aria-label="永久链接：Hystrix" href="#hystrix"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><a href="/OpenFeign/feign/blob/master/hystrix"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">HystrixFeign配置</font></font></a><font style="vertical-align: inherit;"></font><a href="https://github.com/Netflix/Hystrix"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Hystrix</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">提供的断路器支持</font><font style="vertical-align: inherit;">。</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">要将 Hystrix 与 Feign 一起使用，请将 Hystrix 模块添加到类路径中。然后使用</font></font><code>HystrixFeign</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">构建器：</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">MyService</span> <span class="pl-s1">api</span> = <span class="pl-smi">HystrixFeign</span>.<span class="pl-en">builder</span>().<span class="pl-en">target</span>(<span class="pl-smi">MyService</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://myAppProd"</span>);
  }
}</pre><div class="zeroclipboard-container">
 
  </div></div>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">记录器</font></font></h3><a id="user-content-logger" class="anchor" aria-label="永久链接：记录器" href="#logger"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">SLF4J</font></font></h4><a id="user-content-slf4j" class="anchor" aria-label="永久链接：SLF4J" href="#slf4j"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><a href="/OpenFeign/feign/blob/master/slf4j"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">SLF4JModule</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">允许将 Feign 的日志记录定向到</font></font><a href="http://www.slf4j.org/" rel="nofollow"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">SLF4J</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">，允许您轻松使用您选择的日志记录后端（Logback、Log4J 等）</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">要将 SLF4J 与 Feign 结合使用，请将 SLF4J 模块和您选择的 SLF4J 绑定添加到您的类路径中。然后，配置 Feign 使用 Slf4jLogger：</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">GitHub</span> <span class="pl-s1">github</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                     .<span class="pl-en">logger</span>(<span class="pl-k">new</span> <span class="pl-smi">Slf4jLogger</span>())
                     .<span class="pl-en">logLevel</span>(<span class="pl-smi">Level</span>.<span class="pl-c1">FULL</span>)
                     .<span class="pl-en">target</span>(<span class="pl-smi">GitHub</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.github.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
   
  </div></div>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">解码器</font></font></h3><a id="user-content-decoders" class="anchor" aria-label="永久链接：解码器" href="#decoders"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><code>Feign.builder()</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">允许您指定其他配置，例如如何解码响应。</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">如果接口中的任何方法返回除</font></font><code>Response</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">, </font></font><code>String</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">,</font></font><code>byte[]</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">或之外的类型</font></font><code>void</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">，则需要配置非默认</font></font><code>Decoder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">.</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">以下是配置 JSON 解码的方法（使用扩展</font></font><code>feign-gson</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">）：</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">GitHub</span> <span class="pl-s1">github</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                     .<span class="pl-en">decoder</span>(<span class="pl-k">new</span> <span class="pl-smi">GsonDecoder</span>())
                     .<span class="pl-en">target</span>(<span class="pl-smi">GitHub</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.github.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
     
  </div></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">如果您需要在将响应提供给解码器之前对其进行预处理，则可以使用</font></font><code>mapAndDecode</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">构建器方法。一个示例用例是处理仅提供 jsonp 服务的 API，您可能需要在将 jsonp 发送到您选择的 Json 解码器之前解开包装：</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">JsonpApi</span> <span class="pl-s1">jsonpApi</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                         .<span class="pl-en">mapAndDecode</span>((<span class="pl-s1">response</span>, <span class="pl-s1">type</span>) -&gt; <span class="pl-en">jsopUnwrap</span>(<span class="pl-s1">response</span>, <span class="pl-s1">type</span>), <span class="pl-k">new</span> <span class="pl-smi">GsonDecoder</span>())
                         .<span class="pl-en">target</span>(<span class="pl-smi">JsonpApi</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://some-jsonp-api.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
  
  </div></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">如果接口中的任何方法返回类型</font></font><code>Stream</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">，则需要配置一个</font></font><code>StreamDecoder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">.</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">以下是如何在没有委托解码器的情况下配置流解码器：</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">GitHub</span> <span class="pl-s1">github</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
            .<span class="pl-en">decoder</span>(<span class="pl-smi">StreamDecoder</span>.<span class="pl-en">create</span>((<span class="pl-s1">r</span>, <span class="pl-s1">t</span>) -&gt; {
              <span class="pl-smi">BufferedReader</span> <span class="pl-s1">bufferedReader</span> = <span class="pl-k">new</span> <span class="pl-smi">BufferedReader</span>(<span class="pl-s1">r</span>.<span class="pl-en">body</span>().<span class="pl-en">asReader</span>(<span class="pl-c1">UTF_8</span>));
              <span class="pl-k">return</span> <span class="pl-s1">bufferedReader</span>.<span class="pl-en">lines</span>().<span class="pl-en">iterator</span>();
            }))
            .<span class="pl-en">target</span>(<span class="pl-smi">GitHub</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.github.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
  
  </div></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">以下是如何使用委托解码器配置流解码器：</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">GitHub</span> <span class="pl-s1">github</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
            .<span class="pl-en">decoder</span>(<span class="pl-smi">StreamDecoder</span>.<span class="pl-en">create</span>((<span class="pl-s1">r</span>, <span class="pl-s1">t</span>) -&gt; {
              <span class="pl-smi">BufferedReader</span> <span class="pl-s1">bufferedReader</span> = <span class="pl-k">new</span> <span class="pl-smi">BufferedReader</span>(<span class="pl-s1">r</span>.<span class="pl-en">body</span>().<span class="pl-en">asReader</span>(<span class="pl-c1">UTF_8</span>));
              <span class="pl-k">return</span> <span class="pl-s1">bufferedReader</span>.<span class="pl-en">lines</span>().<span class="pl-en">iterator</span>();
            }, (<span class="pl-s1">r</span>, <span class="pl-s1">t</span>) -&gt; <span class="pl-s">"this is delegate decoder"</span>))
            .<span class="pl-en">target</span>(<span class="pl-smi">GitHub</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.github.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
     
  </div></div>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">编码器</font></font></h3><a id="user-content-encoders" class="anchor" aria-label="永久链接：编码器" href="#encoders"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">将请求正文发送到服务器的最简单方法是定义一个</font></font><code>POST</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">方法，该方法具有</font></font><code>String</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">或</font></font><code>byte[]</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">参数，但不带任何注释。您可能需要添加</font></font><code>Content-Type</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">标头。</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">interface</span> <span class="pl-smi">LoginClient</span> {
  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"POST /"</span>)
  <span class="pl-c1">@</span><span class="pl-c1">Headers</span>(<span class="pl-s">"Content-Type: application/json"</span>)
  <span class="pl-smi">void</span> <span class="pl-en">login</span>(<span class="pl-smi">String</span> <span class="pl-s1">content</span>);
}

<span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-s1">client</span>.<span class="pl-en">login</span>(<span class="pl-s">"{<span class="pl-cce">\"</span>user_name<span class="pl-cce">\"</span>: <span class="pl-cce">\"</span>denominator<span class="pl-cce">\"</span>, <span class="pl-cce">\"</span>password<span class="pl-cce">\"</span>: <span class="pl-cce">\"</span>secret<span class="pl-cce">\"</span>}"</span>);
  }
}</pre><div class="zeroclipboard-container">
   
  </div></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">通过配置</font></font><code>Encoder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">，您可以发送类型安全的请求正文。这是使用扩展的示例</font></font><code>feign-gson</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">：</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">static</span> <span class="pl-k">class</span> <span class="pl-smi">Credentials</span> {
  <span class="pl-k">final</span> <span class="pl-smi">String</span> <span class="pl-s1">user_name</span>;
  <span class="pl-k">final</span> <span class="pl-smi">String</span> <span class="pl-s1">password</span>;

  <span class="pl-smi">Credentials</span>(<span class="pl-smi">String</span> <span class="pl-s1">user_name</span>, <span class="pl-smi">String</span> <span class="pl-s1">password</span>) {
    <span class="pl-smi">this</span>.<span class="pl-s1">user_name</span> = <span class="pl-s1">user_name</span>;
    <span class="pl-smi">this</span>.<span class="pl-s1">password</span> = <span class="pl-s1">password</span>;
  }
}

<span class="pl-k">interface</span> <span class="pl-smi">LoginClient</span> {
  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"POST /"</span>)
  <span class="pl-smi">void</span> <span class="pl-en">login</span>(<span class="pl-smi">Credentials</span> <span class="pl-s1">creds</span>);
}

<span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">LoginClient</span> <span class="pl-s1">client</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                              .<span class="pl-en">encoder</span>(<span class="pl-k">new</span> <span class="pl-smi">GsonEncoder</span>())
                              .<span class="pl-en">target</span>(<span class="pl-smi">LoginClient</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://foo.com"</span>);

    <span class="pl-s1">client</span>.<span class="pl-en">login</span>(<span class="pl-k">new</span> <span class="pl-smi">Credentials</span>(<span class="pl-s">"denominator"</span>, <span class="pl-s">"secret"</span>));
  }
}</pre><div class="zeroclipboard-container">
  
  </div></div>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">@Body模板</font></font></h3><a id="user-content-body-templates" class="anchor" aria-label="永久链接：@Body 模板" href="#body-templates"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">该</font></font><code>@Body</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">注释指示使用 注释的参数来扩展的模板</font></font><code>@Param</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">。您可能需要添加</font></font><code>Content-Type</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">标头。</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">interface</span> <span class="pl-smi">LoginClient</span> {

  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"POST /"</span>)
  <span class="pl-c1">@</span><span class="pl-c1">Headers</span>(<span class="pl-s">"Content-Type: application/xml"</span>)
  <span class="pl-c1">@</span><span class="pl-c1">Body</span>(<span class="pl-s">"&lt;login <span class="pl-cce">\"</span>user_name<span class="pl-cce">\"</span>=<span class="pl-cce">\"</span>{user_name}<span class="pl-cce">\"</span> <span class="pl-cce">\"</span>password<span class="pl-cce">\"</span>=<span class="pl-cce">\"</span>{password}<span class="pl-cce">\"</span>/&gt;"</span>)
  <span class="pl-smi">void</span> <span class="pl-en">xml</span>(<span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"user_name"</span>) <span class="pl-smi">String</span> <span class="pl-s1">user</span>, <span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"password"</span>) <span class="pl-smi">String</span> <span class="pl-s1">password</span>);

  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"POST /"</span>)
  <span class="pl-c1">@</span><span class="pl-c1">Headers</span>(<span class="pl-s">"Content-Type: application/json"</span>)
  <span class="pl-c">// json curly braces must be escaped!</span>
  <span class="pl-c1">@</span><span class="pl-c1">Body</span>(<span class="pl-s">"%7B<span class="pl-cce">\"</span>user_name<span class="pl-cce">\"</span>: <span class="pl-cce">\"</span>{user_name}<span class="pl-cce">\"</span>, <span class="pl-cce">\"</span>password<span class="pl-cce">\"</span>: <span class="pl-cce">\"</span>{password}<span class="pl-cce">\"</span>%7D"</span>)
  <span class="pl-smi">void</span> <span class="pl-en">json</span>(<span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"user_name"</span>) <span class="pl-smi">String</span> <span class="pl-s1">user</span>, <span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"password"</span>) <span class="pl-smi">String</span> <span class="pl-s1">password</span>);
}

<span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-s1">client</span>.<span class="pl-en">xml</span>(<span class="pl-s">"denominator"</span>, <span class="pl-s">"secret"</span>); <span class="pl-c">// &lt;login "user_name"="denominator" "password"="secret"/&gt;</span>
    <span class="pl-s1">client</span>.<span class="pl-en">json</span>(<span class="pl-s">"denominator"</span>, <span class="pl-s">"secret"</span>); <span class="pl-c">// {"user_name": "denominator", "password": "secret"}</span>
  }
}</pre><div class="zeroclipboard-container">
   
  </div></div>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">标头</font></font></h3><a id="user-content-headers" class="anchor" aria-label="固定链接：标题" href="#headers"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Feign 支持在请求上设置标头，作为 api 的一部分或作为客户端的一部分，具体取决于用例。</font></font></p>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">使用 api 设置标头</font></font></h4><a id="user-content-set-headers-using-apis" class="anchor" aria-label="永久链接：使用 api 设置标头" href="#set-headers-using-apis"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">如果特定接口或调用应始终设置某些标头值，则将标头定义为 api 的一部分是有意义的。</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">可以使用注释在 api 接口或方法上设置静态标头</font></font><code>@Headers</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">。</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-c1">@</span><span class="pl-c1">Headers</span>(<span class="pl-s">"Accept: application/json"</span>)
<span class="pl-k">interface</span> <span class="pl-smi">BaseApi</span>&lt;<span class="pl-smi">V</span>&gt; {
  <span class="pl-c1">@</span><span class="pl-c1">Headers</span>(<span class="pl-s">"Content-Type: application/json"</span>)
  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"PUT /api/{key}"</span>)
  <span class="pl-smi">void</span> <span class="pl-en">put</span>(<span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"key"</span>) <span class="pl-smi">String</span> <span class="pl-s1">key</span>, <span class="pl-smi">V</span> <span class="pl-s1">value</span>);
}</pre><div class="zeroclipboard-container">
    
  </div></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">方法可以使用</font></font><code>@Headers</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">.</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">interface</span> <span class="pl-smi">Api</span> {
   <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"POST /"</span>)
   <span class="pl-c1">@</span><span class="pl-c1">Headers</span>(<span class="pl-s">"X-Ping: {token}"</span>)
   <span class="pl-smi">void</span> <span class="pl-en">post</span>(<span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"token"</span>) <span class="pl-smi">String</span> <span class="pl-s1">token</span>);
}</pre><div class="zeroclipboard-container">
    
  </div></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">如果标头字段键和值都是动态的，并且可能的键的范围无法提前知道，并且同一 api/客户端中的不同方法调用之间可能会有所不同（例如自定义元数据标头字段，例如“x-amz- meta-*”或“x-goog-meta-*”），可以使用 Map 参数进行注释，以</font></font><code>HeaderMap</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">构造使用映射内容作为其标头参数的查询。</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">interface</span> <span class="pl-smi">Api</span> {
   <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"POST /"</span>)
   <span class="pl-smi">void</span> <span class="pl-en">post</span>(<span class="pl-c1">@</span><span class="pl-c1">HeaderMap</span> <span class="pl-smi">Map</span>&lt;<span class="pl-smi">String</span>, <span class="pl-smi">Object</span>&gt; <span class="pl-s1">headerMap</span>);
}</pre><div class="zeroclipboard-container">
  
  </div></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">这些方法将标头条目指定为 api 的一部分，并且在构建 Feign 客户端时不需要任何自定义。</font></font></p>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">设置每个目标的标头</font></font></h4><a id="user-content-setting-headers-per-target" class="anchor" aria-label="永久链接：设置每个目标的标头" href="#setting-headers-per-target"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">要为 Target 上的每个请求方法自定义标头，可以使用 RequestInterceptor。 RequestInterceptors 可以在 Target 实例之间共享，并且应该是线程安全的。 RequestInterceptors 应用于 Target 上的所有请求方法。</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">如果您需要按方法自定义，则需要自定义 Target，因为 RequestInterceptor 无法访问当前方法元数据。</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">有关使用 设置标头的示例</font></font><code>RequestInterceptor</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">，请参阅 参考资料</font></font><code>Request Interceptors</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">部分。</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">标头可以设置为自定义的一部分</font></font><code>Target</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">。</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre>  <span class="pl-k">static</span> <span class="pl-k">class</span> <span class="pl-smi">DynamicAuthTokenTarget</span>&lt;<span class="pl-smi">T</span>&gt; <span class="pl-k">implements</span> <span class="pl-smi">Target</span>&lt;<span class="pl-smi">T</span>&gt; {
    <span class="pl-k">public</span> <span class="pl-s1">DynamicAuthTokenTarget</span>(<span class="pl-smi">Class</span>&lt;<span class="pl-smi">T</span>&gt; <span class="pl-s1">clazz</span>,
                                  <span class="pl-smi">UrlAndTokenProvider</span> <span class="pl-s1">provider</span>,
                                  <span class="pl-smi">ThreadLocal</span>&lt;<span class="pl-smi">String</span>&gt; <span class="pl-s1">requestIdProvider</span>);

    <span class="pl-c1">@</span><span class="pl-c1">Override</span>
    <span class="pl-k">public</span> <span class="pl-smi">Request</span> <span class="pl-en">apply</span>(<span class="pl-smi">RequestTemplate</span> <span class="pl-s1">input</span>) {
      <span class="pl-smi">TokenIdAndPublicURL</span> <span class="pl-s1">urlAndToken</span> = <span class="pl-s1">provider</span>.<span class="pl-en">get</span>();
      <span class="pl-k">if</span> (<span class="pl-s1">input</span>.<span class="pl-en">url</span>().<span class="pl-en">indexOf</span>(<span class="pl-s">"http"</span>) != <span class="pl-c1">0</span>) {
        <span class="pl-s1">input</span>.<span class="pl-en">insert</span>(<span class="pl-c1">0</span>, <span class="pl-s1">urlAndToken</span>.<span class="pl-s1">publicURL</span>);
      }
      <span class="pl-s1">input</span>.<span class="pl-en">header</span>(<span class="pl-s">"X-Auth-Token"</span>, <span class="pl-s1">urlAndToken</span>.<span class="pl-s1">tokenId</span>);
      <span class="pl-s1">input</span>.<span class="pl-en">header</span>(<span class="pl-s">"X-Request-ID"</span>, <span class="pl-s1">requestIdProvider</span>.<span class="pl-en">get</span>());

      <span class="pl-k">return</span> <span class="pl-s1">input</span>.<span class="pl-en">request</span>();
    }
  }

  <span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
    <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
      <span class="pl-smi">Bank</span> <span class="pl-s1">bank</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
              .<span class="pl-en">target</span>(<span class="pl-k">new</span> <span class="pl-smi">DynamicAuthTokenTarget</span>(<span class="pl-smi">Bank</span>.<span class="pl-k">class</span>, <span class="pl-s1">provider</span>, <span class="pl-s1">requestIdProvider</span>));
    }
  }</pre><div class="zeroclipboard-container">
   
  </div></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">这些方法取决于</font><font style="vertical-align: inherit;">Feign 客户端构建时的自定义</font></font><code>RequestInterceptor</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">或设置，并且可以用作在每个客户端的所有 api 调用上设置标头的方法。</font></font><code>Target</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">这对于执行一些操作非常有用，例如在每个客户端的所有 api 请求的标头中设置身份验证令牌。当在调用 api 调用的线程上进行 api 调用时，这些方法就会运行，这允许在调用时以上下文特定的方式动态设置标头——例如，线程本地存储可用于根据调用线程设置不同的标头值，这对于为请求设置特定于线程的跟踪标识符等事情很有用。</font></font></p>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">高级用法</font></font></h3><a id="user-content-advanced-usage" class="anchor" aria-label="永久链接：高级用法" href="#advanced-usage"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">基础蜜蜂</font></font></h4><a id="user-content-base-apis" class="anchor" aria-label="永久链接：基础 API" href="#base-apis"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">在许多情况下，服务的 api 遵循相同的约定。 Feign 通过单继承接口支持这种模式。</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">考虑这个例子：</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">interface</span> <span class="pl-smi">BaseAPI</span> {
  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"GET /health"</span>)
  <span class="pl-smi">String</span> <span class="pl-en">health</span>();

  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"GET /all"</span>)
  <span class="pl-smi">List</span>&lt;<span class="pl-smi">Entity</span>&gt; <span class="pl-en">all</span>();
}</pre><div class="zeroclipboard-container">
    
  </div></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">您可以定义并定位特定的 api，继承基本方法。</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">interface</span> <span class="pl-smi">CustomAPI</span> <span class="pl-k">extends</span> <span class="pl-smi">BaseAPI</span> {
  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"GET /custom"</span>)
  <span class="pl-smi">String</span> <span class="pl-en">custom</span>();
}</pre><div class="zeroclipboard-container">
 
  </div></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">在许多情况下，资源表示也是一致的。因此，基本 api 接口支持类型参数。</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-c1">@</span><span class="pl-c1">Headers</span>(<span class="pl-s">"Accept: application/json"</span>)
<span class="pl-k">interface</span> <span class="pl-smi">BaseApi</span>&lt;<span class="pl-smi">V</span>&gt; {

  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"GET /api/{key}"</span>)
  <span class="pl-smi">V</span> <span class="pl-en">get</span>(<span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"key"</span>) <span class="pl-smi">String</span> <span class="pl-s1">key</span>);

  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"GET /api"</span>)
  <span class="pl-smi">List</span>&lt;<span class="pl-smi">V</span>&gt; <span class="pl-en">list</span>();

  <span class="pl-c1">@</span><span class="pl-c1">Headers</span>(<span class="pl-s">"Content-Type: application/json"</span>)
  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"PUT /api/{key}"</span>)
  <span class="pl-smi">void</span> <span class="pl-en">put</span>(<span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"key"</span>) <span class="pl-smi">String</span> <span class="pl-s1">key</span>, <span class="pl-smi">V</span> <span class="pl-s1">value</span>);
}

<span class="pl-k">interface</span> <span class="pl-smi">FooApi</span> <span class="pl-k">extends</span> <span class="pl-smi">BaseApi</span>&lt;<span class="pl-smi">Foo</span>&gt; { }

<span class="pl-k">interface</span> <span class="pl-smi">BarApi</span> <span class="pl-k">extends</span> <span class="pl-smi">BaseApi</span>&lt;<span class="pl-smi">Bar</span>&gt; { }</pre><div class="zeroclipboard-container">
    
  </div></div>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">记录</font></font></h4><a id="user-content-logging" class="anchor" aria-label="永久链接：记录" href="#logging"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">您可以通过设置</font></font><code>Logger</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">.这是最简单的方法：</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">GitHub</span> <span class="pl-s1">github</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                     .<span class="pl-en">decoder</span>(<span class="pl-k">new</span> <span class="pl-smi">GsonDecoder</span>())
                     .<span class="pl-en">logger</span>(<span class="pl-k">new</span> <span class="pl-smi">Logger</span>.<span class="pl-smi">JavaLogger</span>(<span class="pl-s">"GitHub.Logger"</span>).<span class="pl-en">appendToFile</span>(<span class="pl-s">"logs/http.log"</span>))
                     .<span class="pl-en">logLevel</span>(<span class="pl-smi">Logger</span>.<span class="pl-s1">Level</span>.<span class="pl-c1">FULL</span>)
                     .<span class="pl-en">target</span>(<span class="pl-smi">GitHub</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.github.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
    
  </div></div>
<blockquote>
<p dir="auto"><strong><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">关于 JavaLogger 的注意事项</font></font></strong><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">：避免使用默认</font></font><code>JavaLogger()</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">构造函数 - 它已被标记为已弃用，并将很快被删除。</font></font></p>
</blockquote>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">SLF4JLogger（见上文）也可能令人感兴趣。</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">要过滤掉授权或令牌等敏感信息，请覆盖方法</font></font><code>shouldLogRequestHeader</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">或</font></font><code>shouldLogResponseHeader</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">.</font></font></p>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">请求拦截器</font></font></h4><a id="user-content-request-interceptors" class="anchor" aria-label="永久链接：请求拦截器" href="#request-interceptors"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">当您需要更改所有请求时，无论其目标是什么，您都需要配置一个</font></font><code>RequestInterceptor</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">.例如，如果您充当中介，您可能想要传播</font></font><code>X-Forwarded-For</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">标头。</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">static</span> <span class="pl-k">class</span> <span class="pl-smi">ForwardedForInterceptor</span> <span class="pl-k">implements</span> <span class="pl-smi">RequestInterceptor</span> {
  <span class="pl-c1">@</span><span class="pl-c1">Override</span> <span class="pl-k">public</span> <span class="pl-smi">void</span> <span class="pl-en">apply</span>(<span class="pl-smi">RequestTemplate</span> <span class="pl-s1">template</span>) {
    <span class="pl-s1">template</span>.<span class="pl-en">header</span>(<span class="pl-s">"X-Forwarded-For"</span>, <span class="pl-s">"origin.host.com"</span>);
  }
}

<span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">Bank</span> <span class="pl-s1">bank</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                 .<span class="pl-en">decoder</span>(<span class="pl-s1">accountDecoder</span>)
                 .<span class="pl-en">requestInterceptor</span>(<span class="pl-k">new</span> <span class="pl-smi">ForwardedForInterceptor</span>())
                 .<span class="pl-en">target</span>(<span class="pl-smi">Bank</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.examplebank.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
    
  </div></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">拦截器的另一个常见示例是身份验证，例如使用内置的</font></font><code>BasicAuthRequestInterceptor</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">.</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">Bank</span> <span class="pl-s1">bank</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                 .<span class="pl-en">decoder</span>(<span class="pl-s1">accountDecoder</span>)
                 .<span class="pl-en">requestInterceptor</span>(<span class="pl-k">new</span> <span class="pl-smi">BasicAuthRequestInterceptor</span>(<span class="pl-s1">username</span>, <span class="pl-s1">password</span>))
                 .<span class="pl-en">target</span>(<span class="pl-smi">Bank</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.examplebank.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
   
  </div></div>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">自定义@Param扩展</font></font></h4><a id="user-content-custom-param-expansion" class="anchor" aria-label="永久链接：自定义@Param扩展" href="#custom-param-expansion"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"></font><code>Param</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">基于其扩展</font><font style="vertical-align: inherit;">注释的参数</font></font><code>toString</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">。通过指定自定义</font></font><code>Param.Expander</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">，用户可以控制此行为，例如格式化日期。</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">interface</span> <span class="pl-smi">Api</span> {
  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"GET /?since={date}"</span>) <span class="pl-smi">Result</span> <span class="pl-en">list</span>(<span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s1">value</span> = <span class="pl-s">"date"</span>, <span class="pl-s1">expander</span> = <span class="pl-smi">DateToMillis</span>.<span class="pl-k">class</span>) <span class="pl-smi">Date</span> <span class="pl-s1">date</span>);
}</pre><div class="zeroclipboard-container">
    
  </div></div>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">动态查询参数</font></font></h4><a id="user-content-dynamic-query-parameters" class="anchor" aria-label="永久链接：动态查询参数" href="#dynamic-query-parameters"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">可以使用 Map 参数进行注释，以</font></font><code>QueryMap</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">构造使用映射内容作为其查询参数的查询。</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">interface</span> <span class="pl-smi">Api</span> {
  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"GET /find"</span>)
  <span class="pl-smi">V</span> <span class="pl-en">find</span>(<span class="pl-c1">@</span><span class="pl-c1">QueryMap</span> <span class="pl-smi">Map</span>&lt;<span class="pl-smi">String</span>, <span class="pl-smi">Object</span>&gt; <span class="pl-s1">queryMap</span>);
}</pre><div class="zeroclipboard-container">
  
  </div></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">这也可以用于使用 .POJO 对象从 POJO 对象生成查询参数</font></font><code>QueryMapEncoder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">。</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">interface</span> <span class="pl-smi">Api</span> {
  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"GET /find"</span>)
  <span class="pl-smi">V</span> <span class="pl-en">find</span>(<span class="pl-c1">@</span><span class="pl-c1">QueryMap</span> <span class="pl-smi">CustomPojo</span> <span class="pl-s1">customPojo</span>);
}</pre><div class="zeroclipboard-container">
     
  </div></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">当以这种方式使用时，如果不指定自定义</font></font><code>QueryMapEncoder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">，将使用成员变量名称作为查询参数名称来生成查询映射。您可以</font></font><code>CustomPojo</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">使用注释来</font><font style="vertical-align: inherit;">注释特定字段，</font></font><code>@Param</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">以便为查询参数指定不同的名称。以下POJO将生成“/find?name={name}&amp;number={number}®ion_id={regionId}”的查询参数（不保证包含的查询参数的顺序，并且像往常一样，如果任何值为null，它将被遗漏）。</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">CustomPojo</span> {
  <span class="pl-k">private</span> <span class="pl-k">final</span> <span class="pl-smi">String</span> <span class="pl-s1">name</span>;
  <span class="pl-k">private</span> <span class="pl-k">final</span> <span class="pl-smi">int</span> <span class="pl-s1">number</span>;
  <span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"region_id"</span>)
  <span class="pl-k">private</span> <span class="pl-k">final</span> <span class="pl-smi">String</span> <span class="pl-s1">regionId</span>;

  <span class="pl-k">public</span> <span class="pl-smi">CustomPojo</span> (<span class="pl-smi">String</span> <span class="pl-s1">name</span>, <span class="pl-smi">int</span> <span class="pl-s1">number</span>, <span class="pl-smi">String</span> <span class="pl-s1">regionId</span>) {
    <span class="pl-smi">this</span>.<span class="pl-s1">name</span> = <span class="pl-s1">name</span>;
    <span class="pl-smi">this</span>.<span class="pl-s1">number</span> = <span class="pl-s1">number</span>;
    <span class="pl-smi">this</span>.<span class="pl-s1">regionId</span> = <span class="pl-s1">regionId</span>;
  }
}</pre><div class="zeroclipboard-container">
    
  </div></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">要设置自定义</font></font><code>QueryMapEncoder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">：</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">MyApi</span> <span class="pl-s1">myApi</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                 .<span class="pl-en">queryMapEncoder</span>(<span class="pl-k">new</span> <span class="pl-smi">MyCustomQueryMapEncoder</span>())
                 .<span class="pl-en">target</span>(<span class="pl-smi">MyApi</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.hostname.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
   
  </div></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">当使用@QueryMap注释对象时，默认编码器使用反射来检查提供的对象字段，以将对象值扩展为查询字符串。如果您希望使用 getter 和 setter 方法构建查询字符串（如 Java Beans API 中所定义），请使用 BeanQueryMapEncoder</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">MyApi</span> <span class="pl-s1">myApi</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                 .<span class="pl-en">queryMapEncoder</span>(<span class="pl-k">new</span> <span class="pl-smi">BeanQueryMapEncoder</span>())
                 .<span class="pl-en">target</span>(<span class="pl-smi">MyApi</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.hostname.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
     
  </div></div>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">错误处理</font></font></h3><a id="user-content-error-handling" class="anchor" aria-label="永久链接：错误处理" href="#error-handling"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">如果您需要更多地控制处理意外响应，Feign 实例可以</font></font><code>ErrorDecoder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">通过构建器注册自定义。</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">MyApi</span> <span class="pl-s1">myApi</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                 .<span class="pl-en">errorDecoder</span>(<span class="pl-k">new</span> <span class="pl-smi">MyErrorDecoder</span>())
                 .<span class="pl-en">target</span>(<span class="pl-smi">MyApi</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.hostname.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
    
  </div></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">所有导致 HTTP 状态不在 2xx 范围内的响应都将触发</font></font><code>ErrorDecoder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">s</font></font><code>decode</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">方法，允许您处理响应、将失败包装到自定义异常中或执行任何其他处理。如果您想再次重试请求，请抛出</font></font><code>RetryableException</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">.这将调用注册的
</font></font><code>Retryer</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">.</font></font></p>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">重试</font></font></h3><a id="user-content-retry" class="anchor" aria-label="永久链接：重试" href="#retry"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">默认情况下，</font></font><code>IOException</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">无论 HTTP 方法如何，Feign 都会自动重试，将它们视为与网络相关的瞬态异常以及</font></font><code>RetryableException</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">从</font></font><code>ErrorDecoder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">.要自定义此行为，请</font></font><code>Retryer</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">通过构建器注册自定义实例。</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">以下示例演示如何刷新令牌并</font></font><code>ErrorDecoder</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">在</font></font><code>Retryer</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">收到 401 响应时重试。</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
    <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
        <span class="pl-smi">var</span> <span class="pl-s1">github</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                .<span class="pl-en">decoder</span>(<span class="pl-k">new</span> <span class="pl-smi">GsonDecoder</span>())
                .<span class="pl-en">retryer</span>(<span class="pl-k">new</span> <span class="pl-smi">MyRetryer</span>(<span class="pl-c1">100</span>, <span class="pl-c1">3</span>))
                .<span class="pl-en">errorDecoder</span>(<span class="pl-k">new</span> <span class="pl-smi">MyErrorDecoder</span>())
                .<span class="pl-en">target</span>(<span class="pl-smi">Github</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.github.com"</span>);

        <span class="pl-smi">var</span> <span class="pl-s1">contributors</span> = <span class="pl-s1">github</span>.<span class="pl-en">contributors</span>(<span class="pl-s">"foo"</span>, <span class="pl-s">"bar"</span>, <span class="pl-s">"invalid_token"</span>);
        <span class="pl-k">for</span> (<span class="pl-smi">var</span> <span class="pl-s1">contributor</span> : <span class="pl-s1">contributors</span>) {
            <span class="pl-smi">System</span>.<span class="pl-s1">out</span>.<span class="pl-en">println</span>(<span class="pl-s1">contributor</span>.<span class="pl-s1">login</span> + <span class="pl-s">" "</span> + <span class="pl-s1">contributor</span>.<span class="pl-s1">contributions</span>);
        }
    }

    <span class="pl-k">static</span> <span class="pl-k">class</span> <span class="pl-smi">MyErrorDecoder</span> <span class="pl-k">implements</span> <span class="pl-smi">ErrorDecoder</span> {

        <span class="pl-k">private</span> <span class="pl-k">final</span> <span class="pl-smi">ErrorDecoder</span> <span class="pl-s1">defaultErrorDecoder</span> = <span class="pl-k">new</span> <span class="pl-smi">Default</span>();

        <span class="pl-c1">@</span><span class="pl-c1">Override</span>
        <span class="pl-k">public</span> <span class="pl-smi">Exception</span> <span class="pl-en">decode</span>(<span class="pl-smi">String</span> <span class="pl-s1">methodKey</span>, <span class="pl-smi">Response</span> <span class="pl-s1">response</span>) {
            <span class="pl-c">// wrapper 401 to RetryableException in order to retry</span>
            <span class="pl-k">if</span> (<span class="pl-s1">response</span>.<span class="pl-en">status</span>() == <span class="pl-c1">401</span>) {
                <span class="pl-k">return</span> <span class="pl-k">new</span> <span class="pl-smi">RetryableException</span>(<span class="pl-s1">response</span>.<span class="pl-en">status</span>(), <span class="pl-s1">response</span>.<span class="pl-en">reason</span>(), <span class="pl-s1">response</span>.<span class="pl-en">request</span>().<span class="pl-en">httpMethod</span>(), <span class="pl-c1">null</span>, <span class="pl-s1">response</span>.<span class="pl-en">request</span>());
            }
            <span class="pl-k">return</span> <span class="pl-s1">defaultErrorDecoder</span>.<span class="pl-en">decode</span>(<span class="pl-s1">methodKey</span>, <span class="pl-s1">response</span>);
        }
    }

    <span class="pl-k">static</span> <span class="pl-k">class</span> <span class="pl-smi">MyRetryer</span> <span class="pl-k">implements</span> <span class="pl-smi">Retryer</span> {

        <span class="pl-k">private</span> <span class="pl-k">final</span> <span class="pl-smi">long</span> <span class="pl-s1">period</span>;
        <span class="pl-k">private</span> <span class="pl-k">final</span> <span class="pl-smi">int</span> <span class="pl-s1">maxAttempts</span>;
        <span class="pl-k">private</span> <span class="pl-smi">int</span> <span class="pl-s1">attempt</span> = <span class="pl-c1">1</span>;

        <span class="pl-k">public</span> <span class="pl-smi">MyRetryer</span>(<span class="pl-smi">long</span> <span class="pl-s1">period</span>, <span class="pl-smi">int</span> <span class="pl-s1">maxAttempts</span>) {
            <span class="pl-smi">this</span>.<span class="pl-s1">period</span> = <span class="pl-s1">period</span>;
            <span class="pl-smi">this</span>.<span class="pl-s1">maxAttempts</span> = <span class="pl-s1">maxAttempts</span>;
        }

        <span class="pl-c1">@</span><span class="pl-c1">Override</span>
        <span class="pl-k">public</span> <span class="pl-smi">void</span> <span class="pl-en">continueOrPropagate</span>(<span class="pl-smi">RetryableException</span> <span class="pl-s1">e</span>) {
            <span class="pl-k">if</span> (++<span class="pl-s1">attempt</span> &gt; <span class="pl-s1">maxAttempts</span>) {
                <span class="pl-k">throw</span> <span class="pl-s1">e</span>;
            }
            <span class="pl-k">if</span> (<span class="pl-s1">e</span>.<span class="pl-en">status</span>() == <span class="pl-c1">401</span>) {
                <span class="pl-c">// remove Authorization first, otherwise Feign will add a new Authorization header</span>
                <span class="pl-c">// cause github responses a 400 bad request</span>
                <span class="pl-s1">e</span>.<span class="pl-en">request</span>().<span class="pl-en">requestTemplate</span>().<span class="pl-en">removeHeader</span>(<span class="pl-s">"Authorization"</span>);
                <span class="pl-s1">e</span>.<span class="pl-en">request</span>().<span class="pl-en">requestTemplate</span>().<span class="pl-en">header</span>(<span class="pl-s">"Authorization"</span>, <span class="pl-s">"Bearer "</span> + <span class="pl-en">getNewToken</span>());
                <span class="pl-k">try</span> {
                    <span class="pl-smi">Thread</span>.<span class="pl-en">sleep</span>(<span class="pl-s1">period</span>);
                } <span class="pl-k">catch</span> (<span class="pl-smi">InterruptedException</span> <span class="pl-s1">ex</span>) {
                    <span class="pl-k">throw</span> <span class="pl-s1">e</span>;
                }
            } <span class="pl-k">else</span> {
                <span class="pl-k">throw</span> <span class="pl-s1">e</span>;
            }
        }

        <span class="pl-c">// Access an external api to obtain new token</span>
        <span class="pl-c">// In this example, we can simply return a fixed token to demonstrate how Retryer works</span>
        <span class="pl-k">private</span> <span class="pl-smi">String</span> <span class="pl-en">getNewToken</span>() {
            <span class="pl-k">return</span> <span class="pl-s">"newToken"</span>;
        }

        <span class="pl-c1">@</span><span class="pl-c1">Override</span>
        <span class="pl-k">public</span> <span class="pl-smi">Retryer</span> <span class="pl-en">clone</span>() {
            <span class="pl-k">return</span> <span class="pl-k">new</span> <span class="pl-smi">MyRetryer</span>(<span class="pl-s1">period</span>, <span class="pl-s1">maxAttempts</span>);
        }
}</pre><div class="zeroclipboard-container">
    
  </div></div>
<p dir="auto"><code>Retryer</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">负责确定是否应该通过返回 a</font></font><code>true</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">或
</font></font><code>false</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">从方法中进行重试</font><font style="vertical-align: inherit;">。将为每次执行创建</font></font><code>continueOrPropagate(RetryableException e);</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">  一个实例</font><font style="vertical-align: inherit;">，允许您在需要时维护每个请求之间的状态。</font></font><code>Retryer</code><font style="vertical-align: inherit;"></font><code>Client</code><font style="vertical-align: inherit;"></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">如果确定重试不成功，</font></font><code>RetryException</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">则抛出最后一次。要抛出导致重试失败的原始原因，请使用该</font></font><code>exceptionPropagationPolicy()</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">选项构建您的 Feign 客户端。</font></font></p>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">响应拦截器</font></font></h4><a id="user-content-response-interceptor" class="anchor" aria-label="永久链接：响应拦截器" href="#response-interceptor"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">如果您需要将错误视为成功并返回结果而不是抛出异常，那么您可以使用</font></font><code>ResponseInterceptor</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">.</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">作为示例，Feign 包含一个简单</font></font><code>RedirectionInterceptor</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">的可用于从重定向响应中提取位置标头。</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">interface</span> <span class="pl-smi">Api</span> {
  <span class="pl-c">// returns a 302 response</span>
  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"GET /location"</span>)
  <span class="pl-smi">String</span> <span class="pl-en">location</span>();
}

<span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">MyApp</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-c">// Configure the HTTP client to ignore redirection</span>
    <span class="pl-smi">Api</span> <span class="pl-s1">api</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                   .<span class="pl-en">options</span>(<span class="pl-k">new</span> <span class="pl-smi">Options</span>(<span class="pl-c1">10</span>, <span class="pl-smi">TimeUnit</span>.<span class="pl-c1">SECONDS</span>, <span class="pl-c1">60</span>, <span class="pl-smi">TimeUnit</span>.<span class="pl-c1">SECONDS</span>, <span class="pl-c1">false</span>))
                   .<span class="pl-en">responseInterceptor</span>(<span class="pl-k">new</span> <span class="pl-smi">RedirectionInterceptor</span>())
                   .<span class="pl-en">target</span>(<span class="pl-smi">Api</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://redirect.example.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
    
  </div></div>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">指标</font></font></h3><a id="user-content-metrics" class="anchor" aria-label="永久链接：指标" href="#metrics"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">默认情况下，feign 不会收集任何指标。</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">但是，可以向任何假客户端添加指标收集功能。</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">指标功能提供了一流的指标 API，用户可以利用该 API 来深入了解请求/响应生命周期。</font></font></p>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Dropwizard 指标 4</font></font></h4><a id="user-content-dropwizard-metrics-4" class="anchor" aria-label="永久链接：Dropwizard Metrics 4" href="#dropwizard-metrics-4"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<div class="snippet-clipboard-content notranslate position-relative overflow-auto"><pre class="notranslate"><code>public class MyApp {
  public static void main(String[] args) {
    GitHub github = Feign.builder()
                         .addCapability(new Metrics4Capability())
                         .target(GitHub.class, "https://api.github.com");

    github.contributors("OpenFeign", "feign");
    // metrics will be available from this point onwards
  }
}
</code></pre><div class="zeroclipboard-container">
   
  </div></div>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Dropwizard 指标 5</font></font></h4><a id="user-content-dropwizard-metrics-5" class="anchor" aria-label="永久链接：Dropwizard Metrics 5" href="#dropwizard-metrics-5"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<div class="snippet-clipboard-content notranslate position-relative overflow-auto"><pre class="notranslate"><code>public class MyApp {
  public static void main(String[] args) {
    GitHub github = Feign.builder()
                         .addCapability(new Metrics5Capability())
                         .target(GitHub.class, "https://api.github.com");

    github.contributors("OpenFeign", "feign");
    // metrics will be available from this point onwards
  }
}
</code></pre><div class="zeroclipboard-container">
    
  </div></div>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">千分尺</font></font></h4><a id="user-content-micrometer" class="anchor" aria-label="永久链接： 千分尺" href="#micrometer"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<div class="snippet-clipboard-content notranslate position-relative overflow-auto"><pre class="notranslate"><code>public class MyApp {
  public static void main(String[] args) {
    GitHub github = Feign.builder()
                         .addCapability(new MicrometerCapability())
                         .target(GitHub.class, "https://api.github.com");

    github.contributors("OpenFeign", "feign");
    // metrics will be available from this point onwards
  }
}
</code></pre><div class="zeroclipboard-container">
  
  </div></div>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">静态和默认方法</font></font></h4><a id="user-content-static-and-default-methods" class="anchor" aria-label="永久链接：静态和默认方法" href="#static-and-default-methods"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Feign 的目标接口可能具有静态或默认方法（如果使用 Java 8+）。这些允许 Feign 客户端包含底层 API 未明确定义的逻辑。例如，静态方法可以轻松指定常见的客户端构建配置；默认方法可用于编写查询或定义默认参数。</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">interface</span> <span class="pl-smi">GitHub</span> {
  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"GET /repos/{owner}/{repo}/contributors"</span>)
  <span class="pl-smi">List</span>&lt;<span class="pl-smi">Contributor</span>&gt; <span class="pl-en">contributors</span>(<span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"owner"</span>) <span class="pl-smi">String</span> <span class="pl-s1">owner</span>, <span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"repo"</span>) <span class="pl-smi">String</span> <span class="pl-s1">repo</span>);

  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"GET /users/{username}/repos?sort={sort}"</span>)
  <span class="pl-smi">List</span>&lt;<span class="pl-smi">Repo</span>&gt; <span class="pl-en">repos</span>(<span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"username"</span>) <span class="pl-smi">String</span> <span class="pl-s1">owner</span>, <span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"sort"</span>) <span class="pl-smi">String</span> <span class="pl-s1">sort</span>);

  <span class="pl-k">default</span> <span class="pl-smi">List</span>&lt;<span class="pl-smi">Repo</span>&gt; <span class="pl-en">repos</span>(<span class="pl-smi">String</span> <span class="pl-s1">owner</span>) {
    <span class="pl-k">return</span> <span class="pl-en">repos</span>(<span class="pl-s1">owner</span>, <span class="pl-s">"full_name"</span>);
  }

  <span class="pl-c">/**</span>
<span class="pl-c">   * Lists all contributors for all repos owned by a user.</span>
<span class="pl-c">   */</span>
  <span class="pl-k">default</span> <span class="pl-smi">List</span>&lt;<span class="pl-smi">Contributor</span>&gt; <span class="pl-en">contributors</span>(<span class="pl-smi">String</span> <span class="pl-s1">user</span>) {
    <span class="pl-smi">MergingContributorList</span> <span class="pl-s1">contributors</span> = <span class="pl-k">new</span> <span class="pl-smi">MergingContributorList</span>();
    <span class="pl-k">for</span>(<span class="pl-smi">Repo</span> <span class="pl-s1">repo</span> : <span class="pl-smi">this</span>.<span class="pl-en">repos</span>(<span class="pl-s1">owner</span>)) {
      <span class="pl-s1">contributors</span>.<span class="pl-en">addAll</span>(<span class="pl-smi">this</span>.<span class="pl-en">contributors</span>(<span class="pl-s1">user</span>, <span class="pl-s1">repo</span>.<span class="pl-en">getName</span>()));
    }
    <span class="pl-k">return</span> <span class="pl-s1">contributors</span>.<span class="pl-en">mergeResult</span>();
  }

  <span class="pl-k">static</span> <span class="pl-smi">GitHub</span> <span class="pl-en">connect</span>() {
    <span class="pl-k">return</span> <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                .<span class="pl-en">decoder</span>(<span class="pl-k">new</span> <span class="pl-smi">GsonDecoder</span>())
                .<span class="pl-en">target</span>(<span class="pl-smi">GitHub</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.github.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
  
  </div></div>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">异步执行通过</font></font><code>CompletableFuture</code></h3><a id="user-content-async-execution-via-completablefuture" class="anchor" aria-label="永久链接：通过 CompletableFuture 异步执行" href="#async-execution-via-completablefuture"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Feign 10.8 引入了一个新的构建器</font></font><code>AsyncFeign</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">，允许方法返回</font></font><code>CompletableFuture</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">实例。</font></font></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">interface</span> <span class="pl-smi">GitHub</span> {
  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"GET /repos/{owner}/{repo}/contributors"</span>)
  <span class="pl-smi">CompletableFuture</span>&lt;<span class="pl-smi">List</span>&lt;<span class="pl-smi">Contributor</span>&gt;&gt; <span class="pl-en">contributors</span>(<span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"owner"</span>) <span class="pl-smi">String</span> <span class="pl-s1">owner</span>, <span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"repo"</span>) <span class="pl-smi">String</span> <span class="pl-s1">repo</span>);
}

<span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">MyApp</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>... <span class="pl-s1">args</span>) {
    <span class="pl-smi">GitHub</span> <span class="pl-s1">github</span> = <span class="pl-smi">AsyncFeign</span>.<span class="pl-en">builder</span>()
                         .<span class="pl-en">decoder</span>(<span class="pl-k">new</span> <span class="pl-smi">GsonDecoder</span>())
                         .<span class="pl-en">target</span>(<span class="pl-smi">GitHub</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.github.com"</span>);

    <span class="pl-c">// Fetch and print a list of the contributors to this library.</span>
    <span class="pl-smi">CompletableFuture</span>&lt;<span class="pl-smi">List</span>&lt;<span class="pl-smi">Contributor</span>&gt;&gt; <span class="pl-s1">contributors</span> = <span class="pl-s1">github</span>.<span class="pl-en">contributors</span>(<span class="pl-s">"OpenFeign"</span>, <span class="pl-s">"feign"</span>);
    <span class="pl-k">for</span> (<span class="pl-smi">Contributor</span> <span class="pl-s1">contributor</span> : <span class="pl-s1">contributors</span>.<span class="pl-en">get</span>(<span class="pl-c1">1</span>, <span class="pl-smi">TimeUnit</span>.<span class="pl-c1">SECONDS</span>)) {
      <span class="pl-smi">System</span>.<span class="pl-s1">out</span>.<span class="pl-en">println</span>(<span class="pl-s1">contributor</span>.<span class="pl-s1">login</span> + <span class="pl-s">" ("</span> + <span class="pl-s1">contributor</span>.<span class="pl-s1">contributions</span> + <span class="pl-s">")"</span>);
    }
  }
}</pre><div class="zeroclipboard-container">
 
  </div></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">初始实现包括 2 个异步客户端：</font></font></p>
<ul dir="auto">
<li><code>AsyncClient.Default</code></li>
<li><code>AsyncApacheHttp5Client</code></li>
</ul>
<div class="markdown-heading" dir="auto"><h2 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">Maven 的物料清单 (BOM)</font></font></h2><a id="user-content-mavens-bill-of-material-bom" class="anchor" aria-label="永久链接：Maven 的物料清单 (BOM)" href="#mavens-bill-of-material-bom"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">将所有 feign 库保持在同一版本对于避免不兼容的二进制文件至关重要。使用外部依赖项时，确保仅存在一个版本可能很棘手。</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">考虑到这一点，feign build 会生成一个名为 的模块，</font></font><code>feign-bom</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">该模块锁定所有模块的版本</font></font><code>feign-*</code><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">。</font></font></p>
<p dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">物料清单是一个特殊的 POM 文件，它将已知有效并经过测试可协同工作的依赖项版本分组。这将减少开发人员必须测试不同版本兼容性的痛苦，并减少版本不匹配的机会。</font></font></p>
<p dir="auto"><a href="https://repo1.maven.org/maven2/io/github/openfeign/feign-bom/11.9/feign-bom-11.9.pom" rel="nofollow"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">以下</font></font></a><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">是 feign BOM 文件的一个示例。</font></font></p>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto"><font style="vertical-align: inherit;"><font style="vertical-align: inherit;">用法</font></font></h4><a id="user-content-usage-1" class="anchor" aria-label="永久链接：用法" href="#usage-1"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<div class="highlight highlight-text-xml notranslate position-relative overflow-auto" dir="auto"><pre>&lt;<span class="pl-ent">project</span>&gt;

...

  &lt;<span class="pl-ent">dependencyManagement</span>&gt;
    &lt;<span class="pl-ent">dependencies</span>&gt;
      &lt;<span class="pl-ent">dependency</span>&gt;
        &lt;<span class="pl-ent">groupId</span>&gt;io.github.openfeign&lt;/<span class="pl-ent">groupId</span>&gt;
        &lt;<span class="pl-ent">artifactId</span>&gt;feign-bom&lt;/<span class="pl-ent">artifactId</span>&gt;
        &lt;<span class="pl-ent">version</span>&gt;??feign.version??&lt;/<span class="pl-ent">version</span>&gt;
        &lt;<span class="pl-ent">type</span>&gt;pom&lt;/<span class="pl-ent">type</span>&gt;
        &lt;<span class="pl-ent">scope</span>&gt;import&lt;/<span class="pl-ent">scope</span>&gt;
      &lt;/<span class="pl-ent">dependency</span>&gt;
    &lt;/<span class="pl-ent">dependencies</span>&gt;
  &lt;/<span class="pl-ent">dependencyManagement</span>&gt;
&lt;/<span class="pl-ent">project</span>&gt;</pre><div class="zeroclipboard-container">
   
  </div></div>
</article></div>
