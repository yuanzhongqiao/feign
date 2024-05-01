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
<li>Async execution support via <code>CompletableFuture</code>
<ul dir="auto">
<li>Allow for <code>Future</code> chaining and executor management for the request/response lifecycle.  <strong>Implementation will require non-backward-compatible breaking changes</strong>.  However this feature is required before Reactive execution can be considered.</li>
</ul>
</li>
<li>Reactive execution support via <a href="https://www.reactive-streams.org/" rel="nofollow">Reactive Streams</a>
<ul dir="auto">
<li>For JDK 9+, consider a native implementation that uses <code>java.util.concurrent.Flow</code>.</li>
<li>Support for <a href="https://projectreactor.io/" rel="nofollow">Project Reactor</a> and <a href="https://github.com/ReactiveX/RxJava">RxJava 2+</a> implementations on JDK 8.</li>
</ul>
</li>
</ul>
<div class="markdown-heading" dir="auto"><h2 tabindex="-1" class="heading-element" dir="auto">Long Term - The future ☁️</h2><a id="user-content-long-term---the-future-️" class="anchor" aria-label="永久链接：长期 - 未来 ☁️" href="#long-term---the-future-️"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<ul dir="auto">
<li>Additional Circuit Breaker Support.
<ul dir="auto">
<li>Support additional Circuit Breaker implementations like <a href="https://resilience4j.readme.io/" rel="nofollow">Resilience4J</a> and Spring Circuit Breaker</li>
</ul>
</li>
</ul>
<hr>
<div class="markdown-heading" dir="auto"><h1 tabindex="-1" class="heading-element" dir="auto">Usage</h1><a id="user-content-usage" class="anchor" aria-label="永久链接：用法" href="#usage"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto">The feign library is available from <a href="https://central.sonatype.com/artifact/io.github.openfeign/feign-core" rel="nofollow">Maven Central</a>.</p>
<div class="highlight highlight-text-xml notranslate position-relative overflow-auto" dir="auto"><pre>&lt;<span class="pl-ent">dependency</span>&gt;
    &lt;<span class="pl-ent">groupId</span>&gt;io.github.openfeign&lt;/<span class="pl-ent">groupId</span>&gt;
    &lt;<span class="pl-ent">artifactId</span>&gt;feign-core&lt;/<span class="pl-ent">artifactId</span>&gt;
    &lt;<span class="pl-ent">version</span>&gt;??feign.version??&lt;/<span class="pl-ent">version</span>&gt;
&lt;/<span class="pl-ent">dependency</span>&gt;</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="<dependency>
    <groupId>io.github.openfeign</groupId>
    <artifactId>feign-core</artifactId>
    <version>??feign.version??</version>
</dependency>" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon">
    <path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none">
    <path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto">Basics</h3><a id="user-content-basics" class="anchor" aria-label="永久链接：基础知识" href="#basics"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto">Usage typically looks like this, an adaptation of the <a href="https://github.com/square/retrofit/blob/master/samples/src/main/java/com/example/retrofit/SimpleService.java">canonical Retrofit sample</a>.</p>
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
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="interface GitHub {
  @RequestLine(&quot;GET /repos/{owner}/{repo}/contributors&quot;)
  List<Contributor> contributors(@Param(&quot;owner&quot;) String owner, @Param(&quot;repo&quot;) String repo);

  @RequestLine(&quot;POST /repos/{owner}/{repo}/issues&quot;)
  void createIssue(Issue issue, @Param(&quot;owner&quot;) String owner, @Param(&quot;repo&quot;) String repo);

}

public static class Contributor {
  String login;
  int contributions;
}

public static class Issue {
  String title;
  String body;
  List<String> assignees;
  int milestone;
  List<String> labels;
}

public class MyApp {
  public static void main(String... args) {
    GitHub github = Feign.builder()
                         .decoder(new GsonDecoder())
                         .target(GitHub.class, &quot;https://api.github.com&quot;);

    // Fetch and print a list of the contributors to this library.
    List<Contributor> contributors = github.contributors(&quot;OpenFeign&quot;, &quot;feign&quot;);
    for (Contributor contributor : contributors) {
      System.out.println(contributor.login + &quot; (&quot; + contributor.contributions + &quot;)&quot;);
    }
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
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto">Interface Annotations</h3><a id="user-content-interface-annotations" class="anchor" aria-label="永久链接：接口注释" href="#interface-annotations"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto">Feign annotations define the <code>Contract</code> between the interface and how the underlying client
should work.  Feign's default contract defines the following annotations:</p>
<table>
<thead>
<tr>
<th>Annotation</th>
<th>Interface Target</th>
<th>Usage</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>@RequestLine</code></td>
<td>Method</td>
<td>Defines the <code>HttpMethod</code> and <code>UriTemplate</code> for request.  <code>Expressions</code>, values wrapped in curly-braces <code>{expression}</code> are resolved using their corresponding <code>@Param</code> annotated parameters.</td>
</tr>
<tr>
<td><code>@Param</code></td>
<td>Parameter</td>
<td>Defines a template variable, whose value will be used to resolve the corresponding template <code>Expression</code>, by name provided as annotation value. If value is missing it will try to get the name from bytecode method parameter name (if the code was compiled with <code>-parameters</code> flag).</td>
</tr>
<tr>
<td><code>@Headers</code></td>
<td>Method, Type</td>
<td>Defines a <code>HeaderTemplate</code>; a variation on a <code>UriTemplate</code>.  that uses <code>@Param</code> annotated values to resolve the corresponding <code>Expressions</code>.  When used on a <code>Type</code>, the template will be applied to every request.  When used on a <code>Method</code>, the template will apply only to the annotated method.</td>
</tr>
<tr>
<td><code>@QueryMap</code></td>
<td>Parameter</td>
<td>Defines a <code>Map</code> of name-value pairs, or POJO, to expand into a query string.</td>
</tr>
<tr>
<td><code>@HeaderMap</code></td>
<td>Parameter</td>
<td>Defines a <code>Map</code> of name-value pairs, to expand into <code>Http Headers</code></td>
</tr>
<tr>
<td><code>@Body</code></td>
<td>Method</td>
<td>Defines a <code>Template</code>, similar to a <code>UriTemplate</code> and <code>HeaderTemplate</code>, that uses <code>@Param</code> annotated values to resolve the corresponding <code>Expressions</code>.</td>
</tr>
</tbody>
</table>
<blockquote>
<p dir="auto"><strong>Overriding the Request Line</strong></p>
<p dir="auto">If there is a need to target a request to a different host then the one supplied when the Feign client was created, or
you want to supply a target host for each request, include a <code>java.net.URI</code> parameter and Feign will use that value
as the request target.</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"POST /repos/{owner}/{repo}/issues"</span>)
<span class="pl-smi">void</span> <span class="pl-s1">createIssue</span>(<span class="pl-smi">URI</span> <span class="pl-s1">host</span>, <span class="pl-smi">Issue</span> <span class="pl-s1">issue</span>, <span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"owner"</span>) <span class="pl-smi">String</span> <span class="pl-s1">owner</span>, <span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"repo"</span>) <span class="pl-smi">String</span> <span class="pl-s1">repo</span>);</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="@RequestLine(&quot;POST /repos/{owner}/{repo}/issues&quot;)
void createIssue(URI host, Issue issue, @Param(&quot;owner&quot;) String owner, @Param(&quot;repo&quot;) String repo);" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon">
    <path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none">
    <path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path>
</svg>
    </clipboard-copy>
  </div></div>
</blockquote>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto">Templates and Expressions</h3><a id="user-content-templates-and-expressions" class="anchor" aria-label="永久链接：模板和表达式" href="#templates-and-expressions"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto">Feign <code>Expressions</code> represent Simple String Expressions (Level 1) as defined by <a href="https://tools.ietf.org/html/rfc6570" rel="nofollow">URI Template - RFC 6570</a>.  <code>Expressions</code> are expanded using
their corresponding <code>Param</code> annotated method parameters.</p>
<p dir="auto"><em>Example</em></p>
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
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public interface GitHub {

  @RequestLine(&quot;GET /repos/{owner}/{repo}/contributors&quot;)
  List<Contributor> contributors(@Param(&quot;owner&quot;) String owner, @Param(&quot;repo&quot;) String repository);

  class Contributor {
    String login;
    int contributions;
  }
}

