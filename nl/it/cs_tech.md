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



# Tecnologia {{site.data.keyword.containerlong_notm}}

Scopri di più sulla tecnologia che sta dietro {{site.data.keyword.containerlong}}.
{:shortdesc}

## Contenitori Docker
{: #docker_containers}

Sviluppato sulla tecnologia dei contenitori Linux (LXC) esistente, il progetto open source denominato Docker ha definito del template relativi a come assemblare software in unità standardizzate, denominate contenitori, che includono tutti gli elementi che occorrono a un'applicazione per l'esecuzione {{site.data.keyword.containerlong_notm}} utilizza `containerd` come il runtime del contenitore per distribuire i contenitori da immagini del contenitore Docker nel tuo cluster.
{:shortdesc}

Ulteriori informazioni sui concetti Docker di base:

<dl>
<dt>Immagine</dt>
<dd>Un'immagine del contenitore è la base per ogni contenitore che vuoi eseguire. Le immagini contenitore vengono sviluppate da un Dockerfile, un file di testo che definisce come creare l'immagine e quali risorse di build includere in essa, come ad esempio l'applicazione, la configurazione dell'applicazione e le relative dipendenze. Le immagini vengono sempre create da altre immagini, rendendole veloci da configurare. Lascia che qualcun altro faccia il grosso del lavoro su un'immagine e perfezionala prima di utilizzarla.</dd>
<dt>Registro</dt>
<dd>Un registro delle immagini è un luogo dove si archiviano, richiamano e condividono immagini contenitore. Le immagini archiviate in un registro possono essere disponibili pubblicamente (registro pubblico)
o essere accessibili da un piccolo gruppo di utenti (registro privato). {{site.data.keyword.containerlong_notm}} offre immagini pubbliche, come ibmliberty, che puoi utilizzare per creare la tua prima applicazione caricata in un contenitore. Quando si tratta di applicazioni aziendali, utilizza un registro privato come quello fornito in {{site.data.keyword.Bluemix_notm}} per proteggere le tue immagini da utilizzi da parte di utenti non autorizzati.
</dd>
<dt>Contenitore</dt>
<dd>Ogni contenitore viene creato da un'immagine. Un contenitore è un'applicazione in pacchetto con tutte le sue dipendenze in modo che l'applicazione possa essere spostata tra gli ambienti ed eseguita senza modifiche. A differenza delle macchine virtuali, i contenitori non virtualizzano un dispositivo, il suo sistema operativo e l'hardware sottostante. Nel contenitore sono impacchettati solo il codice dell'applicazione, il runtime, gli strumenti di sistema, le librerie e le impostazioni. I contenitori sono eseguiti come processi isolati su host di calcolo Ubuntu e condividono il sistema operativo host e le sue risorse hardware. Questo approccio rende un contenitore più leggero, portatile ed efficiente di una macchina virtuale.</dd>
</dl>



### Vantaggi chiave dell'utilizzo di contenitori
{: #container_benefits}

<dl>
<dt>I contenitori sono elementi agile</dt>
<dd>I contenitori semplificano la gestione del sistema, fornendo
ambienti standardizzati alle distribuzioni di sviluppo e produzione. Il runtime leggero consente un ridimensionamento rapido delle distribuzioni. Rimuovi la complessità della gestione di piattaforme di sistemi operativi differenti e le relative infrastrutture sottostanti utilizzando i contenitori che ti aiutano a distribuire ed eseguire una qualsiasi applicazione su qualsiasi infrastruttura in modo rapido e affidabile.</dd>
<dt>I contenitori sono piccoli</dt>
<dd>Puoi sistemare molti contenitori nella stessa quantità di spazio richiesta da una singola macchina virtuale.</dd>
<dt>I contenitori sono portatili</dt>
<dd>
<ul>
  <li>Riutilizza le parti delle immagini per creare i contenitori. </li>
  <li>Sposta velocemente il codice dell'applicazione dall'ambiente in fase di preparazione a quello di produzione.</li>
  <li>Automatizza i tuoi processi con gli strumenti di fornitura continua.</li>
  </ul>
  </dd>

<p>Ulteriori informazioni sulla [protezione delle tue informazioni personali](cs_secure.html#pi) quando utilizzi le immagini del contenitore.</p>

<p>Pronto per approfondire le informazioni su Docker? <a href="https://developer.ibm.com/courses/all/docker-essentials-extend-your-apps-with-containers/" target="_blank">Impara come Docker e {{site.data.keyword.containerlong_notm}} funzionano insieme completando questo corso.</a></p>

</dl>

<br />


## Cluster Kubernetes
{: #kubernetes_basics}

<img src="images/certified-kubernetes-resized.png" style="padding-right: 10px;" align="left" alt="Questo badge indica la certificazione Kubernetes per il servizio IBM Cloud Container."/>Il progetto open source denominato Kubernetes combina l'esecuzione di un'infrastruttura inserita in un contenitore con carichi di lavoro di produzione, contributi open source e strumenti di gestione dei contenitori Docker. L'infrastruttura Kubernetes fornisce una piattaforma applicativa isolata e sicura per la gestione dei contenitori che è portatile, estensibile e con riparazione automatica in caso di failover.
{:shortdesc}

Ulteriori informazioni su alcuni concetti Kubernetes di base sono mostrate nel seguente diagramma.

![Impostazioni di distribuzione](images/cs_app_tutorial_components1.png)

<dl>
<dt>Account</dt>
<dd>L'account fa riferimento al tuo account {{site.data.keyword.Bluemix_notm}}.</dd>

<dt>Cluster</dt>
<dd>Un cluster Kubernetes è formato da uno o più host di calcolo denominati
nodi di lavoro. I nodi di lavoro sono gestiti da un master Kubernetes che controlla e monitora in modo centralizzato tutte le risorse Kubernetes
nel cluster. Per cui quando distribuisci le risorse di un'applicazione inserita in un contenitore, il master Kubernetes decide a quale nodo di lavoro distribuire quelle risorse,
tenendo conto dei requisiti di distribuzione e della capacità disponibile nel cluster. Le risorse Kubernetes includono i servizi, le distribuzioni e i pod.</dd>

<dt>Servizio</dt>
<dd>Un servizio è una risorsa Kubernetes che raggruppa un insieme di pod e fornisce connettività di rete a questi pod senza esporre indirizzo IP privato effettivo di ciascun pod. Puoi utilizzare un servizio per rendere la tua applicazione disponibile nel tuo cluster o pubblicamente su Internet.
</dd>

<dt>Distribuzione</dt>
<dd>Una distribuzione è una risorsa Kubernetes in cui puoi specificare le informazioni sulle altre risorse o sulle funzionalità necessarie per eseguire la tua applicazione,
come i servizi, l'archiviazione persistente o le annotazioni. Dovrai documentare una distribuzione in un file YAML di configurazione e quindi applicarla al cluster. Il master Kubernetes configura le risorse e distribuisce i contenitori nei pod su nodi di lavoro con capacità disponibile.
</br></br>
Definisci le strategie di aggiornamento per la tua applicazione, incluso il numero di pod che vuoi aggiungere durante un aggiornamento continuo e il numero di pod che possono non essere disponibili contemporaneamente. Quando esegui un aggiornamento continuo, la distribuzione controlla se l'aggiornamento funziona e interrompe il rollout quando vengono rilevati errori.</dd>

<dt>Pod</dt>
<dd>Ogni applicazione inserita in un contenitore che viene distribuita in un cluster viene distribuita, eseguita e gestita da una risorsa Kubernetes denominata pod. I pod rappresentano piccole unità distribuibili in un cluster Kubernetes e vengono utilizzati per raggruppare i contenitori che devono essere trattati come una singola unità. Nella maggior parte dei casi, ogni contenitore viene distribuito nel suo pod. Tuttavia, un'applicazione potrebbe richiedere un contenitore e altri contenitori helper per essere distribuita
in un pod, in modo che tali contenitori possano essere indirizzati utilizzando lo stesso indirizzo IP privato.</dd>

<dt>Applicazione</dt>
<dd>Un'applicazione può far riferimento a un'applicazione completa o a un componente di un'applicazione. Potresti distribuire i componenti di un'applicazione in pod o nodi di lavoro separati.</dd>

<p>Ulteriori informazioni sulla [protezione delle tue informazioni personali](cs_secure.html#pi) quando utilizzi le risorse Kubernetes.</p>

<p>Pronto per approfondire le informazioni su Kubernetes?</p>
<ul><li><a href="cs_tutorials.html#cs_cluster_tutorial" target="_blank">Amplia la tua conoscenza della terminologia con l'esercitazione Creazione dei cluster</a>.</li>
<li><a href="https://developer.ibm.com/courses/all/get-started-kubernetes-ibm-cloud-container-service/" target="_blank">Impara come Kubernetes e {{site.data.keyword.containerlong_notm}} funzionano insieme completando questo corso.</a></li></ul>


</dl>

<br />


## Architettura del servizio
{: #architecture}

In un cluster Kubernetes eseguito su {{site.data.keyword.containerlong_notm}}, le tue applicazioni inserite in un contenitore sono ospitate su host di calcolo denominati nodi di lavoro. Per essere più specifici, le applicazioni vengono eseguite nei pod e i pod sono ospitati sui nodi di lavoro. I nodi di lavoro sono gestiti dal master Kubernetes. Il master Kubernetes e i nodi di lavoro comunicano tra loro tramite certificati TLS protetti e una connessione openVPN per orchestrare le configurazioni del tuo cluster.
{: shortdesc}

La seguente immagine mostra i componenti del tuo cluster e il modo in cui interagiscono.
<p>
<figure>
 <img src="images/cs_org_ov.png" alt="{{site.data.keyword.containerlong_notm}} Kubernetes architecture">
 <figcaption>{{site.data.keyword.containerlong_notm}} architecture</figcaption>
</figure>
</p>

Qual è la differenza tra il master Kubernetes e un nodo di lavoro? Grazie di averlo chiesto.

<dl>
  <dt>Master Kubernetes</dt>
    <dd>Il master Kubernetes ha il compito di gestire tutte le risorse di calcolo, rete e archiviazione nel cluster. Il master Kubernetes garantisce che le applicazioni inserite in un contenitore e i servizi siano distribuiti equamente nei nodi di lavoro nel cluster. A seconda del modo in cui configuri l'applicazione e i servizi, il master determina il nodo di lavoro che dispone di risorse sufficienti per soddisfare i requisiti dell'applicazione.</br></br>La seguente tabella descrive i componenti del master Kubernetes.
    <table>
    <caption>Componenti del master Kubernetes</caption>
    <thead>
    <th>Componente master</th>
    <th>Descrizione</th>
    </thead>
    <tbody>
    <tr>
    <td>kube-apiserver</td>
    <td>Il server API Kubernetes funge da punto di ingresso principale per tutte le richieste di gestione del cluster dal nodo di lavoro al master Kubernetes. Il server API Kubernetes convalida e elabora le richieste che modificano lo stato delle risorse Kubernetes, come i pod o i servizi, e archivia questo stato in etcd.</td>
    </tr>
    <tr>
    <td>openvpn-server</td>
    <td>Il server OpenVPN funziona con il client OpenVPN per connettere in modo protetto il master al nodo di lavoro. Questa connessione supporta le chiamate `apiserver proxy` ai tuoi pod e servizi e le chiamate `kubectl exec`, `attach` e `logs` a kubelet.</td>
    </tr>
    <tr>
    <td>etcd</td>
    <td>etcd è un archivio di valori chiave altamente disponibile che archivia lo stato di tutte le risorse Kubernetes di un cluster, quali servizi, distribuzioni e pod. I dati in etcd sono sottoposti a backup su un'istanza di archiviazione crittografata gestita da IBM.</td>
    </tr>
    <tr>
    <td>kube-scheduler</td>
    <td>Il programma di pianificazione (scheduler) Kubernetes controlla se sono presenti dei pod di nuova creazione e decide dove distribuirli in base a capacità, esigenze di prestazioni, vincoli delle politiche, specifiche di anti-affinità e requisiti di carico di lavoro. Se non è possibile trovare alcun nodo di lavoro che corrisponda ai requisiti, il pod non viene distribuito nel cluster.</td>
    </tr>
    <tr>
    <td>kube-controller-manager</td>
    <td>Il gestore controller Kubernetes è un daemon che controlla lo stato delle risorse del cluster, quali le serie di repliche. Quando lo stato di una risorsa viene modificato, ad esempio se si verifica un'interruzione di un pod in una serie di repliche, il gestore controller avvia le azioni correttive per raggiungere lo stato desiderato.</td>
    </tr>
    </tbody></table></dd>
  <dt>Nodo di lavoro</dt>
    <dd>Ogni nodo di lavoro è una macchina fisica (bare metal) o una macchina virtuale che viene eseguita su hardware fisico nell'ambiente cloud. Quando esegui il provisioning di un nodo di lavoro, determini le risorse disponibili per i contenitori ospitati su quel nodo di lavoro. Per impostazione predefinita, i tuoi nodi di lavoro sono configurati con un motore Docker gestito da {{site.data.keyword.IBM_notm}}, risorse di calcolo separate, collegamento di rete e un servizio di volume. Le funzioni di sicurezza integrate forniscono isolamento, funzionalità di gestione delle risorse e conformità di sicurezza dei nodi di lavoro.</br></br>La seguente tabella descrive i componenti di un nodo di lavoro.
    <table>
    <caption>Componenti dei nodi di lavoro</caption>
    <thead>
    <th>Componente del nodo di lavoro</th>
    <th>Spazio dei nomi</th>
    <th>Descrizione</th>
    </thead>
    <tbody>
    <tr>
    <td>ibm-master-proxy</td>
    <td>kube-system</td>
    <td>Per i cluster che eseguono Kubernetes versione 1.10 o successive, `ibm-master-proxy` inoltra le richieste dal nodo di lavoro agli indirizzi IP delle repliche dei master altamente disponibili. Nei cluster a zona singola, il master ha tre repliche su host separati con un indirizzo IP e un nome di dominio del master. Per i cluster che si trovano in una zona che supporta il multizona, il master ha tre repliche che vengono estese tra le zone. In quanto tale, ogni master ha il proprio indirizzo IP registrato con DNS, con un nome di dominio per l'intero master del cluster.</td>
    </tr>
    <tr>
    <td>openvpn-client</td>
    <td>kube-system</td>
    <td>Il client OpenVPN funziona con il server OpenVPN per connettere in modo protetto il master al nodo di lavoro. Questa connessione supporta le chiamate `apiserver proxy` ai tuoi pod e servizi e le chiamate `kubectl exec`, `attach` e `logs` a kubelet.</td>
    </tr>
    <tr>
    <td>kubelet</td>
    <td>kube-system</td>
    <td>Il kubelet è un pod che viene eseguito su ogni nodo di lavoro ed è responsabile del monitoraggio dell'integrità dei pod in esecuzione sul nodo di lavoro e del controllo degli eventi inviati dal server API Kubernetes. In base agli eventi, il kubelet crea o rimuove i pod, garantisce i probe di attività e disponibilità e segnala in risposta lo stato dei pod al server API Kubernetes.</td>
    </tr>
    <tr>
    <td>kube-dns</td>
    <td>kube-system</td>
    <td>Il DNS Kubernetes pianifica un servizio e un pod DNS sul cluster. I contenitori utilizzano automaticamente l'IP del servizio DNS per risolvere i nomi DNS nelle loro ricerche di altri pod e servizi.</td>
    </tr>
    <tr>
    <td>calico</td>
    <td>kube-system</td>
    <td>Calico gestisce le politiche di rete per il tuo cluster e comprende alcuni componenti come i seguenti.
    <ul>
    <li>**calico-cni**: la CNI (container network interface) Calico gestisce la connettività di rete dei contenitori e rimuove le risorse assegnate quando un contenitore viene eliminato.</li>
    <li>**calico-ipam**: l'IPAM Calico gestisce l'assegnazione degli indirizzi IP per i contenitori.</li>
    <li>**calico-node**: il nodo Calico è un contenitore che riunisce i vari componenti necessari per i contenitori di rete con Calico.</li>
    <li>**calico-policy-controller**: il controller politiche Calico controlla il traffico di rete in entrata e in uscita per la conformità alle politiche di rete impostate. Se il traffico non è consentito nel cluster, l'accesso al cluster viene bloccato. Il controller politiche Calico viene inoltre utilizzato per creare e impostare le politiche di rete per un cluster.</li></ul></td>
    </tr>
    <tr>
    <td>kube-proxy</td>
    <td>kube-system</td>
    <td>Il proxy di rete Kubernetes è un daemon che viene eseguito su ogni nodo di lavoro e che inoltra o che bilancia il carico del traffico di rete TCP e UDP per i servizi eseguiti nel cluster.</td>
    </tr>
    <tr>
    <td>kube-dashboard</td>
    <td>kube-system</td>
    <td>Il dashboard Kubernetes è una GUI basata sul web che consente agli utenti di gestire e risolvere i problemi relativi al cluster e alle applicazioni in esecuzione nel cluster.</td>
    </tr>
    <tr>
    <td>heapster</td>
    <td>kube-system</td>
    <td>Heapster è un aggregatore a livello di cluster di dati di monitoraggio e di evento. Il pod Heapster rileva tutti i nodi nel cluster e interroga le informazioni sull'utilizzo dal kubelet di ciascun nodo. Puoi trovare i grafici di utilizzo nel dashboard Kubernetes.</td>
    </tr>
    <tr>
    <td>ALB Ingress</td>
    <td>kube-system</td>
    <td>Ingress è un servizio Kubernetes che puoi utilizzare per bilanciare i carichi di lavoro del traffico di rete nel tuo cluster inoltrando le richieste pubbliche o private a più applicazioni nel tuo cluster. Per esporre le tue applicazioni sulla rete pubblica o privata, devi creare una risorsa Ingress per registrare le tue applicazioni con il programma di bilanciamento del carico (ALB - application load balancer) Ingress. È quindi possibile accedere a più applicazioni utilizzando un singolo URL o indirizzo IP.</td>
    </tr>
    <tr>
    <td>Provider di archiviazione</td>
    <td>kube-system</td>
    <td>Ogni cluster è configurato con un plug-in per eseguire il provisioning dell'archiviazione file. Puoi scegliere di installare altri componenti aggiuntivi, come ad esempio l'archiviazione blocchi.</td>
    </tr>
    <tr>
    <td>Registrazione e metriche</td>
    <td>ibm-system</td>
    <td>Puoi utilizzare i servizi {{site.data.keyword.loganalysislong_notm}} e {{site.data.keyword.monitoringlong_notm}} integrati per espandere le tue funzionalità di raccolta e conservazione quando lavori con log e metriche.</td>
    </tr>
    <tr>
    <td>Programma di bilanciamento del carico</td>
    <td>ibm-system</td>
    <td>Un programma di bilanciamento del carico è un servizio Kubernetes che può essere utilizzato per bilanciare i carichi di lavoro del traffico di rete nel tuo cluster inoltrando richieste pubbliche o private a un'applicazione.</td>
    </tr>
    <tr>
    <td>Servizi e pod dell'applicazione</td>
    <td>default</td>
    <td>Nello spazio dei nomi <code>default</code> o negli spazi dei nomi che crei, puoi distribuire le applicazioni in pod e servizi per comunicare con tali pod.</td>
    </tr>
    </tbody></table></dd>
</dl>

Vuoi vedere in che modo {{site.data.keyword.containerlong_notm}} può essere utilizzato con altri prodotti e servizi? Controlla alcune delle [integrazioni](cs_integrations.html#integrations).
{: tip}
