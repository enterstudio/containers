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



# Ingress mit Annotationen anpassen
{: #ingress_annotation}

Um Ihrer Lastausgleichsfunktion für Ingress-Anwendungen (ALB) Funktionalität hinzuzufügen, können Sie Annotationen als Metadaten in einer Ingress-Ressource angeben.
{: shortdesc}

Bevor Sie Annotationen verwenden, stellen Sie sicher, dass Sie Ihre Ingress-Servicekonfiguration ordnungsgemäß eingerichtet haben. Führen Sie dazu die Schritte im Abschnitt [Apps mit Ingress zugänglich machen](cs_ingress.html) aus. Sobald Sie die Ingress-ALB mit einer Basiskonfiguration eingerichtet haben, können Sie deren Funktionalität durch das Hinzufügen von Annotationen zur Ingress-Ressourcendatei erweitern.
{: note}

<table>
<caption>Allgemeine Annotationen</caption>
<col width="20%">
<col width="20%">
<col width="60%">
 <thead>
 <th>Allgemeine Annotationen</th>
 <th>Name</th>
 <th>Beschreibung</th>
 </thead>
 <tbody>
 <tr>
 <td><a href="#proxy-external-service">Externe Services</a></td>
 <td><code>proxy-external-service</code></td>
 <td>Pfaddefinitionen zu externen Services wie beispielsweise einem in {{site.data.keyword.Bluemix_notm}} gehosteten Service hinzufügen.</td>
 </tr>
 <tr>
 <td><a href="#location-modifier">Positionsmodifikator</a></td>
 <td><code>location-modifier</code></td>
 <td>Die Art und Weise ändern, in der die ALB die Anforderungs-URI mit dem App-Pfad abgleicht.</td>
 </tr>
 <tr>
 <td><a href="#location-snippets">Positionssnippets</a></td>
 <td><code>location-snippets</code></td>
 <td>Angepasste Positionsblockkonfiguration für einen Service hinzufügen.</td>
 </tr>
 <tr>
 <td><a href="#alb-id">Privates ALB-Routing</a></td>
 <td><code>ALB-ID</code></td>
 <td>Eingehende Anforderungen an Ihre Apps mit einer privaten ALB weiterleiten.</td>
 </tr>
 <tr>
 <td><a href="#rewrite-path">Pfade neu schreiben</a></td>
 <td><code>rewrite-path</code></td>
 <td>Eingehenden Netzverkehr an einen anderen Pfad weiterleiten, den Ihre Back-End-App überwacht.</td>
 </tr>
 <tr>
 <td><a href="#server-snippets">Server-Snippets</a></td>
 <td><code>server-snippets</code></td>
 <td>Angepasste Serverblockkonfiguration hinzufügen.</td>
 </tr>
 <tr>
 <td><a href="#tcp-ports">TCP-Ports</a></td>
 <td><code>tcp-ports</code></td>
 <td>Zugriff auf eine App über einen vom Standard abweichenden TCP-Port.</td>
 </tr>
 </tbody></table>

<br>

<table>
<caption>Annotationen für Verbindungen</caption>
<col width="20%">
<col width="20%">
<col width="60%">
 <thead>
 <th>Annotationen für Verbindungen</th>
 <th>Name</th>
 <th>Beschreibung</th>
  </thead>
  <tbody>
  <tr>
  <td><a href="#proxy-connect-timeout">Angepasste Verbindungs- und Lesezeitlimits</a></td>
  <td><code>proxy-connect-timeout, proxy-read-timeout</code></td>
  <td>Zeitraum festlegen, über den die Lastausgleichsfunktion für Anwendungen auf das Herstellen einer Verbindung mit bzw. auf das Lesen von Daten aus der Back-End-App warten soll, bis die Back-End-App als nicht verfügbar betrachtet wird.</td>
  </tr>
  <tr>
  <td><a href="#keepalive-requests">Keepalive-Anforderungen</a></td>
  <td><code>keepalive-requests</code></td>
  <td>Maximale Anzahl von Anforderungen festlegen, die über eine Keepalive-Verbindung bedient werden können.</td>
  </tr>
  <tr>
  <td><a href="#keepalive-timeout">Keepalive-Zeitlimit</a></td>
  <td><code>keepalive-timeout</code></td>
  <td>Maximale Zeitspanne festlegen, die eine Keepalive-Verbindung auf dem Server geöffnet bleibt.</td>
  </tr>
  <tr>
  <td><a href="#proxy-next-upstream-config">Proxy zu nächstem Upstream</a></td>
  <td><code>proxy-next-upstream-config</code></td>
  <td>Festlegen, wann die ALB eine Anforderung an den nächsten Upstream-Server übergeben kann.</td>
  </tr>
  <tr>
  <td><a href="#sticky-cookie-services">Sitzungsaffinität mit Cookies</a></td>
  <td><code>sticky-cookie-services</code></td>
  <td>Eingehenden Netzverkehr mithilfe eines permanenten Cookies immer an denselben Upstream-Server weiterleiten.</td>
  </tr>
  <tr>
  <td><a href="#upstream-fail-timeout">Parameter 'fail_timeout' für Upstream-Server</a></td>
  <td><code>upstream-fail-timeout</code></td>
  <td>Festlegen, wie lange die ALB versuchen kann, eine Verbindung zum Server herzustellen, bevor der Server als nicht verfügbar betrachtet wird.</td>
  </tr>
  <tr>
  <td><a href="#upstream-keepalive">Keepalive-Verbindungen für Upstream-Server</a></td>
  <td><code>upstream-keepalive</code></td>
  <td>Maximale Anzahl der inaktiven Keepalive-Verbindungen für einen Upstream-Server festlegen.</td>
  </tr>
  <tr>
  <td><a href="#upstream-max-fails">Parameter 'max_fails' für Upstream-Server</a></td>
  <td><code>upstream-max-fails</code></td>
  <td>Maximale Anzahl nicht erfolgreicher Versuche festlegen, mit dem Server zu kommunizieren, bevor der Server als nicht verfügbar betrachtet wird.</td>
  </tr>
  </tbody></table>

<br>

  <table>
  <caption>Annotationen für HTTPS- und TLS/SSL-Authentifizierung</caption>
  <col width="20%">
  <col width="20%">
  <col width="60%">
  <thead>
  <th>Annotationen für HTTPS- und TLS/SSL-Authentifizierung</th>
  <th>Name</th>
  <th>Beschreibung</th>
  </thead>
  <tbody>
  <tr>
  <td><a href="#appid-auth">{{site.data.keyword.appid_short}}-Authentifizierung</a></td>
  <td><code>appid-auth</code></td>
  <td>{{site.data.keyword.appid_full}} zur Authentifizierung bei Ihrer App verwenden.</td>
  </tr>
  <tr>
  <td><a href="#custom-port">Angepasste HTTP- und HTTPS-Ports</a></td>
  <td><code>custom-port</code></td>
  <td>Standardports für den HTTP-Netzverkehr (Port 80) und den HTTPS-Netzverkehr (Port 443) ändern.</td>
  </tr>
  <tr>
  <td><a href="#redirect-to-https">HTTP-Weiterleitungen an HTTPS</a></td>
  <td><code>redirect-to-https</code></td>
  <td>Unsichere HTTP-Anforderungen an Ihre Domäne an HTTPS weiterleiten.</td>
  </tr>
  <tr>
  <td><a href="#hsts">HTTP Strict Transport Security (HSTS)</a></td>
  <td><code>hsts</code></td>
  <td>Browser so einstellen, dass nur über HTTPS auf die Domäne zugegriffen wird.</td>
  </tr>
  <tr>
  <td><a href="#mutual-auth">Gegenseitige Authentifizierung</a></td>
  <td><code>mutual-auth</code></td>
  <td>Gegenseitige Authentifizierung für die Lastausgleichsfunktion für Anwendungen (ALB) konfigurieren.</td>
  </tr>
  <tr>
  <td><a href="#ssl-services">Unterstützung für SSL-Services</a></td>
  <td><code>ssl-services</code></td>
  <td>Unterstützung für SSL-Services zulassen, um den Datenverkehr zu Ihren Upstream-Apps, für die HTTPS erforderlich ist, zu verschlüsseln.</td>
  </tr>
  </tbody></table>

<br>

<table>
<caption>Istio-Annotationen</caption>
<col width="20%">
<col width="20%">
<col width="60%">
<thead>
<th>Istio-Annotationen</th>
<th>Name</th>
<th>Beschreibung</th>
</thead>
<tbody>
<tr>
<td><a href="#istio-services">Istio-Services</a></td>
<td><code>istio-services</code></td>
<td>Datenverkehr an Istio-verwaltete Services weiterleiten.</td>
</tr>
</tbody></table>

<br>

<table>
<caption>Annotationen für Proxypuffer</caption>
<col width="20%">
<col width="20%">
<col width="60%">
 <thead>
 <th>Annotationen für Proxypuffer</th>
 <th>Name</th>
 <th>Beschreibung</th>
 </thead>
 <tbody>
 <tr>
 <td><a href="#proxy-buffering">Pufferung von Clientantwortdaten</a></td>
 <td><code>proxy-buffering</code></td>
 <td>Pufferung einer Clientantwort in der Lastausgleichsfunktion für Anwendungen (ALB) inaktivieren, während die Antwort an den Client gesendet wird.</td>
 </tr>
 <tr>
 <td><a href="#proxy-buffers">Proxy-Puffer</a></td>
 <td><code>proxy-buffers</code></td>
 <td>Anzahl und Größe der Puffer festlegen, mit denen eine Antwort für eine einzelne Verbindung von einem Proxy-Server gelesen wird.</td>
 </tr>
 <tr>
 <td><a href="#proxy-buffer-size">Puffergröße des Proxys</a></td>
 <td><code>proxy-buffer-size</code></td>
 <td>Größe des Puffers festlegen, mit dem der erste Teil der Antwort gelesen wird, die vom Proxy-Server empfangen wird.</td>
 </tr>
 <tr>
 <td><a href="#proxy-busy-buffers-size">Größe belegter Puffer des Proxys</a></td>
 <td><code>proxy-busy-buffers-size</code></td>
 <td>Größe für Proxypuffer festlegen, die belegt sein können.</td>
 </tr>
 </tbody></table>

<br>

<table>
<caption>Annotationen für Anforderungen und Antworten</caption>
<col width="20%">
<col width="20%">
<col width="60%">
<thead>
<th>Annotationen für Anforderungen und Antworten</th>
<th>Name</th>
<th>Beschreibung</th>
</thead>
<tbody>
<tr>
<td><a href="#add-host-port">Server-Port zum Host-Header hinzufügen</a></td>
<td><code>add-host-port</code></td>
<td>Server-Port zum Host für Routenanforderungen hinzufügen.</td>
</tr>
<tr>
<td><a href="#client-max-body-size">Größe des Hauptteils der Clientanforderung</a></td>
<td><code>client-max-body-size</code></td>
<td>Die maximale Größe des Hauptteils anpassen, den der Client als Teil der Anforderung senden kann.</td>
</tr>
<tr>
<td><a href="#large-client-header-buffers">Puffer für große Client-Header</a></td>
<td><code>large-client-header-buffers</code></td>
<td>Die maximale Anzahl und Größe der Puffer festlegen, die große Clientanforderungsheader lesen.</td>
</tr>
<tr>
<td><a href="#proxy-add-headers">Zusätzlicher Clientanforderungs- oder -antwortheader</a></td>
<td><code>proxy-add-headers, response-add-headers</code></td>
<td>Einer Clientanforderung Headerinformationen hinzufügen, bevor Sie die Anforderung an Ihre Back-End-App weiterleiten, bzw. einer Clientantwort, bevor Sie die Antwort an den Client senden.</td>
</tr>
<tr>
<td><a href="#response-remove-headers">Entfernen des Clientantwortheaders</a></td>
<td><code>response-remove-headers</code></td>
<td>Headerinformationen aus einer Clientantwort entfernen, bevor die Antwort an den Client weitergeleitet wird.</td>
</tr>
</tbody></table>

<br>

<table>
<caption>Annotationen für Servicegrenzwerte</caption>
<col width="20%">
<col width="20%">
<col width="60%">
<thead>
<th>Annotationen für Servicegrenzwerte</th>
<th>Name</th>
<th>Beschreibung</th>
</thead>
<tbody>
<tr>
<td><a href="#global-rate-limit">Grenzwerte für globale Rate</a></td>
<td><code>global-rate-limit</code></td>
<td>Verarbeitungsrate für Anforderungen und Anzahl der Verbindungen anhand eines definierten Schlüssels für alle Services begrenzen.</td>
</tr>
<tr>
<td><a href="#service-rate-limit">Grenzwerte für Servicerate</a></td>
<td><code>service-rate-limit</code></td>
<td>Verarbeitungsrate für Anforderungen und Anzahl der Verbindungen anhand eines definierten Schlüssels für bestimmte Services begrenzen.</td>
</tr>
</tbody></table>

<br>



## Allgemeine Annotationen
{: #general}

### Externe Services (proxy-external-service)
{: #proxy-external-service}

Hinzufügen von Pfaddefinitionen zu externen Services, wie beispielsweise in {{site.data.keyword.Bluemix_notm}} gehosteten Services.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>Fügen Sie Pfaddefinitionen zu externen Services hinzu. Verwenden Sie diese Annotation nur dann, wenn Ihre App für einen externen Service, nicht für einen Back-End-Service, betrieben wird. Wenn Sie diese Annotation verwenden, um eine externe Serviceroute zu erstellen, dann werden zusammen mit ihr nur die Annotationen `client-max-body-size`, `proxy-read-timeout`, `proxy-connect-timeout` und `proxy-buffering` unterstützt. Darüber hinaus werden keine weiteren Annotationen zusammen mit `proxy-external-service` unterstützt.<p class="note">Es ist nicht möglich, mehrere Hosts für einen einzelnen Service und Pfad anzugeben.</p>
</dd>
<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: cafe-ingress
  annotations:
    ingress.bluemix.net/proxy-external-service: "path=&lt;mein_pfad&gt; external-svc=https:&lt;externer_service&gt; host=&lt;meine_domäne&gt;"
spec:
  tls:
  - hosts:
    - meine_domäne
    secretName: mein_geheimer_schlüssel
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: /
        backend:
          serviceName: mein_service
          servicePort: 80
</code></pre>

<table>
<caption>Erklärung der Komponenten von Annotationen</caption>
 <thead>
 <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
 </thead>
 <tbody>
 <tr>
 <td><code>path</code></td>
 <td>Ersetzen Sie <code>&lt;<em>mein_pfad</em>&gt;</code> durch den Pfad, an dem der externe Service empfangsbereit ist.</td>
 </tr>
 <tr>
 <td><code>external-svc</code></td>
 <td>Ersetzen Sie <code>&lt;<em>externer_service</em>&gt;</code> durch den externen Service, der aufgerufen werden soll. Beispiel: <code>https://&lt;mein_service&gt;.&lt;region&gt;.mybluemix.net</code>.</td>
 </tr>
 <tr>
 <td><code>host</code></td>
 <td>Ersetzen Sie <code>&lt;<em>meine_domäne</em>&gt;</code> durch die Hostdomäne für den externen Service.</td>
 </tr>
 </tbody></table>

 </dd></dl>

<br />


### Positionsmodifikator (location-modifier)
{: #location-modifier}

Die Art und Weise ändern, in der die ALB die Anforderungs-URI mit dem App-Pfad abgleicht.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>Standardmäßig verarbeiten ALBs die Pfade, auf denen Apps empfangsbereit sind, als Präfixe. Wenn eine ALB eine Anforderung an eine App empfängt, prüft die ALB die Ingress-Ressource auf einen Pfad (als Präfix), der mit dem Anfang der Anforderungs-URI übereinstimmt. Wenn eine Übereinstimmung gefunden wurde, wird die Anforderung an die IP-Adresse des Pods weitergeleitet, in dem die App bereitgestellt ist.<br><br>Die Annotation `location-modifier` ändert die Art und Weise, in der die ALB nach Übereinstimmungen sucht, indem die Positionsblockkonfiguration geändert wird. Der Positionsblock bestimmt, wie Anforderungen für den App-Pfad gehandhabt werden.<p class="note">Um reguläre Ausdruckspfade (regex) zu bearbeiten, ist diese Annotation erforderlich.</p></dd>

<dt>Unterstützte Modifikatoren</dt>
<dd>

<table>
<caption>Unterstützte Modifikatoren</caption>
 <col width="10%">
 <col width="90%">
 <thead>
 <th>Modifikator</th>
 <th>Beschreibung</th>
 </thead>
 <tbody>
 <tr>
 <td><code>=</code></td>
 <td>Der Modifikator 'Gleichheitszeichen' bewirkt, dass die ALB nur exakte Übereinstimmungen auswählt. Wenn eine exakte Übereinstimmung gefunden wird, wird die Suche gestoppt, und der übereinstimmende Pfad wird ausgewählt.<br>Wenn Ihre App beispielsweise an <code>/tea</code> empfangsbereit ist, wählt die Lastausgleichsfunktion für Anwendungen (ALB) beim Abgleich einer Anforderung mit Ihrer App nur genaue <code>/tea</code>-Pfade aus.</td>
 </tr>
 <tr>
 <td><code>~</code></td>
 <td>Der Modifikator 'Tilde' bewirkt, dass die ALB während der Suche nach Übereinstimmungen Pfade als regex-Pfade betrachtet, bei denen die Groß-/Kleinschreibung beachtet werden muss.<br>Wenn Ihre App beispielsweise am Verzeichnis <code>/coffee</code> empfangsbereit ist, kann die Lastausgleichsfunktion für Anwendungen (ALB) beim Abgleich einer Anforderung mit Ihrer App Pfade des Typs <code>/ab/coffee</code> oder <code>/123/coffee</code> auswählen, obwohl die Pfade nicht explizit für Ihre App angegeben sind.</td>
 </tr>
 <tr>
 <td><code>~\*</code></td>
 <td>Der Modifikator 'Tilde' gefolgt von einem Modifikator 'Stern' bewirkt, dass die ALB während der Suche nach Übereinstimmungen Pfade als regex-Pfade betrachtet, bei denen die Groß-/Kleinschreibung nicht beachtet werden muss.<br>Wenn Ihre App beispielsweise am Verzeichnis <code>/coffee</code> empfangsbereit ist, kann die Lastausgleichsfunktion für Anwendungen (ALB) beim Abgleich einer Anforderung mit Ihrer App Pfade des Typs <code>/ab/Coffee</code> oder <code>/123/COFFEE</code> auswählen, obwohl die Pfade nicht explizit für Ihre App angegeben sind.</td>
 </tr>
 <tr>
 <td><code>^~</code></td>
 <td>Der Modifikator 'Zirkumflex' gefolgt von einem Modifikator 'Tilde' bewirkt, dass die ALB keinen regex-Pfad, sondern die beste nicht-regex-Übereinstimmung auswählt.</td>
 </tr>
 </tbody>
</table>

</dd>

<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
name: myingress
annotations:
  ingress.bluemix.net/location-modifier: "modifier='&lt;standortmodifikator&gt;' serviceName=&lt;mein_service1&gt;;modifier='&lt;standortmodifikator&gt;' serviceName=&lt;mein_service2&gt;"
spec:
  tls:
  - hosts:
    - meine_domäne
    secretName: mein_geheimer_schlüssel
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: /
        backend:
          serviceName: &lt;mein_service&gt;
          servicePort: 80</code></pre>

 <table>
 <caption>Erklärung der Komponenten von Annotationen</caption>
  <thead>
  <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
  </thead>
  <tbody>
  <tr>
  <td><code>modifier</code></td>
  <td>Ersetzen Sie <code>&lt;<em>standortmodifikator</em>&gt;</code> durch den Positionsmodifikator, den Sie für den Pfad verwenden möchten. Unterstützte Modifikatoren sind <code>'='</code>, <code>'~'</code>, <code>'~\*'</code> und <code>'^~'</code>. Sie müssen die Modifikatoren in einfache Anführungszeichen setzen.</td>
  </tr>
  <tr>
  <td><code>serviceName</code></td>
  <td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen des Kubernetes-Service. dem Sie für Ihre App erstellt haben.</td>
  </tr>
  </tbody></table>
  </dd>
  </dl>

<br />


### Positionssnippets (location-snippets)
{: #location-snippets}

Angepasste Positionsblockkonfiguration für einen Service hinzufügen.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>Ein Serverblock ist eine nginx-Anweisung, die die Konfiguration für den virtuellen ALB-Server definiert. Ein Positionsblock ist eine nginx-Anweisung, die innerhalb des Serverblocks definiert ist. Positionsblöcke definieren, wie Ingress den Anforderungs-URI verarbeitet, oder den Teil der Anforderung, der nach dem Domänennamen oder der IP-Adresse und dem Port kommt.<br><br>Wenn ein Serverblock eine Anforderung empfängt, gleicht der Positionsblock den URI mit einem Pfad ab und die Anforderung wird an die IP-Adresse des Pods weitergeleitet, auf dem die App implementiert ist. Wenn Sie die Annotation <code>location-snippets</code> verwenden, können Sie die Art und Weise ändern, wie der Positionsblock Anforderungen an bestimmte Services weiterleitet.<br><br>Wenn Sie stattdessen den Serverblock als Ganzes ändern möchten, hilft Ihnen die Annotation <a href="#server-snippets">server-snippets</a> weiter.</dd>


<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
name: myingress
annotations:
  ingress.bluemix.net/location-snippets: |
    serviceName=&lt;mein_service1&gt;
    # Example location snippet
    proxy_request_buffering off;
    rewrite_log on;
    proxy_set_header "x-additional-test-header" "location-snippet-header";
    &lt;EOS&gt;
    serviceName=&lt;mein_service2&gt;
    proxy_set_header Authorization "";
    &lt;EOS&gt;
spec:
tls:
- hosts:
  - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
- host: meine_domäne
  http:
    paths:
    - path: /
      backend:
        serviceName: &lt;mein_service&gt;
        servicePort: 8080</code></pre>

<table>
<caption>Erklärung der Komponenten von Annotationen</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
</thead>
<tbody>
<tr>
<td><code>serviceName</code></td>
<td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen des Service, den Sie für Ihre App erstellt haben.</td>
</tr>
<tr>
<td>Positionssnippet</td>
<td>Geben Sie das Konfigurationssnippet an, das Sie für den angegebenen Service verwenden möchten. Dieses Beispielsnippet für den Service <code>mein_service1</code> konfiguriert den Positionsblock, um die Pufferung von Proxy-Anforderungen zu blockieren, Protokollumschreibvorgänge zu aktivieren und zusätzliche Header festzulegen, wenn er eine Anforderung an den Service weiterleitet. Das Beispielsnippet für den Service <code>mein_service2</code> legt einen leeren Header <code>Authorization</code> fest. Jedes Positions-Snippet muss auf den Wert <code>&lt;EOS&gt;</code> enden.</td>
</tr>
</tbody></table>
</dd>
</dl>

<br />


### Private ALB-Weiterleitung (ALB-ID)
{: #alb-id}

Eingehende Anforderungen an Ihre Apps mit einer privaten ALB weiterleiten.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>
Wählen Sie statt der öffentlichen eine private Lastausgleichsfunktion für Anwendungen (ALB) für die Weiterleitung von eingehenden Anforderungen aus.</dd>


<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
name: myingress
annotations:
  ingress.bluemix.net/ALB-ID: "&lt;private_ALB-ID&gt;"
spec:
tls:
- hosts:
  - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
- host: meine_domäne
  http:
    paths:
    - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080</code></pre>

<table>
<caption>Erklärung der Komponenten von Annotationen</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
</thead>
<tbody>
<tr>
<td><code>&lt;private_ALB-ID&gt;</code></td>
<td>Die ID für Ihre private ALB. Führen Sie den Befehl <code>ibmcloud ks albs --cluster &lt;mein_cluster&gt;</code> aus, um nach der privaten ALB-ID zu suchen.<p>
Wenn Sie einen Mehrzonencluster mit mehreren privaten ALB aktiviert haben, können Sie eine Liste mit ALB-IDs bereitstellen, die durch <code>;</code> voneinander getrennt sind. Zum Beispiel: <code>ingress.bluemix.net/ALB-ID: &lt;private_ALB-ID_1&gt;;&lt;private_ALB-ID_2&gt;;&lt;private_ALB-ID_3&gt</code></p>
</td>
</tr>
</tbody></table>
</dd>
</dl>

<br />


### Pfade neu schreiben (rewrite-path)
{: #rewrite-path}

Leiten Sie eingehenden Netzverkehr für den Pfad in der Domäne einer Lastausgleichsfunktion für Anwendungen (ALB) an einen anderen Pfad weiter, an dem die Back-End-App empfangsbereit ist.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>Die Domäne der Ingress-Lastausgleichsfunktion für Anwendungen (Ingress-ALB) leitet eingehenden Netzverkehr für <code>mykubecluster.us-south.containers.appdomain.cloud/beans</code> an Ihre App weiter. Ihre App überwacht <code>/coffee</code> statt <code>/beans</code>. Zum Weiterleiten des eingehenden Netzverkehrs an Ihre App fügen Sie eine Annotation zum erneuten Schreiben (rewrite) zur Konfigurationsdatei der Ingress-Ressource hinzu. Dadurch wird sichergestellt, dass der an <code>/beans</code> eingehende Netzverkehr mithilfe des Pfads <code>/coffee</code> an Ihre App weitergeleitet wird. Wenn Sie mehrere Services einschließen, verwenden Sie nur ein Semikolon (;) zum Trennen der Services.</dd>
<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>
<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/rewrite-path: "serviceName=&lt;mein_service1&gt; rewrite=&lt;zielpfad1&gt;;serviceName=&lt;mein_service2&gt; rewrite=&lt;zielpfad2&gt;"
spec:
  tls:
  - hosts:
    - meine_domäne
    secretName: mein_geheimer_schlüssel
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: /beans
        backend:
          serviceName: mein_service1
          servicePort: 80
</code></pre>

<table>
<caption>Erklärung der Komponenten von Annotationen</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
</thead>
<tbody>
<tr>
<td><code>serviceName</code></td>
<td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen des Kubernetes-Service, den Sie für Ihre App erstellt haben.</td>
</tr>
<tr>
<td><code>rewrite</code></td>
<td>Ersetzen Sie <code>&lt;<em>zielpfad</em>&gt;</code> durch den Pfad, an dem Ihre App empfangsbereit ist. Der eingehende Netzverkehr in der Domäne der Lastausgleichsfunktion für Anwendungen (ALB) wird mithilfe dieses Pfads an den Kubernetes-Service weitergeleitet. Die meisten Apps überwachen keinen bestimmten Pfad, sondern verwenden den Rootpfad und einen bestimmten Port. Im vorstehenden Beispiel wurde der Pfad für 'rewrite' als <code>/coffee</code> definiert.</td>
</tr>
</tbody></table>

</dd></dl>

<br />


### Server-Snippets (server-snippets)
{: #server-snippets}

Fügen Sie eine angepasste Serverblockkonfiguration hinzu.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>Ein Serverblock ist eine nginx-Anweisung, die die Konfiguration für den virtuellen ALB-Server definiert. Wenn Sie die Annotation <code>server-snippets</code> verwenden, können Sie die Art und Weise ändern, wie die ALB Anforderungen verarbeitet, indem Sie ein angepasstes Konfigurationssnippet bereitstellen.</dd>

<dt>YAML-Beispiel einer Ingress-Ressource</dt>
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
  - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
- host: meine_domäne
  http:
    paths:
    - path: /
      backend:
        serviceName: &lt;mein_service&gt;
        servicePort: 8080</code></pre>

<table>
<caption>Erklärung der Komponenten von Annotationen</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
</thead>
<tbody>
<tr>
<td>Server-Snippet</td>
<td>Geben Sie das Konfigurationssnippet an, das Sie verwenden möchten. Dieses Beispielsnippet gibt einen Positionsblock für die Bearbeitung von <code>/health</code>-Anforderungen an. Der Positionsblock ist so konfiguriert, dass er eine Antwort zum einwandfreien Zustand zurückgibt und einen Header hinzufügt, wenn er eine Anforderung weiterleitet.</td>
</tr>
</tbody></table>
</dd>
</dl>

<br />


### TCP-Ports für Lastausgleichsfunktionen für Anwendungen (tcp-ports)
{: #tcp-ports}

Zugriff auf eine App über einen vom Standard abweichenden TC-Port.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>
Verwenden Sie diese Annotation für eine App, für die eine Arbeitslast für TCP-Datenströme ausgeführt wird.

<p class="note">Die Lastausgleichsfunktion für Anwendungen (ALB) arbeitet im Durchgriffsmodus und leitet den Datenverkehr an Back-End-Apps weiter. Die SSL-Terminierung wird in diesem Fall nicht unterstützt. Die TLS-Verbindung wird nicht beendet und der Durchgriff erfolgt ungehindert.</p>
</dd>


<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
name: myingress
annotations:
  ingress.bluemix.net/tcp-ports: "serviceName=&lt;mein_service&gt; ingressPort=&lt;ingress-port&gt; servicePort=&lt;serviceport&gt;"
spec:
  tls:
  - hosts:
    - meine_domäne
    secretName: mein_geheimer_schlüssel
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: /
        backend:
          serviceName: &lt;mein_service&gt;
          servicePort: 80</code></pre>

 <table>
 <caption>Erklärung der Komponenten von Annotationen</caption>
  <thead>
  <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
  </thead>
  <tbody>
  <tr>
  <td><code>serviceName</code></td>
  <td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen des Kubernetes-Service, auf den über einen vom Standard abweichenden TCP-Port zugegriffen werden soll.</td>
  </tr>
  <tr>
  <td><code>ingressPort</code></td>
  <td>Ersetzen Sie <code>&lt;<em>ingress-port</em>&gt;</code> durch den TCP-Port, an dem Sie auf Ihre App zugreifen wollen.</td>
  </tr>
  <tr>
  <td><code>servicePort</code></td>
  <td>Dieser Parameter ist optional. Wenn ein Wert bereitgestellt wird, wird der Port durch diesen Wert ersetzt, bevor der Datenverkehr an die Back-End-App gesendet wird. Andernfalls entspricht der Port weiterhin dem Ingress-Port. Wenn Sie diesen Parameter nicht festlegen möchten, können Sie ihn aus der Konfiguration entfernen. </td>
  </tr>
  </tbody></table>

 </dd>
 <dt>Syntax</dt>
 <dd><ol><li>Überprüfen Sie offene Ports für Ihre ALB.
<pre class="pre">
<code>kubectl get service -n kube-system</code></pre>
Die Ausgabe in der Befehlszeilenschnittstelle (CLI) ähnelt der folgenden:
<pre class="screen">
<code>NAME                                             TYPE           CLUSTER-IP       EXTERNAL-IP    PORT(S)                      AGE
public-cr18e61e63c6e94b658596ca93d087eed9-alb1   LoadBalancer   10.xxx.xx.xxx    169.xx.xxx.xxx 80:30416/TCP,443:32668/TCP   109d</code></pre></li>
<li>Öffnen Sie die ALB-Konfigurationszuordnung.
<pre class="pre">
<code>kubectl edit configmap ibm-cloud-provider-ingress-cm -n kube-system</code></pre></li>
<li>Fügen Sie die TCP-Ports zur Konfigurationszuordnung hinzu. Ersetzen Sie <code>&lt;port&gt;</code> durch die TCP-Ports, die Sie öffnen möchten.<p class="note">Standardmäßig sind Port 80 und 443 geöffnet. Wenn Port 80 und 443 geöffnet bleiben sollen, müssen Sie sie neben allen anderen TCP-Ports einschließen, die Sie im Feld `public-ports` angegeben haben. Wenn Sie eine private Lastausgleichsfunktion für Anwendungen aktiviert haben, müssen Sie auch alle Ports im Feld `private-ports` angeben, die geöffnet bleiben sollen. Weitere Informationen finden Sie im Abschnitt <a href="cs_ingress.html#opening_ingress_ports">Ports für den Ingress-Lastenausgleich öffnen</a>.</p>
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
 <li>Überprüfen Sie, ob Ihre ALB erneut mit den TCP-Ports konfiguriert wurde.
<pre class="pre">
<code>kubectl get service -n kube-system</code></pre>
Die Ausgabe in der Befehlszeilenschnittstelle (CLI) ähnelt der folgenden:
<pre class="screen">
<code>NAME                                             TYPE           CLUSTER-IP       EXTERNAL-IP    PORT(S)                      AGE
public-cr18e61e63c6e94b658596ca93d087eed9-alb1   LoadBalancer   10.xxx.xx.xxx  169.xx.xxx.xxx &lt;port1&gt;:30776/TCP,&lt;port2&gt;:30412/TCP   109d</code></pre></li>
<li>Konfigurieren Sie Ingress für den Zugriff auf Ihre App über einen vom Standard abweichenden TCP-Port. Verwenden Sie die YAML-Beispieldatei in dieser Referenz. </li>
<li>Erstellen Sie entweder eine ALB-Ressource oder aktualisieren Sie Ihre vorhandene ALB-Konfiguration.
<pre class="pre">
<code>        kubectl apply -f myingress.yaml
        </code></pre>
</li>
<li>Führen Sie den Befehl 'curl' für die Ingress-Unterdomäne aus, um auf Ihre App zuzugreifen. Beispiel: <code>curl &lt;domäne&gt;:&lt;ingress-port&gt;</code></li></ol></dd></dl>

<br />


## Annotationen für Verbindungen
{: #connection}

Mithilfe von Verbindungsannotationen können Sie ändern, wie die ALB eine Verbindung zu der Back-End-App und den Upstream-Servern herstellt, und Zeitlimits oder eine maximale Anzahl von Keepalive-Verbindungen festlegen, bevor die App oder der Server als nicht verfügbar angenommen wird. 
{: shortdesc}

### Angepasste Verbindungs- und Lesezeitlimits (proxy-connect-timeout, proxy-read-timeout)
{: #proxy-connect-timeout}

Legen Sie den Zeitraum fest, über den die Lastausgleichsfunktion für Anwendungen auf das Herstellen einer Verbindung mit bzw. auf das Lesen von Daten aus der Back-End-App warten soll, bis die Back-End-App als nicht verfügbar betrachtet wird.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>Wenn eine Clientanforderung an die Ingress-Lastausgleichsfunktion für Anwendungen (Ingress-ALB) gesendet wird, wird von der ALB eine Verbindung mit der Back-End-App geöffnet. Standardmäßig wartet die Lastausgleichsfunktion für Anwendungen (ALB) 60 Sekunden auf eine Antwort von einer Back-End-App. Falls die Back-End-App nicht innerhalb von 60 Sekunden antwortet, wird die Verbindungsanforderung abgebrochen und die Back-End-App als nicht verfügbar angenommen.

</br></br>
Nachdem die Lastausgleichsfunktion für Anwendungen (ALB) mit der Back-End-App verbunden wurde, werden Antwortdaten aus der Back-End-App von der ALB gelesen. Zwischen zwei Leseoperationen wartet die Lastausgleichsfunktion für Anwendungen (ALB) maximal 60 Sekunden auf Daten aus der Back-End-App. Falls die Back-End-App innerhalb von 60 Sekunden keine Daten sendet, wird die Verbindung zur Back-End-App gekappt und die App wird als nicht verfügbar angenommen.
</br></br>
Ein Verbindungszeitlimit und Lesezeitlimit von 60 Sekunden ist die Standardeinstellung auf einem Proxy und sollte in der Regel nicht geändert werden.
</br></br>
Falls die Verfügbarkeit Ihrer App nicht durchgehend gewährleistet ist oder Ihre App aufgrund hoher Workloads langsam antwortet, können Sie die Verbindungs- und Lesezeitlimits nach oben korrigieren. Denken Sie daran, dass sich das Erhöhen des Zeitlimits negativ auf die Leistung der Lastausgleichsfunktion für Anwendungen (ALB) auswirken kann, da die Verbindung mit der Back-End-App geöffnet bleiben muss, bis das Zeitlimit erreicht wurde.
</br></br>
Sie können andererseits das Zeitlimit nach unten korrigieren, um die Leistung der Lastausgleichsfunktion für Anwendungen (ALB) zu verbessern. Stellen Sie sicher, dass Ihre Back-End-App Anforderungen auch bei höheren Workloads innerhalb des angegebenen Zeitlimits verarbeiten kann.</dd>
<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: myingress
 annotations:
   ingress.bluemix.net/proxy-connect-timeout: "serviceName=&lt;mein_service&gt; timeout=&lt;verbindungszeitlimit&gt;"
   ingress.bluemix.net/proxy-read-timeout: "serviceName=&lt;mein_service&gt; timeout=&lt;lesezeitlimit&gt;"
spec:
 tls:
 - hosts:
   - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
 - host: meine_domäne
   http:
     paths:
     - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080</code></pre>

<table>
<caption>Erklärung der Komponenten von Annotationen</caption>
 <thead>
 <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
 </thead>
 <tbody>
 <tr>
 <td><code>&lt;verbindungszeitlimit&gt;</code></td>
 <td>Die Anzahl der Sekunden oder Minuten, die gewartet werden soll, bis eine Verbindung zur Back-End-App hergestellt wird, z. B. <code>65s</code> oder <code>1m</code>. Ein Verbindungszeitlimit kann nicht größer als 75 Sekunden sein.</td>
 </tr>
 <tr>
 <td><code>&lt;lesezeitlimit&gt;</code></td>
 <td>Die Anzahl der Sekunden oder Minuten, die auf das Lesen von Daten aus der Back-End-App gewartet werden soll. Beispiel: <code>65s</code> oder <code>2m</code>.
 </tr>
 </tbody></table>

 </dd></dl>

<br />



### Keepalive-Anforderungen (keepalive-requests)
{: #keepalive-requests}

Maximale Anzahl von Anforderungen festlegen, die über eine Keepalive-Verbindung bedient werden können.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>
Legen Sie die maximale Anzahl von Anforderungen fest, die über eine Keepalive-Verbindung bedient werden können.
</dd>


<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
name: myingress
annotations:
  ingress.bluemix.net/keepalive-requests: "serviceName=&lt;mein_service&gt; requests=&lt;max._anzahl_anforderungen&gt;"
spec:
tls:
- hosts:
  - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
- host: meine_domäne
  http:
    paths:
    - path: /
      backend:
        serviceName: &lt;mein_service&gt;
        servicePort: 8080</code></pre>

<table>
<caption>Erklärung der Komponenten von Annotationen</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
</thead>
<tbody>
<tr>
<td><code>serviceName</code></td>
<td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen des Kubernetes-Service, den Sie für Ihre App erstellt haben. Dieser Parameter ist optional. Die Konfiguration wird auf alle Services auf dem Ingress-Host angewendet, es sei denn, es wird ein Service angegeben. Wird der Parameter bereitgestellt, werden die Keepalive-Anforderung für den angegebenen Service festgelegt. Wird der Parameter nicht bereitgestellt, werden die Keepalive-Anforderungen auf der Serverebene der Datei <code>nginx.conf</code> für alle Services festgelegt, für die die Keepalive-Anforderungen nicht konfiguriert sind.</td>
</tr>
<tr>
<td><code>requests</code></td>
<td>Ersetzen Sie <code>&lt;<em>max._anzahl_anforderungen</em>&gt;</code> durch die maximale Anzahl der Anforderungen, die über eine einzige Keepalive-Verbindung bedient werden können.</td>
</tr>
</tbody></table>

</dd>
</dl>

<br />



### Keepalive-Zeitlimit (keepalive-timeout)
{: #keepalive-timeout}

Maximale Zeitspanne festlegen, die eine Keepalive-Verbindung serverseitig geöffnet bleibt.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>
Maximale Zeitspanne festlegen, die eine Keepalive-Verbindung auf dem Server geöffnet bleibt.
</dd>


<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: myingress
 annotations:
   ingress.bluemix.net/keepalive-timeout: "serviceName=&lt;mein_service&gt; timeout=&lt;zeit&gt;s"
spec:
 tls:
 - hosts:
   - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
 - host: meine_domäne
   http:
     paths:
     - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080</code></pre>

<table>
<caption>Erklärung der Komponenten von Annotationen</caption>
 <thead>
 <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
 </thead>
 <tbody>
 <tr>
 <td><code>serviceName</code></td>
 <td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen des Kubernetes-Service, den Sie für Ihre App erstellt haben. Dieser Parameter ist optional. Wird der Parameter bereitgestellt, wird das Keepalive-Zeitlimit für den angegebenen Service festgelegt. Wird der Parameter nicht bereitgestellt, wird das Keepalive-Zeitlimit auf der Serverebene der Datei <code>nginx.conf</code> für alle Services festgelegt, für die das Keepalive-Zeitlimit nicht konfiguriert ist.</td>
 </tr>
 <tr>
 <td><code>timeout</code></td>
 <td>Ersetzen Sie <code>&lt;<em>zeit</em>&gt;</code> durch den Zeitraum in Sekunden. Beispiel:<code>timeout=20s</code>. Der Wert null inaktiviert die Keepalive-Verbindungen für den Client.</td>
 </tr>
 </tbody></table>

 </dd>
 </dl>

<br />


### Proxy zu nächstem Upstream (proxy-next-upstream-config)
{: #proxy-next-upstream-config}

Festlegen, wann die ALB eine Anforderung an den nächsten Upstream-Server übergeben kann.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>
Die Ingress-Lastausgleichsfunktion für Anwendungen (Ingress-ALB) fungiert als Proxy zwischen der Client-App und Ihrer App. Für einige App-Konfigurationen müssen Sie unter Umständen mehrere Upstream-Server bereitstellen, die eingehende Clientanforderungen von der ALB verarbeiten. Manchmal kann der Proxy-Server, den die ALB verwendet, keine Verbindung mit einem Upstream-Server herstellen, den die App verwendet. Die ALB kann dann versuchen, eine Verbindung mit dem nächsten Upstream-Server herzustellen, um die Anforderung stattdessen an ihn zu übergeben. Sie können die Annotation `proxy-next-upstream-config` verwenden, um festzulegen, in welchen Fällen, wie lange und wie oft die ALB versuchen kann, eine Anforderung an den nächsten Upstream-Server zu übergeben.<p class="note">Wenn Sie `proxy-next-upstream-config` verwenden, ist immer ein Zeitlimit konfiguriert. Fügen Sie deshalb `timeout=true` nicht zu dieser Annotation hinzu.</p>
</dd>
<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>
<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/proxy-next-upstream-config: "serviceName=&lt;mein_service1&gt; retries=&lt;versuche&gt; timeout=&lt;zeit&gt; error=true http_502=true; serviceName=&lt;mein_service2&gt; http_403=true non_idempotent=true"
spec:
  tls:
  - hosts:
    - meine_domäne
    secretName: mein_geheimer_schlüssel
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: /
        backend:
          serviceName: mein_service1
          servicePort: 80
</code></pre>

<table>
<caption>Erklärung der Komponenten von Annotationen</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
</thead>
<tbody>
<tr>
<td><code>serviceName</code></td>
<td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen des Kubernetes-Service, den Sie für Ihre App erstellt haben.</td>
</tr>
<tr>
<td><code>retries</code></td>
<td>Ersetzen Sie <code>&lt;<em>versuche</em>&gt;</code> durch die maximale Anzahl von Versuchen, die der ALB zur Verfügung stehen, um eine Anforderung an den nächsten Upstream-Server zu übergeben. Diese Anzahl beinhaltet die ursprüngliche Anforderung. Um diese Einschränkung zu inaktivieren, geben Sie <code>0</code> an. Wenn Sie keinen Wert angeben, wird der Standardwert <code>0</code> verwendet.
</td>
</tr>
<tr>
<td><code>timeout</code></td>
<td>Ersetzen Sie <code>&lt;<em>zeit</em>&gt;</code> durch die Höchstdauer (in Sekunden), die die ALB versucht, eine Anforderung an den nächsten Upstream-Server zu übergeben. Geben Sie beispielsweise <code>30s</code> ein, um eine Dauer von 30 Sekunden festzulegen. Um diese Einschränkung zu inaktivieren, geben Sie <code>0</code> an. Wenn Sie keinen Wert angeben, wird der Standardwert <code>0</code> verwendet.
</td>
</tr>
<tr>
<td><code>error</code></td>
<td>Hat dieser Parameter den Wert <code>true</code>, übergibt die ALB eine Anforderung an den nächsten Upstream-Server, wenn ein Fehler auftritt, während gleichzeitig eine Verbindung mit dem ersten Upstream-Server eingerichtet, eine Anforderung an ihn übergeben oder der Antwortheader gelesen wird.
</td>
</tr>
<tr>
<td><code>invalid_header</code></td>
<td>Hat dieser Parameter <code>true</code>, übergibt die ALB eine Anforderung an den nächsten Upstream-Server, wenn der erste Upstream-Server eine leere oder ungültige Antwort zurückgibt.
</td>
</tr>
<tr>
<td><code>http_502</code></td>
<td>Hat dieser Parameter den Wert <code>true</code>, übergibt die ALB eine Anforderung an den nächsten Upstream-Server, wenn der erste Upstream-Server eine Antwort mit dem Code 502 zurückgibt. Sie können die folgenden HTTP-Antwortcodes bestimmen: <code>500</code>, <code>502</code>, <code>503</code>, <code>504</code>, <code>403</code>, <code>404</code>, <code>429</code>.
</td>
</tr>
<tr>
<td><code>non_idempotent</code></td>
<td>Hat dieser Parameter den Wert <code>true</code>, kann die ALB Anforderungen mit einer 'non-idempotent'-Methode an den nächsten Upstream-Server übergeben. Standardmäßig übergibt die ALB diese Anforderungen nicht an den nächsten Upstream-Server.
</td>
</tr>
<tr>
<td><code>off</code></td>
<td>Um zu verhindern, dass die ALB Anforderungen an den nächsten Upstream-Server übergibt, setzen Sie diesen Parameter auf <code>true</code>.
</td>
</tr>
</tbody></table>
</dd>
</dl>

<br />


### Sitzungsaffinität mit Cookies (sticky-cookie-services)
{: #sticky-cookie-services}

Verwenden Sie die permanente Cookie-Annotation, um Ihrer Lastausgleichsfunktion für Anwendungen (ALB) Sitzungsaffinität hinzuzufügen und eingehenden Netzverkehr immer an denselben Upstream-Server weiterzuleiten.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>Um eine hohe Verfügbarkeit zu erreichen, müssen Sie bei einigen App-Konfigurationen unter Umständen mehrere Upstream-Server bereitstellen, die eingehende Clientanforderungen verarbeiten. Wenn ein Client eine Verbindung mit Ihrer Back-End-App herstellt, kann ein Client für die Dauer einer Sitzung bzw. für die Zeit, die für den Abschluss einer Task erforderlich ist, von demselben Upstream-Server bedient werden. Sie können Ihre Lastausgleichsfunktion für Anwendungen (ALB) so konfigurieren, dass Sitzungsaffinität sichergestellt ist, indem Sie eingehenden Netzverkehr immer an denselben Upstream-Server weiterleiten.

</br></br>
Jeder Client, der eine Verbindung mit Ihrer Back-End-App herstellt, wird durch die Lastausgleichsfunktion für Anwendungen (ALB) einem der verfügbaren Upstream-Server zugewiesen. Die Lastausgleichsfunktion für Anwendungen (ALB) erstellt ein Sitzungscookie, das in der App des Clients gespeichert wird und das in die Headerinformationen jeder Anforderung zwischen der ALB und dem Client eingeschlossen wird. Die Informationen im Cookie stellen sicher, dass alle Anforderungen während der gesamten Sitzung von demselben Upstream-Server verarbeitet werden.

</br></br>
Wenn Sie mehrere Services einschließen, verwenden Sie ein Semikolon (;) zum Trennen der Services.</dd>
<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/sticky-cookie-services: "serviceName=&lt;mein_service1&gt; name=&lt;cookiename1&gt; expires=&lt;ablaufzeit1&gt; path=&lt;cookiepfad1&gt; hash=&lt;hashalgorithmus1&gt;;serviceName=&lt;mein_service2&gt; name=&lt;cookiename2&gt; expires=&lt;ablaufzeit2&gt; path=&lt;cookiepfad2&gt; hash=&lt;hashalgorithmus2&gt;"
spec:
  tls:
  - hosts:
    - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: /service1_path
        backend:
          serviceName: &lt;mein_service1&gt;
          servicePort: 8080
      - path: /service2_path
        backend:
          serviceName: &lt;mein_service2&gt;
          servicePort: 80</code></pre>

  <table>
  <caption>Erklärung der Komponenten von Annotationen</caption>
  <thead>
  <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
  </thead>
  <tbody>
  <tr>
  <td><code>serviceName</code></td>
  <td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen des Kubernetes-Service, den Sie für Ihre App erstellt haben.</td>
  </tr>
  <tr>
  <td><code>name</code></td>
  <td>Ersetzen Sie <code>&lt;<em>cookiename</em>&gt;</code> durch den Namen eines permanenten Cookies, das während einer Sitzung erstellt wird.</td>
  </tr>
  <tr>
  <td><code>expires</code></td>
  <td>Ersetzen Sie <code>&lt;<em>ablaufzeit</em>&gt;</code> durch den Zeitraum in Sekunden (s), Minuten (m) oder Stunden (h), nach dem das permanente Cookie abläuft. Diese Zeit ist unabhängig von der Benutzeraktivität. Nachdem das Cookie abgelaufen ist, wird es durch den Web-Browser des Clients gelöscht und nicht mehr an die Lastausgleichsfunktion für Anwendungen (ALB) gesendet. Um beispielsweise eine Ablaufzeit von einer Sekunde, einer Minute oder einer Stunde festzulegen, geben Sie <code>1s</code>, <code>1m</code> oder <code>1h</code> ein.</td>
  </tr>
  <tr>
  <td><code>path</code></td>
  <td>Ersetzen Sie <code>&lt;<em>cookiepfad</em>&gt;</code> durch den Pfad, der an die Ingress-Unterdomäne angehängt werden soll und der angibt, für welche Domänen und Unterdomänen das Cookie an die Lastausgleichsfunktion für Anwendungen (ALB) gesendet wird. Wenn Ihre Ingress-Domäne beispielsweise <code>www.myingress.com</code> ist und Sie das Cookie in jeder Clientanforderung senden möchten, müssen Sie <code>path=/</code> festlegen. Wenn Sie das Cookie nur für <code>www.myingress.com/myapp</code> und alle zugehörigen Unterdomänen senden möchten, müssen Sie <code>path=/myapp</code> festlegen.</td>
  </tr>
  <tr>
  <td><code>hash</code></td>
  <td>Ersetzen Sie <code>&lt;<em>hashalgorithmus</em>&gt;</code> durch den Hashalgorithmus, der die Informationen im Cookie schützt. Nur <code>sha1</code> wird unterstützt. SHA1 erstellt eine Hashsumme auf der Grundlage der Informationen im Cookie und hängt die Hashsumme an das Cookie an. Der Server kann die Informationen im Cookie entschlüsseln und die Datenintegrität bestätigen.</td>
  </tr>
  </tbody></table>

 </dd></dl>

<br />


### Parameter 'fail_timeout' für Upstream-Server (upstream-fail-timeout)
{: #upstream-fail-timeout}

Legen Sie fest, wie lange der ALB versuchen kann, eine Verbindung zum Server herzustellen.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>
Legen Sie fest, wie lange der ALB versuchen kann, eine Verbindung zu einem Server herzustellen, bevor der Server als nicht verfügbar betrachtet wird. Damit ein Server als nicht verfügbar betrachtet werden kann, muss die ALB die maximale Anzahl fehlgeschlagener Verbindungsversuche in der festgelegten Zeit erreichen, die durch die Annotation <a href="#upstream-max-fails"><code>upstream-max-failed</code></a> festgelegt wurde. Diese Zeit bestimmt auch, wie lange der Server als nicht verfügbar betrachtet wird.
</dd>


<dt>YAML-Beispiel einer Ingress-Ressource</dt>
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
    - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080</code></pre>

<table>
<thead>
<th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
</thead>
<tbody>
<tr>
<td><code>serviceName (optional)</code></td>
<td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen des Kubernetes-Service, den Sie für Ihre App erstellt haben.</td>
</tr>
<tr>
<td><code>fail-timeout</code></td>
<td>Ersetzen Sie <code>&lt;<em>fail_timeout</em>&gt;</code> durch die Zeit, die die ALB versuchen kann, eine Verbindung zu einem Server herzustellen, bevor der Server als nicht verfügbar betrachtet wird. Der Standardwert ist <code>10s</code>. Die Zeit muss in Sekunden angegeben werden.</td>
</tr>
</tbody></table>
</dd>
</dl>

<br />


### Keepalive-Verbindungen für Upstream-Server (upstream-keepalive)
{: #upstream-keepalive}

Maximale Anzahl der inaktiven Keepalive-Verbindungen für einen Upstream-Server festlegen.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>
Legen Sie die maximale Anzahl inaktiver Keepalive-Verbindungen zum Upstream-Server für einen angegebenen Service fest. Der Upstream-Server verfügt standardmäßig über 64 inaktive Keepalive-Verbindungen.
</dd>


<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/upstream-keepalive: "serviceName=&lt;mein_service&gt; keepalive=&lt;max._anzahl_verbindungen&gt;"
spec:
  tls:
  - hosts:
    - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080</code></pre>

<table>
<caption>Erklärung der Komponenten von Annotationen</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
</thead>
<tbody>
<tr>
<td><code>serviceName</code></td>
<td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen des Kubernetes-Service, den Sie für Ihre App erstellt haben.</td>
</tr>
<tr>
<td><code>keepalive</code></td>
<td>Ersetzen Sie <code>&lt;<em>max._anzahl_verbindungen</em>&gt;</code> durch die maximal zulässige Anzahl der inaktiven Keepalive-Verbindungen zum Upstream-Server. Der Standardwert ist <code>64</code>. Bei Angabe des Werts <code>0</code> werden Keepalive-Verbindungen zum Upstream-Server für den angegebenen Service inaktiviert.</td>
</tr>
</tbody></table>
</dd>
</dl>

<br />


### Parameter 'max_fails' für Upstream-Server (upstream-max-fails)
{: #upstream-max-fails}

Legen Sie die maximale Anzahl nicht erfolgreicher Versuche fest, mit dem Server zu kommunizieren.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>
Legen Sie die maximale Anzahl der fehlgeschlagenen Versuche der ALB zum Herstellen einer Verbindung fest, bevor der Server als nicht verfügbar betrachtet wird. Damit der Server als nicht verfügbar betrachtet werden kann, muss die ALB die maximale Anzahl innerhalb der durch die Annotation <a href="#upstream-fail-timeout"><code>upstream-fail-timeout</code></a> festgelegten Dauer erreichen. Die Zeitdauer, für die der Server als nicht verfügbar betrachtet wird, wird auch durch die Annotation <code>upstream-fail-timeout</code> festgelegt.</dd>


<dt>YAML-Beispiel einer Ingress-Ressource</dt>
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
    - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080</code></pre>

<table>
<thead>
<th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
</thead>
<tbody>
<tr>
<td><code>serviceName (optional)</code></td>
<td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen des Kubernetes-Service, den Sie für Ihre App erstellt haben.</td>
</tr>
<tr>
<td><code>max-fails</code></td>
<td>Ersetzen Sie <code>&lt;<em>max_fails</em>&gt;</code> durch die maximale Anzahl nicht erfolgreicher Versuche der ALB, mit dem Server zu kommunizieren. Der Standardwert ist <code>1</code>. Der Wert <code>0</code> inaktiviert die Annotation.</td>
</tr>
</tbody></table>
</dd>
</dl>

<br />


## Annotationen für HTTPS- und TLS/SSL-Authentifizierung
{: #https-auth}

Mithilfe von HTTPS- und TLS/SSL-Authentifizierungsannotationen können Sie Ihre ALB für HTTPS-Datenverkehr konfigurieren, HTTPS-Standardports ändern, SSL-Verschlüsselung für Datenverkehr aktivieren, der an Ihre Back-End-Apps gesendet wird, oder eine gegenseitige Authentifizierung konfigurieren. 
{: shortdesc}

### {{site.data.keyword.appid_short_notm}} Authentifizierung (appid-auth)
{: #appid-auth}

{{site.data.keyword.appid_full_notm}} zur Authentifizierung bei Ihrer App verwenden.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>
Authentifizieren Sie Web- oder API-HTTP/HTTPS-Anforderungen mit {{site.data.keyword.appid_short_notm}}.

<p>Wenn Sie den Anforderungstyp auf <code>web</code> setzen, wird eine Webanforderung, die ein {{site.data.keyword.appid_short_notm}}-Zugriffstoken enthält, geprüft. Wenn die Tokenprüfung fehlschlägt, wird die Webanforderung zurückgewiesen. Wenn die Anforderung kein Zugriffstoken enthält, wird die Anforderung an die {{site.data.keyword.appid_short_notm}}-Anmeldeseite umgeleitet. Damit die {{site.data.keyword.appid_short_notm}}-Webauthentifizierung funktioniert, müssen Cookies im Browser des Benutzers aktiviert sein.</p>

<p>Wenn Sie den Anforderungstyp auf <code>api</code> setzen, wird eine API-Anforderung, die ein {{site.data.keyword.appid_short_notm}}-Zugriffstoken enthält, geprüft. Wenn die Anforderung kein Zugriffstoken enthält, wird die Fehlernachricht <code>401: Unauthorized</code> an den Benutzer zurückgegeben.</p>

<p class="note">Aus Sicherheitsgründen unterstützt die {{site.data.keyword.appid_short_notm}}-Authentifizierung nur Back-Ends mit aktiviertem TLS/SSL.</p>
</dd>
<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/appid-auth: "bindSecret=&lt;geheimer_bindungsschlüssel&gt; namespace=&lt;namensbereich&gt; requestType=&lt;anforderungstyp&gt; serviceName=&lt;mein_service&gt;"
spec:
  tls:
  - hosts:
    - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080</code></pre>

<table>
<caption>Erklärung der Komponenten von Annotationen</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
</thead>
<tbody>
<tr>
<td><code>bindSecret</code></td>
<td>Ersetzen Sie <em><code>&lt;geheimer_bindungsschlüssel&gt;</code></em> durch den geheimen Kubernetes-Schlüssel, der den geheimen Bindungsschlüssel für Ihre {{site.data.keyword.appid_short_notm}}-Serviceinstanz speichert.</td>
</tr>
<tr>
<td><code>namespace</code></td>
<td>Ersetzen Sie <em><code>&lt;namensbereich&gt;</code></em> durch den Namensbereich des geheimen Bindungsschlüssels. In diesem Feld wird standardmäßig der `Standardname` für den Namensbereich verwendet.</td>
</tr>
<tr>
<td><code>requestType</code></td>
<td>Ersetzen Sie <code><em>&lt;anforderungstyp&gt;</em></code> durch den Anforderungstyp, den Sie an {{site.data.keyword.appid_short_notm}} senden wollen. Gültige Werte sind `web` oder `api`. Der Standardwert ist `api`.</td>
</tr>
<tr>
<td><code>serviceName</code></td>
<td>Ersetzen Sie <code><em>&lt;mein_service&gt;</em></code> durch den Namen des Kubernetes-Service, den Sie für Ihre App erstellt haben. Dieses Feld ist erforderlich. Wenn ein Servicename nicht enthalten ist, wird die Annotation für alle Services aktiviert.  Wenn ein Servicename enthalten ist, wird die Annotation nur für diesen Service aktiviert. Trennen Sie mehrere Services durch ein Komma (,).</td>
</tr>
</tbody></table>
</dd>
<dt>Syntax</dt></dl>

Da die App {{site.data.keyword.appid_short_notm}} für die Authentifizierung verwendet, müssen Sie eine {{site.data.keyword.appid_short_notm}}-Instanz bereitstellen, die Instanz mit gültigen Umleitungs-URIs konfigurieren und einen geheimen Bindungsschlüssel generieren, indem Sie die Instanz an den Cluster binden.

1. Wählen Sie eine vorhandene Instanz aus oder erstellen Sie eine neue {{site.data.keyword.appid_short_notm}}-Instanz.
    * Um eine vorhandene Instanz zu verwenden, stellen Sie sicher, dass der Name der Serviceinstanz keine Leerzeichen enthält. Um Leerzeichen zu entfernen, wählen Sie das Menü für mehr Optionen neben dem Namen der Serviceinstanz und anschließend **Service umbenennen** aus.
    * Gehen Sie wie folgt vor, um eine [neue {{site.data.keyword.appid_short_notm}}-Instanz](https://console.bluemix.net/catalog/services/app-id) bereitzustellen:
        1. Ersetzen Sie den im Feld **Servicename** automatisch eingetragenen Wert durch Ihren eigenen eindeutigen Namen für die Serviceinstanz. Der Name der Serviceinstanz darf keine Leerzeichen enthalten.
        2. Wählen Sie die Region aus, in der Ihr Cluster implementiert ist.
        3. Klicken Sie auf **Erstellen**.
2. Fügen Sie Umleitungs-URLs für Ihre App hinzu. Eine Umleitungs-URL ist der Callback-Endpunkt Ihrer App. Um Phishing-Attacken zu verhindern, validiert die App-ID die Anforderungs-URL gegen die Whitelist von Umleitungs-URLs.
    1. Navigieren Sie in der {{site.data.keyword.appid_short_notm}}-Managementkonsole zu **Identitätsprovider > Verwalten**.
    2. Stellen Sie sicher, dass Sie einen Identitätsprovider ausgewählt haben. Wenn kein Identitätsprovider ausgewählt ist, wird der Benutzer nicht authentifiziert, sondern es wird ein Zugriffstoken für den anonymen Zugriff auf die App ausgegeben.
    3. Fügen Sie im Feld **Web-Weiterleitungs-URLs** Weiterleitungs-URLs für Ihre App im Format `http://<hostname>/<app_path>/appid_callback` oder `https://<hostname>/<app_path>/appid_callback` hinzu.
        * Eine App, die bei der IBM Ingress-Unterdomäne registriert ist, könnte z. B. folgendermaßen aussehen: `https://mycluster.us-south.containers.appdomain.cloud/myapp1path/appid_callback`.
        * Eine App, die bei einer angepassten Domäne registriert ist, könnte folgendermaßen aussehen: `http://mydomain.net/myapp2path/appid_callback`.

3. Binden Sie die {{site.data.keyword.appid_short_notm}}-Serviceinstanz an den Cluster.
    ```
    ibmcloud ks cluster-service-bind <clustername_oder_-id> <namensbereich> <serviceinstanzname>
    ```
    {: pre}
    Wenn der Service erfolgreich zu Ihrem Cluster hinzugefügt worden ist, wird ein geheimer Schlüssel für den Cluster erstellt, der die Berechtigungsnachweise Ihrer Serviceinstanz enthält. CLI-Beispielausgabe:
    ```
    ibmcloud ks cluster-service-bind mycluster mynamespace appid1
    Binding service instance to namespace...
    OK
    Namespace:    mynamespace
    Secret name:  binding-<serviceinstanzname>
    ```
    {: screen}

4. Rufen Sie den geheimer Schlüssel ab, der im Namensbereich Ihres Clusters erstellt wurde.
    ```
    kubectl get secrets --namespace=<namensbereich>
    ```
    {: pre}

5. Verwenden Sie den geheimen Bindungsschlüssel und den Namensbereich des Clusters, um die Annotation `appid-auth` zu Ihrer Ingress-Ressource hinzuzufügen.

<br />



### Angepasste HTTP- und HTTPS-Ports (custom-port)
{: #custom-port}

Änderung der Standardports für den HTTP-Netzverkehr (Port 80) und den HTTPS-Netzverkehr (Port 443).
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>Standardmäßig ist die Ingress-Lastausgleichsfunktion für Anwendungen (ALB) so konfiguriert, dass sie für eingehenden HTTP-Netzverkehr am Port mit der Nummer 80 und für eingehenden HTTPS-Netzverkehr am Port mit der Nummer 443 empfangsbereit ist. Sie können die Standardports ändern, um die Sicherheit der Domäne Ihrer Lastausgleichsfunktion für Anwendungen (ALB) zu verbessern oder um ausschließlich einen HTTPS-Port zu aktivieren.<p class="note">Um die gegenseitige Authentifizierung an einem Port zu ermöglichen, [konfigurieren Sie die Lastausgleichsfunktion für Anwendungen (ALB) zum Öffnen des gültigen Ports](cs_ingress.html#opening_ingress_ports) und geben Sie den Port dann in der Annotation [`mutual-auth` an](#mutual-auth). Verwenden Sie die Annotation `custom-port` nicht, um einen Port für die gegenseitige Authentifizierung anzugeben.</p></dd>


<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: myingress
 annotations:
   ingress.bluemix.net/custom-port: "protocol=&lt;protokoll1&gt; port=&lt;port1&gt;;protocol=&lt;protokoll2&gt;port=&lt;port2&gt;"
spec:
 tls:
 - hosts:
   - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
 - host: meine_domäne
   http:
     paths:
     - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080</code></pre>

<table>
<caption>Erklärung der Komponenten von Annotationen</caption>
 <thead>
 <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
 </thead>
 <tbody>
 <tr>
 <td><code>&lt;protokoll&gt;</code></td>
 <td>Geben Sie <code>http</code> oder <code>https</code> ein, um den Standardport für eingehenden HTTP- bzw. HTTPS-Netzverkehr zu ändern.</td>
 </tr>
 <tr>
 <td><code>&lt;port&gt;</code></td>
 <td>Geben Sie die Portnummer ein, die für den eingehenden HTTP- oder HTTPS-Datenaustausch im Netz verwendet werden soll.  <p class="note">Wenn für HTTP oder HTTPS ein angepasster Port angegeben wird, dann sind die Standardports für HTTP und auch für HTTPS nicht mehr gültig. Um beispielsweise den Standardport für HTTPS in 8443 zu ändern, für HTTP jedoch weiterhin den Standardport zu verwenden, müssen Sie für beide Protokolle angepasste Ports festlegen: <code>custom-port: "protocol=http port=80; protocol=https port=8443"</code>.</p></td>
 </tr>
 </tbody></table>

 </dd>
 <dt>Syntax</dt>
 <dd><ol><li>Überprüfen Sie offene Ports für Ihre ALB.
<pre class="pre">
<code>kubectl get service -n kube-system</code></pre>
Die Ausgabe in der Befehlszeilenschnittstelle (CLI) ähnelt der folgenden:
<pre class="screen">
<code>NAME                                             TYPE           CLUSTER-IP       EXTERNAL-IP    PORT(S)                      AGE
public-cr18e61e63c6e94b658596ca93d087eed9-alb1   LoadBalancer   10.xxx.xx.xxx    169.xx.xxx.xxx 80:30416/TCP,443:32668/TCP   109d</code></pre></li>
<li>Öffnen Sie die ALB-Konfigurationszuordnung.
<pre class="pre">
<code>kubectl edit configmap ibm-cloud-provider-ingress-cm -n kube-system</code></pre></li>
<li>Fügen Sie die nicht dem Standard entsprechenden HTTP- und HTTPS-Ports zur Konfigurationszuordnung hinzu. Ersetzen Sie &lt;port&gt; durch den HTTP- oder HTTPS-Port, der geöffnet werden soll.<p class="note">Standardmäßig sind Port 80 und 443 geöffnet. Wenn Port 80 und 443 geöffnet bleiben sollen, müssen Sie sie neben allen anderen TCP-Ports einschließen, die Sie im Feld `public-ports` angegeben haben. Wenn Sie eine private Lastausgleichsfunktion für Anwendungen aktiviert haben, müssen Sie auch alle Ports im Feld `private-ports` angeben, die geöffnet bleiben sollen. Weitere Informationen finden Sie im Abschnitt <a href="cs_ingress.html#opening_ingress_ports">Ports für den Ingress-Lastenausgleich öffnen</a>.</p>
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
 <li>Überprüfen Sie, ob Ihre ALB erneut mit den nicht dem Standard entsprechenden Ports konfiguriert wurde.
<pre class="pre">
<code>kubectl get service -n kube-system</code></pre>
Die Ausgabe in der Befehlszeilenschnittstelle (CLI) ähnelt der folgenden:
<pre class="screen">
<code>NAME                                             TYPE           CLUSTER-IP       EXTERNAL-IP    PORT(S)                      AGE
public-cr18e61e63c6e94b658596ca93d087eed9-alb1   LoadBalancer   10.xxx.xx.xxx  169.xx.xxx.xxx &lt;port1&gt;:30776/TCP,&lt;port2&gt;:30412/TCP   109d</code></pre></li>
<li>Konfigurieren Sie Ingress zur Verwendung der nicht dem Standard entsprechenden Ports bei der Weiterleitung von eingehendem Netzverkehr an Ihre Services. Verwenden Sie die YAML-Beispieldatei in dieser Referenz. </li>
<li>Aktualisieren Sie Ihre ALB-Konfiguration.
<pre class="pre">
<code>        kubectl apply -f myingress.yaml
        </code></pre>
</li>
<li>Öffnen Sie Ihren bevorzugten Web-Browser, um auf Ihre App zuzugreifen. Beispiel: <code>https://&lt;ibm_domäne&gt;:&lt;port&gt;/&lt;servicepfad&gt;/</code></li></ol></dd></dl>

<br />



### HTTP-Weiterleitungen an HTTPS (redirect-to-https)
{: #redirect-to-https}

Konvertierung von unsicheren HTTP-Clientanforderungen in HTTPS.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>Sie konfigurieren Ihre Ingress-Lastausgleichsfunktion für Anwendungen (Ingress-ALB) für die Sicherung Ihrer Domäne mit dem von IBM bereitgestellten TLS-Zertifikat oder Ihrem angepassten TLS-Zertifikat. Manche Benutzer versuchen unter Umständen, auf Ihre Apps zuzugreifen, indem Sie eine unsichere <code>http</code>-Anforderung an Ihre ALB-Domäne senden; z. B. <code>http://www.myingress.com</code>, anstatt <code>https</code> zu verwenden. Sie können die 'redirect'-Annotation verwenden, um unsichere HTTP-Anforderungen immer in HTTPS zu konvertieren. Wenn Sie diese Annotation nicht verwenden, werden unsichere HTTP-Anforderungen nicht standardmäßig in HTTPS-Anforderungen konvertiert und machen unter Umständen vertrauliche Daten ohne Verschlüsselung öffentlich zugänglich.

</br></br>
Das Umadressieren von HTTP-Anforderungen in HTTPS ist standardmäßig inaktiviert.</dd>

<dt>YAML-Beispiel einer Ingress-Ressource</dt>
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
   - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
 - host: meine_domäne
   http:
     paths:
     - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080</code></pre>

</dd>

</dl>

<br />


### HTTP Strict Transport Security (hsts)
{: #hsts}

<dl>
<dt>Beschreibung</dt>
<dd>
HSTS weist den Browser an, nur über HTTPS auf eine Domäne zuzugreifen. Selbst wenn der Benutzer einen einfachen HTTP-Link eingibt oder einem solchen folgt, aktualisiert der Browser die Verbindung strikt auf HTTPS:
</dd>


<dt>YAML-Beispiel einer Ingress-Ressource</dt>
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
    - meine_domäne
    secretName: mein_geheimer_schlüssel
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: /service1_path
        backend:
          serviceName: mein_service1
          servicePort: 8443
      - path: /service2_path
        backend:
          serviceName: mein_service2
          servicePort: 8444
          </code></pre>

<table>
<caption>Erklärung der Komponenten von Annotationen</caption>
  <thead>
  <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
  </thead>
  <tbody>
  <tr>
  <td><code>enabled</code></td>
  <td>Verwenden Sie <code>true</code>, um HSTS zu aktivieren.</td>
  </tr>
    <tr>
  <td><code>maxAge</code></td>
  <td>Ersetzen Sie <code>&lt;<em>31536000</em>&gt;</code> durch eine ganze Zahl, die angibt, wie viele Sekunden ein Browser Sendeanforderungen direkt an HTTPS zwischenspeichert. Der Standardwert ist <code>31536000</code>, was 1 Jahr entspricht.</td>
  </tr>
  <tr>
  <td><code>includeSubdomains</code></td>
  <td>Verwenden Sie <code>true</code>, um dem Browser mitzuteilen, dass die HSTS-Richtlinie auch für alle Unterdomänen der aktuellen Domäne gilt. Der Standard ist <code>true</code>. </td>
  </tr>
  </tbody></table>

  </dd>
  </dl>


<br />


### Gegenseitige Authentifizierung (mutual-auth)
{: #mutual-auth}

Gegenseitige Authentifizierung für die Lastausgleichsfunktion für Anwendungen (ALB) konfigurieren.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>
Konfigurieren Sie die gegenseitige Authentifizierung für Downstream-Datenverkehr für die Ingress-ALB. Der externe Client authentifiziert den Server und der Server authentifiziert den Client anhand von Zertifikaten. Die gegenseitige Authentifizierung wird auch als zertifikatsbasierte Authentifizierung oder Zweiwegeauthentifizierung bezeichnet.</br></br>
Verwenden Sie die Annotation `mutual-auth` für die SSL-Terminierung zwischen dem Client und der Ingress-Lastausgleichsfunktion für Anwendungen. Verwenden Sie die [Annotation `ssl-services`](#ssl-services) für die SSL-Terminierung zwischen der Ingress-Lastausgleichsfunktion für Anwendungen und der Back-End-App.
</dd>

<dt>Voraussetzungen</dt>
<dd>
<ul>
<li>Sie müssen über einen gültigen geheimen Schlüssel für die gegenseitige Authentifizierung verfügen, der die erforderliche Datei <code>client.crt</code> enthält. Informationen zum Erstellen eines geheimen Schlüssels für gegenseitige Authentifizierung finden Sie in den Schritten am Ende dieses Abschnitts.</li>
<li>Um die gegenseitige Authentifizierung an einem anderen Port als 443 zu ermöglichen, [konfigurieren Sie die Lastausgleichsfunktion für Anwendungen (ALB) zum Öffnen des gültigen Ports](cs_ingress.html#opening_ingress_ports) und geben Sie den Port dann in dieser Annotation an. Verwenden Sie die Annotation `custom-port` nicht, um einen Port für die gegenseitige Authentifizierung anzugeben.</li>
</ul>
</dd>

<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
name: myingress
annotations:
  ingress.bluemix.net/mutual-auth: "secretName=&lt;mein_geheimer_schlüssel&gt; port=&lt;port&gt; serviceName=&lt;servicename1&gt;,&lt;servicename2&gt;"
spec:
  tls:
  - hosts:
    - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080
          </code></pre>

<table>
<caption>Erklärung der Komponenten von Annotationen</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
</thead>
<tbody>
<tr>
<td><code>secretName</code></td>
<td>Ersetzen Sie <code>&lt;<em>mein_geheimer_schlüssel</em>&gt;</code> durch einen Namen für die Ressource mit dem geheimen Schlüssel.</td>
</tr>
<tr>
<td><code>port</code></td>
<td>Ersetzen Sie <code>&lt;<em>port</em>&gt;</code> durch die ALB-Portnummer.</td>
</tr>
<tr>
<td><code>serviceName</code></td>
<td>Ersetzen Sie <code>&lt;<em>servicename</em>&gt;</code> durch den Namen mindestens einer Ingress-Ressource. Dieser Parameter ist optional.</td>
</tr>
</tbody></table>

</dd>
</dl>

**Gehen Sie wie folgt vor, um einen geheimen Schlüssel für die gegenseitige Authentifizierung zu erstellen:**

1. Generieren Sie einen Schlüssel und ein Zertifikat auf eine der folgenden Arten:
    * Generieren Sie ein Zertifikat und einen Schlüssel der Zertifizierungsstelle über Ihren Zertifikatsanbieter. Wenn Sie über eine eigene Domäne verfügen, kaufen Sie ein offizielles TLS-Zertifikat für Ihre Domäne. Stellen Sie sicher, dass der [allgemeine Name (CN, Common Name) ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://support.dnsimple.com/articles/what-is-common-name/) für jedes Zertifikat anders ist.
    * Zu Testzwecken können Sie ein selbst signiertes Zertifikat mit OpenSSL erstellen. Weitere Informationen erhalten Sie in diesem [Lernprogramm zu selbst signierten SSL-Zertifikaten ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.akadia.com/services/ssh_test_certificate.html).
        1. Erstellen Sie einen Schlüssel (`client.key`).
            ```
            openssl genrsa -out client.key 1024
            ```
            {: pre}
        2. Verwenden Sie den Schlüssel zum Erstellen eines Zertifikats (`client.crt`).
            ```
            openssl req -new -x509 -key client.key -out client.crt
            ```
            {: pre}
        3. Verwenden Sie das Zertifikat `client.crt`, um ein selbst signiertes Zertifikat zu erstellen.
            ```
            openssl x509 -req -in example.org.csr -CA client.crt -CAkey client.key -CAcreateserial -out example.org.crt
            ```
            {: pre}
2. [Konvertieren Sie das Zertifikat in Base-64 ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.base64encode.org/).
3. Erstellen Sie anhand des Zertifikats eine YAML-Datei für geheime Schlüssel.
     ```
     apiVersion: v1
     kind: Secret
     metadata:
       name: ssl-my-test
     type: Opaque
     data:
       client.crt: <zertifikat_der_zertifizierungsstelle>
     ```
     {: codeblock}
4. Erstellen Sie das Zertifikat als einen geheimen Kubernetes-Schlüssel.
     ```
     kubectl create -f ssl-my-test
     ```
     {: pre}

<br />



### Unterstützung für SSL-Services (ssl-services)
{: #ssl-services}

Lassen Sie HTTPS-Anforderungen zu und verschlüsseln Sie Datenverkehr zu Ihren Upstream-Apps.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>
Wenn Ihre Ingress-Ressourcenkonfiguration über einen TLS-Abschnitt verfügt, kann die Ingress-ALB mit HTTPS gesicherte URL-Anforderungen an Ihre App verarbeiten. Standardmäßig beendet die ALB die TLS-Terminierung und entschlüsselt die Anforderung, bevor der Datenverkehr an Ihre Apps mithilfe des HTTP-Protokolls weitergeleitet wird. Wenn Sie über Apps verfügen, die das HTTPS-Protokoll benötigen und für die der Datenverkehr verschlüsselt sein muss, verwenden Sie die Annotation `ssl-services`. Mit der Annotation `ssl-services` beendet die ALB die externe TLS-Verbindung und erstellt dann eine neue SSL-Verbindung zwischen der ALB und dem App-Pod. Der Datenverkehr wird erneut verschlüsselt, bevor er an die Upstream-Pods gesendet wird.</br></br>
Wenn Ihre Back-End-App TLS verarbeiten kann und Sie weitere Sicherheitsfunktionalität hinzufügen möchten, können Sie eine unidirektionale oder gegenseitige Authentifizierung hinzufügen, indem Sie ein Zertifikat bereitstellen, das in einem geheimen Schlüssel enthalten ist.</br></br>
Verwenden Sie die Annotation `ssl-services` für die SSL-Terminierung zwischen der Ingress-Lastausgleichsfunktion für Anwendungen und der Back-End-App. Verwenden Sie die [Annotation `mutual-auth`](#mutual-auth) für die SSL-Terminierung zwischen dem Client und der Ingress-Lastausgleichsfunktion für Anwendungen. </dd>

<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: &lt;mein_ingress-name&gt;
  annotations:
    ingress.bluemix.net/ssl-services: |
      ssl-service=&lt;mein_service1&gt; ssl-secret=&lt;geheimer_ssl-schlüssel_für_service1&gt;;
      ssl-service=&lt;mein_service2&gt; ssl-secret=&lt;geheimer_ssl-schlüssel_für_service2&gt;
spec:
  tls:
  - hosts:
    - meine_domäne
    secretName: mein_geheimer_schlüssel
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: /service1_path
        backend:
          serviceName: mein_service1
          servicePort: 8443
      - path: /service2_path
        backend:
          serviceName: mein_service2
          servicePort: 8444
          </code></pre>

<table>
<caption>Erklärung der Komponenten von Annotationen</caption>
  <thead>
  <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
  </thead>
  <tbody>
  <tr>
  <td><code>ssl-service</code></td>
  <td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen des Service, der HTTPS erfordert. Der Datenverkehr wird von der Lastausgleichsfunktion für Anwendungen (ALB) zu diesem App-Service verschlüsselt.</td>
  </tr>
  <tr>
  <td><code>ssl-secret</code></td>
  <td>Wenn Ihre Back-End-App TLS verarbeiten kann und Sie weitere Sicherheitsfunktionalität hinzufügen möchten, ersetzen Sie <code>&lt;<em>service-ssl-secret</em>&gt;</code> durch den geheimen Schlüssel mit unidirektionaler oder gegenseitiger Authentifizierung für den Service.<ul><li>Wenn Sie einen geheimen Schlüssel mit unidirektionaler Authentifizierung bereitstellen, muss er <code>trusted.crt</code> vom Upstream-Server enthalten. Informationen zum Erstellen eines unidirektionalen geheimen Schlüssels finden Sie in den Schritten am Ende dieses Abschnitts.</li><li>Wenn Sie einen geheimen Schlüssel mit gegenseitiger Authentifizierung bereitstellen, muss der Wert die erforderlichen Angaben für <code>client.crt</code> und <code>client.key</code> enthalten, die Ihre App vom Client erwartet. Informationen zum Erstellen eines geheimen Schlüssels für gegenseitige Authentifizierung finden Sie in den Schritten am Ende dieses Abschnitts.</li></ul><p class="important">Wenn Sie keinen geheimen Schlüssel angeben, sind unsichere Verbindungen zulässig. Sie können auf den geheimen Schlüssel verzichten, wenn Sie die Verbindung testen möchten und keine Zertifikate vorliegen oder wenn Ihre Zertifikate abgelaufen sind und Sie unsichere Verbindungen zulassen möchten.</p></td>
  </tr>
  </tbody></table>

  </dd>
  </dl>

**Gehen Sie wie folgt vor, um einen geheimen Schlüssel für eine unidirektionale Authentifizierung zu erstellen:**

1. Rufen Sie die das Zertifikat und den Schlüssel der Zertifizierungsstelle über den Upstream-Server ab.
2. [Konvertieren Sie das Zertifikat in Base-64 ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.base64encode.org/).
3. Erstellen Sie anhand des Zertifikats eine YAML-Datei für geheime Schlüssel.
     ```
     apiVersion: v1
     kind: Secret
     metadata:
       name: ssl-my-test
     type: Opaque
     data:
       trusted.crt: <zertifikat_der_zertifizierungsstelle>
     ```
     {: codeblock}

     Wenn Sie die gegenseitige Authentifizierung auch für den Upstream-Datenverkehr erzwingen möchten, können Sie neben dem Wert für `trusted.crt` im Datenabschnitt auch Werte für `client.crt` und `client.key` bereitstellen.
     {: tip}

4. Erstellen Sie das Zertifikat als einen geheimen Kubernetes-Schlüssel.
     ```
     kubectl create -f ssl-my-test
     ```
     {: pre}

</br>
**Gehen Sie wie folgt vor, um einen geheimen Schlüssel für die gegenseitige Authentifizierung zu erstellen:**

1. Generieren Sie einen Schlüssel und ein Zertifikat auf eine der folgenden Arten:
    * Generieren Sie ein Zertifikat und einen Schlüssel der Zertifizierungsstelle über Ihren Zertifikatsanbieter. Wenn Sie über eine eigene Domäne verfügen, kaufen Sie ein offizielles TLS-Zertifikat für Ihre Domäne. Stellen Sie sicher, dass der [allgemeine Name (CN, Common Name) ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://support.dnsimple.com/articles/what-is-common-name/) für jedes Zertifikat anders ist.
    * Zu Testzwecken können Sie ein selbst signiertes Zertifikat mit OpenSSL erstellen. Weitere Informationen erhalten Sie in diesem [Lernprogramm zu selbst signierten SSL-Zertifikaten ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.akadia.com/services/ssh_test_certificate.html).
        1. Erstellen Sie einen Schlüssel (`client.key`).
            ```
            openssl genrsa -out client.key 1024
            ```
            {: pre}
        2. Verwenden Sie den Schlüssel zum Erstellen eines Zertifikats (`client.crt`).
            ```
            openssl req -new -x509 -key client.key -out client.crt
            ```
            {: pre}
        3. Verwenden Sie das Zertifikat `client.crt`, um ein selbst signiertes Zertifikat zu erstellen.
            ```
            openssl x509 -req -in example.org.csr -CA client.crt -CAkey client.key -CAcreateserial -out example.org.crt
            ```
            {: pre}
2. [Konvertieren Sie das Zertifikat in Base-64 ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.base64encode.org/).
3. Erstellen Sie anhand des Zertifikats eine YAML-Datei für geheime Schlüssel.
     ```
     apiVersion: v1
     kind: Secret
     metadata:
       name: ssl-my-test
     type: Opaque
     data:
       client.crt: <zertifikat_der_zertifizierungsstelle>
     ```
     {: codeblock}
4. Erstellen Sie das Zertifikat als einen geheimen Kubernetes-Schlüssel.
     ```
     kubectl create -f ssl-my-test
     ```
     {: pre}

<br />


## Istio-Annotationen
{: #istio-annotations}

Istio-Annotationen verwenden, um eingehenden Datenverkehr an Istio-verwaltete Services weiterzuleiten. 
{: shortdesc}

### Istio-Services (istio-services)
{: #istio-services}

Datenverkehr an Istio-verwaltete Services weiterleiten.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>
<p class="note">Diese Annotation kann nur mit Istio 0.7 und früheren Versionen verwendet werden.</p>Wenn Sie über Istio-verwaltete Services verfügen, können Sie eine Cluster-ALB verwenden, um HTTP-/HTTPS-Anforderungen an den Istio-Ingress-Controller weiterzuleiten. Der Istio-Ingress-Controller leitet die Anforderungen dann weiter an die App-Services. Damit der Datenverkehr weitergeleitet werden kann, müssen Sie Änderungen an den Ingress-Ressourcen für die Cluster-ALB und den Istio-Ingress-Controller vornehmen.
<br><br>In der Ingress-Ressource für die Cluster-ALB müssen Sie Folgendes tun:
  <ul>
    <li>die Annotation `istio-services` angeben</li>
    <li>den Servicepfad als tatsächlichen Pfad definieren, den die App überwacht</li>
    <li>den Service-Port als Port des Istio-Ingress-Controllers angeben</li>
  </ul>
<br>In der Ingress-Ressource für den Istio-Ingress-Controller müssen Sie Folgendes tun:
  <ul>
    <li>den Servicepfad als tatsächlichen Pfad definieren, den die App überwacht</li>
    <li>den Service-Port als den HTTP-/HTTPS-Port des App-Service definieren, der vom Istio-Ingress-Controller öffentlich zugänglich gemacht wird</li>
</ul>
</dd>

<dt>YAML-Beispiel einer Ingress-Ressource für die Cluster-ALB</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/istio-services: "enable=true serviceName=&lt;mein_service1&gt; istioServiceNamespace=&lt;istio-namensbereich&gt; istioServiceName=&lt;istio-ingress-service&gt;"
spec:
  tls:
  - hosts:
    - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: &lt;/myapp1&gt;
          backend:
            serviceName: &lt;mein_service1&gt;
            servicePort: &lt;istio-ingress-port&gt;
      - path: &lt;/myapp2&gt;
          backend:
            serviceName: &lt;mein_service2&gt;
            servicePort: &lt;istio-ingress-port&gt;</code></pre>

<table>
<caption>Erklärung der Komponenten der YAML-Datei</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der YAML-Dateikomponenten</th>
</thead>
<tbody>
<tr>
<td><code>enable</code></td>
  <td>Um das Weiterleiten von Datenverkehr zu Istio-verwalteten Services zu aktivieren, legen Sie diesen Parameter auf <code>True</code> fest.</td>
</tr>
<tr>
<td><code>serviceName</code></td>
<td>Ersetzen Sie <code><em>&lt;mein_service1&gt;</em></code> durch den Namen des Kubernetes-Service, den Sie für Ihre Istio-verwaltete App erstellt haben. Trennen Sie mehrere Services durch ein Semikolon (;). Dieses Feld ist optional. Wenn Sie keinen Servicenamen angeben, werden alle Istio-verwalteten Services für die Weiterleitung von Datenverkehr aktiviert.</td>
</tr>
<tr>
<td><code>istioServiceNamespace</code></td>
<td>Ersetzen Sie <code><em>&lt;istio-namensbereich&gt;</em></code> durch den Kubernetes-Namensbereich, in dem Istio installiert ist. Dieses Feld ist optional. Wenn Sie keinen Namensbereich angeben, wird der Namensbereich <code>istio-system</code> verwendet.</td>
</tr>
<tr>
<td><code>istioServiceName</code></td>
<td>Ersetzen Sie <code><em>&lt;istio-ingress-service&gt;</em></code> durch den Namen des Istio-Ingress-Service. Dieses Feld ist optional. Wenn Sie den Istio-Ingress-Servicenamen nicht angeben, wird der Servicename <code>istio-ingress</code> verwendet.</td>
</tr>
<tr>
<td><code>path</code></td>
  <td>Ersetzen Sie für jeden Istio-verwalteten Service, an den Sie Datenverkehr weiterleiten möchten, <code><em>&lt;/myapp1&gt;</em></code> durch den Back-End-Pfad, den der Istio-verwaltete Service überwacht. Der Pfad muss dem Pfad entsprechen, den Sie in der Istio-Ingress-Ressource definiert haben.</td>
</tr>
<tr>
<td><code>servicePort</code></td>
<td>Ersetzen Sie für jeden Istio-verwalteten Service, an den Sie Datenverkehr weiterleiten möchten, <code><em>&lt;istio-ingress-port&gt;</em></code> durch den Port des Istio-Ingress-Controllers.</td>
</tr>
</tbody></table>
</dd>

<dt>Syntax</dt></dl>

1. Stellen Sie Ihre App bereit. Die in diesen Schritten bereitgestellten Beispielressourcen verwenden die Istio-Beispielapp [BookInfo ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://archive.istio.io/v0.7/docs/guides/bookinfo.html), die sich im Repository `istio-0.7.1/samples/bookinfo/kube` befindet.
   ```
   kubectl apply -f bookinfo.yaml -n istio-system
   ```
   {: pre}

2. Richten Sie Istio-Routing-Regeln für die App ein. In der Istio-Beispielapp namens BookInfo sind beispielsweise [Routing-Regeln für die einzelnen Mikroservices ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://archive.istio.io/v0.7/docs/tasks/traffic-management/request-routing.html) in der Datei `route-rule-all-v1.yaml` definiert.

3. Stellen Sie die App für den Istio Ingress-Controller durch das Erstellen einer Istio Ingress-Ressource bereit. Die Ressource ermöglicht die Anwendung von Istio-Funktionen, wie z. B. Überwachungs- und Routenregeln, auf den Datenverkehr, der in den Cluster eindringt.
    Die folgende Ressource für die App 'BookInfo' ist beispielsweise in der Datei `bookinfo.yaml` vordefiniert:
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

4. Erstellen Sie die Istio Ingress-Ressource.
    ```
    kubectl create -f istio-ingress-resource.yaml -n istio-system
    ```
    {: pre}
    Die App ist mit dem Istio Ingress-Controller verbunden.

5. Rufen Sie die IBM **Ingress-Unterdomäne** und den **geheimen Ingress-Schlüssel** für Ihren Cluster ab. Die Unterdomäne und der geheime Schlüssel werden für Ihren Cluster vorab registriert und als eindeutige öffentliche URL für Ihr App verwendet.
    ```
    ibmcloud ks cluster-get <clustername_oder_-id>
    ```
    {: pre}

6. Verbinden Sie den Istio Ingress-Controller mit der IBM Ingress-ALB für Ihren Cluster, indem Sie eine IBM Ingress-Ressource erstellen.
    Beispiel für die App 'BookInfo':
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

7. Erstellen Sie die IBM Ingress-Ressource für die ALB.
    ```
    kubectl apply -f ibm-ingress-resource.yaml -n istio-system
    ```
    {: pre}

8. Wechseln Sie in einem Browser zu `https://<hostname>/frontend`, um die Webseite der Anwendung anzuzeigen.

<br />


## Annotationen für Proxypuffer
{: #proxy-buffer}

Die Ingress-Lastausgleichsfunktion für Anwendungen (Ingress-ALB) fungiert als Proxy zwischen Ihrer Back-End-App und dem Client-Web-Browser. Mit Annotationen für Proxypuffer können Sie konfigurieren, wie Daten in Ihrer ALB beim Senden oder Empfangen von Datenpaketen gepuffert werden.  
{: shortdesc}

### Pufferung von Clientantwortdaten (proxy-buffering)
{: #proxy-buffering}

Verwenden Sie die 'buffer'-Annotation, um das Speichern von Antwortdaten in der Lastausgleichsfunktion für Anwendungen (ALB) während des Sendens von Daten an den Client zu inaktivieren.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>Die Ingress-Lastausgleichsfunktion für Anwendungen (Ingress-ALB) fungiert als Proxy zwischen Ihrer Back-End-App und dem Client-Web-Browser. Wenn eine Antwort von der Back-End-App an den Client gesendet wird, werden die Antwortdaten standardmäßig in der Lastausgleichsfunktion für Anwendungen (ALB) gepuffert. Die Lastausgleichsfunktion für Anwendungen (ALB) verarbeitet die Clientantwort als Proxy und beginnt mit dem Senden der Antwort an den Client (in der Geschwindigkeit des Clients). Nachdem alle Daten aus der Back-End-App von der Lastausgleichsfunktion für Anwendungen (ALB) empfangen wurden, wird die Verbindung zur Back-End-App gekappt. Die Verbindung von der Lastausgleichsfunktion für Anwendungen (ALB) zum Client bleibt geöffnet, bis der Client alle Daten empfangen hat.

</br></br>
Wenn die Pufferung von Antwortdaten auf der ALB inaktiviert ist, werden Daten sofort von der ALB an den Client gesendet. Der Client muss eingehende Daten in der Geschwindigkeit der Lastausgleichsfunktion für Anwendungen (ALB) verarbeiten können. Falls der Client zu langsam ist, gehen unter Umständen Daten verloren.
</br></br>
Die Pufferung von Antwortdaten auf der ALB ist standardmäßig aktiviert.</dd>
<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: myingress
 annotations:
   ingress.bluemix.net/proxy-buffering: "enabled=&lt;false&gt; serviceName=&lt;mein_service1&gt;"
spec:
 tls:
 - hosts:
   - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
 - host: meine_domäne
   http:
     paths:
     - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080</code></pre>

<table>
<caption>Erklärung der Komponenten von Annotationen</caption>
 <thead>
 <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
 </thead>
 <tbody>
 <tr>
 <td><code>enabled</code></td>
   <td>Um die Pufferung von Antwortdaten für die Lastausgleichsfunktion für Anwendungen (ALB) zu inaktivieren, setzen Sie diesen Wert auf <code>false</code>.</td>
 </tr>
 <tr>
 <td><code>serviceName</code></td>
 <td>Ersetzen Sie <code><em>&lt;mein_service1&gt;</em></code> durch den Namen des Kubernetes-Service, den Sie für Ihre App erstellt haben. Trennen Sie mehrere Services durch ein Semikolon (;). Dieses Feld ist optional. Wenn Sie keinen Servicenamen angeben, verwenden alle Services diese Annotation.</td>
 </tr>
 </tbody></table>
 </dd>
 </dl>

<br />



### Proxypuffer (proxy-buffers)
{: #proxy-buffers}

Konfiguration der Anzahl und Größe der Proxypuffer für die Lastausgleichsfunktion für Anwendungen (ALB).
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>
Legen Sie die Anzahl und Größe der Puffer fest, mit denen eine Antwort für eine einzelne Verbindung von einem Proxy-Server gelesen wird. Die Konfiguration wird auf alle Services auf dem Ingress-Host angewendet, es sei denn, es wird ein Service angegeben. Wenn beispielsweise eine Konfiguration wie <code>serviceName=SERVICE number=2 size=1k</code> angegeben wird, wird '1k' auf den Service angewendet. Wenn eine Konfiguration wie <code>number=2 size=1k</code> angegeben wird, wird '1k' auf alle Services auf dem Ingress-Host angewendet.</br>
<p class="tip">Wenn Sie die Fehlernachricht `upstream sent too big header while reading response header from upstream` erhalten, hat der Upstream-Server in Ihrem Back-End eine Headergröße größer als die Standardbegrenzung gesendet. Erhöhen Sie die Größe für <code>proxy-buffers</code> und [<code>proxy-buffer-size</code>](#proxy-buffer-size).</p>
</dd>
<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>
<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: proxy-ingress
 annotations:
   ingress.bluemix.net/proxy-buffers: "serviceName=&lt;mein_service&gt; number=&lt;anzahl_puffer&gt; size=&lt;größe&gt;"
spec:
 tls:
 - hosts:
   - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
 - host: meine_domäne
   http:
     paths:
     - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080</code></pre>

<table>
<caption>Erklärung der Komponenten von Annotationen</caption>
 <thead>
 <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
 </thead>
 <tbody>
 <tr>
 <td><code>serviceName</code></td>
 <td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen eines Service, der 'proxy-buffers' anwenden soll.</td>
 </tr>
 <tr>
 <td><code>number</code></td>
 <td>Ersetzen Sie <code>&lt;<em>anzahl_puffer</em>&gt;</code> durch eine Zahl. Beispiel: <em>2</em>.</td>
 </tr>
 <tr>
 <td><code>size</code></td>
 <td>Ersetzen Sie <code>&lt;<em>größe</em>&gt;</code> durch die Größe der einzelnen Puffer in Kilobyte (k oder K). Beispiel: <em>1K</em>.</td>
 </tr>
 </tbody>
 </table>
 </dd></dl>

<br />


### Puffergröße des Proxys (proxy-buffer-size)
{: #proxy-buffer-size}

Konfiguration der Größe des Proxypuffers, der den ersten Teil der Antwort liest.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>
Legen Sie die Größe des Puffers fest, mit dem der erste Teil der Antwort gelesen wird, die vom Proxy-Server empfangen wird. Dieser Teil der Antwort enthält normalerweise einen kleinen Antwortheader. Die Konfiguration wird auf alle Services auf dem Ingress-Host angewendet, es sei denn, es wird ein Service angegeben. Wenn beispielsweise eine Konfiguration wie <code>serviceName=SERVICE size=1k</code> angegeben wird, wird '1k' auf den Service angewendet. Wenn eine Konfiguration wie <code>size=1k</code> angegeben wird, wird '1k' auf alle Services auf dem Ingress-Host angewendet.
</dd>


<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: proxy-ingress
 annotations:
   ingress.bluemix.net/proxy-buffer-size: "serviceName=&lt;mein_service&gt; size=&lt;größe&gt;"
spec:
 tls:
 - hosts:
   - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
 - host: meine_domäne
   http:
     paths:
     - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080
 </code></pre>

<table>
<caption>Erklärung der Komponenten von Annotationen</caption>
 <thead>
 <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
 </thead>
 <tbody>
 <tr>
 <td><code>serviceName</code></td>
 <td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen eines Service, der 'proxy-buffers-size' anwenden soll.</td>
 </tr>
 <tr>
 <td><code>size</code></td>
 <td>Ersetzen Sie <code>&lt;<em>größe</em>&gt;</code> durch die Größe der einzelnen Puffer in Kilobyte (k oder K). Beispiel: <em>1K</em>.</td>
 </tr>
 </tbody></table>

 </dd>
 </dl>

<br />



### Größe belegter Puffer des Proxys (proxy-busy-buffers-size)
{: #proxy-busy-buffers-size}

Konfiguration der Größe für Proxy-Puffer, die belegt sein können.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>
Begrenzen Sie die Größe aller Puffer, die eine Antwort an den Client senden, während die Antwort noch nicht vollständig gelesen wurde. In der Zwischenzeit können die verbleibenden Puffer die Antwort lesen und bei Bedarf einen Teil der Antwort in einer temporären Datei puffern. Die Konfiguration wird auf alle Services auf dem Ingress-Host angewendet, es sei denn, es wird ein Service angegeben. Wenn beispielsweise eine Konfiguration wie <code>serviceName=SERVICE size=1k</code> angegeben wird, wird '1k' auf den Service angewendet. Wenn eine Konfiguration wie <code>size=1k</code> angegeben wird, wird '1k' auf alle Services auf dem Ingress-Host angewendet.
</dd>


<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: proxy-ingress
 annotations:
   ingress.bluemix.net/proxy-busy-buffers-size: "serviceName=&lt;mein_service&gt; size=&lt;größe&gt;"
spec:
 tls:
 - hosts:
   - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
 - host: meine_domäne
   http:
     paths:
     - path: /
       backend:
         serviceName: mein_service
         servicePort: 8080
         </code></pre>

<table>
<caption>Erklärung der Komponenten von Annotationen</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
</thead>
<tbody>
<tr>
<td><code>serviceName</code></td>
<td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen eines Service, der 'proxy-busy-buffers-size' anwenden soll.</td>
</tr>
<tr>
<td><code>size</code></td>
<td>Ersetzen Sie <code>&lt;<em>größe</em>&gt;</code> durch die Größe der einzelnen Puffer in Kilobyte (k oder K). Beispiel: <em>1K</em>.</td>
</tr>
</tbody></table>

 </dd>
 </dl>

<br />



## Annotationen für Anforderungen und Antworten
{: #request-response}

Anforderungs- und Antwortannotationen verwenden, um Headerinformationen zu Client- und Serveranforderungen hinzuzufügen oder daraus zu entfernen und um die Größe des Hauptteils zu ändern, den der Client senden kann. 
{: shortdesc}

### Server-Port zum Host-Header hinzufügen (add-host-port)
{: #add-host-port}

Server-Port zur Clientanforderung hinzufügen, bevor die Anforderung an Ihre Back-End-App weitergeleitet wird. 
{: shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>`:server_port` zum Host-Header einer Clientanforderung hinzufügen, bevor Sie die Anforderung an Ihre Back-End-App weiterleiten.

<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: myingress
 annotations:
   ingress.bluemix.net/add-host-port: "enabled=&lt;true&gt; serviceName=&lt;mein_service&gt;"
spec:
 tls:
 - hosts:
   - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
 - host: meine_domäne
   http:
     paths:
     - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080</code></pre>

<table>
<caption>Erklärung der Komponenten von Annotationen</caption>
 <thead>
 <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
 </thead>
 <tbody>
 <tr>
 <td><code>enabled</code></td>
   <td>Wenn Sie die Einstellung von 'server_port' für den Host aktivieren möchten, setzen Sie die Einstellung auf <code>true</code>.</td>
 </tr>
 <tr>
 <td><code>serviceName</code></td>
 <td>Ersetzen Sie <code><em>&lt;mein_service&gt;</em></code> durch den Namen des Kubernetes-Service, den Sie für Ihre App erstellt haben. Trennen Sie mehrere Services durch ein Semikolon (;). Dieses Feld ist optional. Wenn Sie keinen Servicenamen angeben, verwenden alle Services diese Annotation.</td>
 </tr>
 </tbody></table>
 </dd>
 </dl>

<br />


### Zusätzlicher Clientanforderungs- oder Clientantwortheader (proxy-add-headers, response-add-headers)
{: #proxy-add-headers}

Hinzufügen von zusätzlichen Headerinformationen zu einer Clientanforderung, bevor die Anforderung an die Back-End-App gesendet wird, bzw. zu einer Clientantwort, bevor die Antwort an den Client gesendet wird.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>Die Ingress-Lastausgleichsfunktion für Anwendungen (Ingress-ALB) fungiert als Proxy zwischen der Client-App und Ihrer Back-End-App. Clientanforderungen, die an die Lastausgleichsfunktion für Anwendungen (ALB) gesendet werden, werden (als Proxy) verarbeitet und in eine neue Anforderung umgesetzt, die anschließend an Ihre Back-End-App gesendet wird. In ähnlicher Weise werden die an die ALB gesendeten Back-End-App-Antworten verarbeitet (als Proxy) und in eine neue Antwort gestellt, die dann an den Client gesendet wird. Beim Senden einer Anforderung als Proxy oder Antwort werden HTTP-Headerinformationen entfernt, z. B. der Benutzername, der ursprünglich vom Client oder der Back-End-App gesendet wurde.
<br><br>
Wenn Ihre Back-End-App HTTP-Headerinformationen erfordert, können Sie die Annotation <code>proxy-add-headers</code> verwenden, um Headerinformationen zur Clientanforderung hinzuzufügen, bevor die Anforderung von der ALB an die Back-End-App weitergeleitet wird. Wenn die Client-Web-App HTTP-Headerinformationen erfordert, können Sie die Annotation <code>response-add-headers</code> verwenden, um Headerinformationen zur Antwort hinzuzufügen, bevor die  Antwort von der ALB an die Client-Web-App weitergeleitet wird.<br>

<ul><li>Sie müssen möglicherweise die folgenden X-Forward-Headerinformationen zur Anforderung hinzufügen, bevor sie an Ihre App weitergeleitet wird.
<pre class="screen">
<code>proxy_set_header Host $host;
proxy_set_header X-Real-IP $remote_addr;
proxy_set_header X-Forwarded-Proto $scheme;
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;</code></pre>
Verwenden Sie die Annotation `proxy-add-headers` wie folgt, um die X-Forward-Headerinformationen der Anforderung hinzuzufügen, die an Ihre App gesendet wurde:
<pre class="screen">
<code>ingress.bluemix.net/proxy-add-headers: |
  serviceName=&lt;mein_service1&gt; {
  Host $host;
  X-Real-IP $remote_addr;
  X-Forwarded-Proto $scheme;
  X-Forwarded-For $proxy_add_x_forwarded_for;
  }</code></pre>
</li></ul>
</br>
<p class="tip">Die Annotation <code>response-add-headers</code> unterstützt keine globalen Header für alle Services. Um einen Header für alle Serviceantworten auf Serverebene hinzuzufügen, können Sie die [Annotation <code>server-snippets</code>](#server-snippets) verwenden.</p>
</dd>

<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/proxy-add-headers: |
      serviceName=&lt;mein_service1&gt; {
      &lt;header1&gt; &lt;wert1&gt;;
      &lt;header2&gt; &lt;wert2&gt;;
      }
      serviceName=&lt;mein_service2&gt; {
      &lt;header3&gt; &lt;wert3&gt;;
      }
    ingress.bluemix.net/response-add-headers: |
      serviceName=&lt;mein_service1&gt; {
      &lt;header1&gt;: &lt;wert1&gt;;
      &lt;header2&gt;: &lt;wert2&gt;;
      }
      serviceName=&lt;mein_service2&gt; {
      &lt;header3&gt;: &lt;wert3&gt;;
      }
spec:
  tls:
  - hosts:
    - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: /service1_path
        backend:
          serviceName: &lt;mein_service1&gt;
          servicePort: 8080
      - path: /service2_path
        backend:
          serviceName: &lt;mein_service2&gt;
          servicePort: 80</code></pre>

 <table>
 <caption>Erklärung der Komponenten von Annotationen</caption>
  <thead>
  <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
  </thead>
  <tbody>
  <tr>
  <td><code>serviceName</code></td>
  <td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen des Kubernetes-Service, den Sie für Ihre App erstellt haben.</td>
  </tr>
  <tr>
  <td><code>&lt;header&gt;</code></td>
  <td>Der Schlüssel der Headerinformationen, die der Clientanforderung bzw. der Clientantwort hinzugefügt werden sollen.</td>
  </tr>
  <tr>
  <td><code>&lt;wert&gt;</code></td>
  <td>Der Wert der Headerinformationen, die der Clientanforderung bzw. der Clientantwort hinzugefügt werden sollen.</td>
  </tr>
  </tbody></table>
 </dd></dl>

<br />



### Entfernen des Clientantwortheaders (response-remove-headers)
{: #response-remove-headers}

Entfernen von Headerinformationen, die in der Clientantwort von der Back-End-App eingeschlossen sind, bevor die Antwort an den Client gesendet wird.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>Die Ingress-Lastausgleichsfunktion für Anwendungen (Ingress-ALB) fungiert als Proxy zwischen Ihrer Back-End-App und dem Client-Web-Browser. Clientantworten von der Back-End-App, die an die Lastausgleichsfunktion für Anwendungen (ALB) gesendet werden, werden (als Proxy) verarbeitet und in eine neue Antwort umgesetzt, die anschließend von der Lastausgleichsfunktion für Anwendungen (ALB) an Ihren Client-Web-Browser gesendet wird. Auch wenn beim Senden einer Antwort als Proxy die HTTP-Headerinformationen entfernt werden, die ursprünglich von der Back-End-App gesendet wurden, entfernt dieser Prozess möglicherweise nicht alle Back-End-App-spezifischen Header. Entfernen Sie Headerinformationen aus einer Clientantwort, bevor die Antwort von der Lastausgleichsfunktion für Anwendungen (ALB) an den Client-Web-Browser weitergeleitet wird.</dd>
<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>
<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/response-remove-headers: |
      serviceName=&lt;mein_service1&gt; {
      "&lt;header1&gt;";
      "&lt;header2&gt;";
      }
      serviceName=&lt;mein_service2&gt; {
      "&lt;header3&gt;";
      }
spec:
  tls:
  - hosts:
    - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: /service1_path
        backend:
          serviceName: &lt;mein_service1&gt;
          servicePort: 8080
      - path: /service2_path
        backend:
          serviceName: &lt;mein_service2&gt;
          servicePort: 80</code></pre>

<table>
<caption>Erklärung der Komponenten von Annotationen</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
</thead>
<tbody>
<tr>
<td><code>serviceName</code></td>
<td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen des Kubernetes-Service, den Sie für Ihre App erstellt haben.</td>
</tr>
<tr>
<td><code>&lt;header&gt;</code></td>
<td>Der Schlüssel des Headers, der aus der Clientantwort entfernt werden soll.</td>
</tr>
</tbody></table>
</dd></dl>

<br />


### Größe des Hauptteils der Clientanforderung (client-max-body-size)
{: #client-max-body-size}

Die maximale Größe des Hauptteils anpassen, den der Client als Teil der Anforderung senden kann.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>Um die erwartete Leistung beizubehalten, ist die maximale Größe des Clientanforderungshauptteils auf 1 Megabyte festgelegt. Wenn eine Clientanforderung mit einer das Limit überschreitenden Größe des Hauptteils an die Ingress-Lastausgleichsfunktion für Anwendungen (Ingress-ALB) gesendet wird und der Client das Unterteilen von Daten nicht zulässt, gibt die Lastausgleichsfunktion für Anwendungen (ALB) die HTTP-Antwort 413 (Anforderungsentität zu groß) an den Client zurück. Eine Verbindung zwischen dem Client und der Lastausgleichsfunktion für Anwendungen (ALB) ist erst möglich, wenn der Anforderungshauptteil verkleinert wird. Wenn der Client das Unterteilen in mehrere Blöcke zulässt, werden die Daten in Pakete von 1 Megabyte aufgeteilt und an die Lastausgleichsfunktion für Anwendungen (ALB) gesendet.

</br></br>
Wenn Sie Clientanforderungen mit einer Hauptteilgröße über 1 Megabyte erwarten, können Sie die maximale Größe des Hauptteils erhöhen. Beispiel: Sie möchten, dass Ihr Client große Dateien hochladen kann. Das Erhöhen der maximalen Größe des Anforderungshauptteils kann sich negativ auf die Leistung Ihrer Lastausgleichsfunktion für Anwendungen (ALB) auswirken, weil die Verbindung mit dem Client geöffnet bleiben muss, bis die Anforderung empfangen wird.
</br></br>
<p class="note">Einige Client-Web-Browser können die HTTP-Antwortnachricht 413 nicht ordnungsgemäß anzeigen.</p></dd>
<dt>YAML-Beispiel einer Ingress-Ressource</dt>
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
   - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
 - host: meine_domäne
   http:
     paths:
     - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080</code></pre>

<table>
<caption>Erklärung der Komponenten von Annotationen</caption>
 <thead>
 <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
 </thead>
 <tbody>
 <tr>
 <td><code>&lt;größe&gt;</code></td>
 <td>Die maximal zulässige Größe des Hauptteils der Clientantwort. Um die maximale Größe beispielsweise auf 200 Megabyte festzulegen, definieren Sie <code>200m</code>. Sie können die Größe auf '0' festlegen, um die Prüfung der Größe des Clientanforderungshauptteils zu inaktivieren.</td>
 </tr>
 </tbody></table>

 </dd></dl>

<br />


### Puffer für große Client-Header (large-client-header-buffers)
{: #large-client-header-buffers}

Die maximale Anzahl und Größe der Puffer festlegen, die große Clientanforderungsheader lesen.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>Puffer, die große Clientanforderungsheader lesen, werden nur nach Bedarf zugeordnet: Wenn eine Verbindung nach der Verarbeitung der Anforderungsendeverarbeitung in den Keepalive-Status übergegangen ist, werden diese Puffer freigegeben. Standardmäßig ist die Puffergröße gleich <code>8K</code> Byte. Wenn eine Anforderungszeile die festgelegte maximale Größe eines Puffers überschreitet, wird der Fehler <code>414 Request-URI Too Large</code> an den Client zurückgegeben. Wenn außerdem ein Anforderungsfeld die festgelegte maximale Größe eines Puffers überschreitet, wird der Fehler <code>400 Bad Request Large</code> an den Client zurückgegeben. Sie können die maximale Anzahl und Größe der Puffer anpassen, die zum Lesen großer Clientanforderungsheader verwendet werden.

<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
 name: myingress
 annotations:
   ingress.bluemix.net/large-client-header-buffers: "number=&lt;anzahl&gt; size=&lt;größe&gt;"
spec:
 tls:
 - hosts:
   - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
 - host: meine_domäne
   http:
     paths:
     - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080</code></pre>

<table>
<caption>Erklärung der Komponenten von Annotationen</caption>
 <thead>
 <th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
 </thead>
 <tbody>
 <tr>
 <td><code>&lt;anzahl&gt;</code></td>
 <td>Die maximale Anzahl an Puffern, die zum Lesen großer Clientanforderungsheader zugeordnet werden sollte. Um beispielsweise 4 Puffer zu verwenden, legen Sie <code>4</code> fest.</td>
 </tr>
 <tr>
 <td><code>&lt;größe&gt;</code></td>
 <td>Die maximale Größe der Puffer, die große Clientanforderungsheader lesen. Um beispielsweise 16 Kilobyte zu verwenden, definieren Sie <code>16k</code>. Die Größe muss mit einem <code>k</code> für Kilobyte oder <code>m</code> für Megabyte enden.</td>
 </tr>
</tbody></table>
</dd>
</dl>

<br />


## Annotationen für Servicegrenzwerte
{: #service-limit}

Mit Annotationen für Servicegrenzwerte können Sie die Standardverarbeitungsrate von Anforderungen und die Anzahl von Verbindungen ändern, die von einer einzelnen IP-Adresse stammen. 
{: shortdesc}

### Grenzwerte für globale Rate (global-rate-limit)
{: #global-rate-limit}

Begrenzung der Verarbeitungsrate für Anforderungen und Anzahl der Verbindungen anhand eines definierten Schlüssels für alle Services.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>
Begrenzen Sie für alle Services anhand eines definierten Schlüssels die Verarbeitungsrate für Anforderungen und die Anzahl der Verbindungen, die von einer einzelnen IP-Adresse für alle Pfade der ausgewählten Back-End-Systeme kommen.
</dd>


<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/global-rate-limit: "key=&lt;schlüssel&gt; rate=&lt;rate&gt; conn=&lt;anzahl_der_verbindungen&gt;"
spec:
  tls:
  - hosts:
    - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080</code></pre>

<table>
<caption>Erklärung der Komponenten von Annotationen</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
</thead>
<tbody>
<tr>
<td><code>key</code></td>
<td>Um einen globalen Grenzwert für eingehenden Anforderungen basierend auf der Zone des Service festzulegen, verwenden Sie `key=zone`. Um einen globalen Grenzwert für eingehenden Anforderungen basierend auf dem Header festzulegen, verwenden Sie `X-USER-ID key=$http_x_user_id`.</td>
</tr>
<tr>
<td><code>rate</code></td>
<td>Ersetzen Sie <code>&lt;<em>rate</em>&gt;</code> durch die Verarbeitungsrate. Geben Sie einen Wert als Rate pro Sekunde (r/s) oder Rate pro Minute (r/m) an. Beispiel: <code>50r/m</code>.</td>
</tr>
<tr>
<td><code>conn</code></td>
<td>Ersetzen Sie <code>&lt;<em>anzahl_der_verbindungen</em>&gt;</code> durch die Anzahl der Verbindungen.</td>
</tr>
</tbody></table>

</dd>
</dl>

<br />



### Grenzwerte für Servicerate (service-rate-limit)
{: #service-rate-limit}

Begrenzung der Verarbeitungsrate für Anforderungen und Anzahl der Verbindungen für bestimmte Services.
{:shortdesc}

<dl>
<dt>Beschreibung</dt>
<dd>Begrenzen Sie für bestimmte Services die Verarbeitungsrate für Anforderungen und die Anzahl der Verbindungen anhand eines definierten Schlüssels, die von einer einzelnen IP-Adresse für alle Pfade der ausgewählten Back-End-Systeme kommen.
</dd>


<dt>YAML-Beispiel einer Ingress-Ressource</dt>
<dd>

<pre class="codeblock">
<code>apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: myingress
  annotations:
    ingress.bluemix.net/service-rate-limit: "serviceName=&lt;mein_service&gt; key=&lt;schlüssel&gt; rate=&lt;rate&gt; conn=&lt;anzahl_der_verbindungen&gt;"
spec:
  tls:
  - hosts:
    - meine_domäne
    secretName: mein_geheimer_tls-schlüssel
  rules:
  - host: meine_domäne
    http:
      paths:
      - path: /
        backend:
          serviceName: mein_service
          servicePort: 8080</code></pre>

<table>
<caption>Erklärung der Komponenten von Annotationen</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der Komponenten von Annotationen</th>
</thead>
<tbody>
<tr>
<td><code>serviceName</code></td>
<td>Ersetzen Sie <code>&lt;<em>mein_service</em>&gt;</code> durch den Namen des Service, für den Sie die Verarbeitungsrate begrenzen wollen.</li>
</tr>
<tr>
<td><code>key</code></td>
<td>Um einen globalen Grenzwert für eingehenden Anforderungen basierend auf der Zone des Service festzulegen, verwenden Sie `key=zone`. Um einen globalen Grenzwert für eingehenden Anforderungen basierend auf dem Header festzulegen, verwenden Sie `X-USER-ID key=$http_x_user_id`.</td>
</tr>
<tr>
<td><code>rate</code></td>
<td>Ersetzen Sie <code>&lt;<em>rate</em>&gt;</code> durch die Verarbeitungsrate. Um eine Rate pro Sekunde zu definieren, verwenden Sie 'r/s': <code>10r/s</code>. Um eine Rate pro Minute zu definieren, verwenden Sie 'r/m': <code>50r/m</code>.</td>
</tr>
<tr>
<td><code>conn</code></td>
<td>Ersetzen Sie <code>&lt;<em>anzahl_der_verbindungen</em>&gt;</code> durch die Anzahl der Verbindungen.</td>
</tr>
</tbody></table>
</dd>
</dl>

<br />