public class MyApp {
  public static void main(String[] args) {
    GitHub github = Feign.builder()
                         .decoder(new GsonDecoder())
                         .target(GitHub.class, &quot;https://api.github.com&quot;);

    /* The owner and repository parameters will be used to expand the owner and repo expressions
     * defined in the RequestLine.
     *
     * the resulting uri will be https://api.github.com/repos/OpenFeign/feign/contributors
     */
    github.contributors(&quot;OpenFeign&quot;, &quot;feign&quot;);
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
<p dir="auto">Expressions must be enclosed in curly braces <code>{}</code> and may contain regular expression patterns, separated by a colon <code>:</code>  to restrict
resolved values.  <em>Example</em> <code>owner</code> must be alphabetic. <code>{owner:[a-zA-Z]*}</code></p>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">Request Parameter Expansion</h4><a id="user-content-request-parameter-expansion" class="anchor" aria-label="永久链接：请求参数扩展" href="#request-parameter-expansion"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><code>RequestLine</code> and <code>QueryMap</code> templates follow the <a href="https://tools.ietf.org/html/rfc6570" rel="nofollow">URI Template - RFC 6570</a> specification for Level 1 templates, which specifies the following:</p>
<ul dir="auto">
<li>Unresolved expressions are omitted.</li>
<li>All literals and variable values are pct-encoded, if not already encoded or marked <code>encoded</code> via a <code>@Param</code> annotation.</li>
</ul>
<p dir="auto">We also have limited support for Level 3, Path Style Expressions, with the following restrictions:</p>
<ul dir="auto">
<li>Maps and Lists are expanded by default.</li>
<li>Only Single variable templates are supported.</li>
</ul>
<p dir="auto"><em>Examples:</em></p>
<div class="snippet-clipboard-content notranslate position-relative overflow-auto"><pre class="notranslate"><code>{;who}             ;who=fred
{;half}            ;half=50%25
{;empty}           ;empty
{;list}            ;list=red;list=green;list=blue
{;map}             ;semi=%3B;dot=.;comma=%2C
</code></pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="{;who}             ;who=fred
{;half}            ;half=50%25
{;empty}           ;empty
{;list}            ;list=red;list=green;list=blue
{;map}             ;semi=%3B;dot=.;comma=%2C" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon">
    <path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none">
    <path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">interface</span> <span class="pl-smi">MatrixService</span> {

  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"GET /repos{;owners}"</span>)
  <span class="pl-smi">List</span>&lt;<span class="pl-smi">Contributor</span>&gt; <span class="pl-en">contributors</span>(<span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"owners"</span>) <span class="pl-smi">List</span>&lt;<span class="pl-smi">String</span>&gt; <span class="pl-s1">owners</span>);

  <span class="pl-k">class</span> <span class="pl-smi">Contributor</span> {
    <span class="pl-smi">String</span> <span class="pl-s1">login</span>;
    <span class="pl-smi">int</span> <span class="pl-s1">contributions</span>;
  }
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public interface MatrixService {

  @RequestLine(&quot;GET /repos{;owners}&quot;)
  List<Contributor> contributors(@Param(&quot;owners&quot;) List<String> owners);

  class Contributor {
    String login;
    int contributions;
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
<p dir="auto">If <code>owners</code> in the above example is defined as <code>Matt, Jeff, Susan</code>, the uri will expand to <code>/repos;owners=Matt;owners=Jeff;owners=Susan</code></p>
<p dir="auto">For more information see <a href="https://datatracker.ietf.org/doc/html/rfc6570#section-3.2.7" rel="nofollow">RFC 6570, Section 3.2.7</a></p>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">Undefined vs. Empty Values</h4><a id="user-content-undefined-vs-empty-values" class="anchor" aria-label="永久链接：未定义与空值" href="#undefined-vs-empty-values"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto">Undefined expressions are expressions where the value for the expression is an explicit <code>null</code> or no value is provided.
Per <a href="https://tools.ietf.org/html/rfc6570" rel="nofollow">URI Template - RFC 6570</a>, it is possible to provide an empty value
for an expression.  When Feign resolves an expression, it first determines if the value is defined, if it is then
the query parameter will remain.  If the expression is undefined, the query parameter is removed.  See below
for a complete breakdown.</p>
<p dir="auto"><em>Empty String</em></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-smi">void</span> <span class="pl-s1">test</span>() {
   <span class="pl-smi">Map</span>&lt;<span class="pl-smi">String</span>, <span class="pl-smi">Object</span>&gt; <span class="pl-s1">parameters</span> = <span class="pl-k">new</span> <span class="pl-smi">LinkedHashMap</span>&lt;&gt;();
   <span class="pl-s1">parameters</span>.<span class="pl-en">put</span>(<span class="pl-s">"param"</span>, <span class="pl-s">""</span>);
   <span class="pl-smi">this</span>.<span class="pl-s1">demoClient</span>.<span class="pl-en">test</span>(<span class="pl-s1">parameters</span>);
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public void test() {
   Map<String, Object> parameters = new LinkedHashMap<>();
   parameters.put(&quot;param&quot;, &quot;&quot;);
   this.demoClient.test(parameters);
}" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon">
    <path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none">
    <path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<p dir="auto">Result</p>
<div class="snippet-clipboard-content notranslate position-relative overflow-auto"><pre class="notranslate"><code>http://localhost:8080/test?param=
</code></pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="http://localhost:8080/test?param=" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon">
    <path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none">
    <path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<p dir="auto"><em>Missing</em></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-smi">void</span> <span class="pl-s1">test</span>() {
   <span class="pl-smi">Map</span>&lt;<span class="pl-smi">String</span>, <span class="pl-smi">Object</span>&gt; <span class="pl-s1">parameters</span> = <span class="pl-k">new</span> <span class="pl-smi">LinkedHashMap</span>&lt;&gt;();
   <span class="pl-smi">this</span>.<span class="pl-s1">demoClient</span>.<span class="pl-en">test</span>(<span class="pl-s1">parameters</span>);
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public void test() {
   Map<String, Object> parameters = new LinkedHashMap<>();
   this.demoClient.test(parameters);
}" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon">
    <path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none">
    <path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<p dir="auto">Result</p>
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
<p dir="auto"><em>Undefined</em></p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-smi">void</span> <span class="pl-s1">test</span>() {
   <span class="pl-smi">Map</span>&lt;<span class="pl-smi">String</span>, <span class="pl-smi">Object</span>&gt; <span class="pl-s1">parameters</span> = <span class="pl-k">new</span> <span class="pl-smi">LinkedHashMap</span>&lt;&gt;();
   <span class="pl-s1">parameters</span>.<span class="pl-en">put</span>(<span class="pl-s">"param"</span>, <span class="pl-c1">null</span>);
   <span class="pl-smi">this</span>.<span class="pl-s1">demoClient</span>.<span class="pl-en">test</span>(<span class="pl-s1">parameters</span>);
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public void test() {
   Map<String, Object> parameters = new LinkedHashMap<>();
   parameters.put(&quot;param&quot;, null);
   this.demoClient.test(parameters);
}" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon">
    <path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none">
    <path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<p dir="auto">Result</p>
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
<p dir="auto">See <a href="#advanced-usage">Advanced Usage</a> for more examples.</p>
<blockquote>
<p dir="auto"><strong>What about slashes? <code>/</code></strong></p>
<p dir="auto">@RequestLine templates do not encode slash <code>/</code> characters by default.  To change this behavior, set the <code>decodeSlash</code> property on the <code>@RequestLine</code> to <code>false</code>.</p>
</blockquote>
<blockquote>
<p dir="auto"><strong>What about plus? <code>+</code></strong></p>
<p dir="auto">Per the URI specification, a <code>+</code> sign is allowed in both the path and query segments of a URI, however, handling of
the symbol on the query can be inconsistent.  In some legacy systems, the <code>+</code> is equivalent to the a space.  Feign takes the approach of modern systems, where a
<code>+</code> symbol should not represent a space and is explicitly encoded as <code>%2B</code> when found on a query string.</p>
<p dir="auto">If you wish to use <code>+</code> as a space, then use the literal <code> </code> character or encode the value directly as <code>%20</code></p>
</blockquote>
<div class="markdown-heading" dir="auto"><h5 tabindex="-1" class="heading-element" dir="auto">Custom Expansion</h5><a id="user-content-custom-expansion" class="anchor" aria-label="永久链接：自定义扩展" href="#custom-expansion"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto">The <code>@Param</code> annotation has an optional property <code>expander</code> allowing for complete control over the individual parameter's expansion.
The <code>expander</code> property must reference a class that implements the <code>Expander</code> interface:</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">interface</span> <span class="pl-smi">Expander</span> {
    <span class="pl-smi">String</span> <span class="pl-en">expand</span>(<span class="pl-smi">Object</span> <span class="pl-s1">value</span>);
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public interface Expander {
    String expand(Object value);
}" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon">
    <path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none">
    <path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<p dir="auto">The result of this method adheres to the same rules stated above.  If the result is <code>null</code> or an empty string,
the value is omitted.  If the value is not pct-encoded, it will be.  See <a href="#custom-param-expansion">Custom @Param Expansion</a> for more examples.</p>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">Request Headers Expansion</h4><a id="user-content-request-headers-expansion" class="anchor" aria-label="永久链接：请求标头扩展" href="#request-headers-expansion"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><code>Headers</code> and <code>HeaderMap</code> templates follow the same rules as <a href="#request-parameter-expansion">Request Parameter Expansion</a>
with the following alterations:</p>
<ul dir="auto">
<li>Unresolved expressions are omitted.  If the result is an empty header value, the entire header is removed.</li>
<li>No pct-encoding is performed.</li>
</ul>
<p dir="auto">See <a href="#headers">Headers</a> for examples.</p>
<blockquote>
<p dir="auto"><strong>A Note on <code>@Param</code> parameters and their names</strong>:</p>
<p dir="auto">All expressions with the same name, regardless of their position on the <code>@RequestLine</code>, <code>@QueryMap</code>, <code>@BodyTemplate</code>, or <code>@Headers</code> will resolve to the same value.
In the following example, the value of <code>contentType</code>, will be used to resolve both the header and path expression:</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">interface</span> <span class="pl-smi">ContentService</span> {
  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"GET /api/documents/{contentType}"</span>)
  <span class="pl-c1">@</span><span class="pl-c1">Headers</span>(<span class="pl-s">"Accept: {contentType}"</span>)
  <span class="pl-smi">String</span> <span class="pl-en">getDocumentByType</span>(<span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"contentType"</span>) <span class="pl-smi">String</span> <span class="pl-s1">type</span>);
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public interface ContentService {
  @RequestLine(&quot;GET /api/documents/{contentType}&quot;)
  @Headers(&quot;Accept: {contentType}&quot;)
  String getDocumentByType(@Param(&quot;contentType&quot;) String type);
}" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon">
    <path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none">
    <path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<p dir="auto">Keep this in mind when designing your interfaces.</p>
</blockquote>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">Request Body Expansion</h4><a id="user-content-request-body-expansion" class="anchor" aria-label="永久链接：请求正文扩展" href="#request-body-expansion"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><code>Body</code> templates follow the same rules as <a href="#request-parameter-expansion">Request Parameter Expansion</a>
with the following alterations:</p>
<ul dir="auto">
<li>Unresolved expressions are omitted.</li>
<li>Expanded value will <strong>not</strong> be passed through an <code>Encoder</code> before being placed on the request body.</li>
<li>A <code>Content-Type</code> header must be specified.  See <a href="#body-templates">Body Templates</a> for examples.</li>
</ul>
<hr>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto">Customization</h3><a id="user-content-customization" class="anchor" aria-label="固定链接：定制" href="#customization"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto">Feign has several aspects that can be customized.<br>
For simple cases, you can use <code>Feign.builder()</code> to construct an API interface with your custom components.<br>
For request setting, you can use <code>options(Request.Options options)</code> on <code>target()</code> to set connectTimeout, connectTimeoutUnit, readTimeout, readTimeoutUnit, followRedirects.<br>
For example:</p>
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
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="interface Bank {
  @RequestLine(&quot;POST /account/{id}&quot;)
  Account getAccountInfo(@Param(&quot;id&quot;) String id);
}

