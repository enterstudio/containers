---

copyright:
  years: 2014, 2018
lastupdated: "2018-12-05"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}



# 使用注释定制 Ingress
{: #ingress_annotation}

要向 Ingress 应用程序负载均衡器 (ALB) 添加功能，您可以将注释指定为 Ingress 资源中的元数据。
{: shortdesc}

在使用注释之前，请确保通过执行[使用 Ingress 公开应用程序](cs_ingress.html)中的步骤来正确设置 Ingress 服务配置。使用基本配置设置 Ingress ALB 后，可以通过向 Ingress 资源文件添加注释来扩展其功能。
{: note}

<table>
<caption>一般注释</caption>
<col width="20%">
<col width="20%">
<col width="60%">
 <thead>
 <th>一般注释</th>
 <th>名称</th>
 <th>描述</th>
 </thead>
 <tbody>
 <tr>
 <td><a href="#proxy-external-service">外部服务</a></td>
 <td><code>proxy-external-service</code></td>
 <td>添加外部服务（例如，{{site.data.keyword.Bluemix_notm}} 中托管的服务）的路径定义。</td>
 </tr>
 <tr>
 <td><a href="#location-modifier">位置修饰符</a></td>
 <td><code>location-modifier</code></td>
 <td>修改 ALB 将请求 URI 与应用程序路径相匹配的方式。</td>
 </tr>
 <tr>
 <td><a href="#location-snippets">位置片段</a></td>
 <td><code>location-snippets</code></td>
 <td>为服务添加定制位置块配置。</td>
 </tr>
 <tr>
 <td><a href="#alb-id">专用 ALB 路由</a></td>
 <td><code>ALB-ID</code></td>
 <td>使用专用 ALB 将入局请求路由到应用程序。</td>
 </tr>
 <tr>
 <td><a href="#rewrite-path">重写路径</a></td>
 <td><code>rewrite-path</code></td>
 <td>将入局网络流量路由到后端应用程序侦听的其他路径。</td>
 </tr>
 <tr>
 <td><a href="#server-snippets">服务器片段</a></td>
 <td><code>server-snippets</code></td>
 <td>添加定制服务器块配置。</td>
 </tr>
 <tr>
 <td><a href="#tcp-ports">TCP 端口</a></td>
 <td><code>tcp-ports</code></td>
 <td>通过非标准 TCP 端口访问应用程序。</td>
 </tr>
 </tbody></table>

<br>

<table>
<caption>连接注释</caption>
<col width="20%">
<col width="20%">
<col width="60%">
 <thead>
 <th>连接注释</th>
 <th>名称</th>
 <th>描述</th>
  </thead>
  <tbody>
  <tr>
  <td><a href="#proxy-connect-timeout">定制连接超时和读取超时</a></td>
  <td><code>proxy-connect-timeout，proxy-read-timeout</code></td>
  <td>设置 ALB 等待连接到后端应用程序以及从后端应用程序进行读取的时间，超过该时间后，后端应用程序将视为不可用。</td>
  </tr>
  <tr>
  <td><a href="#keepalive-requests">保持活动请求数</a></td>
  <td><code>keepalive-requests</code></td>
  <td>设置可通过一个保持活动连接处理的最大请求数。</td>
  </tr>
  <tr>
  <td><a href="#keepalive-timeout">保持活动超时</a></td>
  <td><code>keepalive-timeout</code></td>
  <td>设置保持活动连接在服务器上保持打开状态的最长时间。</td>
  </tr>
  <tr>
  <td><a href="#proxy-next-upstream-config">作为代理传递到下一个上游</a></td>
  <td><code>proxy-next-upstream-config</code></td>
  <td>设置 ALB 何时可以向下一个上游服务器传递请求。</td>
  </tr>
  <tr>
  <td><a href="#sticky-cookie-services">使用 cookie 确保会话亲缘关系</a></td>
  <td><code>sticky-cookie-services</code></td>
  <td>使用粘性 cookie 始终将入局网络流量路由到同一个上游服务器。</td>
  </tr>
  <tr>
  <td><a href="#upstream-fail-timeout">上游故障超时</a></td>
  <td><code>upstream-fail-timeout</code></td>
  <td>设置在服务器被视为不可用之前，ALB 可以尝试连接到服务器的时间量。</td>
  </tr>
  <tr>
  <td><a href="#upstream-keepalive">上游保持活动连接数</a></td>
  <td><code>upstream-keepalive</code></td>
  <td>设置上游服务器的最大空闲保持活动连接数。</td>
  </tr>
  <tr>
  <td><a href="#upstream-max-fails">上游最大失败次数</a></td>
  <td><code>upstream-max-fails</code></td>
  <td>设置在服务器被视为不可用之前，尝试与服务器通信失败的最大次数。</td>
  </tr>
  </tbody></table>

<br>

  <table>
  <caption>HTTPS 和 TLS/SSL 认证注释</caption>
  <col width="20%">
  <col width="20%">
  <col width="60%">
  <thead>
  <th>HTTPS 和 TLS/SSL 认证注释</th>
  <th>名称</th>
  <th>描述</th>
  </thead>
  <tbody>
  <tr>
  <td><a href="#appid-auth">{{site.data.keyword.appid_short}} 认证</a></td>
  <td><code>appid-auth</code></td>
  <td>使用 {{site.data.keyword.appid_full}} 向应用程序进行认证。</td>
  </tr>
  <tr>
  <td><a href="#custom-port">定制 HTTP 和 HTTPS 端口</a></td>
  <td><code>custom-port</code></td>
  <td>更改 HTTP（端口 80）和 HTTPS（端口 443）网络流量的缺省端口。</td>
  </tr>
  <tr>
  <td><a href="#redirect-to-https">HTTP 重定向到 HTTPS</a></td>
  <td><code>redirect-to-https</code></td>
  <td>将域上的不安全的 HTTP 请求重定向到 HTTPS。</td>
  </tr>
  <tr>
  <td><a href="#hsts">HTTP 严格传输安全性 (HSTS)</a></td>
  <td><code>hsts</code></td>
  <td>将浏览器设置为仅使用 HTTPS 访问域。</td>
  </tr>
  <tr>
  <td><a href="#mutual-auth">相互认证</a></td>
  <td><code>mutual-auth</code></td>
  <td>为 ALB 配置相互认证。</td>
  </tr>
  <tr>
  <td><a href="#ssl-services">SSL 服务支持</a></td>
  <td><code>ssl-services</code></td>
  <td>允许 SSL 服务支持加密流至需要 HTTPS 的上游应用程序的流量。</td>
  </tr>
  </tbody></table>

<br>

<table>
<caption>Istio 注释</caption>
<col width="20%">
<col width="20%">
<col width="60%">
<thead>
<th>Istio 注释</th>
<th>名称</th>
<th>描述</th>
</thead>
<tbody>
<tr>
<td><a href="#istio-services">Istio 服务</a></td>
<td><code>istio-services</code></td>
<td>将流量路由到 Istio 管理的服务。</td>
</tr>
</tbody></table>

<br>

<table>
<caption>代理缓冲区注释</caption>
<col width="20%">
<col width="20%">
<col width="60%">
 <thead>
 <th>代理缓冲区注释</th>
 <th>名称</th>
 <th>描述</th>
 </thead>
 <tbody>
 <tr>
 <td><a href="#proxy-buffering">客户机响应数据缓冲</a></td>
 <td><code>proxy-buffering</code></td>
 <td>禁止在向客户机发送响应时，在 ALB 上对客户机响应进行缓冲。</td>
 </tr>
 <tr>
 <td><a href="#proxy-buffers">代理缓冲区数</a></td>
 <td><code>proxy-buffers</code></td>
 <td>设置缓冲区的数目和大小，这些缓冲区用于读取来自通过代理传递的服务器的单个连接的响应。</td>
 </tr>
 <tr>
 <td><a href="#proxy-buffer-size">代理缓冲区大小</a></td>
 <td><code>proxy-buffer-size</code></td>
 <td>设置缓冲区的大小，该缓冲区用于读取从通过代理传递的服务器收到的响应的第一部分。</td>
 </tr>
 <tr>
 <td><a href="#proxy-busy-buffers-size">代理繁忙缓冲区大小</a></td>
 <td><code>proxy-busy-buffers-size</code></td>
 <td>设置可以处于繁忙状态的代理缓冲区的大小。</td>
 </tr>
 </tbody></table>

<br>

<table>
<caption>请求和响应注释</caption>
<col width="20%">
<col width="20%">
<col width="60%">
<thead>
<th>请求和响应注释</th>
<th>名称</th>
<th>描述</th>
</thead>
<tbody>
<tr>
<td><a href="#add-host-port">将服务器端口添加到主机头</a></td>
<td><code>add-host-port</code></td>
<td>将服务器端口添加到主机以路由请求。</td>
</tr>
<tr>
<td><a href="#client-max-body-size">客户机请求主体大小</a></td>
<td><code>client-max-body-size</code></td>
<td>设置客户机可以作为请求一部分发送的主体的最大大小。</td>
</tr>
<tr>
<td><a href="#large-client-header-buffers">大型客户机头缓冲区</a></td>
<td><code>large-client-header-buffers</code></td>
<td>设置读取大型客户机请求头的缓冲区的最大数目和大小。</td>
</tr>
<tr>
<td><a href="#proxy-add-headers">额外的客户机请求或响应头</a></td>
<td><code>proxy-add-headers，response-add-headers</code></td>
<td>向客户机请求添加头信息，然后将该请求转发到后端应用程序，或者向客户机响应添加头信息，然后将该响应发送到客户机。</td>
</tr>
<tr>
<td><a href="#response-remove-headers">除去客户机响应头</a></td>
<td><code>response-remove-headers</code></td>
<td>从客户机响应中除去头信息，然后将该响应转发到客户机。</td>
</tr>
</tbody></table>

<br>

<table>
<caption>服务限制注释</caption>
<col width="20%">
<col width="20%">
<col width="60%">
<thead>
<th>服务限制注释</th>
<th>名称</th>
<th>描述</th>
</thead>
<tbody>
<tr>
<td><a href="#global-rate-limit">全局速率限制</a></td>
<td><code>global-rate-limit</code></td>
<td>对于所有服务，按定义的键限制请求处理速率和连接数。</td>
</tr>
<tr>
<td><a href="#service-rate-limit">服务速率限制</a></td>
<td><code>service-rate-limit</code></td>
<td>对于特定服务，按定义的键限制请求处理速率和连接数。</td>
</tr>
</tbody></table>

<br>



## 一般注释
{: #general}

### 外部服务 (proxy-external-service)
{: #proxy-external-service}

添加外部服务（例如，{{site.data.keyword.Bluemix_notm}} 中托管的服务）的路径定义。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>添加外部服务的路径定义。仅当应用程序在外部服务（而不是后端服务）上运行时，才可使用此注释。使用此注释来创建外部服务路径时，仅支持 `client-max-body-size`、`proxy-read-timeout`、`proxy-connect-timeout` 和 `proxy-buffering` 注释一起使用。不支持其他任何注释与 `proxy-external-service` 一起使用。
<p class="note">不能为单个服务和路径指定多个主机。</p>
</dd>
<dt>样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: cafe-ingress
annotations:
    ingress.bluemix.net/proxy-external-service: "path=&lt;mypath&gt; external-svc=https:&lt;external_service&gt; host=&lt;mydomain&gt;"
spec:
tls:
  - hosts:
    - mydomain
    secretName: mysecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /
        backend:
          serviceName: myservice
          servicePort: 80
</code></pre>

<table>
<caption>了解注释的组成部分</caption>
 <thead>
 <th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
 </thead>
 <tbody>
 <tr>
 <td><code>path</code></td>
 <td>将 <code>&lt;<em>mypath</em>&gt;</code> 替换为外部服务侦听的路径。</td>
 </tr>
 <tr>
 <td><code>external-svc</code></td>
 <td>将 <code>&lt;<em>external_service</em>&gt;</code> 替换为要调用的外部服务。例如，<code>https://&lt;myservice&gt;.&lt;region&gt;.mybluemix.net</code>。</td>
 </tr>
 <tr>
 <td><code>host</code></td>
 <td>将 <code>&lt;<em>mydomain</em>&gt;</code> 替换为外部服务的主机域。</td>
 </tr>
 </tbody></table>

 </dd></dl>

<br />


### 位置修饰符 (location-modifier)
{: #location-modifier}

修改 ALB 将请求 URI 与应用程序路径相匹配的方式。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>缺省情况下，ALB 会将应用程序侦听的路径作为前缀进行处理。ALB 接收到对应用程序的请求时，ALB 会检查 Ingress 资源以查找与请求 URI 的开头相匹配的路径（作为前缀）。如果找到匹配项，那么会将请求转发到部署了应用程序的 pod 的 IP 地址。<br><br>`location-modifier` 注释通过修改位置块配置来更改 ALB 搜索匹配项的方式。位置块用于确定如何处理请求中的应用程序路径。<p class="note">要处理正则表达式 (regex) 路径，此注释是必需的。</p></dd>

<dt>支持的修饰符</dt>
<dd>

<table>
<caption>支持的修饰符</caption>
 <col width="10%">
 <col width="90%">
 <thead>
 <th>修饰符</th>
 <th>描述</th>
 </thead>
 <tbody>
 <tr>
 <td><code>=</code></td>
 <td>等号修饰符使 ALB 仅选择完全匹配项。找到完全匹配项时，搜索将停止，并选择匹配路径。<br>例如，如果应用程序侦听的是 <code>/tea</code>，那么 ALB 在匹配对应用程序的请求时，仅选择完全匹配的 <code>/tea</code> 路径。</td>
 </tr>
 <tr>
 <td><code>~</code></td>
 <td>波浪号修饰符使 ALB 在匹配期间将路径作为区分大小写的 regex 路径进行处理。<br>例如，如果应用程序侦听的是 <code>/coffee</code>，那么 ALB 在匹配对应用程序的请求时，可以选择 <code>/ab/coffee</code> 或 <code>/123/coffee</code> 路径，即便并未为应用程序显式设置这些路径也不例外。</td>
 </tr>
 <tr>
 <td><code>~\*</code></td>
 <td>波浪号后跟星号修饰符使 ALB 在匹配期间将路径作为不区分大小写的 regex 路径进行处理。<br>例如，如果应用程序侦听的是 <code>/coffee</code>，那么 ALB 在匹配对应用程序的请求时，可以选择 <code>/ab/Coffee</code> 或 <code>/123/COFFEE</code> 路径，即便并未为应用程序显式设置这些路径也不例外。</td>
 </tr>
 <tr>
 <td><code>^~</code></td>
 <td>重音符后跟波浪号修饰符使 ALB 选择最佳的非 regex 匹配项，而不选择 regex 路径。</td>
 </tr>
 </tbody>
</table>

</dd>

<dt>样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
annotations:
  ingress.bluemix.net/location-modifier: "modifier='&lt;location_modifier&gt;' serviceName=&lt;myservice1&gt;;modifier='&lt;location_modifier&gt;' serviceName=&lt;myservice2&gt;"
spec:
tls:
  - hosts:
    - mydomain
    secretName: mysecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /
        backend:
          serviceName: &lt;myservice&gt;
          servicePort: 80</code></pre>

 <table>
 <caption>了解注释的组成部分</caption>
  <thead>
  <th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
  </thead>
  <tbody>
  <tr>
  <td><code>modifier</code></td>
  <td>将 <code>&lt;<em>location_modifier</em>&gt;</code> 替换为要用于路径的位置修饰符。支持的修饰符为 <code>'='</code>、<code>'~'</code>、<code>'~\*'</code> 和 <code>'^~'</code>。必须用单引号将修饰符括起。</td>
  </tr>
  <tr>
  <td><code>serviceName</code></td>
  <td>将 <code>&lt;<em>myservice</em>&gt;</code> 替换为针对应用程序创建的 Kubernetes 服务的名称。</td>
  </tr>
  </tbody></table>
  </dd>
  </dl>

<br />


### 位置片段 (location-snippets)
{: #location-snippets}

为服务添加定制位置块配置。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>服务器块是 Nginx 伪指令，用于定义 ALB 虚拟服务器的配置。位置块是在服务器块中定义的 Nginx 伪指令。位置块定义 Ingress 如何处理请求 URI，或者定义请求中在域名或 IP 地址和端口之后的部分。<br><br>服务器块收到请求时，位置块会将 URI 与路径相匹配，并将请求转发到部署了应用程序的 pod 的 IP 地址。通过使用 <code>location-snippets</code> 注释，可以修改位置块如何将请求转发到特定服务。<br><br>要改为修改整个服务器块，请参阅 <a href="#server-snippets">server-snippets</a> 注释。</dd>


<dt>样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
annotations:
  ingress.bluemix.net/location-snippets: |
    serviceName=&lt;myservice1&gt;
    # Example location snippet
    proxy_request_buffering off;
    rewrite_log on;
    proxy_set_header "x-additional-test-header" "location-snippet-header";
    &lt;EOS&gt;
    serviceName=&lt;myservice2&gt;
    proxy_set_header Authorization "";
    &lt;EOS&gt;
spec:
tls:
- hosts:
  - mydomain
    secretName: mytlssecret
  rules:
- host: mydomain
  http:
paths:
    - path: /
      backend:
        serviceName: &lt;myservice&gt;
        servicePort: 8080</code></pre>

<table>
<caption>了解注释的组成部分</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
</thead>
<tbody>
<tr>
<td><code>serviceName</code></td>
<td>将 <code>&lt;<em>myservice</em>&gt;</code> 替换针对应用程序创建的服务的名称。</td>
</tr>
<tr>
<td>位置片段</td>
<td>提供要用于指定服务的配置片段。用于 <code>myservice1</code> 服务的样本片段将位置块配置为关闭代理请求缓冲，开启日志重写，并在将请求转发到该服务时设置额外的头。用于 <code>myservice2</code> 服务的样本片段设置空的 <code>Authorization</code> 头。每个位置片段都必须以值 <code>&lt;EOS&gt;</code> 结尾。</td>
</tr>
</tbody></table>
</dd>
</dl>

<br />


### 专用 ALB 路由 (ALB-ID)
{: #alb-id}

使用专用 ALB 将入局请求路由到应用程序。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>
选择专用 ALB 来路由入局请求，而不选择公共 ALB。</dd>


<dt>样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
annotations:
    ingress.bluemix.net/ALB-ID: "&lt;private_ALB_ID&gt;"
spec:
tls:
- hosts:
  - mydomain
    secretName: mytlssecret
  rules:
- host: mydomain
  http:
paths:
    - path: /
       backend:
         serviceName: myservice
         servicePort: 8080</code></pre>

<table>
<caption>了解注释的组成部分</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
</thead>
<tbody>
<tr>
<td><code>&lt;private_ALB_ID&gt;</code></td>
<td>专用 ALB 的标识。要查找专用 ALB 标识，请运行 <code>ibmcloud ks albs --cluster &lt;my_cluster&gt;</code>。
<p>
如果您的多专区集群启用了多个专用 ALB，那么可以提供使用 <code>;</code> 分隔的 ALB 标识的列表。例如：<code>ingress.bluemix.net/ALB-ID: &lt;private_ALB_ID_1&gt;;&lt;private_ALB_ID_2&gt;;&lt;private_ALB_ID_3&gt</code></p>
</td>
</tr>
</tbody></table>
</dd>
</dl>

<br />


### 重写路径 (rewrite-path)
{: #rewrite-path}

将 ALB 域路径上的入局网络流量路由到后端应用程序侦听的其他路径。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>Ingress ALB 域将 <code>mykubecluster.us-south.containers.appdomain.cloud/beans</code> 上的入局网络流量路由到应用程序。应用程序侦听的是 <code>/coffee</code>，而不是 <code>/beans</code>。要将入局网络流量转发到应用程序，请将 rewrite 注释添加到 Ingress 资源配置文件。rewrite 注释可确保使用 <code>/coffee</code> 路径将 <code>/beans</code> 上的入局网络流量转发到应用程序。当包含多个服务时，请仅使用分号 (;) 来分隔这些服务。</dd>
<dt>样本 Ingress 资源 YAML</dt>
<dd>
<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
annotations:
    ingress.bluemix.net/rewrite-path: "serviceName=&lt;myservice1&gt; rewrite=&lt;target_path1&gt;;serviceName=&lt;myservice2&gt; rewrite=&lt;target_path2&gt;"
spec:
tls:
  - hosts:
    - mydomain
    secretName: mysecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /beans
        backend:
          serviceName: myservice1
          servicePort: 80
</code></pre>

<table>
<caption>了解注释的组成部分</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
</thead>
<tbody>
<tr>
<td><code>serviceName</code></td>
<td>将 <code>&lt;<em>myservice</em>&gt;</code> 替换为您针对应用程序创建的 Kubernetes 服务的名称。</td>
</tr>
<tr>
<td><code>rewrite</code></td>
<td>将 <code>&lt;<em>target_path</em>&gt;</code> 替换为应用程序侦听的路径。ALB 域上的入局网络流量会使用此路径转发到 Kubernetes 服务。大多数应用程序不会侦听特定路径，而是使用根路径和特定端口。在上例中，rewrite 路径定义为 <code>/coffee</code>。</td>
</tr>
</tbody></table>

</dd></dl>

<br />


### 服务器片段 (server-snippets)
{: #server-snippets}

添加定制服务器块配置。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>服务器块是 Nginx 伪指令，用于定义 ALB 虚拟服务器的配置。通过使用 <code>server-snippets</code> 注释，可以提供定制配置片段来修改 ALB 处理请求的方式。</dd>

<dt>样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
annotations:
  ingress.bluemix.net/server-snippets: |
    location = /health {
    return 200 'Healthy';
    add_header Content-Type text/plain;
    }
spec:
tls:
- hosts:
  - mydomain
    secretName: mytlssecret
  rules:
- host: mydomain
  http:
paths:
    - path: /
      backend:
        serviceName: &lt;myservice&gt;
        servicePort: 8080</code></pre>

<table>
<caption>了解注释的组成部分</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
</thead>
<tbody>
<tr>
<td>服务器片段</td>
<td>提供要使用的配置片段。此样本片段指定用于处理 <code>/health</code> 请求的位置块。位置块配置为返回运行正常的响应，并在转发请求时添加头。</td>
</tr>
</tbody></table>
</dd>
</dl>

<br />


### 用于应用程序负载均衡器的 TCP 端口 (tcp-ports)
{: #tcp-ports}

通过非标准 TCP 端口访问应用程序。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>
将此注释用于在运行 TCP 流工作负载的应用程序。



<p class="note">ALB 以通过方式运行，并将流量转发到后端应用程序。在此情况下，不支持 SSL 终止。TLS 连接不会终止，也不会通过非接触方式传递。</p>
</dd>


<dt>样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
annotations:
  ingress.bluemix.net/tcp-ports: "serviceName=&lt;myservice&gt; ingressPort=&lt;ingress_port&gt; servicePort=&lt;service_port&gt;"
spec:
tls:
  - hosts:
    - mydomain
    secretName: mysecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /
        backend:
          serviceName: &lt;myservice&gt;
          servicePort: 80</code></pre>

 <table>
 <caption>了解注释的组成部分</caption>
  <thead>
  <th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
  </thead>
  <tbody>
  <tr>
  <td><code>serviceName</code></td>
  <td>将 <code>&lt;<em>myservice</em>&gt;</code> 替换为要通过非标准 TCP 端口访问的 Kubernetes 服务的名称。</td>
  </tr>
  <tr>
  <td><code>ingressPort</code></td>
  <td>将 <code><em>&lt;ingress_port&gt;</em></code> 替换为要用于访问应用程序的 TCP 端口。</td>
  </tr>
  <tr>
  <td><code>servicePort</code></td>
  <td>此参数是可选的。如果提供了此参数，那么在将流量发送到后端应用程序之前，会将端口替换为此值。否则，该端口与 Ingress 端口保持相同。如果不想设置此参数，那么可以将其从配置中除去。</td>
  </tr>
  </tbody></table>

 </dd>
 <dt>用法</dt>
 <dd><ol><li>查看 ALB 的打开端口。
<pre class="pre">
<code>kubectl get service -n kube-system</code></pre>
CLI 输出类似于以下内容：
<pre class="screen">
<code>NAME                                             TYPE           CLUSTER-IP       EXTERNAL-IP    PORT(S)                      AGE
public-cr18e61e63c6e94b658596ca93d087eed9-alb1   LoadBalancer   10.xxx.xx.xxx    169.xx.xxx.xxx 80:30416/TCP,443:32668/TCP   109d</code></pre></li>
<li>打开 ALB 配置映射。
<pre class="pre">
<code>kubectl edit configmap ibm-cloud-provider-ingress-cm -n kube-system</code></pre></li>
<li>将 TCP 端口添加到配置映射。将 <code>&lt;port&gt;</code> 替换为要打开的 TCP 端口。
<p class="note">缺省情况下，端口 80 和 443 已打开。如果要使 80 和 443 保持打开，那么必须在 `public-ports` 字段中包含这两个端口以及您指定的其他任何 TCP 端口。如果启用了专用 ALB，那么还必须在 `private-ports` 字段中指定要保持打开的任何端口。有关更多信息，请参阅<a href="cs_ingress.html#opening_ingress_ports">在 Ingress ALB 中打开端口</a>。
</p>
<pre class="codeblock">
<code>apiVersion: v1
kind: ConfigMap
data:
 public-ports: 80;443;&lt;port1&gt;;&lt;port2&gt;
metadata:
  creationTimestamp: 2017-08-22T19:06:51Z
  name: ibm-cloud-provider-ingress-cm
  namespace: kube-system
  resourceVersion: "1320"
  selfLink: /api/v1/namespaces/kube-system/configmaps/ibm-cloud-provider-ingress-cm
  uid: &lt;uid&gt;</code></pre></li>
 <li>验证是否将 ALB 重新配置为使用 TCP 端口。
<pre class="pre">
<code>kubectl get service -n kube-system</code></pre>
CLI 输出类似于以下内容：
<pre class="screen">
<code>NAME                                             TYPE           CLUSTER-IP       EXTERNAL-IP    PORT(S)                      AGE
public-cr18e61e63c6e94b658596ca93d087eed9-alb1   LoadBalancer   10.xxx.xx.xxx  169.xx.xxx.xxx &lt;port1&gt;:30776/TCP,&lt;port2&gt;:30412/TCP   109d</code></pre></li>
<li>将 Ingress 配置为通过非标准 TCP 端口访问应用程序。在此引用中使用样本 YAML 文件。</li>
<li>创建 ALB 资源或更新现有 ALB 配置。
<pre class="pre">
<code>kubectl apply -f myingress.yaml</code></pre>
</li>
<li>通过 Curl 命令获取用于访问应用程序的 Ingress 子域。示例：<code>curl &lt;domain&gt;:&lt;ingressPort&gt;</code></li></ol></dd></dl>

<br />


## 连接注释
{: #connection}

通过使用连接注释，可以更改 ALB 连接到后端应用程序和上游服务器的方式，并设置应用程序或服务器被视为不可用之前的超时或最大保持活动连接数。
{: shortdesc}

### 定制连接超时和读取超时（proxy-connect-timeout 和 proxy-read-timeout）
{: #proxy-connect-timeout}

设置 ALB 等待连接到后端应用程序以及从后端应用程序进行读取的时间，超过该时间后，后端应用程序将视为不可用。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>将客户机请求发送到 Ingress ALB 时，ALB 会打开与后端应用程序的连接。缺省情况下，ALB 会等待 60 秒以接收来自后端应用程序的应答。如果后端应用程序在 60 秒内未应答，那么连接请求将异常中止，并且后端应用程序将视为不可用。



</br></br>
ALB 连接到后端应用程序后，ALB 会从后端应用程序读取响应数据。在此读操作期间，ALB 在两次读操作之间等待最长 60 秒以接收来自后端应用程序的数据。如果后端应用程序在 60 秒内未发送数据，那么与后端应用程序的连接请求将关闭，并且后端应用程序将视为不可用。
</br></br>
60 秒连接超时和读取超时是代理上的缺省超时，通常不应进行更改。
</br></br>
如果由于工作负载过高而导致应用程序的可用性不稳定或应用程序响应速度缓慢，那么您可能会希望增大连接超时或读取超时。请记住，增大超时会影响 ALB 的性能，因为与后端应用程序的连接必须保持打开状态，直至达到超时为止。
</br></br>
另一方面，您可以减小超时以提高 ALB 的性能。确保后端应用程序能够在指定的超时内处理请求，即使在更高的工作负载期间。</dd>
<dt>样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
annotations:
   ingress.bluemix.net/proxy-connect-timeout: "serviceName=&lt;myservice&gt; timeout=&lt;connect_timeout&gt;"
   ingress.bluemix.net/proxy-read-timeout: "serviceName=&lt;myservice&gt; timeout=&lt;read_timeout&gt;"
spec:
tls:
 - hosts:
   - mydomain
    secretName: mytlssecret
  rules:
 - host: mydomain
   http:
paths:
     - path: /
       backend:
         serviceName: myservice
         servicePort: 8080</code></pre>

<table>
<caption>了解注释的组成部分</caption>
 <thead>
 <th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
 </thead>
 <tbody>
 <tr>
 <td><code>&lt;connect_timeout&gt;</code></td>
 <td>等待连接到后端应用程序的秒数或分钟数，例如 <code>65s</code> 或 <code>1m</code>。连接超时不能超过 75 秒。</td>
 </tr>
 <tr>
 <td><code>&lt;read_timeout&gt;</code></td>
 <td>读取后端应用程序之前等待的秒数或分钟数，例如 <code>65s</code> 或 <code>2m</code>。
 </tr>
 </tbody></table>

 </dd></dl>

<br />



### 保持活动请求数 (keepalive-requests)
{: #keepalive-requests}

设置可通过一个保持活动连接处理的最大请求数。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>
 设置可通过一个保持活动连接处理的最大请求数。
 </dd>


<dt>样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
annotations:
  ingress.bluemix.net/keepalive-requests: "serviceName=&lt;myservice&gt; requests=&lt;max_requests&gt;"
spec:
tls:
- hosts:
  - mydomain
    secretName: mytlssecret
  rules:
- host: mydomain
  http:
paths:
    - path: /
      backend:
        serviceName: &lt;myservice&gt;
        servicePort: 8080</code></pre>

<table>
<caption>了解注释的组成部分</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
</thead>
<tbody>
<tr>
<td><code>serviceName</code></td>
<td>将 <code>&lt;<em>myservice</em>&gt;</code> 替换为您针对应用程序创建的 Kubernetes 服务的名称。此参数是可选的。除非指定了服务，否则配置将应用于 Ingress 主机中的所有服务。如果提供了此参数，那么将为给定的服务设置保持活动请求数。如果未提供此参数，那么将在 <code>nginx.conf</code> 的服务器级别为所有未配置保持活动请求数的服务设置保持活动请求数。</td>
</tr>
<tr>
<td><code>requests</code></td>
<td>将 <code>&lt;<em>max_requests</em>&gt;</code> 替换为可通过一个保持活动连接处理的最大请求数。</td>
</tr>
</tbody></table>

</dd>
</dl>

<br />



### 保持活动超时 (keepalive-timeout)
{: #keepalive-timeout}

设置保持活动连接在服务器端保持打开状态的最长时间。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>
设置保持活动连接在服务器上保持打开状态的最长时间。
</dd>


<dt>样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
annotations:
   ingress.bluemix.net/keepalive-timeout: "serviceName=&lt;myservice&gt; timeout=&lt;time&gt;s"
spec:
tls:
 - hosts:
   - mydomain
    secretName: mytlssecret
  rules:
 - host: mydomain
   http:
paths:
     - path: /
       backend:
         serviceName: myservice
         servicePort: 8080</code></pre>

<table>
<caption>了解注释的组成部分</caption>
 <thead>
 <th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
 </thead>
 <tbody>
 <tr>
 <td><code>serviceName</code></td>
 <td>将 <code>&lt;<em>myservice</em>&gt;</code> 替换为您针对应用程序创建的 Kubernetes 服务的名称。此参数是可选的。如果提供了此参数，那么将为给定的服务设置保持活动超时。如果未提供此参数，那么将在 <code>nginx.conf</code> 的服务器级别为所有未配置保持活动超时的服务设置保持活动超时。</td>
 </tr>
 <tr>
 <td><code>timeout</code></td>
 <td>将 <code>&lt;<em>time</em>&gt;</code> 替换为时间长度（以秒为单位）。示例：<code>timeout=20s</code>。值为零将禁用保持活动客户机连接。</td>
 </tr>
 </tbody></table>

 </dd>
 </dl>

<br />


### 作为代理传递到下一个上游 (proxy-next-upstream-config)
{: #proxy-next-upstream-config}

设置 ALB 何时可以向下一个上游服务器传递请求。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>
Ingress ALB 充当客户机应用程序和您的应用程序之间的代理。某些应用程序设置需要多个上游服务器来处理来自 ALB 的入局客户机请求。有时，ALB 使用的代理服务器无法与应用程序使用的上游服务器建立连接。于是 ALB 可以尝试与下一个上游服务器建立连接，以改为将请求传递到这一个上游服务器。可以使用 `proxy-next-upstream-config` 注释来设置在哪些情况下 ALB 可以尝试将请求传递到下一个上游服务器，以及尝试的时间长度和次数。<p class="note">使用 `proxy-next-upstream-config` 时，始终会配置超时，所以不要将 `timeout=true` 添加到此注释。</p>
</dd>
<dt>样本 Ingress 资源 YAML</dt>
<dd>
<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
annotations:
    ingress.bluemix.net/proxy-next-upstream-config: "serviceName=&lt;myservice1&gt; retries=&lt;tries&gt; timeout=&lt;time&gt; error=true http_502=true; serviceName=&lt;myservice2&gt; http_403=true non_idempotent=true"
spec:
tls:
  - hosts:
    - mydomain
    secretName: mysecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /
        backend:
          serviceName: myservice1
          servicePort: 80
</code></pre>

<table>
<caption>了解注释的组成部分</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
</thead>
<tbody>
<tr>
<td><code>serviceName</code></td>
<td>将 <code>&lt;<em>myservice</em>&gt;</code> 替换为您针对应用程序创建的 Kubernetes 服务的名称。</td>
</tr>
<tr>
<td><code>retries</code></td>
<td>将 <code>&lt;<em>tries</em>&gt;</code> 替换为 ALB 尝试将请求传递到下一个上游服务器的最大次数。此数字包括原始请求。要关闭此限制，请使用 <code>0</code>。如果不指定值，将使用缺省值 <code>0</code>。
</td>
</tr>
<tr>
<td><code>timeout</code></td>
<td>将 <code>&lt;<em>time</em>&gt;</code> 替换为 ALB 尝试将请求传递到下一个上游服务器的最长时间（以秒为单位）。例如，要设置 30 秒时间，请输入 <code>30s</code>。要关闭此限制，请使用 <code>0</code>。如果不指定值，将使用缺省值 <code>0</code>。
</td>
</tr>
<tr>
<td><code>error</code></td>
<td>如果设置为 <code>true</code>，那么在与第一个上游服务器建立连接，向其传递请求或读取响应头时发生错误的情况下，ALB 会将请求传递到下一个上游服务器。
</td>
</tr>
<tr>
<td><code>invalid_header</code></td>
<td>如果设置为 <code>true</code>，那么在第一个上游服务器返回空响应或无效响应时，ALB 会将请求传递到下一个上游服务器。
</td>
</tr>
<tr>
<td><code>http_502</code></td>
<td>如果设置为 <code>true</code>，那么在第一个上游服务器返回代码为 502 的响应时，ALB 会将请求传递到下一个上游服务器。可以指定以下 HTTP 响应代码：<code>500</code>、<code>502</code>、<code>503</code>、<code>504</code>、<code>403</code>、<code>404</code> 或 <code>429</code>。
</td>
</tr>
<tr>
<td><code>non_idempotent</code></td>
<td>如果设置为 <code>true</code>，那么 ALB 可以使用非幂等方法将请求传递到下一个上游服务器。缺省情况下，ALB 不会将这些请求传递到下一个上游服务器。
</td>
</tr>
<tr>
<td><code>off</code></td>
<td>要阻止 ALB 将请求传递到下一个上游服务器，请设置为 <code>true</code>。
</td>
</tr>
</tbody></table>
</dd>
</dl>

<br />


### 使用 cookie 确保会话亲缘关系 (sticky-cookie-services)
{: #sticky-cookie-services}

使用粘性 cookie 注释向 ALB 添加会话亲缘关系，并始终将入局网络流量路由到同一个上游服务器。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>为了实现高可用性，某些应用程序设置要求您部署多个上游服务器来处理入局客户机请求。客户机连接到后端应用程序后，可以使用会话亲缘关系，使得在会话期间或完成任务所需的时间内，客户机由同一个上游服务器处理。您可以将 ALB 配置为始终将入局网络流量路由到同一个上游服务器来确保会话亲缘关系。


</br></br>
连接到后端应用程序的每个客户机都会由 ALB 分配其中一个可用的上游服务器。ALB 会创建会话 cookie，该会话 cookie 存储在客户机的应用程序中，并且包含在 ALB 和客户机之间每个请求的头信息中。该 cookie 中的信息将确保在整个会话中的所有请求都由同一个上游服务器进行处理。


</br></br>
当包含多个服务时，请使用分号 (;) 来分隔这些服务。</dd>
<dt>样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
annotations:
    ingress.bluemix.net/sticky-cookie-services: "serviceName=&lt;myservice1&gt; name=&lt;cookie_name1&gt; expires=&lt;expiration_time1&gt; path=&lt;cookie_path1&gt; hash=&lt;hash_algorithm1&gt;;serviceName=&lt;myservice2&gt; name=&lt;cookie_name2&gt; expires=&lt;expiration_time2&gt; path=&lt;cookie_path2&gt; hash=&lt;hash_algorithm2&gt;"
spec:
tls:
  - hosts:
    - mydomain
    secretName: mytlssecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /service1_path
        backend:
          serviceName: &lt;myservice1&gt;
          servicePort: 8080
      - path: /service2_path
        backend:
          serviceName: &lt;myservice2&gt;
          servicePort: 80</code></pre>

  <table>
  <caption>了解注释的组成部分</caption>
  <thead>
  <th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
  </thead>
  <tbody>
  <tr>
  <td><code>serviceName</code></td>
  <td>将 <code>&lt;<em>myservice</em>&gt;</code> 替换为您针对应用程序创建的 Kubernetes 服务的名称。</td>
  </tr>
  <tr>
  <td><code>name</code></td>
  <td>将 <code><em>&lt;cookie_name&gt;</em></code> 替换为在会话期间创建的粘性 cookie 的名称。</td>
  </tr>
  <tr>
  <td><code>expires</code></td>
  <td>将 <code>&lt;<em>expiration_time</em>&gt;</code> 替换为时间，以秒 (s)、分钟 (m) 或小时 (h) 为单位；超过该时间后，粘性 cookie 到期。此时间与用户活动无关。该 cookie 到期后，会被客户机 Web 浏览器删除，并且不会再发送到 ALB。例如，要将到期时间设置为 1 秒、1 分钟或 1 小时，请输入 <code>1s</code>、<code>1m</code> 或 <code>1h</code>。</td>
  </tr>
  <tr>
  <td><code>path</code></td>
  <td>将 <code><em>&lt;cookie_path&gt;</em></code> 替换为附加到 Ingress 子域的路径，该路径指示针对哪些域和子域将 cookie 发送到 ALB。例如，如果 Ingress 域为 <code>www.myingress.com</code>，并且您希望在每个客户机请求中都发送 cookie，那么必须设置 <code>path=/</code>。如果希望仅针对 <code>www.myingress.com/myapp</code> 及其所有子域发送 cookie，那么必须设置 <code>path=/myapp</code>。</td>
  </tr>
  <tr>
  <td><code>hash</code></td>
  <td>将 <code><em>&lt;hash_algorithm&gt;</em></code> 替换为用于保护 cookie 中信息的散列算法。仅支持 <code>sha1</code>。SHA1 基于 cookie 中的信息创建散列总和，并将此散列总和附加到 cookie。服务器可以解密 cookie 中的信息并验证数据完整性。</td>
  </tr>
  </tbody></table>

 </dd></dl>

<br />


### 上游故障超时 (upstream-fail-timeout)
{: #upstream-fail-timeout}

设置 ALB 可以尝试连接到服务器的时间量。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>
设置在服务器被视为不可用之前，ALB 可以尝试连接到服务器的时间量。如果要将服务器视为不可用，ALB 必须在设置的时间量内达到 <a href="#upstream-max-fails"><code>upstream-max-fails</code> 注释</a>设置的最大失败连接尝试次数。此时间量还可确定服务器被视为不可用的持续时间。
</dd>


<dt>样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
annotations:
    ingress.bluemix.net/upstream-fail-timeout: "serviceName=&lt;myservice&gt; fail-timeout=&lt;fail_timeout&gt;"
spec:
tls:
  - hosts:
    - mydomain
    secretName: mytlssecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /
        backend:
          serviceName: myservice
          servicePort: 8080</code></pre>

<table>
<thead>
<th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
</thead>
<tbody>
<tr>
<td><code>serviceName（可选）</code></td>
<td>将 <code>&lt;<em>myservice</em>&gt;</code> 替换为您针对应用程序创建的 Kubernetes 服务的名称。</td>
</tr>
<tr>
<td><code>fail-timeout</code></td>
<td>将 <code>&lt;<em>fail_timeout</em>&gt;</code> 替换为在服务器被视为不可用之前，ALB 可以尝试连接到服务器的时间量。缺省值为 <code>10s</code>。时间必须以秒为单位。</td>
</tr>
</tbody></table>
</dd>
</dl>

<br />


### 上游保持活动连接数 (upstream-keepalive)
{: #upstream-keepalive}

设置上游服务器的最大空闲保持活动连接数。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>
设置给定服务的上游服务器的最大空闲保持活动连接数。缺省情况下，上游服务器具有 64 个空闲保持活动连接。
  </dd>


<dt>样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
annotations:
    ingress.bluemix.net/upstream-keepalive: "serviceName=&lt;myservice&gt; keepalive=&lt;max_connections&gt;"
spec:
tls:
  - hosts:
    - mydomain
    secretName: mytlssecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /
        backend:
          serviceName: myservice
          servicePort: 8080</code></pre>

<table>
<caption>了解注释的组成部分</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
</thead>
<tbody>
<tr>
<td><code>serviceName</code></td>
<td>将 <code>&lt;<em>myservice</em>&gt;</code> 替换为您针对应用程序创建的 Kubernetes 服务的名称。</td>
</tr>
<tr>
<td><code>keepalive</code></td>
<td>将 <code>&lt;<em>max_connections</em>&gt;</code> 替换为上游服务器的最大空闲保持活动连接数。缺省值为 <code>64</code>。值为 <code>0</code> 将禁用给定服务的上游保持活动连接。</td>
</tr>
</tbody></table>
</dd>
</dl>

<br />


### 上游最大失败次数 (upstream-max-fails)
{: #upstream-max-fails}

设置尝试与服务器通信失败的最大次数。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>
设置在服务器被视为不可用之前，ALB 可以尝试连接到服务器失败的最大次数。如果要将服务器视为不可用，ALB 必须在 <a href="#upstream-fail-timeout"><code>upstream-fail-timeout</code> 注释</a>设置的持续时间内达到最大次数。此外，还可通过 <code>upstream-fail-timeout</code> 注释设置服务器被视为不可用的持续时间。</dd>


<dt>样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
annotations:
    ingress.bluemix.net/upstream-max-fails: "serviceName=&lt;myservice&gt; max-fails=&lt;max_fails&gt;"
spec:
tls:
  - hosts:
    - mydomain
    secretName: mytlssecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /
        backend:
          serviceName: myservice
          servicePort: 8080</code></pre>

<table>
<thead>
<th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
</thead>
<tbody>
<tr>
<td><code>serviceName（可选）</code></td>
<td>将 <code>&lt;<em>myservice</em>&gt;</code> 替换为您针对应用程序创建的 Kubernetes 服务的名称。</td>
</tr>
<tr>
<td><code>max-fails</code></td>
<td>将 <code>&lt;<em>max_fails</em>&gt;</code> 替换为 ALB 可以尝试与服务器通信失败的最大次数。缺省值为 <code>1</code>。<code>0</code> 值将禁用此注释。</td>
</tr>
</tbody></table>
</dd>
</dl>

<br />


## HTTPS 和 TLS/SSL 认证注释
{: #https-auth}

通过使用 HTTPS 和 TLS/SSL 认证注释，可以配置 ALB 用于 HTTPS 流量，更改缺省 HTTPS 端口，对发送到后端应用程序的流量启用 SSL 加密，或设置相互认证。
{: shortdesc}

### {{site.data.keyword.appid_short_notm}} 认证 (appid-auth)
{: #appid-auth}

使用 {{site.data.keyword.appid_full_notm}} 向应用程序进行认证。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>
  使用 {{site.data.keyword.appid_short_notm}} 对 Web 或 API HTTP/HTTPS 请求进行认证。

<p>如果将请求类型设置为 <code>web</code>，那么将验证包含 {{site.data.keyword.appid_short_notm}} 访问令牌的 Web 请求。如果令牌验证失败，将拒绝 Web 请求。如果请求不包含访问令牌，那么会将请求重定向到 {{site.data.keyword.appid_short_notm}} 登录页面。要使 {{site.data.keyword.appid_short_notm}} Web 认证能够正常运作，必须在用户的浏览器中启用 cookie。</p>

<p>如果将请求类型设置为 <code>api</code>，那么将验证包含 {{site.data.keyword.appid_short_notm}} 访问令牌的 API 请求。如果请求不包含访问令牌，将向用户返回 <code>401: Unauthorized</code> 错误消息。</p>

<p class="note">出于安全原因，{{site.data.keyword.appid_short_notm}} 认证仅支持启用了 TLS/SSL 的后端。</p>
</dd>
<dt>样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
annotations:
      ingress.bluemix.net/appid-auth: "bindSecret=&lt;bind_secret&gt; namespace=&lt;namespace&gt; requestType=&lt;request_type&gt; serviceName=&lt;myservice&gt;"
spec:
tls:
  - hosts:
    - mydomain
    secretName: mytlssecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /
        backend:
          serviceName: myservice
          servicePort: 8080</code></pre>

<table>
<caption>了解注释的组成部分</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
</thead>
<tbody>
<tr>
<td><code>bindSecret</code></td>
<td>将 <em><code>&lt;bind_secret&gt;</code></em> 替换为存储 {{site.data.keyword.appid_short_notm}} 服务实例的绑定私钥的 Kubernetes 私钥。</td>
</tr>
<tr>
<td><code>namespace</code></td>
<td>将 <em><code>&lt;namespace&gt;</code></em> 替换为绑定私钥的名称空间。此字段缺省为 `default` 名称空间。</td>
</tr>
<tr>
<td><code>requestType</code></td>
<td>将 <code><em>&lt;request_type&gt;</em></code> 替换为要发送到 {{site.data.keyword.appid_short_notm}} 的请求的类型。接受的值为 `web` 或 `api`。缺省值为 `api`。</td>
</tr>
<tr>
<td><code>serviceName</code></td>
<td>将 <code><em>&lt;myservice&gt;</em></code> 替换为您针对应用程序创建的 Kubernetes 服务的名称。这是必填字段。如果未包含服务名称，那么将对所有服务启用注释。如果包含服务名称，那么仅对该服务启用注释。使用逗号 (,) 分隔多个服务。</td>
</tr>
</tbody></table>
</dd>
<dt>用法</dt></dl>

由于应用程序使用 {{site.data.keyword.appid_short_notm}} 进行认证，因此必须供应 {{site.data.keyword.appid_short_notm}} 实例，使用有效的重定向 URI 来配置实例，并通过将实例绑定到集群来生成绑定私钥。

1. 选择现有或创建新的 {{site.data.keyword.appid_short_notm}} 实例。
    * 要使用现有实例，请确保服务实例名称不包含空格。要除去空格，请选择服务实例名称旁边的“更多选项”菜单，然后选择**重命名服务**。
    * 要供应[新 {{site.data.keyword.appid_short_notm}} 实例](https://console.bluemix.net/catalog/services/app-id)，请执行以下操作：
        1. 将自动填充的**服务名称**替换为您自己的服务实例唯一名称。
            服务实例名称不能包含空格。
        2. 选择部署了您的集群的区域。
        3. 单击**创建**。
2. 添加应用程序的重定向 URL。重定向 URL 是应用程序的回调端点。要防止钓鱼攻击，应用程序标识将根据重定向 URL 的白名单来验证请求 URL。
    1. 在 {{site.data.keyword.appid_short_notm}} 管理控制台中，浏览至**身份提供者 > 管理**。
    2. 确保已选择身份提供者。如果未选择身份提供者，那么不会对用户进行认证，但会向用户颁发访问令牌以供匿名访问应用程序。
    3. 在**添加 Web 重定向 URL** 字段中，以 `http://<hostname>/<app_path>/appid_callback` 或 `https://<hostname>/<app_path>/appid_callback` 格式添加应用程序的重定向 URL。
        * 例如，向 IBM Ingress 子域注册的应用程序可能类似于 `https://mycluster.us-south.containers.appdomain.cloud/myapp1path/appid_callback`。
        * 向定制域注册的应用程序可能类似于 `http://mydomain.net/myapp2path/appid_callback`。

3. 将 {{site.data.keyword.appid_short_notm}} 服务实例与集群绑定。
    ```
    ibmcloud ks cluster-service-bind <cluster_name_or_ID> <namespace> <service_instance_name>
    ```
    {: pre}
服务成功添加到集群后，将创建集群私钥，用于保存服务实例的凭证。示例 CLI 输出：
    ```
    ibmcloud ks cluster-service-bind mycluster mynamespace appid1
    Binding service instance to namespace...
    OK
    Namespace:    mynamespace
    Secret name:  binding-<service_instance_name>
    ```
    {: screen}

4. 获取在集群名称空间中创建的私钥。
    ```
    kubectl get secrets --namespace=<namespace>
    ```
    {: pre}

5. 使用绑定私钥和集群名称空间，将 `appid-auth` 注释添加到 Ingress 资源。

<br />



### 定制 HTTP 和 HTTPS 端口 (custom-port)
{: #custom-port}

更改 HTTP（端口 80）和 HTTPS（端口 443）网络流量的缺省端口。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>缺省情况下，Ingress ALB 配置为在端口 80 上侦听入局 HTTP 网络流量，在端口 443 上侦听入局 HTTPS 网络流量。您可以更改缺省端口以向 ALB 域添加安全性，或仅启用 HTTPS 端口。

<p class="note">要在端口上启用相互认证，请[配置 ALB 以打开有效端口](cs_ingress.html#opening_ingress_ports)，然后在 [`mutual-auth` 注释](#mutual-auth)中指定该端口。不要使用 `custom-port` 注释来指定用于相互认证的端口。</p></dd>


<dt>样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
annotations:
    ingress.bluemix.net/custom-port: "protocol=&lt;protocol1&gt; port=&lt;port1&gt;;protocol=&lt;protocol2&gt;port=&lt;port2&gt;"
spec:
tls:
 - hosts:
   - mydomain
    secretName: mytlssecret
  rules:
 - host: mydomain
   http:
paths:
     - path: /
       backend:
         serviceName: myservice
         servicePort: 8080</code></pre>

<table>
<caption>了解注释的组成部分</caption>
 <thead>
 <th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
 </thead>
 <tbody>
 <tr>
 <td><code>&lt;protocol&gt;</code></td>
 <td>输入 <code>http</code> 或 <code>https</code> 以更改入局 HTTP 或 HTTPS 网络流量的缺省端口。</td>
 </tr>
 <tr>
 <td><code>&lt;port&gt;</code></td>
 <td>输入要用于入局 HTTP 或 HTTPS 网络流量的端口号。<p class="note">指定定制端口用于 HTTP 或 HTTPS 时，缺省端口对于 HTTP 和 HTTPS 都不再有效。例如，要将 HTTPS 的缺省端口更改为 8443，而对 HTTP 使用缺省端口，那么必须为两者设置定制端口：<code>custom-port: "protocol=http port=80; protocol=https port=8443"</code>。</p></td>
 </tr>
 </tbody></table>

 </dd>
 <dt>用法</dt>
 <dd><ol><li>查看 ALB 的打开端口。
<pre class="pre">
<code>kubectl get service -n kube-system</code></pre>
CLI 输出类似于以下内容：
<pre class="screen">
<code>NAME                                             TYPE           CLUSTER-IP       EXTERNAL-IP    PORT(S)                      AGE
public-cr18e61e63c6e94b658596ca93d087eed9-alb1   LoadBalancer   10.xxx.xx.xxx    169.xx.xxx.xxx 80:30416/TCP,443:32668/TCP   109d</code></pre></li>
<li>打开 ALB 配置映射。
<pre class="pre">
<code>kubectl edit configmap ibm-cloud-provider-ingress-cm -n kube-system</code></pre></li>
<li>将非缺省 HTTP 和 HTTPS 端口添加到配置映射。将 &lt;port&gt; 替换为要打开的 HTTP 或 HTTPS 端口。
<p class="note">缺省情况下，端口 80 和 443 已打开。如果要使 80 和 443 保持打开，那么必须在 `public-ports` 字段中包含这两个端口以及您指定的其他任何 TCP 端口。如果启用了专用 ALB，那么还必须在 `private-ports` 字段中指定要保持打开的任何端口。有关更多信息，请参阅<a href="cs_ingress.html#opening_ingress_ports">在 Ingress ALB 中打开端口</a>。
</p>
<pre class="codeblock">
<code>apiVersion: v1
kind: ConfigMap
data:
  public-ports: &lt;port1&gt;;&lt;port2&gt;
metadata:
  creationTimestamp: 2017-08-22T19:06:51Z
  name: ibm-cloud-provider-ingress-cm
  namespace: kube-system
  resourceVersion: "1320"
  selfLink: /api/v1/namespaces/kube-system/configmaps/ibm-cloud-provider-ingress-cm
  uid: &lt;uid&gt;</code></pre></li>
 <li>验证是否已将 ALB 重新配置为使用非缺省端口。
<pre class="pre">
<code>kubectl get service -n kube-system</code></pre>
CLI 输出类似于以下内容：
<pre class="screen">
<code>NAME                                             TYPE           CLUSTER-IP       EXTERNAL-IP    PORT(S)                      AGE
public-cr18e61e63c6e94b658596ca93d087eed9-alb1   LoadBalancer   10.xxx.xx.xxx  169.xx.xxx.xxx &lt;port1&gt;:30776/TCP,&lt;port2&gt;:30412/TCP   109d</code></pre></li>
<li>配置 Ingress 以在将入局网络流量路由到服务时使用非缺省端口。在此引用中使用样本 YAML 文件。</li>
<li>更新 ALB 配置。
<pre class="pre">
<code>kubectl apply -f myingress.yaml</code></pre>
</li>
<li>打开首选 Web 浏览器以访问您的应用程序。示例：<code>https://&lt;ibmdomain&gt;:&lt;port&gt;/&lt;service_path&gt;/</code></li></ol></dd></dl>

<br />



### HTTP 重定向到 HTTPS (redirect-to-https)
{: #redirect-to-https}

将不安全的 HTTP 客户机请求转换为 HTTPS。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>将 Ingress ALB 设置为通过 IBM 提供的 TLS 证书或定制 TLS 证书来保护域。某些用户可能会尝试向 ALB 域发出不安全的 <code>http</code> 请求（例如 <code>http://www.myingress.com</code>，而不是使用 <code>https</code>）来访问应用程序。可以使用重定向注释始终将不安全的 HTTP 请求转换为 HTTPS。如果不使用此注释，缺省情况下，不安全的 HTTP 请求不会转换为 HTTPS 请求，并且可能会向公众公开未加密的保密信息。

 

</br></br>
缺省情况下，HTTP 请求到 HTTPS 的重定向是禁用的。</dd>

<dt>样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
annotations:
    ingress.bluemix.net/redirect-to-https: "True"
spec:
tls:
 - hosts:
   - mydomain
    secretName: mytlssecret
  rules:
 - host: mydomain
   http:
paths:
     - path: /
       backend:
         serviceName: myservice
         servicePort: 8080</code></pre>

</dd>

</dl>

<br />


### HTTP 严格传输安全性 (hsts)
{: #hsts}

<dl>
<dt>描述</dt>
<dd>
HSTS 指示浏览器仅使用 HTTPS 访问域。即使用户输入或访问普通 HTTP 链接，浏览器也会严格地将连接升级到 HTTPS。
</dd>


<dt>样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
annotations:
    ingress.bluemix.net/hsts: enabled=true maxAge=&lt;31536000&gt; includeSubdomains=true
spec:
tls:
  - hosts:
    - mydomain
    secretName: mysecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /service1_path
        backend:
          serviceName: myservice1
          servicePort: 8443
      - path: /service2_path
        backend:
          serviceName: myservice2
          servicePort: 8444
          </code></pre>

<table>
<caption>了解注释的组成部分</caption>
  <thead>
  <th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
  </thead>
  <tbody>
  <tr>
  <td><code>enabled</code></td>
  <td>使用 <code>true</code> 以启用 HSTS。</td>
  </tr>
    <tr>
  <td><code>maxAge</code></td>
  <td>将 <code>&lt;<em>31536000</em>&gt;</code> 替换为整数，该整数表示浏览器将发送的请求直接高速缓存到 HTTPS 的秒数。缺省值为 <code>31536000</code>，等于 1 年。</td>
  </tr>
  <tr>
  <td><code>includeSubdomains</code></td>
  <td>使用 <code>true</code> 以指示浏览器 HSTS 策略也适用于当前域的所有子域。缺省值为 <code>true</code>。</td>
  </tr>
  </tbody></table>

  </dd>
  </dl>


<br />


### 相互认证 (mutual-auth)
{: #mutual-auth}

为 ALB 配置相互认证。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>
为 Ingress ALB 配置下游流量的相互认证。外部客户机会认证服务器，而服务器也会使用证书来认证客户机。相互认证也称为基于证书的认证或双向认证。
 </br></br>
对于客户机与 Ingress ALB 之间的 SSL 终止，请使用 `mutual-auth` 注释。对于 Ingress ALB 与后端应用程序之间的 SSL 终止，请使用 [`ssl-services` 注释](#ssl-services)。</dd>

<dt>先决条件</dt>
<dd>
<ul>
<li>您必须具有包含所需 <code>client.crt</code> 的有效相互认证私钥。要创建相互认证私钥，请参阅此部分末尾的步骤。</li>
<li>要在 443 之外的端口上启用相互认证，请[配置 ALB 以打开有效端口](cs_ingress.html#opening_ingress_ports)，然后在此注释中指定该端口。不要使用 `custom-port` 注释来指定用于相互认证的端口。</li>
</ul>
</dd>

<dt>样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
annotations:
  ingress.bluemix.net/mutual-auth: "secretName=&lt;mysecret&gt; port=&lt;port&gt; serviceName=&lt;servicename1&gt;,&lt;servicename2&gt;"
spec:
tls:
  - hosts:
    - mydomain
    secretName: mytlssecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /
        backend:
          serviceName: myservice
          servicePort: 8080</code></pre>

<table>
<caption>了解注释的组成部分</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
</thead>
<tbody>
<tr>
<td><code>secretName</code></td>
<td>将 <code>&lt;<em>mysecret</em>&gt;</code> 替换为私钥资源的名称。</td>
</tr>
<tr>
<td><code>port</code></td>
<td>将 <code>&lt;<em>port</em>&gt;</code> 替换为 ALB 端口号。</td>
</tr>
<tr>
<td><code>serviceName</code></td>
<td>将 <code><em>&lt;serviceName&gt;</em></code> 替换为一个或多个 Ingress 资源的名称。此参数是可选的。</td>
</tr>
</tbody></table>

</dd>
</dl>

**要创建相互认证私钥，请执行以下操作：**

1. 通过下列其中一种方式生成密钥和证书：
    * 通过证书提供者生成认证中心 (CA) 证书和密钥。如果您有自己的域，请为您的域购买正式的 TLS 证书。请确保每个证书的 [CN ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://support.dnsimple.com/articles/what-is-common-name/) 都是不同的。
    * 出于测试目的，可以使用 OpenSSL 创建自签名证书。有关更多信息，请参阅此[自签名 SSL 证书教程 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.akadia.com/services/ssh_test_certificate.html)。
        1. 创建 `client.key`。
            ```
            openssl genrsa -out client.key 1024
            ```
            {: pre}
        2. 使用密钥创建 `client.crt`。
            ```
            openssl req -new -x509 -key client.key -out client.crt
            ```
            {: pre}
        3. 使用 `client.crt` 创建自签名证书。
            ```
            openssl x509 -req -in example.org.csr -CA client.crt -CAkey client.key -CAcreateserial -out example.org.crt
            ```
            {: pre}
2. [将证书转换为 Base64 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.base64encode.org/)。
3. 使用证书创建私钥 YAML 文件。
     ```
     apiVersion: v1
     kind: Secret
     metadata:
       name: ssl-my-test
     type: Opaque
     data:
       client.crt: <ca_certificate>
     ```
     {: codeblock}
4. 将证书创建为 Kubernetes 私钥。
     ```
     kubectl create -f ssl-my-test
     ```
     {: pre}

<br />



### SSL 服务支持 (ssl-services)
{: #ssl-services}

允许对上游应用程序进行 HTTPS 请求，并对流入上游应用程序的流量加密。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>
Ingress 资源配置具有 TLS 部分时，Ingress ALB 可以处理向应用程序发出的通过 HTTPS 保护的 URL 请求。缺省情况下，ALB 会终止 TLS 终止，并在使用 HTTP 协议将流量转发到应用程序之前对请求解密。如果您具有需要 HTTPS 协议且需要对流量加密的应用程序，请使用 `ssl-services` 注释。通过使用 `ssl-services` 注释，ALB 将终止外部 TLS 连接，然后在 ALB 和应用程序 pod 之间创建新的 SSL 连接。在将流量发送到上游 pod 之前，会对流量重新加密。</br></br>
如果后端应用程序可以处理 TLS，并且您希望添加额外的安全性，那么可以通过提供私钥中包含的证书来添加单向或相互认证。</br></br>
对于 Ingress ALB 与后端应用程序之间的 SSL 终止，请使用 `ssl-services` 注释。对于客户机与 Ingress ALB 之间的 SSL 终止，请使用 [`mutual-auth` 注释](#mutual-auth)。</dd>

<dt>样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: &lt;myingressname&gt;
annotations:
    ingress.bluemix.net/ssl-services: |
      ssl-service=&lt;myservice1&gt; ssl-secret=&lt;service1-ssl-secret&gt;;
      ssl-service=&lt;myservice2&gt; ssl-secret=&lt;service2-ssl-secret&gt;
spec:
tls:
  - hosts:
    - mydomain
    secretName: mysecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /service1_path
        backend:
          serviceName: myservice1
          servicePort: 8443
      - path: /service2_path
        backend:
          serviceName: myservice2
          servicePort: 8444
          </code></pre>

<table>
<caption>了解注释的组成部分</caption>
  <thead>
  <th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
  </thead>
  <tbody>
  <tr>
  <td><code>ssl-service</code></td>
  <td>将 <code>&lt;<em>myservice</em>&gt;</code> 替换为需要 HTTPS 的服务的名称。将加密从 ALB 到此应用程序服务的流量。</td>
  </tr>
  <tr>
  <td><code>ssl-secret</code></td>
  <td>如果后端应用程序可以处理 TLS，并且您希望添加额外的安全性，请将 <code>&lt;<em>service-ssl-secret</em>&gt;</code> 替换为该服务的单向或相互认证私钥。<ul><li>如果提供了单向认证私钥，那么该值必须包含来自上游服务器的 <code>trusted.crt</code>。要创建单向认证私钥，请参阅此部分末尾的步骤。</li><li>如果提供了相互认证私钥，那么值必须包含应用程序期望从客户机收到的必需的 <code>client.crt</code> 和 <code>client.key</code>。要创建相互认证私钥，请参阅此部分末尾的步骤。</li></ul><p class="important">如果未提供私钥，系统会允许不安全连接。如果要测试连接并且证书尚未就绪，或者如果证书已到期并且您希望允许不安全的连接，那么可选择省略私钥。</p></td>
  </tr>
  </tbody></table>

  </dd>
  </dl>

**要创建单向认证私钥，请执行以下操作：**

1. 从上游服务器获取认证中心 (CA) 密钥和证书。
2. [将证书转换为 Base64 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.base64encode.org/)。
3. 使用证书创建私钥 YAML 文件。
     ```
     apiVersion: v1
     kind: Secret
     metadata:
       name: ssl-my-test
     type: Opaque
     data:
       trusted.crt: <ca_certificate>
     ```
     {: codeblock}

     如果您还希望对上游流量强制执行相互认证，那么除了在 data 部分中提供 `trusted.crt` 外，还可以提供 `client.crt` 和 `client.key`。
     {: tip}

4. 将证书创建为 Kubernetes 私钥。
     ```
     kubectl create -f ssl-my-test
     ```
     {: pre}

</br>
**要创建相互认证私钥，请执行以下操作：**

1. 通过下列其中一种方式生成密钥和证书：
    * 通过证书提供者生成认证中心 (CA) 证书和密钥。如果您有自己的域，请为您的域购买正式的 TLS 证书。请确保每个证书的 [CN ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://support.dnsimple.com/articles/what-is-common-name/) 都是不同的。
    * 出于测试目的，可以使用 OpenSSL 创建自签名证书。有关更多信息，请参阅此[自签名 SSL 证书教程 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.akadia.com/services/ssh_test_certificate.html)。
        1. 创建 `client.key`。
            ```
            openssl genrsa -out client.key 1024
            ```
            {: pre}
        2. 使用密钥创建 `client.crt`。
            ```
            openssl req -new -x509 -key client.key -out client.crt
            ```
            {: pre}
        3. 使用 `client.crt` 创建自签名证书。
            ```
            openssl x509 -req -in example.org.csr -CA client.crt -CAkey client.key -CAcreateserial -out example.org.crt
            ```
            {: pre}
2. [将证书转换为 Base64 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.base64encode.org/)。
3. 使用证书创建私钥 YAML 文件。
     ```
     apiVersion: v1
     kind: Secret
     metadata:
       name: ssl-my-test
     type: Opaque
     data:
       client.crt: <ca_certificate>
     ```
     {: codeblock}
4. 将证书创建为 Kubernetes 私钥。
     ```
     kubectl create -f ssl-my-test
     ```
     {: pre}

<br />


## Istio 注释
{: #istio-annotations}

使用 Istio 注释将入局流量路由到 Istio 管理的服务。
{: shortdesc}

### Istio 服务 (istio-services)
{: #istio-services}

将流量路由到 Istio 管理的服务。
  {:shortdesc}

<dl>
<dt>描述</dt>
<dd>
<p class="note">此注释仅适用于 Istio 0.7 和更早版本。</p>  如果您有 Istio 管理的服务，那么可以使用集群 ALB 将 HTTP/HTTPS 请求路由到 Istio Ingress 控制器。然后，Istio Ingress 控制器会将请求路由到应用程序服务。为了路由流量，必须对集群 ALB 和 Istio Ingress 控制器的 Ingress 资源进行更改。
    <br><br>在集群 ALB 的 Ingress 资源中，必须：
      <ul>
    <li>指定 `istio-services` 注释</li>
    <li>将服务路径定义为应用程序侦听的实际路径</li>
    <li>将服务端口定义为 Istio Ingress 控制器的端口</li>
  </ul>
<br>在 Istio Ingress 控制器的 Ingress 资源中，必须：
      <ul>
    <li>将服务路径定义为应用程序侦听的实际路径</li>
    <li>将服务端口定义为 Istio Ingress 控制器公开的应用程序服务的 HTTP/HTTPS 端口</li>
</ul>
</dd>

<dt>集群 ALB 的样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
annotations:
    ingress.bluemix.net/istio-services: "enable=true serviceName=&lt;myservice1&gt; istioServiceNamespace=&lt;istio-namespace&gt; istioServiceName=&lt;istio-ingress-service&gt;"
spec:
tls:
  - hosts:
    - mydomain
    secretName: mytlssecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: &lt;/myapp1&gt;
          backend:
            serviceName: &lt;myservice1&gt;
            servicePort: &lt;istio_ingress_port&gt;
      - path: &lt;/myapp2&gt;
          backend:
            serviceName: &lt;myservice2&gt;
            servicePort: &lt;istio_ingress_port&gt;</code></pre>

<table>
<caption>了解 YAML 文件的组成部分</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解 YAML 文件的组成部分</th>
</thead>
<tbody>
<tr>
<td><code>enable</code></td>
  <td>要允许将流量路由到 Istio 管理的服务，请设置为 <code>True</code>。</td>
</tr>
<tr>
<td><code>serviceName</code></td>
<td>将 <code><em>&lt;myservice1&gt;</em></code> 替换为您针对 Istio 管理的应用程序创建的 Kubernetes 服务的名称。使用分号 (;) 分隔多个服务。此字段是可选的。如果未指定服务名称，那么将针对流量路由启用所有 Istio 管理的服务。</td>
</tr>
<tr>
<td><code>istioServiceNamespace</code></td>
<td>将 <code><em>&lt;istio-namespace&gt;</em></code> 替换为安装了 Istio 的 Kubernetes 名称空间。此字段是可选的。如果未指定名称空间，那么将使用 <code>istio-system</code> 名称空间。</td>
</tr>
<tr>
<td><code>istioServiceName</code></td>
<td>将 <code><em>&lt;istio-ingress-service&gt;</em></code> 替换为 Istio Ingress 服务的名称。此字段是可选的。如果未指定 Istio Ingress 服务名称，那么将使用服务名称 <code>istio-ingress</code>。</td>
</tr>
<tr>
<td><code>path</code></td>
  <td>对于要将流量路由到的每个 Istio 管理的服务，请将 <code><em>&lt;/myapp1&gt;</em></code> 替换为该 Istio 管理的服务所侦听的后端路径。该路径必须对应于 Istio Ingress 资源中定义的路径。</td>
</tr>
<tr>
<td><code>servicePort</code></td>
<td>对于要将流量路由到的每个 Istio 管理的服务，请将 <code><em>&lt;istio_ingress_port&gt;</em></code> 替换为 Istio Ingress 控制器的端口。</td>
</tr>
</tbody></table>
</dd>

<dt>用法</dt></dl>

1. 部署应用程序。这些步骤中提供的示例资源使用名为 [BookInfo ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://archive.istio.io/v0.7/docs/guides/bookinfo.html) 的 Istio 样本应用程序，该样本可在 `istio-0.7.1/samples/bookinfo/kube` 存储库中找到。
   ```
   kubectl apply -f bookinfo.yaml -n istio-system
   ```
   {: pre}

2. 为应用程序设置 Istio 路由规则。例如，在名为 BookInfo 的 Istio 样本应用程序中，`route-rule-all-v1.yaml` 文件中定义了[每个微服务的路由规则 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://archive.istio.io/v0.7/docs/tasks/traffic-management/request-routing.html)。

3. 通过创建 Istio Ingress 资源，将应用程序公开给 Istio Ingress 控制器。该资源允许对进入集群的流量应用 Istio 功能，如监视和路由规则。
    例如，BookInfo 应用程序的以下资源已在 `bookinfo.yaml` 文件中预定义：
    ```
    apiVersion: extensions/v1beta1
    kind: Ingress
    metadata:
      name: istio-ingress-resource
      annotations:
        kubernetes.io/ingress.class: "istio"
    spec:
      rules:
      - http:
          paths:
          - path: /productpage
            backend:
              serviceName: productpage
              servicePort: 9080
          - path: /login
            backend:
              serviceName: productpage
              servicePort: 9080
          - path: /logout
            backend:
              serviceName: productpage
              servicePort: 9080
          - path: /api/v1/products.*
            backend:
              serviceName: productpage
              servicePort: 9080
    ```
    {: codeblock}

4. 创建 Istio Ingress 资源。
    ```
    kubectl create -f istio-ingress-resource.yaml -n istio-system
    ```
    {: pre}
    应用程序已连接到 Istio Ingress 控制器。

5. 获取集群的 IBM **Ingress 子域**和 **Ingress 私钥**。子域和私钥已针对集群预先注册，并用作应用程序的唯一公共 URL。
    ```
    ibmcloud ks cluster-get <cluster_name_or_ID>
    ```
    {: pre}

6. 通过创建 IBM Ingress 资源，将 Istio Ingress 控制器连接到集群的 IBM Ingress ALB。
    BookInfo 应用程序的示例：
    ```
    apiVersion: extensions/v1beta1
    kind: Ingress
    metadata:
      name: ibm-ingress-resource
      annotations:
        ingress.bluemix.net/istio-services: "enabled=true serviceName=productpage istioServiceName=istio-ingress-resource"
    spec:
      tls:
      - hosts:
        - mycluster-459249.us-south.containers.mybluemix.net
        secretName: mycluster-459249
      rules:
      - host: mycluster-459249.us-south.containers.mybluemix.net
        http:
          paths:
          - path: /productpage
            backend:
              serviceName: productpage
              servicePort: 9080
          - path: /login
            backend:
              serviceName: productpage
              servicePort: 9080
          - path: /logout
            backend:
              serviceName: productpage
              servicePort: 9080
          - path: /api/v1/products.*
            backend:
              serviceName: productpage
              servicePort: 9080
    ```
    {: codeblock}

7. 创建 IBM ALB Ingress 资源。
    ```
    kubectl apply -f ibm-ingress-resource.yaml -n istio-system
    ```
    {: pre}

8. 在浏览器中，转至 `https://<hostname>/frontend` 以查看应用程序 Web 页面。

<br />


## 代理缓冲区注释
{: #proxy-buffer}

Ingress ALB 充当后端应用程序和客户机 Web 浏览器之间的代理。通过使用代理缓冲区注释，可以配置在发送或接收数据包时如何在 ALB 上对数据进行缓冲。  
{: shortdesc}

### 客户机响应数据缓冲 (proxy-buffering)
{: #proxy-buffering}

使用缓冲注释可禁止在将数据发送到客户机期间，在 ALB 上存储响应数据。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>Ingress ALB 充当后端应用程序和客户机 Web 浏览器之间的代理。当响应从后端应用程序发送到客户机时，缺省情况下会在 ALB 上对响应数据进行缓冲。ALB 作为代理传递客户机响应，并开始按客户机的速度将响应发送到客户机。ALB 接收到来自后端应用程序的所有数据后，会关闭与后端应用程序的连接。ALB 与客户机的连接会保持打开状态，直到客户机接收完所有数据为止。

</br></br>
如果在 ALB 上禁用响应数据缓冲，那么数据会立即从 ALB 发送到客户机。客户机必须能够按 ALB 的速度来处理入局数据。如果客户机速度太慢，数据可能会丢失。
</br></br>
缺省情况下，ALB 上启用了响应数据缓冲。</dd>
<dt>样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
annotations:
   ingress.bluemix.net/proxy-buffering: "enabled=&lt;false&gt; serviceName=&lt;myservice1&gt;"
spec:
tls:
 - hosts:
   - mydomain
    secretName: mytlssecret
  rules:
 - host: mydomain
   http:
paths:
     - path: /
       backend:
         serviceName: myservice
         servicePort: 8080</code></pre>

<table>
<caption>了解注释的组成部分</caption>
 <thead>
 <th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
 </thead>
 <tbody>
 <tr>
 <td><code>enabled</code></td>
   <td>要禁用 ALB 上的响应数据缓冲，请设置为 <code>false</code>。</td>
 </tr>
 <tr>
 <td><code>serviceName</code></td>
 <td>将 <code><em>&lt;myservice1&gt;</em></code> 替换为您针对应用程序创建的 Kubernetes 服务的名称。使用分号 (;) 分隔多个服务。此字段是可选的。如果未指定服务名称，那么所有服务都将使用此注释。</td>
 </tr>
 </tbody></table>
 </dd>
 </dl>

<br />



### 代理缓冲区 (proxy-buffers)
{: #proxy-buffers}

为 ALB 配置代理缓冲区的数目和大小。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>
设置缓冲区的数目和大小，这些缓冲区用于读取来自通过代理传递的服务器的单个连接的响应。除非指定了服务，否则配置将应用于 Ingress 主机中的所有服务。例如，如果指定如 <code>serviceName=SERVICE number=2 size=1k</code> 这样的配置，那么会对该服务应用 1k。如果指定如 <code>number=2 size=1k</code> 这样的配置，那么会对 Ingress 主机中的所有服务应用 1k。
</br>
<p class="tip">如果收到错误消息 `upstream sent too big header while reading response header from upstream`，说明后端中的上游服务器发送的头大小大于缺省限制。请增大 <code>proxy-buffers</code> 和 [<code>proxy-buffer-size</code>](#proxy-buffer-size) 的大小。</p>
</dd>
<dt>样本 Ingress 资源 YAML</dt>
<dd>
<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: proxy-ingress
annotations:
   ingress.bluemix.net/proxy-buffers: "serviceName=&lt;myservice&gt; number=&lt;number_of_buffers&gt; size=&lt;size&gt;"
spec:
tls:
 - hosts:
   - mydomain
    secretName: mytlssecret
  rules:
 - host: mydomain
   http:
paths:
     - path: /
       backend:
         serviceName: myservice
         servicePort: 8080</code></pre>

<table>
<caption>了解注释的组成部分</caption>
 <thead>
 <th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
 </thead>
 <tbody>
 <tr>
 <td><code>serviceName</code></td>
 <td>将 <code>&lt;<em>myservice</em>&gt;</code> 替换为要应用 proxy-buffers 的服务的名称。</td>
 </tr>
 <tr>
 <td><code>number</code></td>
 <td>将 <code>&lt;<em>number_of_buffers</em>&gt;</code> 替换为数字，例如 <em>2</em>。</td>
 </tr>
 <tr>
 <td><code>size</code></td>
 <td>将 <code>&lt;<em>size</em>&gt;</code> 替换为每个缓冲区的大小（以千字节（k 或 K）为单位），例如 <em>1K</em>。</td>
 </tr>
 </tbody>
 </table>
 </dd></dl>

<br />


### 代理缓冲区大小 (proxy-buffer-size)
{: #proxy-buffer-size}

配置代理缓冲区的大小，该缓冲区用于读取响应的第一部分。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>
设置缓冲区的大小，该缓冲区用于读取从通过代理传递的服务器收到的响应的第一部分。响应的这一部分通常包含小型响应头。除非指定了服务，否则配置将应用于 Ingress 主机中的所有服务。例如，如果指定如 <code>serviceName=SERVICE size=1k</code> 这样的配置，那么会对该服务应用 1k。如果指定如 <code>size=1k</code> 这样的配置，那么会对 Ingress 主机中的所有服务应用 1k。</dd>


<dt>样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: proxy-ingress
annotations:
   ingress.bluemix.net/proxy-buffer-size: "serviceName=&lt;myservice&gt; size=&lt;size&gt;"
spec:
tls:
 - hosts:
   - mydomain
    secretName: mytlssecret
  rules:
 - host: mydomain
   http:
paths:
     - path: /
        backend:
          serviceName: myservice
          servicePort: 8080
</code></pre>

<table>
<caption>了解注释的组成部分</caption>
 <thead>
 <th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
 </thead>
 <tbody>
 <tr>
 <td><code>serviceName</code></td>
 <td>将 <code>&lt;<em>myservice</em>&gt;</code> 替换为要应用 proxy-buffers-size 的服务的名称。</td>
 </tr>
 <tr>
 <td><code>size</code></td>
 <td>将 <code>&lt;<em>size</em>&gt;</code> 替换为每个缓冲区的大小（以千字节（k 或 K）为单位），例如 <em>1K</em>。</td>
 </tr>
 </tbody></table>

 </dd>
 </dl>

<br />



### 代理繁忙缓冲区大小 (proxy-busy-buffers-size)
{: #proxy-busy-buffers-size}

配置可以处于繁忙状态的代理缓冲区的大小。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>
限制在尚未完全读取响应期间，向客户机发送响应的任何缓冲区的大小。在此期间，其余缓冲区可用于读取响应，并可以根据需要将响应的一部分缓冲到临时文件。除非指定了服务，否则配置将应用于 Ingress 主机中的所有服务。例如，如果指定如 <code>serviceName=SERVICE size=1k</code> 这样的配置，那么会对该服务应用 1k。如果指定如 <code>size=1k</code> 这样的配置，那么会对 Ingress 主机中的所有服务应用 1k。</dd>


<dt>样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: proxy-ingress
annotations:
   ingress.bluemix.net/proxy-busy-buffers-size: "serviceName=&lt;myservice&gt; size=&lt;size&gt;"
spec:
tls:
 - hosts:
   - mydomain
    secretName: mytlssecret
  rules:
 - host: mydomain
   http:
paths:
     - path: /
       backend:
         serviceName: myservice
         servicePort: 8080
         </code></pre>

<table>
<caption>了解注释的组成部分</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
</thead>
<tbody>
<tr>
<td><code>serviceName</code></td>
<td>将 <code>&lt;<em>myservice</em>&gt;</code> 替换为要应用 proxy-busy-buffers-size 的服务的名称。</td>
</tr>
<tr>
<td><code>size</code></td>
<td>将 <code>&lt;<em>size</em>&gt;</code> 替换为每个缓冲区的大小（以千字节（k 或 K）为单位），例如 <em>1K</em>。</td>
</tr>
</tbody></table>

 </dd>
 </dl>

<br />



## 请求和响应注释
{: #request-response}

使用请求和响应注释可在客户机和服务器请求中添加或除去头信息，以及更改客户机可以发送的主体的大小。
{: shortdesc}

### 将服务器端口添加到主机头 (add-host-port)
{: #add-host-port}

向客户机请求添加服务器端口，然后将该请求转发到后端应用程序。
{: shortdesc}

<dl>
<dt>描述</dt>
<dd>将 `:server_port` 添加到客户机请求的主机头，然后将该请求转发到后端应用程序。

<dt>样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
annotations:
   ingress.bluemix.net/add-host-port: "enabled=&lt;true&gt; serviceName=&lt;myservice&gt;"
spec:
tls:
 - hosts:
   - mydomain
    secretName: mytlssecret
  rules:
 - host: mydomain
   http:
paths:
     - path: /
       backend:
         serviceName: myservice
         servicePort: 8080</code></pre>

<table>
<caption>了解注释的组成部分</caption>
 <thead>
 <th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
 </thead>
 <tbody>
 <tr>
 <td><code>enabled</code></td>
   <td>要启用主机的 server_port 设置，请设置为 <code>true</code>。</td>
 </tr>
 <tr>
 <td><code>serviceName</code></td>
 <td>将 <code><em>&lt;myservice&gt;</em></code> 替换为您针对应用程序创建的 Kubernetes 服务的名称。使用分号 (;) 分隔多个服务。此字段是可选的。如果未指定服务名称，那么所有服务都将使用此注释。</td>
 </tr>
 </tbody></table>
 </dd>
 </dl>

<br />


### 额外的客户机请求或响应头 (proxy-add-headers, response-add-headers)
{: #proxy-add-headers}

向客户机请求添加额外的头信息，然后将该请求发送到后端应用程序，或者向客户机响应添加额外的头信息，然后将该响应发送到客户机。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>Ingress ALB 充当客户机应用程序和后端应用程序之间的代理。发送到 ALB 的客户机请求经过处理（通过代理传递）后放入新的请求中，然后将该新请求发送到后端应用程序。与此类似，发送到 ALB 的后端应用程序响应经过处理（通过代理传递）后放入新的响应中，然后将该新响应发送到客户机。通过代理传递请求或响应会除去初始从客户机或后端应用程序发送的 HTTP 头信息，例如用户名。<br><br>
如果后端应用程序需要 HTTP 头信息，那么可以使用 <code>proxy-add-headers</code> 注释向客户机请求添加头信息，然后由 ALB 将该请求转发到后端应用程序。如果客户机 Web 应用程序需要 HTTP 头信息，那么可以使用 <code>response-add-headers</code> 注释将头信息添加到响应，然后由 ALB 将响应转发到客户机 Web 应用程序。<br>

<ul><li>例如，在将请求转发到应用程序之前，可能需要将以下 X-Forward 头信息添加到请求中：<pre class="screen">
<code>proxy_set_header Host $host;
proxy_set_header X-Real-IP $remote_addr;
proxy_set_header X-Forwarded-Proto $scheme;
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;</code></pre>
要将 X-Forward 头信息添加到发送到应用程序的请求中，请按以下方式使用 `proxy-add-headers` 注释：
<pre class="screen">
<code>ingress.bluemix.net/proxy-add-headers: |
      serviceName=&lt;myservice1&gt; {
  Host $host;
  X-Real-IP $remote_addr;
  X-Forwarded-Proto $scheme;
  X-Forwarded-For $proxy_add_x_forwarded_for;
  }</code></pre>
</li></ul>
</br>
<p class="tip"><code>response-add-headers</code> 注释不支持用于所有服务的全局头。要在服务器级别添加用于所有服务响应的头，可以使用 [<code>server-snippets</code> 注释](#server-snippets)。</p>
</dd>

<dt>样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
annotations:
    ingress.bluemix.net/proxy-add-headers: |
      serviceName=&lt;myservice1&gt; {
      &lt;header1&gt; &lt;value1&gt;;
      &lt;header2&gt; &lt;value2&gt;;
      }
      serviceName=&lt;myservice2&gt; {
      &lt;header3&gt; &lt;value3&gt;;
      }
    ingress.bluemix.net/response-add-headers: |
      serviceName=&lt;myservice1&gt; {
      &lt;header1&gt;: &lt;value1&gt;;
      &lt;header2&gt;: &lt;value2&gt;;
      }
      serviceName=&lt;myservice2&gt; {
      &lt;header3&gt;: &lt;value3&gt;;
      }
spec:
tls:
  - hosts:
    - mydomain
    secretName: mytlssecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /service1_path
        backend:
          serviceName: &lt;myservice1&gt;
          servicePort: 8080
      - path: /service2_path
        backend:
          serviceName: &lt;myservice2&gt;
          servicePort: 80</code></pre>

 <table>
 <caption>了解注释的组成部分</caption>
  <thead>
  <th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
  </thead>
  <tbody>
  <tr>
  <td><code>service_name</code></td>
  <td>将 <code>&lt;<em>myservice</em>&gt;</code> 替换为您针对应用程序创建的 Kubernetes 服务的名称。</td>
  </tr>
  <tr>
  <td><code>&lt;header&gt;</code></td>
  <td>要添加到客户机请求或客户机响应的头信息的键。</td>
  </tr>
  <tr>
  <td><code>&lt;value&gt;</code></td>
  <td>要添加到客户机请求或客户机响应的头信息的值。</td>
  </tr>
  </tbody></table>
 </dd></dl>

<br />



### 除去客户机响应头 (response-remove-headers)
{: #response-remove-headers}

除去后端应用程序的客户机响应中包含的头信息，然后将该响应发送到客户机。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>Ingress ALB 充当后端应用程序和客户机 Web 浏览器之间的代理。发送到 ALB 的来自后端应用程序的客户机响应经过处理（通过代理传递）后放入新的响应中，然后将该新响应从 ALB 发送到客户机 Web 浏览器。尽管通过代理传递响应会除去初始从后端应用程序发送的 HTTP 头信息，但此过程可能不会除去所有特定于后端应用程序的头。从客户机响应中除去头信息，然后将该响应从 ALB 转发到客户机 Web 浏览器。</dd>
<dt>样本 Ingress 资源 YAML</dt>
<dd>
<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
annotations:
    ingress.bluemix.net/response-remove-headers: |
      serviceName=&lt;myservice1&gt; {
      "&lt;header1&gt;";
      "&lt;header2&gt;";
      }
      serviceName=&lt;myservice2&gt; {
      "&lt;header3&gt;";
      }
spec:
tls:
  - hosts:
    - mydomain
    secretName: mytlssecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /service1_path
        backend:
          serviceName: &lt;myservice1&gt;
          servicePort: 8080
      - path: /service2_path
        backend:
          serviceName: &lt;myservice2&gt;
          servicePort: 80</code></pre>

<table>
<caption>了解注释的组成部分</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
</thead>
<tbody>
<tr>
<td><code>service_name</code></td>
<td>将 <code>&lt;<em>myservice</em>&gt;</code> 替换为您针对应用程序创建的 Kubernetes 服务的名称。</td>
</tr>
<tr>
<td><code>&lt;header&gt;</code></td>
<td>要从客户机响应中除去的头的键。</td>
</tr>
</tbody></table>
</dd></dl>

<br />


### 客户机请求主体大小 (client-max-body-size)
{: #client-max-body-size}

设置客户机可以作为请求一部分发送的主体的最大大小。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>为了保持期望的性能，最大客户机请求主体大小设置为 1 兆字节。将主体大小超出此限制的客户机请求发送到 Ingress ALB，并且客户机不允许拆分数据时，ALB 会向客户机返回 413（请求实体太大）HTTP 响应。除非减小请求主体的大小，否则无法在客户机和 ALB 之间建立连接。客户机允许数据拆分为多个区块时，数据将分成 1 兆字节的包并发送到 ALB。

</br></br>
您可能希望增大最大主体大小，因为您预期客户机请求的主体大小大于 1 兆字节。例如，您希望客户机能够上传大型文件。增大最大请求主体大小可能会影响 ALB 的性能，因为与客户机的连接必须保持打开状态，直到接收完请求为止。
</br></br>
<p class="note">某些客户机 Web 浏览器无法正确显示 413 HTTP 响应消息。</p></dd>
<dt>样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
annotations:
   ingress.bluemix.net/client-max-body-size: size=&lt;size&gt;
spec:
tls:
 - hosts:
   - mydomain
    secretName: mytlssecret
  rules:
 - host: mydomain
   http:
paths:
     - path: /
       backend:
         serviceName: myservice
         servicePort: 8080</code></pre>

<table>
<caption>了解注释的组成部分</caption>
 <thead>
 <th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
 </thead>
 <tbody>
 <tr>
 <td><code>&lt;size&gt;</code></td>
 <td>客户机响应主体的最大大小。例如，要将最大大小设置为 200 兆字节，请定义 <code>200m</code>。可以将大小设置为 0 以禁止检查客户机请求主体大小。</td>
 </tr>
 </tbody></table>

 </dd></dl>

<br />


### 大型客户机头缓冲区 (large-client-header-buffers)
{: #large-client-header-buffers}

设置读取大型客户机请求头的缓冲区的最大数目和大小。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>读取大型客户机请求头的缓冲区仅按需进行分配：如果在请求结尾处理后连接已转换为保持活动状态，那么将释放这些缓冲区。缺省情况下，缓冲区大小等于 <code>8K</code> 字节。如果请求行超过一个缓冲区的设定最大大小，那么会向客户机返回 <code>414 Request-URI Too Large</code> 错误。此外，如果请求头字段超过一个缓冲区的设定最大大小，那么会向客户机返回 <code>400 Bad Request</code> 错误。可以调整用于读取大型客户机请求头的缓冲区的最大数目和大小。

<dt>样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
annotations:
   ingress.bluemix.net/large-client-header-buffers: "number=&lt;number&gt; size=&lt;size&gt;"
spec:
tls:
 - hosts:
   - mydomain
    secretName: mytlssecret
  rules:
 - host: mydomain
   http:
paths:
     - path: /
       backend:
         serviceName: myservice
         servicePort: 8080</code></pre>

<table>
<caption>了解注释的组成部分</caption>
 <thead>
 <th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
 </thead>
 <tbody>
 <tr>
 <td><code>&lt;number&gt;</code></td>
 <td>应该为读取大型客户机请求头而分配的最大缓冲区数。例如，要将其设置为 4，请定义 <code>4</code>。</td>
 </tr>
 <tr>
 <td><code>&lt;size&gt;</code></td>
 <td>读取大型客户机请求头的缓冲区的最大大小。例如，要将其设置为 16 千字节，请定义 <code>16k</code>。
   对于千字节，大小必须以 <code>k</code> 结尾，对于兆字节，必须以 <code>m</code> 结尾。</td>
 </tr>
</tbody></table>
</dd>
</dl>

<br />


## 服务限制注释
{: #service-limit}

通过使用服务限制注释，可以更改可来自单个 IP 地址的缺省请求处理速率和连接数。
{: shortdesc}

### 全局速率限制 (global-rate-limit)
{: #global-rate-limit}

对于所有服务，按定义的键限制请求处理速率和连接数。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>
对于所有服务，按定义的键限制来自所选后端中所有路径的单个 IP 地址的请求处理速率和连接数。
</dd>


<dt>样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
annotations:
    ingress.bluemix.net/global-rate-limit: "key=&lt;key&gt; rate=&lt;rate&gt; conn=&lt;number_of_connections&gt;"
spec:
tls:
  - hosts:
    - mydomain
    secretName: mytlssecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /
        backend:
          serviceName: myservice
          servicePort: 8080</code></pre>

<table>
<caption>了解注释的组成部分</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
</thead>
<tbody>
<tr>
<td><code>key</code></td>
<td>要基于专区或服务来设置入局请求的全局限制，请使用 `key=zone`。要基于头来设置入局请求的全局限制，请使用 `X-USER-ID key=$http_x_user_id`。</td>
</tr>
<tr>
<td><code>rate</code></td>
<td>将 <code>&lt;<em>rate</em>&gt;</code> 替换为处理速率。输入以每秒速率 (r/s) 或每分钟速率 (r/m) 为单位的值。示例：<code>50r/m</code>。</td>
</tr>
<tr>
<td><code>number-of_connections</code></td>
<td>将 <code>&lt;<em>conn</em>&gt;</code> 替换为连接数。</td>
</tr>
</tbody></table>

</dd>
</dl>

<br />



### 服务速率限制 (service-rate-limit)
{: #service-rate-limit}

限制特定服务的请求处理速率和连接数。
{:shortdesc}

<dl>
<dt>描述</dt>
<dd>对于特定服务，按定义的键限制来自所选后端中所有路径的单个 IP 地址的请求处理速率和连接数。
</dd>


<dt>样本 Ingress 资源 YAML</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
annotations:
    ingress.bluemix.net/service-rate-limit: "serviceName=&lt;myservice&gt; key=&lt;key&gt; rate=&lt;rate&gt; conn=&lt;number_of_connections&gt;"
spec:
tls:
  - hosts:
    - mydomain
    secretName: mytlssecret
  rules:
  - host: mydomain
    http:
      paths:
      - path: /
        backend:
          serviceName: myservice
          servicePort: 8080</code></pre>

<table>
<caption>了解注释的组成部分</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="“构想”图标"/> 了解注释的组成部分</th>
</thead>
<tbody>
<tr>
<td><code>serviceName</code></td>
<td>将 <code>&lt;<em>myservice</em>&gt;</code> 替换为要限制其处理速率的服务的名称。</li>
</tr>
<tr>
<td><code>key</code></td>
<td>要基于专区或服务来设置入局请求的全局限制，请使用 `key=zone`。要基于头来设置入局请求的全局限制，请使用 `X-USER-ID key=$http_x_user_id`。</td>
</tr>
<tr>
<td><code>rate</code></td>
<td>将 <code>&lt;<em>rate</em>&gt;</code> 替换为处理速率。要定义每秒速率，请使用 r/s：<code>10r/s</code>。要定义每分钟速率，请使用 r/m：<code>50r/m</code>。</td>
</tr>
<tr>
<td><code>number-of_connections</code></td>
<td>将 <code>&lt;<em>conn</em>&gt;</code> 替换为连接数。</td>
</tr>
</tbody></table>
</dd>
</dl>

<br />