public class BankService {
  public static void main(String[] args) {
    Bank bank = Feign.builder()
        .decoder(new AccountDecoder())
        .options(new Request.Options(10, TimeUnit.SECONDS, 60, TimeUnit.SECONDS, true))
        .target(Bank.class, &quot;https://api.examplebank.com&quot;);
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
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto">Multiple Interfaces</h3><a id="user-content-multiple-interfaces" class="anchor" aria-label="永久链接：多个接口" href="#multiple-interfaces"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto">Feign can produce multiple api interfaces.  These are defined as <code>Target&lt;T&gt;</code> (default <code>HardCodedTarget&lt;T&gt;</code>), which allow for dynamic discovery and decoration of requests prior to execution.</p>
<p dir="auto">For example, the following pattern might decorate each request with the current url and auth token from the identity service.</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">CloudService</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">CloudDNS</span> <span class="pl-s1">cloudDNS</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
      .<span class="pl-en">target</span>(<span class="pl-k">new</span> <span class="pl-smi">CloudIdentityTarget</span>&lt;<span class="pl-smi">CloudDNS</span>&gt;(<span class="pl-s1">user</span>, <span class="pl-s1">apiKey</span>));
  }

  <span class="pl-k">class</span> <span class="pl-smi">CloudIdentityTarget</span> <span class="pl-k">extends</span> <span class="pl-smi">Target</span>&lt;<span class="pl-smi">CloudDNS</span>&gt; {
    <span class="pl-c">/* implementation of a Target */</span>
  }
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public class CloudService {
  public static void main(String[] args) {
    CloudDNS cloudDNS = Feign.builder()
      .target(new CloudIdentityTarget<CloudDNS>(user, apiKey));
  }

  class CloudIdentityTarget extends Target<CloudDNS> {
    /* implementation of a Target */
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
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto">Examples</h3><a id="user-content-examples" class="anchor" aria-label="永久链接：示例" href="#examples"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto">Feign includes example <a href="/OpenFeign/feign/blob/master/example-github">GitHub</a> and <a href="/OpenFeign/feign/blob/master/example-wikipedia">Wikipedia</a> clients. The denominator project can also be scraped for Feign in practice. Particularly, look at its <a href="https://github.com/Netflix/denominator/tree/master/example-daemon">example daemon</a>.</p>
<hr>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto">Integrations</h3><a id="user-content-integrations" class="anchor" aria-label="永久链接：集成" href="#integrations"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto">Feign intends to work well with other Open Source tools.  Modules are welcome to integrate with your favorite projects!</p>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto">Encoder/Decoder</h3><a id="user-content-encoderdecoder" class="anchor" aria-label="永久链接：编码器/解码器" href="#encoderdecoder"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">Gson</h4><a id="user-content-gson" class="anchor" aria-label="永久链接：Gson" href="#gson"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><a href="/OpenFeign/feign/blob/master/gson">Gson</a> includes an encoder and decoder you can use with a JSON API.</p>
<p dir="auto">Add <code>GsonEncoder</code> and/or <code>GsonDecoder</code> to your <code>Feign.Builder</code> like so:</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">GsonCodec</span> <span class="pl-s1">codec</span> = <span class="pl-k">new</span> <span class="pl-smi">GsonCodec</span>();
    <span class="pl-smi">GitHub</span> <span class="pl-s1">github</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                         .<span class="pl-en">encoder</span>(<span class="pl-k">new</span> <span class="pl-smi">GsonEncoder</span>())
                         .<span class="pl-en">decoder</span>(<span class="pl-k">new</span> <span class="pl-smi">GsonDecoder</span>())
                         .<span class="pl-en">target</span>(<span class="pl-smi">GitHub</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.github.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public class Example {
  public static void main(String[] args) {
    GsonCodec codec = new GsonCodec();
    GitHub github = Feign.builder()
                         .encoder(new GsonEncoder())
                         .decoder(new GsonDecoder())
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
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">Jackson</h4><a id="user-content-jackson" class="anchor" aria-label="永久链接：杰克逊" href="#jackson"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><a href="/OpenFeign/feign/blob/master/jackson">Jackson</a> includes an encoder and decoder you can use with a JSON API.</p>
<p dir="auto">Add <code>JacksonEncoder</code> and/or <code>JacksonDecoder</code> to your <code>Feign.Builder</code> like so:</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
      <span class="pl-smi">GitHub</span> <span class="pl-s1">github</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                     .<span class="pl-en">encoder</span>(<span class="pl-k">new</span> <span class="pl-smi">JacksonEncoder</span>())
                     .<span class="pl-en">decoder</span>(<span class="pl-k">new</span> <span class="pl-smi">JacksonDecoder</span>())
                     .<span class="pl-en">target</span>(<span class="pl-smi">GitHub</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.github.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public class Example {
  public static void main(String[] args) {
      GitHub github = Feign.builder()
                     .encoder(new JacksonEncoder())
                     .decoder(new JacksonDecoder())
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
<p dir="auto">For the lighter weight Jackson Jr, use <code>JacksonJrEncoder</code> and <code>JacksonJrDecoder</code> from
the <a href="/OpenFeign/feign/blob/master/jackson-jr">Jackson Jr Module</a>.</p>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">Moshi</h4><a id="user-content-moshi" class="anchor" aria-label="永久链接：莫西" href="#moshi"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><a href="/OpenFeign/feign/blob/master/moshi">Moshi</a> includes an encoder and decoder you can use with a JSON API.
Add <code>MoshiEncoder</code> and/or <code>MoshiDecoder</code> to your <code>Feign.Builder</code> like so:</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-smi">GitHub</span> <span class="pl-s1">github</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                     .<span class="pl-en">encoder</span>(<span class="pl-k">new</span> <span class="pl-smi">MoshiEncoder</span>())
                     .<span class="pl-en">decoder</span>(<span class="pl-k">new</span> <span class="pl-smi">MoshiDecoder</span>())
                     .<span class="pl-en">target</span>(<span class="pl-smi">GitHub</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.github.com"</span>);</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="GitHub github = Feign.builder()
                     .encoder(new MoshiEncoder())
                     .decoder(new MoshiDecoder())
                     .target(GitHub.class, &quot;https://api.github.com&quot;);" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon">
    <path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none">
    <path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">Sax</h4><a id="user-content-sax" class="anchor" aria-label="永久链接：萨克斯" href="#sax"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><a href="/OpenFeign/feign/blob/master/sax">SaxDecoder</a> allows you to decode XML in a way that is compatible with normal JVM and also Android environments.</p>
<p dir="auto">Here's an example of how to configure Sax response parsing:</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
      <span class="pl-smi">Api</span> <span class="pl-s1">api</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
         .<span class="pl-en">decoder</span>(<span class="pl-smi">SAXDecoder</span>.<span class="pl-en">builder</span>()
                            .<span class="pl-en">registerContentHandler</span>(<span class="pl-smi">UserIdHandler</span>.<span class="pl-k">class</span>)
                            .<span class="pl-en">build</span>())
         .<span class="pl-en">target</span>(<span class="pl-smi">Api</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://apihost"</span>);
    }
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public class Example {
  public static void main(String[] args) {
      Api api = Feign.builder()
         .decoder(SAXDecoder.builder()
                            .registerContentHandler(UserIdHandler.class)
                            .build())
         .target(Api.class, &quot;https://apihost&quot;);
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
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">JAXB</h4><a id="user-content-jaxb" class="anchor" aria-label="永久链接：JAXB" href="#jaxb"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><a href="/OpenFeign/feign/blob/master/jaxb">JAXB</a> includes an encoder and decoder you can use with an XML API.</p>
<p dir="auto">Add <code>JAXBEncoder</code> and/or <code>JAXBDecoder</code> to your <code>Feign.Builder</code> like so:</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">Api</span> <span class="pl-s1">api</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
             .<span class="pl-en">encoder</span>(<span class="pl-k">new</span> <span class="pl-smi">JAXBEncoder</span>())
             .<span class="pl-en">decoder</span>(<span class="pl-k">new</span> <span class="pl-smi">JAXBDecoder</span>())
             .<span class="pl-en">target</span>(<span class="pl-smi">Api</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://apihost"</span>);
  }
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public class Example {
  public static void main(String[] args) {
    Api api = Feign.builder()
             .encoder(new JAXBEncoder())
             .decoder(new JAXBDecoder())
             .target(Api.class, &quot;https://apihost&quot;);
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
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">SOAP</h4><a id="user-content-soap" class="anchor" aria-label="永久链接： 肥皂" href="#soap"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><a href="/OpenFeign/feign/blob/master/soap">SOAP</a> includes an encoder and decoder you can use with an XML API.</p>
<p dir="auto">This module adds support for encoding and decoding SOAP Body objects via JAXB and SOAPMessage. It also provides SOAPFault decoding capabilities by wrapping them into the original <code>javax.xml.ws.soap.SOAPFaultException</code>, so that you'll only need to catch <code>SOAPFaultException</code> in order to handle SOAPFault.</p>
<p dir="auto">Add <code>SOAPEncoder</code> and/or <code>SOAPDecoder</code> to your <code>Feign.Builder</code> like so:</p>
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
<p dir="auto">NB: you may also need to add <code>SOAPErrorDecoder</code> if SOAP Faults are returned in response with error http codes (4xx, 5xx, ...)</p>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">Fastjson2</h4><a id="user-content-fastjson2" class="anchor" aria-label="永久链接：Fastjson2" href="#fastjson2"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><a href="/OpenFeign/feign/blob/master/fastjson2">fastjson2</a> includes an encoder and decoder you can use with a JSON API.</p>
<p dir="auto">Add <code>Fastjson2Encoder</code> and/or <code>Fastjson2Decoder</code> to your <code>Feign.Builder</code> like so:</p>
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
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto">Contract</h3><a id="user-content-contract" class="anchor" aria-label="永久链接：合同" href="#contract"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">JAX-RS</h4><a id="user-content-jax-rs" class="anchor" aria-label="永久链接：JAX-RS" href="#jax-rs"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><a href="/OpenFeign/feign/blob/master/jaxrs">JAXRSContract</a> overrides annotation processing to instead use standard ones supplied by the JAX-RS specification.  This is currently targeted at the 1.1 spec.</p>
<p dir="auto">Here's the example above re-written to use JAX-RS:</p>
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
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto">Client</h3><a id="user-content-client" class="anchor" aria-label="永久链接： 客户端" href="#client"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">OkHttp</h4><a id="user-content-okhttp" class="anchor" aria-label="永久链接：OkHttp" href="#okhttp"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><a href="/OpenFeign/feign/blob/master/okhttp">OkHttpClient</a> directs Feign's http requests to <a href="http://square.github.io/okhttp/" rel="nofollow">OkHttp</a>, which enables SPDY and better network control.</p>
<p dir="auto">To use OkHttp with Feign, add the OkHttp module to your classpath. Then, configure Feign to use the OkHttpClient:</p>
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
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">Ribbon</h4><a id="user-content-ribbon" class="anchor" aria-label="永久链接： 丝带" href="#ribbon"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><a href="/OpenFeign/feign/blob/master/ribbon">RibbonClient</a> overrides URL resolution of Feign's client, adding smart routing and resiliency capabilities provided by <a href="https://github.com/Netflix/ribbon">Ribbon</a>.</p>
<p dir="auto">Integration requires you to pass your ribbon client name as the host part of the url, for example <code>myAppProd</code>.</p>
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
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">Java 11 Http2</h4><a id="user-content-java-11-http2" class="anchor" aria-label="永久链接：Java 11 Http2" href="#java-11-http2"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><a href="/OpenFeign/feign/blob/master/java11">Http2Client</a> directs Feign's http requests to Java11 <a href="https://openjdk.java.net/jeps/321" rel="nofollow">New HTTP/2 Client</a> that implements HTTP/2.</p>
<p dir="auto">To use New HTTP/2 Client with Feign, use Java SDK 11. Then, configure Feign to use the Http2Client:</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-smi">GitHub</span> <span class="pl-s1">github</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                     .<span class="pl-en">client</span>(<span class="pl-k">new</span> <span class="pl-smi">Http2Client</span>())
                     .<span class="pl-en">target</span>(<span class="pl-smi">GitHub</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.github.com"</span>);</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="GitHub github = Feign.builder()
                     .client(new Http2Client())
                     .target(GitHub.class, &quot;https://api.github.com&quot;);" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon">
    <path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none">
    <path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto">Breaker</h3><a id="user-content-breaker" class="anchor" aria-label="永久链接：断路器" href="#breaker"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">Hystrix</h4><a id="user-content-hystrix" class="anchor" aria-label="永久链接：Hystrix" href="#hystrix"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><a href="/OpenFeign/feign/blob/master/hystrix">HystrixFeign</a> configures circuit breaker support provided by <a href="https://github.com/Netflix/Hystrix">Hystrix</a>.</p>
<p dir="auto">To use Hystrix with Feign, add the Hystrix module to your classpath. Then use the <code>HystrixFeign</code> builder:</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">MyService</span> <span class="pl-s1">api</span> = <span class="pl-smi">HystrixFeign</span>.<span class="pl-en">builder</span>().<span class="pl-en">target</span>(<span class="pl-smi">MyService</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://myAppProd"</span>);
  }
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public class Example {
  public static void main(String[] args) {
    MyService api = HystrixFeign.builder().target(MyService.class, &quot;https://myAppProd&quot;);
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
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto">Logger</h3><a id="user-content-logger" class="anchor" aria-label="永久链接：记录器" href="#logger"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">SLF4J</h4><a id="user-content-slf4j" class="anchor" aria-label="永久链接：SLF4J" href="#slf4j"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><a href="/OpenFeign/feign/blob/master/slf4j">SLF4JModule</a> allows directing Feign's logging to <a href="http://www.slf4j.org/" rel="nofollow">SLF4J</a>, allowing you to easily use a logging backend of your choice (Logback, Log4J, etc.)</p>
<p dir="auto">To use SLF4J with Feign, add both the SLF4J module and an SLF4J binding of your choice to your classpath.  Then, configure Feign to use the Slf4jLogger:</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">GitHub</span> <span class="pl-s1">github</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                     .<span class="pl-en">logger</span>(<span class="pl-k">new</span> <span class="pl-smi">Slf4jLogger</span>())
                     .<span class="pl-en">logLevel</span>(<span class="pl-smi">Level</span>.<span class="pl-c1">FULL</span>)
                     .<span class="pl-en">target</span>(<span class="pl-smi">GitHub</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.github.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public class Example {
  public static void main(String[] args) {
    GitHub github = Feign.builder()
                     .logger(new Slf4jLogger())
                     .logLevel(Level.FULL)
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
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto">Decoders</h3><a id="user-content-decoders" class="anchor" aria-label="永久链接：解码器" href="#decoders"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto"><code>Feign.builder()</code> allows you to specify additional configuration such as how to decode a response.</p>
<p dir="auto">If any methods in your interface return types besides <code>Response</code>, <code>String</code>, <code>byte[]</code> or <code>void</code>, you'll need to configure a non-default <code>Decoder</code>.</p>
<p dir="auto">Here's how to configure JSON decoding (using the <code>feign-gson</code> extension):</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">GitHub</span> <span class="pl-s1">github</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                     .<span class="pl-en">decoder</span>(<span class="pl-k">new</span> <span class="pl-smi">GsonDecoder</span>())
                     .<span class="pl-en">target</span>(<span class="pl-smi">GitHub</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.github.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public class Example {
  public static void main(String[] args) {
    GitHub github = Feign.builder()
                     .decoder(new GsonDecoder())
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
<p dir="auto">If you need to pre-process the response before give it to the Decoder, you can use the <code>mapAndDecode</code> builder method.
An example use case is dealing with an API that only serves jsonp, you will maybe need to unwrap the jsonp before
send it to the Json decoder of your choice:</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">JsonpApi</span> <span class="pl-s1">jsonpApi</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                         .<span class="pl-en">mapAndDecode</span>((<span class="pl-s1">response</span>, <span class="pl-s1">type</span>) -&gt; <span class="pl-en">jsopUnwrap</span>(<span class="pl-s1">response</span>, <span class="pl-s1">type</span>), <span class="pl-k">new</span> <span class="pl-smi">GsonDecoder</span>())
                         .<span class="pl-en">target</span>(<span class="pl-smi">JsonpApi</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://some-jsonp-api.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public class Example {
  public static void main(String[] args) {
    JsonpApi jsonpApi = Feign.builder()
                         .mapAndDecode((response, type) -> jsopUnwrap(response, type), new GsonDecoder())
                         .target(JsonpApi.class, &quot;https://some-jsonp-api.com&quot;);
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
<p dir="auto">If any methods in your interface return type <code>Stream</code>, you'll need to configure a <code>StreamDecoder</code>.</p>
<p dir="auto">Here's how to configure Stream decoder without delegate decoder:</p>
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
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public class Example {
  public static void main(String[] args) {
    GitHub github = Feign.builder()
            .decoder(StreamDecoder.create((r, t) -> {
              BufferedReader bufferedReader = new BufferedReader(r.body().asReader(UTF_8));
              return bufferedReader.lines().iterator();
            }))
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
<p dir="auto">Here's how to configure Stream decoder with delegate decoder:</p>
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
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="
public class Example {
  public static void main(String[] args) {
    GitHub github = Feign.builder()
            .decoder(StreamDecoder.create((r, t) -> {
              BufferedReader bufferedReader = new BufferedReader(r.body().asReader(UTF_8));
              return bufferedReader.lines().iterator();
            }, (r, t) -> &quot;this is delegate decoder&quot;))
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
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto">Encoders</h3><a id="user-content-encoders" class="anchor" aria-label="永久链接：编码器" href="#encoders"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto">The simplest way to send a request body to a server is to define a <code>POST</code> method that has a <code>String</code> or <code>byte[]</code> parameter without any annotations on it. You will likely need to add a <code>Content-Type</code> header.</p>
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
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="interface LoginClient {
  @RequestLine(&quot;POST /&quot;)
  @Headers(&quot;Content-Type: application/json&quot;)
  void login(String content);
}

public class Example {
  public static void main(String[] args) {
    client.login(&quot;{\&quot;user_name\&quot;: \&quot;denominator\&quot;, \&quot;password\&quot;: \&quot;secret\&quot;}&quot;);
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
<p dir="auto">By configuring an <code>Encoder</code>, you can send a type-safe request body. Here's an example using the <code>feign-gson</code> extension:</p>
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
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="static class Credentials {
  final String user_name;
  final String password;

  Credentials(String user_name, String password) {
    this.user_name = user_name;
    this.password = password;
  }
}

interface LoginClient {
  @RequestLine(&quot;POST /&quot;)
  void login(Credentials creds);
}

public class Example {
  public static void main(String[] args) {
    LoginClient client = Feign.builder()
                              .encoder(new GsonEncoder())
                              .target(LoginClient.class, &quot;https://foo.com&quot;);

    client.login(new Credentials(&quot;denominator&quot;, &quot;secret&quot;));
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
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto">@Body templates</h3><a id="user-content-body-templates" class="anchor" aria-label="永久链接：@Body 模板" href="#body-templates"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto">The <code>@Body</code> annotation indicates a template to expand using parameters annotated with <code>@Param</code>. You will likely need to add a <code>Content-Type</code> header.</p>
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
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="interface LoginClient {

  @RequestLine(&quot;POST /&quot;)
  @Headers(&quot;Content-Type: application/xml&quot;)
  @Body(&quot;<login \&quot;user_name\&quot;=\&quot;{user_name}\&quot; \&quot;password\&quot;=\&quot;{password}\&quot;/>&quot;)
  void xml(@Param(&quot;user_name&quot;) String user, @Param(&quot;password&quot;) String password);

  @RequestLine(&quot;POST /&quot;)
  @Headers(&quot;Content-Type: application/json&quot;)
  // json curly braces must be escaped!
  @Body(&quot;%7B\&quot;user_name\&quot;: \&quot;{user_name}\&quot;, \&quot;password\&quot;: \&quot;{password}\&quot;%7D&quot;)
  void json(@Param(&quot;user_name&quot;) String user, @Param(&quot;password&quot;) String password);
}

public class Example {
  public static void main(String[] args) {
    client.xml(&quot;denominator&quot;, &quot;secret&quot;); // <login &quot;user_name&quot;=&quot;denominator&quot; &quot;password&quot;=&quot;secret&quot;/>
    client.json(&quot;denominator&quot;, &quot;secret&quot;); // {&quot;user_name&quot;: &quot;denominator&quot;, &quot;password&quot;: &quot;secret&quot;}
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
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto">Headers</h3><a id="user-content-headers" class="anchor" aria-label="固定链接：标题" href="#headers"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto">Feign supports settings headers on requests either as part of the api or as part of the client
depending on the use case.</p>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">Set headers using apis</h4><a id="user-content-set-headers-using-apis" class="anchor" aria-label="永久链接：使用 api 设置标头" href="#set-headers-using-apis"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto">In cases where specific interfaces or calls should always have certain header values set, it
makes sense to define headers as part of the api.</p>
<p dir="auto">Static headers can be set on an api interface or method using the <code>@Headers</code> annotation.</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-c1">@</span><span class="pl-c1">Headers</span>(<span class="pl-s">"Accept: application/json"</span>)
<span class="pl-k">interface</span> <span class="pl-smi">BaseApi</span>&lt;<span class="pl-smi">V</span>&gt; {
  <span class="pl-c1">@</span><span class="pl-c1">Headers</span>(<span class="pl-s">"Content-Type: application/json"</span>)
  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"PUT /api/{key}"</span>)
  <span class="pl-smi">void</span> <span class="pl-en">put</span>(<span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"key"</span>) <span class="pl-smi">String</span> <span class="pl-s1">key</span>, <span class="pl-smi">V</span> <span class="pl-s1">value</span>);
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="@Headers(&quot;Accept: application/json&quot;)
interface BaseApi<V> {
  @Headers(&quot;Content-Type: application/json&quot;)
  @RequestLine(&quot;PUT /api/{key}&quot;)
  void put(@Param(&quot;key&quot;) String key, V value);
}" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon">
    <path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none">
    <path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<p dir="auto">Methods can specify dynamic content for static headers using variable expansion in <code>@Headers</code>.</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">interface</span> <span class="pl-smi">Api</span> {
   <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"POST /"</span>)
   <span class="pl-c1">@</span><span class="pl-c1">Headers</span>(<span class="pl-s">"X-Ping: {token}"</span>)
   <span class="pl-smi">void</span> <span class="pl-en">post</span>(<span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s">"token"</span>) <span class="pl-smi">String</span> <span class="pl-s1">token</span>);
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public interface Api {
   @RequestLine(&quot;POST /&quot;)
   @Headers(&quot;X-Ping: {token}&quot;)
   void post(@Param(&quot;token&quot;) String token);
}" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon">
    <path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none">
    <path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<p dir="auto">In cases where both the header field keys and values are dynamic and the range of possible keys cannot
be known ahead of time and may vary between different method calls in the same api/client (e.g. custom
metadata header fields such as "x-amz-meta-*" or "x-goog-meta-*"), a Map parameter can be annotated
with <code>HeaderMap</code> to construct a query that uses the contents of the map as its header parameters.</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">interface</span> <span class="pl-smi">Api</span> {
   <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"POST /"</span>)
   <span class="pl-smi">void</span> <span class="pl-en">post</span>(<span class="pl-c1">@</span><span class="pl-c1">HeaderMap</span> <span class="pl-smi">Map</span>&lt;<span class="pl-smi">String</span>, <span class="pl-smi">Object</span>&gt; <span class="pl-s1">headerMap</span>);
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public interface Api {
   @RequestLine(&quot;POST /&quot;)
   void post(@HeaderMap Map<String, Object> headerMap);
}" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon">
    <path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none">
    <path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<p dir="auto">These approaches specify header entries as part of the api and do not require any customizations
when building the Feign client.</p>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">Setting headers per target</h4><a id="user-content-setting-headers-per-target" class="anchor" aria-label="永久链接：设置每个目标的标头" href="#setting-headers-per-target"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto">To customize headers for each request method on a Target, a RequestInterceptor can be used. RequestInterceptors can be
shared across Target instances and are expected to be thread-safe. RequestInterceptors are applied to all request
methods on a Target.</p>
<p dir="auto">If you need per method customization, a custom Target is required, as the a RequestInterceptor does not have access to
the current method metadata.</p>
<p dir="auto">For an example of setting headers using a <code>RequestInterceptor</code>, see the <code>Request Interceptors</code> section.</p>
<p dir="auto">Headers can be set as part of a custom <code>Target</code>.</p>
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
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="  static class DynamicAuthTokenTarget<T> implements Target<T> {
    public DynamicAuthTokenTarget(Class<T> clazz,
                                  UrlAndTokenProvider provider,
                                  ThreadLocal<String> requestIdProvider);

    @Override
    public Request apply(RequestTemplate input) {
      TokenIdAndPublicURL urlAndToken = provider.get();
      if (input.url().indexOf(&quot;http&quot;) != 0) {
        input.insert(0, urlAndToken.publicURL);
      }
      input.header(&quot;X-Auth-Token&quot;, urlAndToken.tokenId);
      input.header(&quot;X-Request-ID&quot;, requestIdProvider.get());

      return input.request();
    }
  }

  public class Example {
    public static void main(String[] args) {
      Bank bank = Feign.builder()
              .target(new DynamicAuthTokenTarget(Bank.class, provider, requestIdProvider));
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
<p dir="auto">These approaches depend on the custom <code>RequestInterceptor</code> or <code>Target</code> being set on the Feign
client when it is built and can be used as a way to set headers on all api calls on a per-client
basis. This can be useful for doing things such as setting an authentication token in the header
of all api requests on a per-client basis. The methods are run when the api call is made on the
thread that invokes the api call, which allows the headers to be set dynamically at call time and
in a context-specific manner -- for example, thread-local storage can be used to set different
header values depending on the invoking thread, which can be useful for things such as setting
thread-specific trace identifiers for requests.</p>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto">Advanced usage</h3><a id="user-content-advanced-usage" class="anchor" aria-label="永久链接：高级用法" href="#advanced-usage"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">Base Apis</h4><a id="user-content-base-apis" class="anchor" aria-label="永久链接：基础 API" href="#base-apis"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto">In many cases, apis for a service follow the same conventions. Feign supports this pattern via single-inheritance interfaces.</p>
<p dir="auto">Consider the example:</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">interface</span> <span class="pl-smi">BaseAPI</span> {
  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"GET /health"</span>)
  <span class="pl-smi">String</span> <span class="pl-en">health</span>();

  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"GET /all"</span>)
  <span class="pl-smi">List</span>&lt;<span class="pl-smi">Entity</span>&gt; <span class="pl-en">all</span>();
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="interface BaseAPI {
  @RequestLine(&quot;GET /health&quot;)
  String health();

  @RequestLine(&quot;GET /all&quot;)
  List<Entity> all();
}" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon">
    <path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none">
    <path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<p dir="auto">You can define and target a specific api, inheriting the base methods.</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">interface</span> <span class="pl-smi">CustomAPI</span> <span class="pl-k">extends</span> <span class="pl-smi">BaseAPI</span> {
  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"GET /custom"</span>)
  <span class="pl-smi">String</span> <span class="pl-en">custom</span>();
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="interface CustomAPI extends BaseAPI {
  @RequestLine(&quot;GET /custom&quot;)
  String custom();
}" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon">
    <path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none">
    <path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<p dir="auto">In many cases, resource representations are also consistent. For this reason, type parameters are supported on the base api interface.</p>
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
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="@Headers(&quot;Accept: application/json&quot;)
interface BaseApi<V> {

  @RequestLine(&quot;GET /api/{key}&quot;)
  V get(@Param(&quot;key&quot;) String key);

  @RequestLine(&quot;GET /api&quot;)
  List<V> list();

  @Headers(&quot;Content-Type: application/json&quot;)
  @RequestLine(&quot;PUT /api/{key}&quot;)
  void put(@Param(&quot;key&quot;) String key, V value);
}

interface FooApi extends BaseApi<Foo> { }

interface BarApi extends BaseApi<Bar> { }" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon">
    <path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none">
    <path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">Logging</h4><a id="user-content-logging" class="anchor" aria-label="永久链接：记录" href="#logging"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto">You can log the http messages going to and from the target by setting up a <code>Logger</code>.  Here's the easiest way to do that:</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">GitHub</span> <span class="pl-s1">github</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                     .<span class="pl-en">decoder</span>(<span class="pl-k">new</span> <span class="pl-smi">GsonDecoder</span>())
                     .<span class="pl-en">logger</span>(<span class="pl-k">new</span> <span class="pl-smi">Logger</span>.<span class="pl-smi">JavaLogger</span>(<span class="pl-s">"GitHub.Logger"</span>).<span class="pl-en">appendToFile</span>(<span class="pl-s">"logs/http.log"</span>))
                     .<span class="pl-en">logLevel</span>(<span class="pl-smi">Logger</span>.<span class="pl-s1">Level</span>.<span class="pl-c1">FULL</span>)
                     .<span class="pl-en">target</span>(<span class="pl-smi">GitHub</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.github.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public class Example {
  public static void main(String[] args) {
    GitHub github = Feign.builder()
                     .decoder(new GsonDecoder())
                     .logger(new Logger.JavaLogger(&quot;GitHub.Logger&quot;).appendToFile(&quot;logs/http.log&quot;))
                     .logLevel(Logger.Level.FULL)
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
<blockquote>
<p dir="auto"><strong>A Note on JavaLogger</strong>:
Avoid using of default <code>JavaLogger()</code> constructor - it was marked as deprecated and will be removed soon.</p>
</blockquote>
<p dir="auto">The SLF4JLogger (see above) may also be of interest.</p>
<p dir="auto">To filter out sensitive information like authorization or tokens
override methods <code>shouldLogRequestHeader</code> or <code>shouldLogResponseHeader</code>.</p>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">Request Interceptors</h4><a id="user-content-request-interceptors" class="anchor" aria-label="永久链接：请求拦截器" href="#request-interceptors"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto">When you need to change all requests, regardless of their target, you'll want to configure a <code>RequestInterceptor</code>.
For example, if you are acting as an intermediary, you might want to propagate the <code>X-Forwarded-For</code> header.</p>
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
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="static class ForwardedForInterceptor implements RequestInterceptor {
  @Override public void apply(RequestTemplate template) {
    template.header(&quot;X-Forwarded-For&quot;, &quot;origin.host.com&quot;);
  }
}

public class Example {
  public static void main(String[] args) {
    Bank bank = Feign.builder()
                 .decoder(accountDecoder)
                 .requestInterceptor(new ForwardedForInterceptor())
                 .target(Bank.class, &quot;https://api.examplebank.com&quot;);
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
<p dir="auto">Another common example of an interceptor would be authentication, such as using the built-in <code>BasicAuthRequestInterceptor</code>.</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">Bank</span> <span class="pl-s1">bank</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                 .<span class="pl-en">decoder</span>(<span class="pl-s1">accountDecoder</span>)
                 .<span class="pl-en">requestInterceptor</span>(<span class="pl-k">new</span> <span class="pl-smi">BasicAuthRequestInterceptor</span>(<span class="pl-s1">username</span>, <span class="pl-s1">password</span>))
                 .<span class="pl-en">target</span>(<span class="pl-smi">Bank</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.examplebank.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public class Example {
  public static void main(String[] args) {
    Bank bank = Feign.builder()
                 .decoder(accountDecoder)
                 .requestInterceptor(new BasicAuthRequestInterceptor(username, password))
                 .target(Bank.class, &quot;https://api.examplebank.com&quot;);
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
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">Custom @Param Expansion</h4><a id="user-content-custom-param-expansion" class="anchor" aria-label="永久链接：自定义@Param扩展" href="#custom-param-expansion"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto">Parameters annotated with <code>Param</code> expand based on their <code>toString</code>. By
specifying a custom <code>Param.Expander</code>, users can control this behavior,
for example formatting dates.</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">interface</span> <span class="pl-smi">Api</span> {
  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"GET /?since={date}"</span>) <span class="pl-smi">Result</span> <span class="pl-en">list</span>(<span class="pl-c1">@</span><span class="pl-c1">Param</span>(<span class="pl-s1">value</span> = <span class="pl-s">"date"</span>, <span class="pl-s1">expander</span> = <span class="pl-smi">DateToMillis</span>.<span class="pl-k">class</span>) <span class="pl-smi">Date</span> <span class="pl-s1">date</span>);
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public interface Api {
  @RequestLine(&quot;GET /?since={date}&quot;) Result list(@Param(value = &quot;date&quot;, expander = DateToMillis.class) Date date);
}" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon">
    <path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none">
    <path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">Dynamic Query Parameters</h4><a id="user-content-dynamic-query-parameters" class="anchor" aria-label="永久链接：动态查询参数" href="#dynamic-query-parameters"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto">A Map parameter can be annotated with <code>QueryMap</code> to construct a query that uses the contents of the map as its query parameters.</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">interface</span> <span class="pl-smi">Api</span> {
  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"GET /find"</span>)
  <span class="pl-smi">V</span> <span class="pl-en">find</span>(<span class="pl-c1">@</span><span class="pl-c1">QueryMap</span> <span class="pl-smi">Map</span>&lt;<span class="pl-smi">String</span>, <span class="pl-smi">Object</span>&gt; <span class="pl-s1">queryMap</span>);
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public interface Api {
  @RequestLine(&quot;GET /find&quot;)
  V find(@QueryMap Map<String, Object> queryMap);
}" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon">
    <path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none">
    <path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<p dir="auto">This may also be used to generate the query parameters from a POJO object using a <code>QueryMapEncoder</code>.</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">interface</span> <span class="pl-smi">Api</span> {
  <span class="pl-c1">@</span><span class="pl-c1">RequestLine</span>(<span class="pl-s">"GET /find"</span>)
  <span class="pl-smi">V</span> <span class="pl-en">find</span>(<span class="pl-c1">@</span><span class="pl-c1">QueryMap</span> <span class="pl-smi">CustomPojo</span> <span class="pl-s1">customPojo</span>);
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public interface Api {
  @RequestLine(&quot;GET /find&quot;)
  V find(@QueryMap CustomPojo customPojo);
}" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon">
    <path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none">
    <path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path>
</svg>
    </clipboard-copy>
  </div></div>
<p dir="auto">When used in this manner, without specifying a custom <code>QueryMapEncoder</code>, the query map will be generated using member variable names as query parameter names. You can annotate a specific field of <code>CustomPojo</code> with the <code>@Param</code> annotation to specify a different name to the query parameter. The following POJO will generate query params of "/find?name={name}&amp;number={number}&amp;region_id={regionId}" (order of included query parameters not guaranteed, and as usual, if any value is null, it will be left out).</p>
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
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public class CustomPojo {
  private final String name;
  private final int number;
  @Param(&quot;region_id&quot;)
  private final String regionId;

  public CustomPojo (String name, int number, String regionId) {
    this.name = name;
    this.number = number;
    this.regionId = regionId;
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
<p dir="auto">To setup a custom <code>QueryMapEncoder</code>:</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">MyApi</span> <span class="pl-s1">myApi</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                 .<span class="pl-en">queryMapEncoder</span>(<span class="pl-k">new</span> <span class="pl-smi">MyCustomQueryMapEncoder</span>())
                 .<span class="pl-en">target</span>(<span class="pl-smi">MyApi</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.hostname.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public class Example {
  public static void main(String[] args) {
    MyApi myApi = Feign.builder()
                 .queryMapEncoder(new MyCustomQueryMapEncoder())
                 .target(MyApi.class, &quot;https://api.hostname.com&quot;);
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
<p dir="auto">When annotating objects with @QueryMap, the default encoder uses reflection to inspect provided objects Fields to expand the objects values into a query string. If you prefer that the query string be built using getter and setter methods, as defined in the Java Beans API, please use the BeanQueryMapEncoder</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">MyApi</span> <span class="pl-s1">myApi</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                 .<span class="pl-en">queryMapEncoder</span>(<span class="pl-k">new</span> <span class="pl-smi">BeanQueryMapEncoder</span>())
                 .<span class="pl-en">target</span>(<span class="pl-smi">MyApi</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.hostname.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public class Example {
  public static void main(String[] args) {
    MyApi myApi = Feign.builder()
                 .queryMapEncoder(new BeanQueryMapEncoder())
                 .target(MyApi.class, &quot;https://api.hostname.com&quot;);
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
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto">Error Handling</h3><a id="user-content-error-handling" class="anchor" aria-label="永久链接：错误处理" href="#error-handling"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto">If you need more control over handling unexpected responses, Feign instances can
register a custom <code>ErrorDecoder</code> via the builder.</p>
<div class="highlight highlight-source-java notranslate position-relative overflow-auto" dir="auto"><pre><span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-smi">Example</span> {
  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-smi">void</span> <span class="pl-en">main</span>(<span class="pl-smi">String</span>[] <span class="pl-s1">args</span>) {
    <span class="pl-smi">MyApi</span> <span class="pl-s1">myApi</span> = <span class="pl-smi">Feign</span>.<span class="pl-en">builder</span>()
                 .<span class="pl-en">errorDecoder</span>(<span class="pl-k">new</span> <span class="pl-smi">MyErrorDecoder</span>())
                 .<span class="pl-en">target</span>(<span class="pl-smi">MyApi</span>.<span class="pl-k">class</span>, <span class="pl-s">"https://api.hostname.com"</span>);
  }
}</pre><div class="zeroclipboard-container">
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public class Example {
  public static void main(String[] args) {
    MyApi myApi = Feign.builder()
                 .errorDecoder(new MyErrorDecoder())
                 .target(MyApi.class, &quot;https://api.hostname.com&quot;);
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
<p dir="auto">All responses that result in an HTTP status not in the 2xx range will trigger the <code>ErrorDecoder</code>'s <code>decode</code> method, allowing
you to handle the response, wrap the failure into a custom exception or perform any additional processing.
If you want to retry the request again, throw a <code>RetryableException</code>.  This will invoke the registered
<code>Retryer</code>.</p>
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto">Retry</h3><a id="user-content-retry" class="anchor" aria-label="永久链接：重试" href="#retry"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto">Feign, by default, will automatically retry <code>IOException</code>s, regardless of HTTP method, treating them as transient network
related exceptions, and any <code>RetryableException</code> thrown from an <code>ErrorDecoder</code>.  To customize this
behavior, register a custom <code>Retryer</code> instance via the builder.</p>
<p dir="auto">The following example shows how to refresh token and retry with <code>ErrorDecoder</code> and <code>Retryer</code> when received a 401 response.</p>
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
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public class Example {
    public static void main(String[] args) {
        var github = Feign.builder()
                .decoder(new GsonDecoder())
                .retryer(new MyRetryer(100, 3))
                .errorDecoder(new MyErrorDecoder())
                .target(Github.class, &quot;https://api.github.com&quot;);

        var contributors = github.contributors(&quot;foo&quot;, &quot;bar&quot;, &quot;invalid_token&quot;);
        for (var contributor : contributors) {
            System.out.println(contributor.login + &quot; &quot; + contributor.contributions);
        }
    }

    static class MyErrorDecoder implements ErrorDecoder {

        private final ErrorDecoder defaultErrorDecoder = new Default();

        @Override
        public Exception decode(String methodKey, Response response) {
            // wrapper 401 to RetryableException in order to retry
            if (response.status() == 401) {
                return new RetryableException(response.status(), response.reason(), response.request().httpMethod(), null, response.request());
            }
            return defaultErrorDecoder.decode(methodKey, response);
        }
    }

    static class MyRetryer implements Retryer {

        private final long period;
        private final int maxAttempts;
        private int attempt = 1;

        public MyRetryer(long period, int maxAttempts) {
            this.period = period;
            this.maxAttempts = maxAttempts;
        }

        @Override
        public void continueOrPropagate(RetryableException e) {
            if (++attempt > maxAttempts) {
                throw e;
            }
            if (e.status() == 401) {
                // remove Authorization first, otherwise Feign will add a new Authorization header
                // cause github responses a 400 bad request
                e.request().requestTemplate().removeHeader(&quot;Authorization&quot;);
                e.request().requestTemplate().header(&quot;Authorization&quot;, &quot;Bearer &quot; + getNewToken());
                try {
                    Thread.sleep(period);
                } catch (InterruptedException ex) {
                    throw e;
                }
            } else {
                throw e;
            }
        }

        // Access an external api to obtain new token
        // In this example, we can simply return a fixed token to demonstrate how Retryer works
        private String getNewToken() {
            return &quot;newToken&quot;;
        }

        @Override
        public Retryer clone() {
            return new MyRetryer(period, maxAttempts);
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
<p dir="auto"><code>Retryer</code>s are responsible for determining if a retry should occur by returning either a <code>true</code> or
<code>false</code> from the method <code>continueOrPropagate(RetryableException e);</code>  A <code>Retryer</code> instance will be
created for each <code>Client</code> execution, allowing you to maintain state bewteen each request if desired.</p>
<p dir="auto">If the retry is determined to be unsuccessful, the last <code>RetryException</code> will be thrown.  To throw the original
cause that led to the unsuccessful retry, build your Feign client with the <code>exceptionPropagationPolicy()</code> option.</p>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">Response Interceptor</h4><a id="user-content-response-interceptor" class="anchor" aria-label="永久链接：响应拦截器" href="#response-interceptor"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto">If you need to treat what would otherwise be an error as a success and return a result rather than throw an exception then you may use a <code>ResponseInterceptor</code>.</p>
<p dir="auto">As an example Feign includes a simple <code>RedirectionInterceptor</code> that can be used to extract the location header from redirection responses.</p>
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
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public interface Api {
  // returns a 302 response
  @RequestLine(&quot;GET /location&quot;)
  String location();
}

public class MyApp {
  public static void main(String[] args) {
    // Configure the HTTP client to ignore redirection
    Api api = Feign.builder()
                   .options(new Options(10, TimeUnit.SECONDS, 60, TimeUnit.SECONDS, false))
                   .responseInterceptor(new RedirectionInterceptor())
                   .target(Api.class, &quot;https://redirect.example.com&quot;);
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
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto">Metrics</h3><a id="user-content-metrics" class="anchor" aria-label="永久链接：指标" href="#metrics"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto">By default, feign won't collect any metrics.</p>
<p dir="auto">But, it's possible to add metric collection capabilities to any feign client.</p>
<p dir="auto">Metric Capabilities provide a first-class Metrics API that users can tap into to gain insight into the request/response lifecycle.</p>
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">Dropwizard Metrics 4</h4><a id="user-content-dropwizard-metrics-4" class="anchor" aria-label="永久链接：Dropwizard Metrics 4" href="#dropwizard-metrics-4"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
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
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public class MyApp {
  public static void main(String[] args) {
    GitHub github = Feign.builder()
                         .addCapability(new Metrics4Capability())
                         .target(GitHub.class, &quot;https://api.github.com&quot;);

    github.contributors(&quot;OpenFeign&quot;, &quot;feign&quot;);
    // metrics will be available from this point onwards
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
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">Dropwizard Metrics 5</h4><a id="user-content-dropwizard-metrics-5" class="anchor" aria-label="永久链接：Dropwizard Metrics 5" href="#dropwizard-metrics-5"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
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
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public class MyApp {
  public static void main(String[] args) {
    GitHub github = Feign.builder()
                         .addCapability(new Metrics5Capability())
                         .target(GitHub.class, &quot;https://api.github.com&quot;);

    github.contributors(&quot;OpenFeign&quot;, &quot;feign&quot;);
    // metrics will be available from this point onwards
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
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">Micrometer</h4><a id="user-content-micrometer" class="anchor" aria-label="永久链接： 千分尺" href="#micrometer"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
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
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="public class MyApp {
  public static void main(String[] args) {
    GitHub github = Feign.builder()
                         .addCapability(new MicrometerCapability())
                         .target(GitHub.class, &quot;https://api.github.com&quot;);

    github.contributors(&quot;OpenFeign&quot;, &quot;feign&quot;);
    // metrics will be available from this point onwards
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
<div class="markdown-heading" dir="auto"><h4 tabindex="-1" class="heading-element" dir="auto">Static and Default Methods</h4><a id="user-content-static-and-default-methods" class="anchor" aria-label="永久链接：静态和默认方法" href="#static-and-default-methods"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto">Interfaces targeted by Feign may have static or default methods (if using Java 8+).
These allows Feign clients to contain logic that is not expressly defined by the underlying API.
For example, static methods make it easy to specify common client build configurations; default methods can be used to compose queries or define default parameters.</p>
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
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="interface GitHub {
  @RequestLine(&quot;GET /repos/{owner}/{repo}/contributors&quot;)
  List<Contributor> contributors(@Param(&quot;owner&quot;) String owner, @Param(&quot;repo&quot;) String repo);

  @RequestLine(&quot;GET /users/{username}/repos?sort={sort}&quot;)
  List<Repo> repos(@Param(&quot;username&quot;) String owner, @Param(&quot;sort&quot;) String sort);

  default List<Repo> repos(String owner) {
    return repos(owner, &quot;full_name&quot;);
  }

  /**
   * Lists all contributors for all repos owned by a user.
   */
  default List<Contributor> contributors(String user) {
    MergingContributorList contributors = new MergingContributorList();
    for(Repo repo : this.repos(owner)) {
      contributors.addAll(this.contributors(user, repo.getName()));
    }
    return contributors.mergeResult();
  }

  static GitHub connect() {
    return Feign.builder()
                .decoder(new GsonDecoder())
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
<div class="markdown-heading" dir="auto"><h3 tabindex="-1" class="heading-element" dir="auto">Async execution via <code>CompletableFuture</code></h3><a id="user-content-async-execution-via-completablefuture" class="anchor" aria-label="永久链接：通过 CompletableFuture 异步执行" href="#async-execution-via-completablefuture"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
<p dir="auto">Feign 10.8 introduces a new builder <code>AsyncFeign</code> that allow methods to return <code>CompletableFuture</code> instances.</p>
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
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="interface GitHub {
  @RequestLine(&quot;GET /repos/{owner}/{repo}/contributors&quot;)
  CompletableFuture<List<Contributor>> contributors(@Param(&quot;owner&quot;) String owner, @Param(&quot;repo&quot;) String repo);
}

public class MyApp {
  public static void main(String... args) {
    GitHub github = AsyncFeign.builder()
                         .decoder(new GsonDecoder())
                         .target(GitHub.class, &quot;https://api.github.com&quot;);

    // Fetch and print a list of the contributors to this library.
    CompletableFuture<List<Contributor>> contributors = github.contributors(&quot;OpenFeign&quot;, &quot;feign&quot;);
    for (Contributor contributor : contributors.get(1, TimeUnit.SECONDS)) {
      System.out.println(contributor.login + &quot; (&quot; + contributor.contributions + &quot;)&quot;);
    }
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
<p dir="auto">Initial implementation include 2 async clients:</p>
<ul dir="auto">
<li><code>AsyncClient.Default</code></li>
<li><code>AsyncApacheHttp5Client</code></li>
</ul>
<div class="markdown-heading" dir="auto"><h2 tabindex="-1" class="heading-element" dir="auto">Maven’s Bill of Material (BOM)</h2><a id="user-content-mavens-bill-of-material-bom" class="anchor" aria-label="永久链接：Maven 的物料清单 (BOM)" href="#mavens-bill-of-material-bom"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path d="m7.775 3.275 1.25-1.25a3.5 3.5 0 1 1 4.95 4.95l-2.5 2.5a3.5 3.5 0 0 1-4.95 0 .751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018 1.998 1.998 0 0 0 2.83 0l2.5-2.5a2.002 2.002 0 0 0-2.83-2.83l-1.25 1.25a.751.751 0 0 1-1.042-.018.751.751 0 0 1-.018-1.042Zm-4.69 9.64a1.998 1.998 0 0 0 2.83 0l1.25-1.25a.751.751 0 0 1 1.042.018.751.751 0 0 1 .018 1.042l-1.25 1.25a3.5 3.5 0 1 1-4.95-4.95l2.5-2.5a3.5 3.5 0 0 1 4.95 0 .751.751 0 0 1-.018 1.042.751.751 0 0 1-1.042.018 1.998 1.998 0 0 0-2.83 0l-2.5 2.5a1.998 1.998 0 0 0 0 2.83Z"></path></svg></a></div>
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
    <clipboard-copy aria-label="Copy" class="ClipboardButton btn btn-invisible js-clipboard-copy m-2 p-0 tooltipped-no-delay d-flex flex-justify-center flex-items-center" data-copy-feedback="Copied!" data-tooltip-direction="w" value="<project>

...

  <dependencyManagement>
    <dependencies>
      <dependency>
        <groupId>io.github.openfeign</groupId>
        <artifactId>feign-bom</artifactId>
        <version>??feign.version??</version>
        <type>pom</type>
        <scope>import</scope>
      </dependency>
    </dependencies>
  </dependencyManagement>
</project>" tabindex="0" role="button">
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-copy js-clipboard-copy-icon">
    <path d="M0 6.75C0 5.784.784 5 1.75 5h1.5a.75.75 0 0 1 0 1.5h-1.5a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-1.5a.75.75 0 0 1 1.5 0v1.5A1.75 1.75 0 0 1 9.25 16h-7.5A1.75 1.75 0 0 1 0 14.25Z"></path><path d="M5 1.75C5 .784 5.784 0 6.75 0h7.5C15.216 0 16 .784 16 1.75v7.5A1.75 1.75 0 0 1 14.25 11h-7.5A1.75 1.75 0 0 1 5 9.25Zm1.75-.25a.25.25 0 0 0-.25.25v7.5c0 .138.112.25.25.25h7.5a.25.25 0 0 0 .25-.25v-7.5a.25.25 0 0 0-.25-.25Z"></path>
</svg>
      <svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-check js-clipboard-check-icon color-fg-success d-none">
    <path d="M13.78 4.22a.75.75 0 0 1 0 1.06l-7.25 7.25a.75.75 0 0 1-1.06 0L2.22 9.28a.751.751 0 0 1 .018-1.042.751.751 0 0 1 1.042-.018L6 10.94l6.72-6.72a.75.75 0 0 1 1.06 0Z"></path>
</svg>
    </clipboard-copy>
  </div></div>
</article></div>
