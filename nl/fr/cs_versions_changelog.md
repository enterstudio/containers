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



# Journal des modifications de version
{: #changelog}

Affichez des informations sur les modifications de version correspondant à des mises à jour de version principale, de version secondaire ou de correctif disponibles pour vos clusters Kubernetes {{site.data.keyword.containerlong}}. Les modifications comprennent des mises à jour pour les composants de Kubernetes et d'{{site.data.keyword.Bluemix_notm}} Provider.
{:shortdesc}

Pour plus d'informations sur les versions principales et secondaires, les versions de correctifs et les actions de préparation entre les versions secondaires, voir [Versions Kubernetes](cs_versions.html). 
{: tip}

Pour plus d'informations sur les modifications apportées depuis la version précédente, voir les journaux de modifications suivants.
-  [Journal des modifications](#112_changelog) - Version 1.12.
-  [Journal des modifications](#111_changelog) - Version 1.11.
-  [Journal des modifications](#110_changelog) - Version 1.10.
-  [Archive](#changelog_archive) des journaux des modifications pour les versions dépréciées ou non prises en charge.

Certains journaux de modifications concernent les _groupes de correctifs de noeud worker_ et s'appliquent uniquement aux noeuds worker. Vous devez [appliquer ces correctifs](cs_cli_reference.html#cs_worker_update) pour garantir la conformité de vos noeuds worker aux normes de sécurité. D'autres journaux de modifications pour les _groupes de correctifs du maître_ et s'appliquent uniquement au noeud maître du cluster. Les groupes de correctifs du maître ne s'appliquent pas forcément automatiquement. Vous pouvez choisir de les [appliquer manuellement](cs_cli_reference.html#cs_cluster_update). Pour plus d'informations sur les types de correctif, voir [Types de mise à jour](cs_versions.html#update_types).
{: note}

</br>

## Journal des modifications - Version 1.12
{: #112_changelog}

Passez en revue le journal des modifications de la version 1.12. 
{: shortdesc}

### Journal des modifications pour la version 1.12.3_1531, publié le 5 décembre 2018
{: #1123_1531}

Le tableau suivant présente les modifications incluses dans le correctif 1.12.3_1531.
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.12.2_1530">
<caption>Modifications depuis la version 1.12.2_1530</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>v1.12.2-68</td>
<td>v1.12.3-91</td>
<td>Mise à jour pour prendre en charge l'édition Kubernetes 1.12.3.</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>v1.12.2</td>
<td>v1.12.3</td>
<td>Voir les [notes sur l'édition de Kubernetes ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/kubernetes/releases/tag/v1.12.3). La mise à jour résout la vulnérabilité [CVE-2018-1002105 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/kubernetes/issues/71411).</td>
</tr>
</tbody>
</table>

### Journal des modifications de noeud worker - Groupe de correctifs 1.12.2_1530, publié le 4 décembre 2018
{: #1122_1530}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.12.2_1530.
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.12.2_1529">
<caption>Modifications depuis la version 1.12.2_1529</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Utilisation des ressources de noeud worker</td>
<td>N/A</td>
<td>N/A</td>
<td>Ajout de groupes cgroups pour le kubelet et containerd pour empêcher ces composants d'être à court de ressources. Pour plus d'informations, voir [Réserves de ressources de noeud worker](cs_clusters_planning.html#resource_limit_node).</td>
</tr>
</tbody>
</table>



### Journal des modifications pour la version 1.12.2_1529, publié le 27 novembre 2018
{: #1122_1529}

Le tableau suivant présente les modifications incluses dans le correctif 1.12.2_1529.
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.12.2_1528">
<caption>Modifications depuis la version 1.12.2_1528</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Calico</td>
<td>v3.2.1</td>
<td>v3.3.1</td>
<td>Voir les [notes sur l'édition de Calico ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://docs.projectcalico.org/v3.3/releases/#v331). La mise à jour résout [Tigera Technical Advisory TTA-2018-001 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.projectcalico.org/security-bulletins/).</td>
</tr>
<tr>
<td>Configuration du DNS de cluster</td>
<td>N/A</td>
<td>N/A</td>
<td>Correction d'un bogue pouvant entraîner l'exécution des pods Kubernetes DNS et CoreDNS après la création du cluster ou des opérations de mise à jour.</td>
</tr>
<tr>
<td>containerd</td>
<td>v1.2.0</td>
<td>v1.1.5</td>
<td>Voir les [notes sur l'édition de containerd![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/containerd/containerd/releases/tag/v1.1.5). Mise à jour de containerd pour corriger un interblocage pouvant [empêcher les pods de s'arrêter ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/containerd/containerd/issues/2744).</td>
</tr>
<tr>
<td>Serveur et client OpenVPN</td>
<td>2.4.4-r1-6</td>
<td>2.4.6-r3-IKS-8</td>
<td>Mise à jour d'une image pour [CVE-2018-0732 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-0732) et [CVE-2018-0737 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-0737).</td>
</tr>
</tbody>
</table>

### Journal des modifications de noeud worker - Groupe de correctifs 1.12.2_1528, publié le 19 novembre 2018
{: #1122_1528}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.12.2_1528. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.12.2_1527">
<caption>Modifications depuis la version 1.12.2_1527</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Noyau</td>
<td>4.4.0-137</td>
<td>4.4.0-139</td>
<td>Mise à jour des images de noeud worker avec la mise à jour du noyau pour [CVE-2018-7755 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://changelogs.ubuntu.com/changelogs/pool/main/l/linux/linux_4.4.0-139.165/changelog).</td>
</tr>
</tbody>
</table>


### Journal des modifications pour la version 1.12.2_1527, publié le 7 novembre 2018
{: #1122_1527}

Le tableau suivant présente les modifications incluses dans le correctif 1.12.2_1527. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.11.3_1533">
<caption>Modifications depuis la version 1.11.3_1533</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Configuration de Calico</td>
<td>N/A</td>
<td>N/A</td>
<td>Les pods `calico-*` de Calico dans l'espace de nom `kube-system` définissent désormais les demandes de ressources d'UC et de mémoire pour tous les conteneurs.</td>
</tr>
<tr>
<td>Fournisseur DNS de cluster</td>
<td>N/A</td>
<td>N/A</td>
<td>Kubernetes DNS (KubeDNS) reste le fournisseur DNS de cluster par défaut. Vous avez toutefois la possibilité de [remplacer le fournisseur DNS de cluster par CoreDNS](cs_cluster_update.html#dns).</td>
</tr>
<tr>
<td>Fournisseur de métriques de cluster</td>
<td>N/A</td>
<td>N/A</td>
<td>Le serveur Kubernetes Metrics Server remplace Kubernetes Heapster (déprécié depuis la version 1.8 de Kubernetes) comme fournisseur de métriques de cluster. Pour les éléments action, voir [l'action de préparation `metrics-server`](cs_versions.html#metrics-server).</td>
</tr>
<tr>
<td>containerd</td>
<td>1.1.4</td>
<td>1.2.0</td>
<td>Voir les [notes sur l'édition de containerd![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/containerd/containerd/releases/tag/v1.2.0).</td>
</tr>
<tr>
<td>CoreDNS</td>
<td>N/A</td>
<td>1.2.2</td>
<td>Voir les [notes sur l'édition de CoreDNS![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/coredns/coredns/releases/tag/v1.2.2).</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>v1.11.3</td>
<td>v1.12.2</td>
<td>Voir les [notes sur l'édition de Kubernetes ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/kubernetes/releases/tag/v1.12.2).</td>
</tr>
<tr>
<td>Configuration de Kubernetes</td>
<td>N/A</td>
<td>N/A</td>
<td>Ajout de trois nouvelles politiques de sécurité de pod IBM et des rôles de cluster associés. Pour plus d'informations, voir [Description des ressources par défaut pour la gestion de cluster IBM](cs_psp.html#ibm_psp).</td>
</tr>
<tr>
<td>Tableau de bord Kubernetes</td>
<td>v1.8.3</td>
<td>v1.10.0</td>
<td>Voir les [notes sur l'édition du tableau de bord Kubernetes![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/dashboard/releases/tag/v1.10.0).<br><br>
Si vous accédez au tableau de bord via `kubectl proxy`, le bouton **SKIP** sur la page de connexion a été retiré. Utilisez à la place un **Jeton** pour vous connecter. De plus, vous pouvez désormais augmenter le nombre de pods du tableau de bord Kubernetes en exécutant la commande `kubectl -n kube-system scale deploy kubernetes-dashboard --replicas=3`.</td>
</tr>
<tr>
<td>Kubernetes DNS</td>
<td>1.14.10</td>
<td>1.14.13</td>
<td>Voir les [notes sur l'édition de Kubernetes DNS![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/dns/releases/tag/1.14.13).</td>
</tr>
<tr>
<td>Kubernetes Metrics Server</td>
<td>N/A</td>
<td>v0.3.1</td>
<td>Voir les [notes sur l'édition de Kubernetes Metrics Server![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes-incubator/metrics-server/releases/tag/v0.3.1).</td>
</tr>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>v1.11.3-118</td>
<td>v1.12.2-68</td>
<td>Mise à jour pour prendre en charge l'édition Kubernetes 1.12. Autres modifications incluses :
<ul><li>Les pods d'équilibreur de charge (`ibm-cloud-provider-ip-*` dans l'espace de nom `ibm-system`) définissent désormais les demandes de ressources d'UC et de mémoire.</li>
<li>L'annotation `service.kubernetes.io/ibm-load-balancer-cloud-provider-vlan` a été ajoutée pour spécifier le réseau local virtuel (VLAN) sur lequel est déployé le service d'équilibreur de charge. Pour voir les VLAN disponibles dans votre cluster, exécutez la commande `ibmcloud ks vlans --zone <zone>`.</li>
<li>Un nouvel [équilibreur de charge 2.0](cs_loadbalancer.html#planning_ipvs) est disponible en version bêta.</li></ul></td>
</tr>
<tr>
<td>Configuration du client OpenVPN</td>
<td>N/A</td>
<td>N/A</td>
<td>Le client OpenVPN `vpn-* pod` dans l'espace de nom `kube-system` définit désormais les demandes de ressources d'UC et de mémoire.</td>
</tr>
</tbody>
</table>

## Journal des modifications - Version 1.11
{: #111_changelog}

Passez en revue le journal des modifications de la version 1.11.

### Journal des modifications pour la version 1.11.5_1537, publié le 5 décembre 2018
{: #1115_1537}

Le tableau suivant présente les modifications incluses dans le correctif 1.11.5_1537.
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.11.4_1536">
<caption>Modifications depuis la version 1.11.4_1536</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>v1.11.4-142</td>
<td>v1.11.5-152</td>
<td>Mise à jour pour prendre en charge l'édition Kubernetes 1.11.5.</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>v1.11.4</td>
<td>v1.11.5</td>
<td>Voir les [notes sur l'édition de Kubernetes ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/kubernetes/releases/tag/v1.11.5). La mise à jour résout la vulnérabilité [CVE-2018-1002105 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/kubernetes/issues/71411).</td>
</tr>
</tbody>
</table>

### Journal des modifications de noeud worker - Groupe de correctifs 1.11.4_1536, publié le 4 décembre 2018
{: #1114_1536}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.11.4_1536.
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.11.4_1535">
<caption>Modifications depuis la version 1.11.4_1535</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Utilisation des ressources de noeud worker</td>
<td>N/A</td>
<td>N/A</td>
<td>Ajout de groupes cgroups pour le kubelet et containerd pour empêcher ces composants d'être à court de ressources. Pour plus d'informations, voir [Réserves de ressources de noeud worker](cs_clusters_planning.html#resource_limit_node).</td>
</tr>
</tbody>
</table>

### Journal des modifications pour la version 1.11.4_1535, publié le 27 novembre 2018
{: #1114_1535}

Le tableau suivant présente les modifications incluses dans le correctif 1.11.4_1535.
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.11.3_1534">
<caption>Modifications depuis la version 1.11.3_1534</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Calico</td>
<td>v3.2.1</td>
<td>v3.3.1</td>
<td>Voir les [notes sur l'édition de Calico ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://docs.projectcalico.org/v3.3/releases/#v331). La mise à jour résout [Tigera Technical Advisory TTA-2018-001 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.projectcalico.org/security-bulletins/).</td>
</tr>
<tr>
<td>containerd</td>
<td>v1.1.4</td>
<td>v1.1.5</td>
<td>Voir les [notes sur l'édition de containerd![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/containerd/containerd/releases/tag/v1.1.5). Mise à jour de containerd pour corriger un interblocage pouvant [empêcher les pods de s'arrêter ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/containerd/containerd/issues/2744).</td>
</tr>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>v1.11.3-127</td>
<td>v1.11.4-142</td>
<td>Mise à jour pour prendre en charge l'édition Kubernetes 1.11.4.</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>v1.11.3</td>
<td>v1.11.4</td>
<td>Voir les [notes sur l'édition de Kubernetes ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/kubernetes/releases/tag/v1.11.4).</td>
</tr>
<tr>
<td>Serveur et client OpenVPN</td>
<td>2.4.4-r1-6</td>
<td>2.4.6-r3-IKS-8</td>
<td>Mise à jour d'une image pour [CVE-2018-0732 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-0732) et [CVE-2018-0737 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-0737).</td>
</tr>
</tbody>
</table>

### Journal des modifications de noeud worker - Groupe de correctifs 1.11.3_1534, publié le 19 novembre 2018
{: #1113_1534}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.11.3_1534. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.11.3_1533">
<caption>Modifications depuis la version 1.11.3_1533</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Noyau</td>
<td>4.4.0-137</td>
<td>4.4.0-139</td>
<td>Mise à jour des images de noeud worker avec la mise à jour du noyau pour [CVE-2018-7755 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://changelogs.ubuntu.com/changelogs/pool/main/l/linux/linux_4.4.0-139.165/changelog).</td>
</tr>
</tbody>
</table>


### Journal des modifications pour la version 1.11.3_1533, publié le 7 novembre 2018
{: #1113_1533}

Le tableau suivant présente les modifications incluses dans le correctif 1.11.3_1533. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.11.3_1531">
<caption>Modifications depuis la version 1.11.3_1531</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Mise à jour des maîtres à haute disponibilité (HA)</td>
<td>N/A</td>
<td>N/A</td>
<td>Correction de la mise à jour des maîtres à haute disponibilité (HA) pour les clusters qui utilisent des webhooks d'admission, tels qu'`initializerconfigurations`, `mutatingwebhookconfigurations` ou `validatingwebhookconfigurations`. Vous pouvez utiliser ces webhooks avec des chartes Helm comme pour [Container Image Security Enforcement](/docs/services/Registry/registry_security_enforce.html#security_enforce).</td>
</tr>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>v1.11.3-100</td>
<td>v1.11.3-127</td>
<td>Ajout de l'annotation `service.kubernetes.io/ibm-load-balancer-cloud-provider-vlan` pour spécifier le réseau local virtuel (VLAN) sur lequel est déployé le service d'équilibreur de charge. Pour voir les VLAN disponibles dans votre cluster, exécutez la commande `ibmcloud ks vlans --zone <zone>`.</td>
</tr>
<tr>
<td>Noyau avec puce TPM activée</td>
<td>N/A</td>
<td>N/A</td>
<td>Les noeuds worker bare metal avec des puces TPM pour la fonction de calcul sécurisé utilisent le noyau Ubuntu par défaut jusqu'à ce que la fonction de confiance (trust) soit activée. Si vous [activez la fonction de confiance](cs_cli_reference.html#cs_cluster_feature_enable) sur un cluster existant, vous devez [recharger](cs_cli_reference.html#cs_worker_reload) tous les noeuds worker bare metal existants avec des puces TPM. Pour vérifier si un noeud worker bare metal comporte une puce TPM, vérifiez la zone **Trustable** après avoir exécuté la [commande](cs_cli_reference.html#cs_machine_types) `ibmcloud ks machine-types --zone`.</td>
</tr>
</tbody>
</table>

### Journal des modifications du maître - Groupe de correctifs 1.11.3_1531, publié le 1er novembre 2018
{: #1113_1531_ha-master}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs du maître 1.11.3_1531. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.11.3_1527">
<caption>Modifications depuis la version 1.11.3_1527</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Maître de cluster</td>
<td>N/A</td>
<td>N/A</td>
<td>Mise à jour de la configuration du noeud maître du cluster pour accroître la haute disponibilité (HA). Désormais, les clusters ont trois répliques du maître Kubernetes conçues avec une configuration haute disponibilité (HA), chaque maître étant déployé sur des hôtes physiques distincts. Par ailleurs, si votre cluster se trouve dans une zone compatible avec plusieurs zones, les maîtres sont répartis sur les différentes zones.<br>Pour connaître les actions que vous devez effectuer, voir [Mise à jour des maîtres de cluster pour la haute disponibilité](cs_versions.html#ha-masters). Ces actions de préparation sont applicables dans les cas suivants :<ul>
<li>Si vous disposez d'un pare-feu ou de règles réseau Calico personnalisées.</li>
<li>Si vous utilisez les ports d'hôte `2040` ou `2041` sur vos noeuds worker.</li>
<li>Si vous avez utilisé l'adresse IP du noeud maître du cluster pour accéder au maître depuis le cluster.</li>
<li>Si vous disposez d'un processus automatique pour appeler l'API ou l'interface de ligne de commande Calico (`calicoctl`), par exemple pour créer des règles Calico.</li>
<li>Si vous utilisez des règles réseau Kubernetes ou Calico pour contrôler l'accès du trafic sortant du pod vers le maître.</li></ul></td>
</tr>
<tr>
<td>Proxy du maître de cluster HA</td>
<td>N/A</td>
<td>1.8.12-alpine</td>
<td>Ajout d'un pod `ibm-master-proxy-*` pour l'équilibrage de charge côté client sur tous les noeuds worker, de sort que chaque client de noeud worker puisse acheminer les demandes à une réplique de maître HA disponible.</td>
</tr>
<tr>
<td>etcd</td>
<td>v3.2.18</td>
<td>v3.3.1</td>
<td>Voir les [notes sur l'édition d'etcd ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/coreos/etcd/releases/v3.3.1).</td>
</tr>
<tr>
<td>Chiffrement des données dans etcd</td>
<td>N/A</td>
<td>N/A</td>
<td>Auparavant, les données etcd étaient stockées sur une instance de stockage de fichiers NFS d'un maître chiffrée au repos. Désormais, les données etcd sont stockées sur le disque local du maître et sauvegardées dans {{site.data.keyword.cos_full_notm}}. Les données sont chiffrées lors du transit vers {{site.data.keyword.cos_full_notm}} et au repos. Cependant, les données etcd sur le disque local du maître ne sont pas chiffrées. Si vous souhaitez que les données etcd locales de votre maître soient chiffrées, [activez {{site.data.keyword.keymanagementservicelong_notm}} dans votre cluster](cs_encrypt.html#keyprotect).</td>
</tr>
</tbody>
</table>

### Journal des modifications de noeud worker - Groupe de correctifs 1.11.3_1531, publié le 26 octobre 2018
{: #1113_1531}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.11.3_1531. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.11.3_1525">
<caption>Modifications depuis la version 1.11.3_1525</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Traitement des interruptions du système d'exploitation</td>
<td>N/A</td>
<td>N/A</td>
<td>Remplacement du démon du système IRQ (Interrupt Request) avec un gestionnaire d'interruption plus performant.</td>
</tr>
</tbody>
</table>

### Journal des modifications du maître - Groupe de correctifs 1.11.3_1527, publié le 15 octobre 2018
{: #1113_1527}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs du maître 1.11.3_1527. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.11.3_1524">
<caption>Modifications depuis la version 1.11.3_1524</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Configuration de Calico</td>
<td>N/A</td>
<td>N/A</td>
<td>La sonde de conteneur Readiness Probe `calico-node` a été corrigée pour mieux traiter les défaillances de noeuds.</td>
</tr>
<tr>
<td>Mise à jour de cluster</td>
<td>N/A</td>
<td>N/A</td>
<td>Correction du problème de mise à jour des modules complémentaires de cluster lorsque le maître est mis à jour à partir d'une version non prise en charge.</td>
</tr>
</tbody>
</table>

### Journal des modifications de noeud worker - Groupe de correctifs 1.11.3_1525, publié le 10 octobre 2018
{: #1113_1525}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.11.3_1525. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.11.3_1524">
<caption>Modifications depuis la version 1.11.3_1524</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Noyau</td>
<td>4.4.0-133</td>
<td>4.4.0-137</td>
<td>Mise à jour des images de noeud worker avec la mise à jour du noyau pour [CVE-2018-14633, CVE-2018-17182 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://changelogs.ubuntu.com/changelogs/pool/main/l/linux/linux_4.4.0-137.163/changelog).</td>
</tr>
<tr>
<td>Délai d'inactivité de session</td>
<td>N/A</td>
<td>N/A</td>
<td>Le délai d'inactivité de session a été fixé à 5 minutes pour des raisons de conformité.</td>
</tr>
</tbody>
</table>


### Journal des modifications pour la version 1.11.3_1524, publié le 2 octobre 2018
{: #1113_1524}

Le tableau suivant présente les modifications incluses dans le correctif 1.11.3_1524. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.11.3_1521">
<caption>Modifications depuis la version 1.11.3_1521</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>containerd</td>
<td>1.1.3</td>
<td>1.1.4</td>
<td>Voir les [notes sur l'édition de containerd![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/containerd/containerd/releases/tag/v1.1.4).</td>
</tr>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>v1.11.3-91</td>
<td>v1.11.3-100</td>
<td>Mise à jour du lien vers la documentation dans les messages d'erreur de l'équilibreur de charge.</td>
</tr>
<tr>
<td>Classes de stockage de fichiers d'IBM</td>
<td>N/A</td>
<td>N/A</td>
<td>Suppression du paramètre `reclaimPolicy` en double dans les classes de stockage de fichiers d'IBM.<br><br>
Désormais, lorsque vous mettez à jour le noeud maître du cluster, la classe de stockage de fichiers d'IBM reste inchangée. Si vous souhaitez modifier la classe de stockage par défaut, exécutez la commande `kubectl patch storageclass <storageclass> -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'` et remplacez `<storageclass>` par le nom de la classe de stockage.</td>
</tr>
</tbody>
</table>

### Journal des modifications pour la version 1.11.3_1521, publié le 20 septembre 2018
{: #1113_1521}

Le tableau suivant présente les modifications incluses dans le correctif 1.11.3_1521. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.11.2_1516">
<caption>Modifications depuis la version 1.11.2_1516</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>v1.11.2-71</td>
<td>v1.11.3-91</td>
<td>Mise à jour pour prendre en charge l'édition Kubernetes 1.11.3.</td>
</tr>
<tr>
<td>Classes de stockage de fichiers d'IBM</td>
<td>N/A</td>
<td>N/A</td>
<td>Suppression de `mountOptions` dans les classes de stockage de fichiers d'IBM afin d'utiliser la valeur par défaut fournie par le noeud worker.<br><br>
Désormais, lorsque vous mettez à jour le noeud maître du cluster, la classe de stockage de fichiers d'IBM reste `ibmc-file-bronze`. Si vous souhaitez modifier la classe de stockage par défaut, exécutez la commande `kubectl patch storageclass <storageclass> -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'` et remplacez `<storageclass>` par le nom de la classe de stockage.</td>
</tr>
<tr>
<td>Fournisseur de service de gestion des clés (KMS)</td>
<td>N/A</td>
<td>N/A</td>
<td>Possibilité d'utiliser le service de gestion des clés (KMS) de Kubernetes dans le cluster pour prendre en charge {{site.data.keyword.keymanagementservicefull}}. Lorsque vous [activez {{site.data.keyword.keymanagementserviceshort}} dans votre cluster](cs_encrypt.html#keyprotect), toutes vos valeurs confidentielles (secrets) Kubernetes sont chiffrées.</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>v1.11.2</td>
<td>v1.11.3</td>
<td>Voir les [notes sur l'édition de Kubernetes![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/kubernetes/releases/tag/v1.11.3).</td>
</tr>
<tr>
<td>Mise à l'échelle automatique de DNS avec Kubernetes</td>
<td>1.1.2-r2</td>
<td>1.2.0</td>
<td>Voir les [notes sur l'édition de la fonction Kubernetes de mise à l'échelle automatique (autoscaler) de DNS ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes-incubator/cluster-proportional-autoscaler/releases/tag/1.2.0).</td>
</tr>
<tr>
<td>Rotation des journaux</td>
<td>N/A</td>
<td>N/A</td>
<td>Passage à l'utilisation de fichiers timer `systemd` au lieu de travaux `cronjobs` pour empêcher l'échec de la rotation des journaux (`logrotate`) sur les noeuds worker qui ne sont pas rechargés ou mis à niveau dans les 90 jours. **Remarque** : dans toutes les versions antérieures à cette version secondaire, le disque principal se remplit après l'échec d'un travail cron car il est impossible de faire tourner les journaux. Le travail cron échoue lorsque le noeud worker est actif pendant une durée de 90 jours sans être mis à jour ou rechargé. Si les journaux remplissent la totalité du disque principal, le noeud worker passe à l'état d'échec. Le noeud worker peut être corrigé en exécutant la [commande](cs_cli_reference.html#cs_worker_reload) `ibmcloud ks worker-reload` ou la [commande](cs_cli_reference.html#cs_worker_update) `ibmcloud ks worker-update` .</td>
</tr>
<tr>
<td>Expiration du mot de passe root</td>
<td>N/A</td>
<td>N/A</td>
<td>Les mots de passe root des noeuds worker expirent au bout de 90 jours pour des raisons de conformité. Si vos outils d'automatisation doivent se connecter au noeud worker en tant que root ou dépendent de travaux cron qui s'exécutent en tant que root, vous pouvez désactiver l'expiration du mot de passe en vous connectant au noeud worker et en exécutant la commande `chage -M -1 root`. **Remarque** : si vos exigences de conformité en matière de sécurité vous empêchent toute exécution en tant que root ou l'annulation de l'expiration du mot de passe, ne désactivez pas l'expiration. Vous pouvez à la place [mettre à jour](cs_cli_reference.html#cs_worker_update) ou [recharger](cs_cli_reference.html#cs_worker_reload) vos noeuds worker au moins tous les 90 jours.</td>
</tr>
<tr>
<td>Composants d'exécution de noeud worker (`kubelet`, `kube-proxy`, `containerd`)</td>
<td>N/A</td>
<td>N/A</td>
<td>Suppression des dépendances des composants d'exécution sur le disque principal. Cette amélioration empêche l'échec des noeuds worker lorsque le disque principal est plein.</td>
</tr>
<tr>
<td>Systemd</td>
<td>N/A</td>
<td>N/A</td>
<td>Nettoyage régulier des unités de montage transitoires pour leur éviter de devenir illimitées. Cette action corrige l'erreur [Kubernetes 57345 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/kubernetes/issues/57345).</td>
</tr>
</tbody>
</table>

### Journal des modifications pour la version 1.11.2_1516, publié le 4 septembre 2018
{: #1112_1516}

Le tableau suivant présente les modifications incluses dans le correctif 1.11.2_1516. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.11.2_1514">
<caption>Modifications depuis la version 1.11.2_1514</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Calico</td>
<td>v3.1.3</td>
<td>v3.2.1</td>
<td>Voir les [notes sur l'édition de Calico ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://docs.projectcalico.org/v3.2/releases/#v321).</td>
</tr>
<tr>
<td>containerd</td>
<td>1.1.2</td>
<td>1.1.3</td>
<td>Voir les [notes sur l'édition de `containerd` ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/containerd/containerd/releases/tag/v1.1.3).</td>
</tr>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>v1.11.2-60</td>
<td>v1.11.2-71</td>
<td>La configuration du fournisseur de cloud a changé pour mieux gérer les mises à jour des services d'équilibreur de charge avec l'élément `externalTrafficPolicy` défini sur `local`.</td>
</tr>
<tr>
<td>Configuration du plug-in de stockage de fichiers d'IBM</td>
<td>N/A</td>
<td>N/A</td>
<td>La version NFS par défaut a été supprimée des options de montage dans les classes de stockage de fichiers fournies par IBM. Désormais, le système d'exploitation de l'hôte négocie la version NFS avec le serveur NFS de l'infrastructure IBM Cloud (SoftLayer). Pour définir manuellement une version NFS spécifique ou modifier la version NFS de votre volume persistant qui a été négociée par le système d'exploitation de l'hôte, voir [Modification de la version NFS par défaut](cs_storage_file.html#nfs_version_class).</td>
</tr>
</tbody>
</table>

### Journal des modifications de noeud worker - Groupe de correctifs 1.11.2_1514, publié le 23 août 2018
{: #1112_1514}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.11.2_1514. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.11.2_1513">
<caption>Modifications depuis la version 1.11.2_1513</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>`systemd`</td>
<td>229</td>
<td>230</td>
<td>Mise à jour de `systemd` pour corriger la fuite liée à `cgroup`.</td>
</tr>
<tr>
<td>Noyau</td>
<td>4.4.0-127</td>
<td>4.4.0-133</td>
<td>Mise à jour des images de noeud worker avec la mise à jour du noyau pour [CVE-2018-3620, CVE-2018-3646 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://usn.ubuntu.com/3741-1/).</td>
</tr>
</tbody>
</table>

### Journal des modifications pour la version 1.11.2_1513, publié le 14 août 2018
{: #1112_1513}

Le tableau suivant présente les modifications incluses dans le correctif 1.11.2_1513. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.10.5_1518">
<caption>Modifications depuis la version 1.10.5_1518</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>containerd</td>
<td>N/A</td>
<td>1.1.2</td>
<td>`containerd` est le nouvel environnement de conteneur de Kubernetes qui remplace Docker. Voir les [notes sur l'édition de `containerd` ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/containerd/containerd/releases/tag/v1.1.2). Pour connaître les actions que vous devez effectuer, voir [Mise à jour vers l'environnement d'exécution `containerd`](cs_versions.html#containerd).</td>
</tr>
<tr>
<td>Docker</td>
<td>N/A</td>
<td>N/A</td>
<td>`containerd` est le nouvel environnement d'exécution de conteneur de Kubernetes qui remplace Docker afin d'améliorer les performances. Pour connaître les actions que vous devez effectuer, voir [Mise à jour vers l'environnement d'exécution `containerd`](cs_versions.html#containerd).</td>
</tr>
<tr>
<td>etcd</td>
<td>v3.2.14</td>
<td>v3.2.18</td>
<td>Voir les [notes sur l'édition d'etcd ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/coreos/etcd/releases/v3.2.18).</td>
</tr>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>v1.10.5-118</td>
<td>v1.11.2-60</td>
<td>Mise à jour pour prendre en charge l'édition Kubernetes 1.11. En outre, les pods d'équilibreur de charge utilisent désormais la nouvelle classe de priorité de pod `ibm-app-cluster-critical`.</td>
</tr>
<tr>
<td>Plug-in IBM File Storage</td>
<td>334</td>
<td>338</td>
<td>Mise à jour d'`incubator` à la version 1.8. Le stockage de fichiers est mis à disposition dans la zone spécifique que vous sélectionnez. Vous ne pouvez pas mettre à jour des libellés d'une instance de volume persistant (statique) existante, à moins d'utiliser un cluster à zones multiples et de nécessiter [l'ajout de libellés de région et de zone](cs_storage_basics.html#multizone).</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>v1.10.5</td>
<td>v1.11.2</td>
<td>Voir les [notes sur l'édition de Kubernetes![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/kubernetes/releases/tag/v1.11.2).</td>
</tr>
<tr>
<td>Configuration de Kubernetes</td>
<td>N/A</td>
<td>N/A</td>
<td>Mise à jour de la configuration OpenID Connect pour le serveur d'API Kubernetes du cluster pour prendre en charge les groupes d'accès Identity Access and Management (IAM) d'{{site.data.keyword.Bluemix_notm}}. Ajout de `Priority` dans l'option `--enable-admission-plugins` pour le serveur d'API Kubernetes du cluster et configuration du cluster pour prendre en charge la priorité des pods. Pour plus d'informations, voir :
<ul><li>[Groupes d'accès {{site.data.keyword.Bluemix_notm}} IAM](cs_users.html#rbac)</li>
<li>[Configuration de la priorité de pod](cs_pod_priority.html#pod_priority)</li></ul></td>
</tr>
<tr>
<td>Kubernetes Heapster</td>
<td>v1.5.2</td>
<td>v.1.5.4</td>
<td>Augmentation des limites de ressources pour le conteneur `heapster-nanny`. Voir les [notes sur l'édition de Kubernetes Heapster ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/heapster/releases/tag/v1.5.4).</td>
</tr>
<tr>
<td>Configuration de consignation</td>
<td>N/A</td>
<td>N/A</td>
<td>Le répertoire de consignation du conteneur est désormais `/var/log/pods/` au lieu de `/var/lib/docker/containers/`.</td>
</tr>
</tbody>
</table>

<br />


## Journal des modifications - Version 1.10
{: #110_changelog}

Passez en revue le journal des modifications de la version 1.10.

### Journal des modifications pour la version 1.10.11_1536, publié le 4 décembre 2018
{: #11011_1536}

Le tableau suivant présente les modifications incluses dans le correctif 1.10.11_1536.
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.10.8_1532">
<caption>Modifications depuis la version 1.10.8_1532</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Calico</td>
<td>v3.2.1</td>
<td>v3.3.1</td>
<td>Voir les [notes sur l'édition de Calico ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://docs.projectcalico.org/v3.3/releases/#v331). La mise à jour résout [Tigera Technical Advisory TTA-2018-001 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.projectcalico.org/security-bulletins/).</td>
</tr>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>v1.10.8-197</td>
<td>v1.10.11-219</td>
<td>Mise à jour pour prendre en charge l'édition Kubernetes 1.10.11.</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>v1.10.8</td>
<td>v1.10.11</td>
<td>Voir les [notes sur l'édition de Kubernetes ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/kubernetes/releases/tag/v1.10.11). La mise à jour résout la vulnérabilité [CVE-2018-1002105 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/kubernetes/issues/71411).</td>
</tr>
<tr>
<td>Serveur et client OpenVPN</td>
<td>2.4.4-r1-6</td>
<td>2.4.6-r3-IKS-8</td>
<td>Mise à jour d'une image pour [CVE-2018-0732 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-0732) et [CVE-2018-0737 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-0737).</td>
</tr>
<tr>
<td>Utilisation des ressources de noeud worker</td>
<td>N/A</td>
<td>N/A</td>
<td>Ajout de groupes cgroups pour le kubelet et docker pour empêcher ces composants d'être à court de ressources. Pour plus d'informations, voir [Réserves de ressources de noeud worker](cs_clusters_planning.html#resource_limit_node).</td>
</tr>
</tbody>
</table>

### Journal des modifications de noeud worker - Groupe de correctifs 1.10.8_1532, publié le 27 novembre 2018
{: #1108_1532}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.10.8_1532.
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.10.8_1531">
<caption>Modifications depuis la version 1.10.8_1531</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Docker</td>
<td>17.06.2</td>
<td>18.06.1</td>
<td>Voir les [notes sur l'édition de Docker ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://docs.docker.com/engine/release-notes/#18061-ce).</td>
</tr>
</tbody>
</table>

### Journal des modifications de noeud worker - Groupe de correctifs 1.10.8_1531, publié le 19 novembre 2018
{: #1108_1531}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.10.8_1531. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.10.8_1530">
<caption>Modifications depuis la version 1.10.8_1530</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Noyau</td>
<td>4.4.0-137</td>
<td>4.4.0-139</td>
<td>Mise à jour des images de noeud worker avec la mise à jour du noyau pour [CVE-2018-7755 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://changelogs.ubuntu.com/changelogs/pool/main/l/linux/linux_4.4.0-139.165/changelog).</td>
</tr>
</tbody>
</table>

### Journal des modifications pour la version 1.10.8_1530, publié le 7 novembre 2018
{: #1108_1530_ha-master}

Le tableau suivant présente les modifications incluses dans le correctif 1.10.8_1530. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.10.8_1528">
<caption>Modifications depuis la version 1.10.8_1528</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Maître de cluster</td>
<td>N/A</td>
<td>N/A</td>
<td>Mise à jour de la configuration du noeud maître du cluster pour accroître la haute disponibilité (HA). Désormais, les clusters ont trois répliques du maître Kubernetes conçues avec une configuration haute disponibilité (HA), chaque maître étant déployé sur des hôtes physiques distincts. Par ailleurs, si votre cluster se trouve dans une zone compatible avec plusieurs zones, les maîtres sont répartis sur les différentes zones.<br>Pour connaître les actions que vous devez effectuer, voir [Mise à jour des maîtres de cluster pour la haute disponibilité](cs_versions.html#ha-masters). Ces actions de préparation sont applicables dans les cas suivants :<ul>
<li>Si vous disposez d'un pare-feu ou de règles réseau Calico personnalisées.</li>
<li>Si vous utilisez les ports d'hôte `2040` ou `2041` sur vos noeuds worker.</li>
<li>Si vous avez utilisé l'adresse IP du noeud maître du cluster pour accéder au maître depuis le cluster.</li>
<li>Si vous disposez d'un processus automatique pour appeler l'API ou l'interface de ligne de commande Calico (`calicoctl`), par exemple pour créer des règles Calico.</li>
<li>Si vous utilisez des règles réseau Kubernetes ou Calico pour contrôler l'accès du trafic sortant du pod vers le maître.</li></ul></td>
</tr>
<tr>
<td>Proxy du maître de cluster HA</td>
<td>N/A</td>
<td>1.8.12-alpine</td>
<td>Ajout d'un pod `ibm-master-proxy-*` pour l'équilibrage de charge côté client sur tous les noeuds worker, de sort que chaque client de noeud worker puisse acheminer les demandes à une réplique de maître HA disponible.</td>
</tr>
<tr>
<td>etcd</td>
<td>v3.2.18</td>
<td>v3.3.1</td>
<td>Voir les [notes sur l'édition d'etcd ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/coreos/etcd/releases/v3.3.1).</td>
</tr>
<tr>
<td>Chiffrement des données dans etcd</td>
<td>N/A</td>
<td>N/A</td>
<td>Auparavant, les données etcd étaient stockées sur une instance de stockage de fichiers NFS d'un maître chiffrée au repos. Désormais, les données etcd sont stockées sur le disque local du maître et sauvegardées dans {{site.data.keyword.cos_full_notm}}. Les données sont chiffrées lors du transit vers {{site.data.keyword.cos_full_notm}} et au repos. Cependant, les données etcd sur le disque local du maître ne sont pas chiffrées. Si vous souhaitez que les données etcd locales de votre maître soient chiffrées, [activez {{site.data.keyword.keymanagementservicelong_notm}} dans votre cluster](cs_encrypt.html#keyprotect).</td>
</tr>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>v1.10.8-172</td>
<td>v1.10.8-197</td>
<td>Ajout de l'annotation `service.kubernetes.io/ibm-load-balancer-cloud-provider-vlan` pour spécifier le réseau local virtuel (VLAN) sur lequel est déployé le service d'équilibreur de charge. Pour voir les VLAN disponibles dans votre cluster, exécutez la commande `ibmcloud ks vlans --zone <zone>`.</td>
</tr>
<tr>
<td>Noyau avec puce TPM activée</td>
<td>N/A</td>
<td>N/A</td>
<td>Les noeuds worker bare metal avec des puces TPM pour la fonction de calcul sécurisé utilisent le noyau Ubuntu par défaut jusqu'à ce que la fonction de confiance (trust) soit activée. Si vous [activez la fonction de confiance](cs_cli_reference.html#cs_cluster_feature_enable) sur un cluster existant, vous devez [recharger](cs_cli_reference.html#cs_worker_reload) tous les noeuds worker bare metal existants avec des puces TPM. Pour vérifier si un noeud worker bare metal comporte une puce TPM, vérifiez la zone **Trustable** après avoir exécuté la [commande](cs_cli_reference.html#cs_machine_types) `ibmcloud ks machine-types --zone`.</td>
</tr>
</tbody>
</table>

### Journal des modifications de noeud worker - Groupe de correctifs 1.10.8_1528, publié le 26 octobre 2018
{: #1108_1528}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.10.8_1528. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.10.8_1527">
<caption>Modifications depuis la version 1.10.8_1527</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Traitement des interruptions du système d'exploitation</td>
<td>N/A</td>
<td>N/A</td>
<td>Remplacement du démon du système IRQ (Interrupt Request) avec un gestionnaire d'interruption plus performant.</td>
</tr>
</tbody>
</table>

### Journal des modifications du maître - Groupe de correctifs 1.10.8_1527, publié le 15 octobre 2018
{: #1108_1527}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs du maître 1.10.8_1527. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.10.8_1524">
<caption>Modifications depuis la version 1.10.8_1524</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Configuration de Calico</td>
<td>N/A</td>
<td>N/A</td>
<td>La sonde de conteneur Readiness Probe `calico-node` a été corrigée pour mieux traiter les défaillances de noeuds.</td>
</tr>
<tr>
<td>Mise à jour de cluster</td>
<td>N/A</td>
<td>N/A</td>
<td>Correction du problème de mise à jour des modules complémentaires de cluster lorsque le maître est mis à jour à partir d'une version non prise en charge.</td>
</tr>
</tbody>
</table>

### Journal des modifications de noeud worker - Groupe de correctifs 1.10.8_1525, publié le 10 octobre 2018
{: #1108_1525}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.10.8_1525. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.10.8_1524">
<caption>Modifications depuis la version 1.10.8_1524</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Noyau</td>
<td>4.4.0-133</td>
<td>4.4.0-137</td>
<td>Mise à jour des images de noeud worker avec la mise à jour du noyau pour [CVE-2018-14633, CVE-2018-17182 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://changelogs.ubuntu.com/changelogs/pool/main/l/linux/linux_4.4.0-137.163/changelog).</td>
</tr>
<tr>
<td>Délai d'inactivité de session</td>
<td>N/A</td>
<td>N/A</td>
<td>Le délai d'inactivité de session a été fixé à 5 minutes pour des raisons de conformité.</td>
</tr>
</tbody>
</table>


### Journal des modifications pour la version 1.10.8_1524, publié le 2 octobre 2018
{: #1108_1524}

Le tableau suivant présente les modifications incluses dans le correctif 1.10.8_1524. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.10.7_1520">
<caption>Modifications depuis la version 1.10.7_1520</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Fournisseur de service de gestion des clés (KMS)</td>
<td>N/A</td>
<td>N/A</td>
<td>Possibilité d'utiliser le service de gestion des clés (KMS) de Kubernetes dans le cluster pour prendre en charge {{site.data.keyword.keymanagementservicefull}}. Lorsque vous [activez {{site.data.keyword.keymanagementserviceshort}} dans votre cluster](cs_encrypt.html#keyprotect), toutes vos valeurs confidentielles (secrets) Kubernetes sont chiffrées.</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>v1.10.7</td>
<td>v1.10.8</td>
<td>Voir les [notes sur l'édition de Kubernetes![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/kubernetes/releases/tag/v1.10.8).</td>
</tr>
<tr>
<td>Mise à l'échelle automatique de DNS avec Kubernetes</td>
<td>1.1.2-r2</td>
<td>1.2.0</td>
<td>Voir les [notes sur l'édition de la fonction Kubernetes de mise à l'échelle automatique (autoscaler) de DNS ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes-incubator/cluster-proportional-autoscaler/releases/tag/1.2.0).</td>
</tr>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>v1.10.7-146</td>
<td>v1.10.8-172</td>
<td>Mise à jour pour prendre en charge l'édition Kubernetes 1.10.8. Avec en plus la mise à jour du lien vers la documentation dans les messages d'erreur de l'équilibreur de charge.</td>
</tr>
<tr>
<td>Classes de stockage de fichiers d'IBM</td>
<td>N/A</td>
<td>N/A</td>
<td>Suppression de `mountOptions` dans les classes de stockage de fichiers d'IBM afin d'utiliser la valeur par défaut fournie par le noeud worker. Suppression du paramètre `reclaimPolicy` en double dans les classes de stockage de fichiers d'IBM.<br><br>
Désormais, lorsque vous mettez à jour le noeud maître du cluster, la classe de stockage de fichiers d'IBM reste inchangée. Si vous souhaitez modifier la classe de stockage par défaut, exécutez la commande `kubectl patch storageclass <storageclass> -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'` et remplacez `<storageclass>` par le nom de la classe de stockage.</td>
</tr>
</tbody>
</table>

### Journal des modifications de noeud worker - Groupe de correctifs 1.10.7_1521, publié le 20 septembre 2018
{: #1107_1521}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.10.7_1521. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.10.7_1520">
<caption>Modifications depuis la version 1.10.7_1520</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Rotation des journaux</td>
<td>N/A</td>
<td>N/A</td>
<td>Passage à l'utilisation de fichiers timer `systemd` au lieu de travaux `cronjobs` pour empêcher l'échec de la rotation des journaux (`logrotate`) sur les noeuds worker qui ne sont pas rechargés ou mis à niveau dans les 90 jours. **Remarque** : dans toutes les versions antérieures à cette version secondaire, le disque principal se remplit après l'échec d'un travail cron car il est impossible de faire tourner les journaux. Le travail cron échoue lorsque le noeud worker est actif pendant une durée de 90 jours sans être mis à jour ou rechargé. Si les journaux remplissent la totalité du disque principal, le noeud worker passe à l'état d'échec. Le noeud worker peut être corrigé en exécutant la [commande](cs_cli_reference.html#cs_worker_reload) `ibmcloud ks worker-reload` ou la [commande](cs_cli_reference.html#cs_worker_update) `ibmcloud ks worker-update` .</td>
</tr>
<tr>
<td>Composants d'exécution de noeud worker (`kubelet`, `kube-proxy`, `docker`)</td>
<td>N/A</td>
<td>N/A</td>
<td>Suppression des dépendances des composants d'exécution sur le disque principal. Cette amélioration empêche l'échec des noeuds worker lorsque le disque principal est plein.</td>
</tr>
<tr>
<td>Expiration du mot de passe root</td>
<td>N/A</td>
<td>N/A</td>
<td>Les mots de passe root des noeuds worker expirent au bout de 90 jours pour des raisons de conformité. Si vos outils d'automatisation doivent se connecter au noeud worker en tant que root ou dépendent de travaux cron qui s'exécutent en tant que root, vous pouvez désactiver l'expiration du mot de passe en vous connectant au noeud worker et en exécutant la commande `chage -M -1 root`. **Remarque** : si vos exigences de conformité en matière de sécurité vous empêchent toute exécution en tant que root ou l'annulation de l'expiration du mot de passe, ne désactivez pas l'expiration. Vous pouvez à la place [mettre à jour](cs_cli_reference.html#cs_worker_update) ou [recharger](cs_cli_reference.html#cs_worker_reload) vos noeuds worker au moins tous les 90 jours.</td>
</tr>
<tr>
<td>Systemd</td>
<td>N/A</td>
<td>N/A</td>
<td>Nettoyage régulier des unités de montage transitoires pour leur éviter de devenir illimitées. Cette action corrige l'erreur [Kubernetes 57345 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/kubernetes/issues/57345).</td>
</tr>
<tr>
<td>Docker</td>
<td>N/A</td>
<td>N/A</td>
<td>Désactivation du pont Docker par défaut pour que la plage d'adresses IP `172.17.0.0/16` soit désormais utilisée pour les routes privées. Si vos conteneurs Docker doivent être construits en exécutant des commandes `docker` directement sur l'hôte ou en utilisant un pod qui monte le socket Docker, choisissez l'une des options suivantes.<ul><li>Pour assurer la connectivité avec le réseau externe lorsque vous construisez le conteneur, exécutez la commande `docker build . --network host`.</li>
<li>Pour créer de manière explicite un réseau à utiliser lorsque vous construisez le conteneur, exécutez la commande `docker network create`, puis utilisez ce réseau.</li></ul>
**Remarque** : vous avez des dépendances sur le socket Docker ou directement sur Docker ? [Effectuez une mise à jour pour passer à l'environnement d'exécution de conteneur `containerd` au lieu de `docker`](cs_versions.html#containerd) pour que vos clusters soient prêts à exécuter Kubernetes version 1.11 ou ultérieure.</td>
</tr>
</tbody>
</table>

### Journal des modifications pour la version 1.10.7_1520, publié le 4 septembre 2018
{: #1107_1520}

Le tableau suivant présente les modifications incluses dans le correctif 1.10.7_1520. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.10.5_1519">
<caption>Modifications depuis la version 1.10.5_1519</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Calico</td>
<td>v3.1.3</td>
<td>v3.2.1</td>
<td>Voir les [notes sur l'édition de Calico ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://docs.projectcalico.org/v3.2/releases/#v321).</td>
</tr>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>v1.10.5-118</td>
<td>v1.10.7-146</td>
<td>Mise à jour pour prendre en charge l'édition Kubernetes 1.10.7. En outre, la configuration du fournisseur de cloud a changé pour mieux gérer les mises à jour des services d'équilibreur de charge avec l'élément `externalTrafficPolicy` défini sur `local`.</td>
</tr>
<tr>
<td>Plug-in IBM File Storage</td>
<td>334</td>
<td>338</td>
<td>Mise à jour d'incubateur à la version 1.8. Le stockage de fichiers est mis à disposition dans la zone spécifique que vous sélectionnez. Vous ne pouvez pas mettre à jour des libellés d'une instance de volume persistant (statique) existante, à moins d'utiliser un cluster à zones multiples et de nécessiter l'ajout de libellés de région et de zone.<br><br> La version NFS par défaut a été supprimée des options de montage dans les classes de stockage de fichiers fournies par IBM. Désormais, le système d'exploitation de l'hôte négocie la version NFS avec le serveur NFS de l'infrastructure IBM Cloud (SoftLayer). Pour définir manuellement une version NFS spécifique ou modifier la version NFS de votre volume persistant qui a été négociée par le système d'exploitation de l'hôte, voir [Modification de la version NFS par défaut](cs_storage_file.html#nfs_version_class).</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>v1.10.5</td>
<td>v1.10.7</td>
<td>Voir les [notes sur l'édition de Kubernetes ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/kubernetes/releases/tag/v1.10.7).</td>
</tr>
<tr>
<td>Configuration de Kubernetes Heapster</td>
<td>N/A</td>
<td>N/A</td>
<td>Augmentation des limites de ressources pour le conteneur `heapster-nanny`.</td>
</tr>
</tbody>
</table>

### Journal des modifications de noeud worker - Groupe de correctifs 1.10.5_1519, publié le 23 août 2018
{: #1105_1519}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.10.5_1519. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.10.5_1518">
<caption>Modifications depuis la version 1.10.5_1518</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>`systemd`</td>
<td>229</td>
<td>230</td>
<td>Mise à jour de `systemd` pour corriger la fuite liée à `cgroup`.</td>
</tr>
<tr>
<td>Noyau</td>
<td>4.4.0-127</td>
<td>4.4.0-133</td>
<td>Mise à jour des images de noeud worker avec la mise à jour du noyau pour [CVE-2018-3620, CVE-2018-3646 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://usn.ubuntu.com/3741-1/).</td>
</tr>
</tbody>
</table>


### Journal des modifications de noeud worker - Groupe de correctifs 1.10.5_1518, publié le 13 août 2018
{: #1105_1518}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.10.5_1518. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.10.5_1517">
<caption>Modifications depuis la version 1.10.5_1517</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Packages Ubuntu</td>
<td>N/A</td>
<td>N/A</td>
<td>Mises à jour des packages Ubuntu installés.</td>
</tr>
</tbody>
</table>

### Journal des modifications pour la version 1.10.5_1517, publié le 27 juillet 2018
{: #1105_1517}

Le tableau suivant présente les modifications incluses dans le correctif 1.10.5_1517. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.10.3_1514">
<caption>Modifications depuis la version 1.10.3_1514</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Calico</td>
<td>v3.1.1</td>
<td>v3.1.3</td>
<td>Voir les [notes sur l'édition de Calico ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://docs.projectcalico.org/v3.1/releases/#v313).</td>
</tr>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>v1.10.3-85</td>
<td>v1.10.5-118</td>
<td>Mise à jour pour prendre en charge l'édition Kubernetes 1.10.5. En outre, les événements `create failure` du service LoadBalancer incluent désormais toutes les erreurs des sous-réseaux portables.</td>
</tr>
<tr>
<td>Plug-in IBM File Storage</td>
<td>320</td>
<td>334</td>
<td>Le délai de création d'un volume persistant a augmenté pour passer de 15 à 30 minutes. Le type de facturation par défaut a été changé pour passer à une facturation à l'heure (`hourly`). Des options de montage ont été ajoutées aux classes de stockage prédéfinies. Dans l'instance de stockage de fichiers NFS dans votre compte d'infrastructure IBM Cloud (SoftLayer), la zone **Notes** est désormais au format JSON et l'espace de nom Kubernetes dans lequel le volume persistant est déployé a été ajouté. Pour prendre en charge les clusters à zones multiples, des libellés de zone et de région ont été ajoutés pour les volumes persistants.</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>v1.10.3</td>
<td>v1.10.5</td>
<td>Voir les [notes sur l'édition de Kubernetes ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/kubernetes/releases/tag/v1.10.5).</td>
</tr>
<tr>
<td>Noyau</td>
<td>N/A</td>
<td>N/A</td>
<td>De légères améliorations ont été apportées aux paramètres réseau des noeuds worker pour les charges de travail réseau à hautes performances.</td>
</tr>
<tr>
<td>Client OpenVPN</td>
<td>N/A</td>
<td>N/A</td>
<td>Le déploiement du `vpn` du client OpenVPN qui s'exécute dans l'espace de nom `kube-system` est désormais géré par le gestionnaire `addon-manager` de Kubernetes.</td>
</tr>
</tbody>
</table>

### Journal des modifications de noeud worker - Groupe de correctifs 1.10.3_1514, publié le 3 juillet 2018
{: #1103_1514}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.10.3_1514. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.10.3_1513">
<caption>Modifications depuis la version 1.10.3_1513</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Noyau</td>
<td>N/A</td>
<td>N/A</td>
<td>Optimisation de `sysctl` pour les charges de travail réseau hautes performances.</td>
</tr>
</tbody>
</table>


### Journal des modifications de noeud worker - Groupe de correctifs 1.10.3_1513, publié le 21 juin 2018
{: #1103_1513}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.10.3_1513. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.10.3_1512">
<caption>Modifications depuis la version 1.10.3_1512</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Docker</td>
<td>N/A</td>
<td>N/A</td>
<td>Pour les types de machine non chiffrés, le disque secondaire est nettoyé en obtenant un nouveau système de fichiers lors du rechargement ou de la mise à jour du noeud worker.</td>
</tr>
</tbody>
</table>

### Journal des modifications pour la version 1.10.3_1512, publié le 12 juin 2018
{: #1103_1512}

Le tableau suivant présente les modifications incluses dans le correctif 1.10.3_1512. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.10.1_1510">
<caption>Modifications depuis la version 1.10.1_1510</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubernetes</td>
<td>v1.10.1</td>
<td>v1.10.3</td>
<td>Voir les [notes sur l'édition de Kubernetes ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/kubernetes/releases/tag/v1.10.3).</td>
</tr>
<tr>
<td>Configuration de Kubernetes</td>
<td>N/A</td>
<td>N/A</td>
<td>Ajout de `PodSecurityPolicy` dans l'option `--enable-admission-plugins` pour le serveur d'API Kubernetes du cluster et configuration du cluster pour prendre en charge les politiques de sécurité de pod. Pour plus d'informations, voir [Configuration de politiques de sécurité de pod](cs_psp.html).</td>
</tr>
<tr>
<td>Configuration de Kubelet</td>
<td>N/A</td>
<td>N/A</td>
<td>L'option `--authentication-token-webhook` a été activée pour prendre en charge les jetons porteur pour API et les jetons de compte de service pour l'authentification avec le noeud final HTTPS `kubelet`.</td>
</tr>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>v1.10.1-52</td>
<td>v1.10.3-85</td>
<td>Mise à jour pour prendre en charge l'édition Kubernetes 1.10.3.</td>
</tr>
<tr>
<td>Client OpenVPN</td>
<td>N/A</td>
<td>N/A</td>
<td>Ajout de `livenessProbe` dans le déploiement du `vpn` du client OpenVPN qui s'exécute dans l'espace de nom `kube-system`.</td>
</tr>
<tr>
<td>Mise à jour du noyau</td>
<td>4.4.0-116</td>
<td>4.4.0-127</td>
<td>Mise à jour des images de noeud worker avec la mise à jour du noyau pour [CVE-2018-3639 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-3639).</td>
</tr>
</tbody>
</table>



### Journal des modifications de noeud worker - Groupe de correctifs 1.10.1_1510, publié le 18 mai 2018
{: #1101_1510}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.10.1_1510. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.10.1_1509">
<caption>Modifications depuis la version 1.10.1_1509</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubelet</td>
<td>N/A</td>
<td>N/A</td>
<td>Correctif pour résoudre un bogue qui se produisait lorsque vous utilisiez le plug-in de stockage par blocs.</td>
</tr>
</tbody>
</table>

### Journal des modifications de noeud worker - Groupe de correctifs 1.10.1_1509, publié le 16 mai 2018
{: #1101_1509}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.10.1_1509. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.10.1_1508">
<caption>Modifications depuis la version 1.10.1_1508</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubelet</td>
<td>N/A</td>
<td>N/A</td>
<td>Les données que vous stockez dans le répertoire racine `kubelet` sont désormais sauvegardées dans un disque secondaire plus volumineux de la machine du noeud worker.</td>
</tr>
</tbody>
</table>

### Journal des modifications pour la version 10. 1_1508, publié le 1er mai 2018
{: #1101_1508}

Le tableau suivant présente les modifications incluses dans le correctif 1.10.1_1508. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.9.7_1510">
<caption>Modifications depuis la version 1.9.7_1510</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Calico</td>
<td>v2.6.5</td>
<td>v3.1.1</td>
<td>Voir les [notes sur l'édition de Calico ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://docs.projectcalico.org/v3.1/releases/#v311).</td>
</tr>
<tr>
<td>Kubernetes Heapster</td>
<td>v1.5.0</td>
<td>v1.5.2</td>
<td>Voir les [notes sur l'édition de Kubernetes Heapster ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/heapster/releases/tag/v1.5.2).</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>v1.9.7</td>
<td>v1.10.1</td>
<td>Voir les [notes sur l'édition de Kubernetes ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/kubernetes/releases/tag/v1.10.1).</td>
</tr>
<tr>
<td>Configuration de Kubernetes</td>
<td>N/A</td>
<td>N/A</td>
<td>Ajout de <code>StorageObjectInUseProtection</code> à l'option <code>--enable-admission-plugins</code> pour le serveur d'API Kubernetes du cluster.</td>
</tr>
<tr>
<td>Kubernetes DNS</td>
<td>1.14.8</td>
<td>1.14.10</td>
<td>Voir les [notes sur l'édition de Kubernetes DNS ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/dns/releases/tag/1.14.10).</td>
</tr>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>v1.9.7-102</td>
<td>v1.10.1-52</td>
<td>Mis à jour pour prendre en charge la version Kubernetes 1.10.</td>
</tr>
<tr>
<td>Prise en charge de GPU</td>
<td>N/A</td>
<td>N/A</td>
<td>La prise en charge des [charges de travail de conteneur d'unité de traitement graphique (GPU)](cs_app.html#gpu_app) est désormais disponible pour la planification et l'exécution. Pour obtenir la liste des types de machine GPU disponibles, voir [Matériel pour les noeuds worker](cs_clusters_planning.html#shared_dedicated_node). Pour plus d'informations, voir la documentation Kubernetes relative à la [planification d'unités GPU ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://kubernetes.io/docs/tasks/manage-gpus/scheduling-gpus/).</td>
</tr>
</tbody>
</table>

<br />


## Archive
{: #changelog_archive}

Versions de Kubernetes non prises en charge :
*  [Version 1.9](#19_changelog)
*  [Version 1.8](#18_changelog)
*  [Version 1.7](#17_changelog)

### Journal des modifications pour la version 1.9 (dépréciée, non prise en charge depuis le 27 décembre 2018)
{: #19_changelog}

Passez en revue le journal des modifications de la version 1.9.

### Journal des modifications de noeud worker - Groupe de correctifs 1.9.11_1538, publié le 4 décembre 2018
{: #1911_1538}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.9.11_1538.
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.9.11_1537">
<caption>Modifications depuis la version 1.9.11_1537</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Utilisation des ressources de noeud worker</td>
<td>N/A</td>
<td>N/A</td>
<td>Ajout de groupes cgroups pour le kubelet et docker pour empêcher ces composants d'être à court de ressources. Pour plus d'informations, voir [Réserves de ressources de noeud worker](cs_clusters_planning.html#resource_limit_node).</td>
</tr>
</tbody>
</table>

### Journal des modifications de noeud worker - Groupe de correctifs 1.9.11_1537, publié le 27 novembre 2018
{: #1911_1537}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.9.11_1537.
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.9.11_1536">
<caption>Modifications depuis la version 1.9.11_1536</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Docker</td>
<td>17.06.2</td>
<td>18.06.1</td>
<td>Voir les [notes sur l'édition de Docker ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://docs.docker.com/engine/release-notes/#18061-ce).</td>
</tr>
</tbody>
</table>

### Journal des modifications pour la version 1.9.11_1536, publié le 19 novembre 2018
{: #1911_1536}

Le tableau suivant présente les modifications incluses dans le correctif 1.9.11_1536. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.9.10_1532">
<caption>Modifications depuis la version 1.9.10_1532</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Calico</td>
<td>v2.6.5</td>
<td>v2.6.12</td>
<td>Voir les [notes sur l'édition de Calico ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://docs.projectcalico.org/v2.6/releases/#v2612). La mise à jour résout [Tigera Technical Advisory TTA-2018-001 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.projectcalico.org/security-bulletins/).</td>
</tr>
<tr>
<td>Noyau</td>
<td>4.4.0-137</td>
<td>4.4.0-139</td>
<td>Mise à jour des images de noeud worker avec la mise à jour du noyau pour [CVE-2018-7755 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://changelogs.ubuntu.com/changelogs/pool/main/l/linux/linux_4.4.0-139.165/changelog).</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>v1.9.10</td>
<td>v1.9.11</td>
<td>Voir les [notes sur l'édition de Kubernetes ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/kubernetes/releases/tag/v1.9.11).</td>
</tr>
<tr>
<td>{{site.data.keyword.Bluemix_notm}}</td>
<td>v1.9.10-219</td>
<td>v1.9.11-249</td>
<td>Mise à jour pour prendre en charge l'édition Kubernetes 1.9.11.</td>
</tr>
<tr>
<td>Serveur et client OpenVPN</td>
<td>2.4.4-r2</td>
<td>2.4.6-r3-IKS-8</td>
<td>Mise à jour d'une image pour [CVE-2018-0732 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-0732) et [CVE-2018-0737 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-0737).</td>
</tr>
</tbody>
</table>

### Journal des modifications de noeud worker - Groupe de correctifs 1.9.10_1532, publié le 7 novembre 2018
{: #1910_1532}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.9.11_1532. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.9.10_1531">
<caption>Modifications depuis la version 1.9.10_1531</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Noyau avec puce TPM activée</td>
<td>N/A</td>
<td>N/A</td>
<td>Les noeuds worker bare metal avec des puces TPM pour la fonction de calcul sécurisé utilisent le noyau Ubuntu par défaut jusqu'à ce que la fonction de confiance (trust) soit activée. Si vous [activez la fonction de confiance](cs_cli_reference.html#cs_cluster_feature_enable) sur un cluster existant, vous devez [recharger](cs_cli_reference.html#cs_worker_reload) tous les noeuds worker bare metal existants avec des puces TPM. Pour vérifier si un noeud worker bare metal comporte une puce TPM, vérifiez la zone **Trustable** après avoir exécuté la [commande](cs_cli_reference.html#cs_machine_types) `ibmcloud ks machine-types --zone`.</td>
</tr>
</tbody>
</table>

### Journal des modifications de noeud worker - Groupe de correctifs 1.9.10_1531, publié le 26 octobre 2018
{: #1910_1531}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.9.10_1531. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.9.10_1530">
<caption>Modifications depuis la version 1.9.10_1530</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Traitement des interruptions du système d'exploitation</td>
<td>N/A</td>
<td>N/A</td>
<td>Remplacement du démon du système IRQ (Interrupt Request) avec un gestionnaire d'interruption plus performant.</td>
</tr>
</tbody>
</table>

### Journal des modifications du maître - Groupe de correctifs 1.9.10_1530, publié le 15 octobre 2018
{: #1910_1530}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.9.10_1530. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.9.10_1527">
<caption>Modifications depuis la version 1.9.10_1527</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Mise à jour de cluster</td>
<td>N/A</td>
<td>N/A</td>
<td>Correction du problème de mise à jour des modules complémentaires de cluster lorsque le maître est mis à jour à partir d'une version non prise en charge.</td>
</tr>
</tbody>
</table>

### Journal des modifications de noeud worker - Groupe de correctifs 1.9.10_1528, publié le 10 octobre 2018
{: #1910_1528}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.9.10_1528. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.9.10_1527">
<caption>Modifications depuis la version 1.9.10_1527</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Noyau</td>
<td>4.4.0-133</td>
<td>4.4.0-137</td>
<td>Mise à jour des images de noeud worker avec la mise à jour du noyau pour [CVE-2018-14633, CVE-2018-17182 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://changelogs.ubuntu.com/changelogs/pool/main/l/linux/linux_4.4.0-137.163/changelog).</td>
</tr>
<tr>
<td>Délai d'inactivité de session</td>
<td>N/A</td>
<td>N/A</td>
<td>Le délai d'inactivité de session a été fixé à 5 minutes pour des raisons de conformité.</td>
</tr>
</tbody>
</table>


### Journal des modifications pour la version 1.9.10_1527, publié le 2 octobre 2018
{: #1910_1527}

Le tableau suivant présente les modifications incluses dans le correctif 1.9.10_1527. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.9.10_1523">
<caption>Modifications depuis la version 1.9.10_1523</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>v1.9.10-192</td>
<td>v1.9.10-219</td>
<td>Mise à jour du lien vers la documentation dans les messages d'erreur de l'équilibreur de charge.</td>
</tr>
<tr>
<td>Classes de stockage de fichiers d'IBM</td>
<td>N/A</td>
<td>N/A</td>
<td>Suppression de `mountOptions` dans les classes de stockage de fichiers d'IBM afin d'utiliser la valeur par défaut fournie par le noeud worker. Suppression du paramètre `reclaimPolicy` en double dans les classes de stockage de fichiers d'IBM.<br><br>
Désormais, lorsque vous mettez à jour le noeud maître du cluster, la classe de stockage de fichiers d'IBM reste inchangée. Si vous souhaitez modifier la classe de stockage par défaut, exécutez la commande `kubectl patch storageclass <storageclass> -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'` et remplacez `<storageclass>` par le nom de la classe de stockage.</td>
</tr>
</tbody>
</table>

### Journal des modifications de noeud worker - Groupe de correctifs 1.9.10_1524, publié le 20 septembre 2018
{: #1910_1524}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.9.10_1524. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.9.10_1523">
<caption>Modifications depuis la version 1.9.10_1523</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Rotation des journaux</td>
<td>N/A</td>
<td>N/A</td>
<td>Passage à l'utilisation de fichiers timer `systemd` au lieu de travaux `cronjobs` pour empêcher l'échec de la rotation des journaux (`logrotate`) sur les noeuds worker qui ne sont pas rechargés ou mis à niveau dans les 90 jours. **Remarque** : dans toutes les versions antérieures à cette version secondaire, le disque principal se remplit après l'échec d'un travail cron car il est impossible de faire tourner les journaux. Le travail cron échoue lorsque le noeud worker est actif pendant une durée de 90 jours sans être mis à jour ou rechargé. Si les journaux remplissent la totalité du disque principal, le noeud worker passe à l'état d'échec. Le noeud worker peut être corrigé en exécutant la [commande](cs_cli_reference.html#cs_worker_reload) `ibmcloud ks worker-reload` ou la [commande](cs_cli_reference.html#cs_worker_update) `ibmcloud ks worker-update` .</td>
</tr>
<tr>
<td>Composants d'exécution de noeud worker (`kubelet`, `kube-proxy`, `docker`)</td>
<td>N/A</td>
<td>N/A</td>
<td>Suppression des dépendances des composants d'exécution sur le disque principal. Cette amélioration empêche l'échec des noeuds worker lorsque le disque principal est plein.</td>
</tr>
<tr>
<td>Expiration du mot de passe root</td>
<td>N/A</td>
<td>N/A</td>
<td>Les mots de passe root des noeuds worker expirent au bout de 90 jours pour des raisons de conformité. Si vos outils d'automatisation doivent se connecter au noeud worker en tant que root ou dépendent de travaux cron qui s'exécutent en tant que root, vous pouvez désactiver l'expiration du mot de passe en vous connectant au noeud worker et en exécutant la commande `chage -M -1 root`. **Remarque** : si vos exigences de conformité en matière de sécurité vous empêchent toute exécution en tant que root ou l'annulation de l'expiration du mot de passe, ne désactivez pas l'expiration. Vous pouvez à la place [mettre à jour](cs_cli_reference.html#cs_worker_update) ou [recharger](cs_cli_reference.html#cs_worker_reload) vos noeuds worker au moins tous les 90 jours.</td>
</tr>
<tr>
<td>Systemd</td>
<td>N/A</td>
<td>N/A</td>
<td>Nettoyage régulier des unités de montage transitoires pour leur éviter de devenir illimitées. Cette action corrige l'erreur [Kubernetes 57345 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/kubernetes/issues/57345).</td>
</tr>
<tr>
<td>Docker</td>
<td>N/A</td>
<td>N/A</td>
<td>Désactivation du pont Docker par défaut pour que la plage d'adresses IP `172.17.0.0/16` soit désormais utilisée pour les routes privées. Si vos conteneurs Docker doivent être construits en exécutant des commandes `docker` directement sur l'hôte ou en utilisant un pod qui monte le socket Docker, choisissez l'une des options suivantes.<ul><li>Pour assurer la connectivité avec le réseau externe lorsque vous construisez le conteneur, exécutez la commande `docker build . --network host`.</li>
<li>Pour créer de manière explicite un réseau à utiliser lorsque vous construisez le conteneur, exécutez la commande `docker network create`, puis utilisez ce réseau.</li></ul>
**Remarque** : vous avez des dépendances sur le socket Docker ou directement sur Docker ? [Effectuez une mise à jour pour passer à l'environnement d'exécution de conteneur `containerd` au lieu de `docker`](cs_versions.html#containerd) pour que vos clusters soient prêts à exécuter Kubernetes version 1.11 ou ultérieure.</td>
</tr>
</tbody>
</table>

### Journal des modifications pour la version 1.9.10_1523, publié le 4 septembre 2018
{: #1910_1523}

Le tableau suivant présente les modifications incluses dans le correctif 1.9.10_1523. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.9.9_1522">
<caption>Modifications depuis la version 1.9.9_1522</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>v1.9.9-167</td>
<td>v1.9.10-192</td>
<td>Mise à jour pour prendre en charge l'édition Kubernetes 1.9.10. En outre, la configuration du fournisseur de cloud a changé pour mieux gérer les mises à jour des services d'équilibreur de charge avec l'élément `externalTrafficPolicy` défini sur `local`.</td>
</tr>
<tr>
<td>Plug-in IBM File Storage</td>
<td>334</td>
<td>338</td>
<td>Mise à jour d'incubateur à la version 1.8. Le stockage de fichiers est mis à disposition dans la zone spécifique que vous sélectionnez. Vous ne pouvez pas mettre à jour des libellés d'une instance de volume persistant (statique) existante, à moins d'utiliser un cluster à zones multiples et de nécessiter l'ajout de libellés de région et de zone.<br><br>La version NFS par défaut a été supprimée des options de montage dans les classes de stockage de fichiers fournies par IBM. Désormais, le système d'exploitation de l'hôte négocie la version NFS avec le serveur NFS de l'infrastructure IBM Cloud (SoftLayer). Pour définir manuellement une version NFS spécifique ou modifier la version NFS de votre volume persistant qui a été négociée par le système d'exploitation de l'hôte, voir [Modification de la version NFS par défaut](cs_storage_file.html#nfs_version_class).</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>v1.9.9</td>
<td>v1.9.10</td>
<td>Voir les [notes sur l'édition de Kubernetes ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/kubernetes/releases/tag/v1.9.10).</td>
</tr>
<tr>
<td>Configuration de Kubernetes Heapster</td>
<td>N/A</td>
<td>N/A</td>
<td>Augmentation des limites de ressources pour le conteneur `heapster-nanny`.</td>
</tr>
</tbody>
</table>

### Journal des modifications de noeud worker - Groupe de correctifs 1.9.9_1522, publié le 23 août 2018
{: #199_1522}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.9.9_1522. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.9.9_1521">
<caption>Modifications depuis la version 1.9.9_1521</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>`systemd`</td>
<td>229</td>
<td>230</td>
<td>Mise à jour de `systemd` pour corriger la fuite liée à `cgroup`.</td>
</tr>
<tr>
<td>Noyau</td>
<td>4.4.0-127</td>
<td>4.4.0-133</td>
<td>Mise à jour des images de noeud worker avec la mise à jour du noyau pour [CVE-2018-3620, CVE-2018-3646 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://usn.ubuntu.com/3741-1/).</td>
</tr>
</tbody>
</table>


### Journal des modifications de noeud worker - Groupe de correctifs 1.9.9_1521, publié le 13 août 2018
{: #199_1521}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.9.9_1521. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.9.9_1520">
<caption>Modifications depuis la version 1.9.9_1520</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Packages Ubuntu</td>
<td>N/A</td>
<td>N/A</td>
<td>Mises à jour des packages Ubuntu installés.</td>
</tr>
</tbody>
</table>

### Journal des modifications pour la version 1.9.9_1520, publié le 27 juillet 2018
{: #199_1520}

Le tableau suivant présente les modifications incluses dans le correctif 1.9.9_1520. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.9.8_1517">
<caption>Modifications depuis la version 1.9.8_1517</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>v1.9.8-141</td>
<td>v1.9.9-167</td>
<td>Mise à jour pour prendre en charge l'édition Kubernetes 1.9.9. En outre, les événements `create failure` du service LoadBalancer incluent désormais toutes les erreurs des sous-réseaux portables.</td>
</tr>
<tr>
<td>Plug-in IBM File Storage</td>
<td>320</td>
<td>334</td>
<td>Le délai de création d'un volume persistant a augmenté pour passer de 15 à 30 minutes. Le type de facturation par défaut a été changé pour passer à une facturation à l'heure (`hourly`). Des options de montage ont été ajoutées aux classes de stockage prédéfinies. Dans l'instance de stockage de fichiers NFS dans votre compte d'infrastructure IBM Cloud (SoftLayer), la zone **Notes** est désormais au format JSON et l'espace de nom Kubernetes dans lequel le volume persistant est déployé a été ajouté. Pour prendre en charge les clusters à zones multiples, des libellés de zone et de région ont été ajoutés pour les volumes persistants.</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>v1.9.8</td>
<td>v1.9.9</td>
<td>Voir les [notes sur l'édition de Kubernetes ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/kubernetes/releases/tag/v1.9.9).</td>
</tr>
<tr>
<td>Noyau</td>
<td>N/A</td>
<td>N/A</td>
<td>De légères améliorations ont été apportées aux paramètres réseau des noeuds worker pour les charges de travail réseau à hautes performances.</td>
</tr>
<tr>
<td>Client OpenVPN</td>
<td>N/A</td>
<td>N/A</td>
<td>Le déploiement du `vpn` du client OpenVPN qui s'exécute dans l'espace de nom `kube-system` est désormais géré par le gestionnaire `addon-manager` de Kubernetes.</td>
</tr>
</tbody>
</table>

### Journal des modifications de noeud worker - Groupe de correctifs 1.9.8_1517, publié le 3 juillet 2018
{: #198_1517}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.9.8_1517. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.9.8_1516">
<caption>Modifications depuis la version 1.9.8_1516</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Noyau</td>
<td>N/A</td>
<td>N/A</td>
<td>Optimisation de `sysctl` pour les charges de travail réseau hautes performances.</td>
</tr>
</tbody>
</table>


### Journal des modifications de noeud worker - Groupe de correctifs 1.9.8_1516, publié le 21 juin 2018
{: #198_1516}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.9.8_1516. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.9.8_1515">
<caption>Modifications depuis la version 1.9.8_1515</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Docker</td>
<td>N/A</td>
<td>N/A</td>
<td>Pour les types de machine non chiffrés, le disque secondaire est nettoyé en obtenant un nouveau système de fichiers lors du rechargement ou de la mise à jour du noeud worker.</td>
</tr>
</tbody>
</table>

### Journal des modifications pour la version 1.9.8_1515, publié le 19 juin 2018
{: #198_1515}

Le tableau suivant présente les modifications incluses dans le correctif 1.9.8_1515. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.9.7_1513">
<caption>Modifications depuis la version 1.9.7_1513</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubernetes</td>
<td>v1.9.7</td>
<td>v1.9.8</td>
<td>Voir les [notes sur l'édition de Kubernetes![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/kubernetes/releases/tag/v1.9.8).</td>
</tr>
<tr>
<td>Configuration de Kubernetes</td>
<td>N/A</td>
<td>N/A</td>
<td>Ajout de PodSecurityPolicy dans l'option --admission-control pour le serveur d'API Kubernetes du cluster et configuration du cluster pour prendre en charge les politiques de sécurité de pod. Pour plus d'informations, voir [Configuration de politiques de sécurité de pod](cs_psp.html).</td>
</tr>
<tr>
<td>IBM Cloud Provider</td>
<td>v1.9.7-102</td>
<td>v1.9.8-141</td>
<td>Mise à jour pour prendre en charge l'édition Kubernetes 1.9.8.</td>
</tr>
<tr>
<td>Client OpenVPN</td>
<td>N/A</td>
<td>N/A</td>
<td>Ajout de <code>livenessProbe</code> dans le déploiement du <code>vpn</code> du client OpenVPN qui s'exécute dans l'espace de nom <code>kube-system</code>.</td>
</tr>
</tbody>
</table>


### Journal des modifications de noeud worker - Groupe de correctifs 1.9.7_1513, publié le 11 juin 2018
{: #197_1513}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.9.7_1513. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.9.7_1512">
<caption>Modifications depuis la version 1.9.7_1512</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Mise à jour du noyau</td>
<td>4.4.0-116</td>
<td>4.4.0-127</td>
<td>Mise à jour des images de noeud worker avec la mise à jour du noyau pour [CVE-2018-3639 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-3639).</td>
</tr>
</tbody>
</table>

### Journal des modifications de noeud worker - Groupe de correctifs 1.9.7_1512, publié le 18 mai 2018
{: #197_1512}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.9.7_1512. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.9.7_1511">
<caption>Modifications depuis la version 1.9.7_1511</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubelet</td>
<td>N/A</td>
<td>N/A</td>
<td>Correctif pour résoudre un bogue qui se produisait lorsque vous utilisiez le plug-in de stockage par blocs.</td>
</tr>
</tbody>
</table>

### Journal des modifications de noeud worker - Groupe de correctifs 1.9.7_1511, publié le 16 mai 2018
{: #197_1511}

Le tableau suivant présente les modifications incluses dans le groupe de correctifs de noeud worker 1.9.7_1511. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.9.7_1510">
<caption>Modifications depuis la version 1.9.7_1510</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubelet</td>
<td>N/A</td>
<td>N/A</td>
<td>Les données que vous stockez dans le répertoire racine `kubelet` sont désormais sauvegardées dans un disque secondaire plus volumineux de la machine du noeud worker.</td>
</tr>
</tbody>
</table>

### Journal des modifications pour la version 1.9.7_1510, publié le 30 avril 2018
{: #197_1510}

Le tableau suivant présente les modifications incluses dans le correctif 1.9.7_1510. 
{: shortdesc}

<table summary="Modifications effectuées depuis la version 1.9.3_1506">
<caption>Modifications depuis la version 1.9.3_1506</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubernetes</td>
<td>v1.9.3</td>
<td>v1.9.7	</td>
<td><p>Voir les [notes sur l'édition de Kubernetes![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/kubernetes/releases/tag/v1.9.7). Cette édition traite les vulnérabilités [CVE-2017-1002101 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-1002101) et [CVE-2017-1002102 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-1002102).</p><p><strong>Remarque</strong> : désormais les éléments `secret`, `configMap`, `downwardAPI` et les volumes projetés sont montés en lecture seule. Auparavant, les applications pouvaient écrire des données dans ces volumes, mais le système pouvait les rétablir automatiquement. Si vos applications s'appuient sur ce comportement peu fiable en matière de sécurité, modifiez-les en conséquence.</p></td>
</tr>
<tr>
<td>Configuration de Kubernetes</td>
<td>N/A</td>
<td>N/A</td>
<td>Ajout de `admissionregistration.k8s.io/v1alpha1=true` à l'option `--runtime-config` pour le serveur d'API Kubernetes du cluster.</td>
</tr>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>v1.9.3-71</td>
<td>v1.9.7-102</td>
<td>Les services `NodePort` et `LoadBalancer` prennent désormais en charge la [conservation de l'adresse IP source du client](cs_loadbalancer.html#node_affinity_tolerations) en définissant l'élément `service.spec.externalTrafficPolicy` sur `Local`.</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>Correction de la configuration de tolérance des [noeuds de périphérie](cs_edge.html#edge) pour les clusters plus anciens.</td>
</tr>
</tbody>
</table>

<br />


### Journal des modifications pour la version 1.8 (non prise en charge)
{: #18_changelog}

Passez en revue les modifications suivantes.

### Journal des modifications de noeud worker - Groupe de correctifs 1.8.15_1521, publié le 20 septembre 2018
{: #1815_1521}

<table summary="Modifications effectuées depuis la version 1.8.15_1520">
<caption>Modifications depuis la version 1.8.15_1520</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Rotation des journaux</td>
<td>N/A</td>
<td>N/A</td>
<td>Passage à l'utilisation de fichiers timer `systemd` au lieu de travaux `cronjobs` pour empêcher l'échec de la rotation des journaux (`logrotate`) sur les noeuds worker qui ne sont pas rechargés ou mis à niveau dans les 90 jours. **Remarque** : dans toutes les versions antérieures à cette version secondaire, le disque principal se remplit après l'échec d'un travail cron car il est impossible de faire tourner les journaux. Le travail cron échoue lorsque le noeud worker est actif pendant une durée de 90 jours sans être mis à jour ou rechargé. Si les journaux remplissent la totalité du disque principal, le noeud worker passe à l'état d'échec. Le noeud worker peut être corrigé en exécutant la [commande](cs_cli_reference.html#cs_worker_reload) `ibmcloud ks worker-reload` ou la [commande](cs_cli_reference.html#cs_worker_update) `ibmcloud ks worker-update` .</td>
</tr>
<tr>
<td>Composants d'exécution de noeud worker (`kubelet`, `kube-proxy`, `docker`)</td>
<td>N/A</td>
<td>N/A</td>
<td>Suppression des dépendances des composants d'exécution sur le disque principal. Cette amélioration empêche l'échec des noeuds worker lorsque le disque principal est plein.</td>
</tr>
<tr>
<td>Expiration du mot de passe root</td>
<td>N/A</td>
<td>N/A</td>
<td>Les mots de passe root des noeuds worker expirent au bout de 90 jours pour des raisons de conformité. Si vos outils d'automatisation doivent se connecter au noeud worker en tant que root ou dépendent de travaux cron qui s'exécutent en tant que root, vous pouvez désactiver l'expiration du mot de passe en vous connectant au noeud worker et en exécutant la commande `chage -M -1 root`. **Remarque** : si vos exigences de conformité en matière de sécurité vous empêchent toute exécution en tant que root ou l'annulation de l'expiration du mot de passe, ne désactivez pas l'expiration. Vous pouvez à la place [mettre à jour](cs_cli_reference.html#cs_worker_update) ou [recharger](cs_cli_reference.html#cs_worker_reload) vos noeuds worker au moins tous les 90 jours.</td>
</tr>
<tr>
<td>Systemd</td>
<td>N/A</td>
<td>N/A</td>
<td>Nettoyage régulier des unités de montage transitoires pour leur éviter de devenir illimitées. Cette action corrige l'erreur [Kubernetes 57345 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/kubernetes/issues/57345).</td>
</tr>
</tbody>
</table>

### Journal des modifications de noeud worker - Groupe de correctifs 1.8.15_1520, publié le 23 août 2018
{: #1815_1520}

<table summary="Modifications effectuées depuis la version 1.8.15_1519">
<caption>Modifications depuis la version 1.8.15_1519</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>`systemd`</td>
<td>229</td>
<td>230</td>
<td>Mise à jour de `systemd` pour corriger la fuite liée à `cgroup`.</td>
</tr>
<tr>
<td>Noyau</td>
<td>4.4.0-127</td>
<td>4.4.0-133</td>
<td>Mise à jour des images de noeud worker avec la mise à jour du noyau pour [CVE-2018-3620, CVE-2018-3646 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://usn.ubuntu.com/3741-1/).</td>
</tr>
</tbody>
</table>

### Journal des modifications de noeud worker - Groupe de correctifs 1.8.15_1519, publié le 13 août 2018
{: #1815_1519}

<table summary="Modifications effectuées depuis la version 1.8.15_1518">
<caption>Modifications depuis la version 1.8.15_1518</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Packages Ubuntu</td>
<td>N/A</td>
<td>N/A</td>
<td>Mises à jour des packages Ubuntu installés.</td>
</tr>
</tbody>
</table>

### Journal des modifications pour la version 1.8.15_1518, publié le 27 juillet 2018
{: #1815_1518}

<table summary="Modifications effectuées depuis la version 1.8.13_1516">
<caption>Modifications depuis la version 1.8.13_1516</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>v1.8.13-176</td>
<td>v1.8.15-204</td>
<td>Mise à jour pour prendre en charge l'édition Kubernetes 1.8.15. En outre, les événements `create failure` du service LoadBalancer incluent désormais toutes les erreurs des sous-réseaux portables.</td>
</tr>
<tr>
<td>Plug-in IBM File Storage</td>
<td>320</td>
<td>334</td>
<td>Le délai de création d'un volume persistant a augmenté pour passer de 15 à 30 minutes. Le type de facturation par défaut a été changé pour passer à une facturation à l'heure (`hourly`). Des options de montage ont été ajoutées aux classes de stockage prédéfinies. Dans l'instance de stockage de fichiers NFS dans votre compte d'infrastructure IBM Cloud (SoftLayer), la zone **Notes** est désormais au format JSON et l'espace de nom Kubernetes dans lequel le volume persistant est déployé a été ajouté. Pour prendre en charge les clusters à zones multiples, des libellés de zone et de région ont été ajoutés pour les volumes persistants.</td>
</tr>
<tr>
<td>Kubernetes</td>
<td>v1.8.13</td>
<td>v1.8.15</td>
<td>Voir les [notes sur l'édition de Kubernetes ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/kubernetes/releases/tag/v1.8.15).</td>
</tr>
<tr>
<td>Noyau</td>
<td>N/A</td>
<td>N/A</td>
<td>De légères améliorations ont été apportées aux paramètres réseau des noeuds worker pour les charges de travail réseau à hautes performances.</td>
</tr>
<tr>
<td>Client OpenVPN</td>
<td>N/A</td>
<td>N/A</td>
<td>Le déploiement du `vpn` du client OpenVPN qui s'exécute dans l'espace de nom `kube-system` est désormais géré par le gestionnaire `addon-manager` de Kubernetes.</td>
</tr>
</tbody>
</table>

### Journal des modifications de noeud worker - Groupe de correctifs 1.8.13_1516, publié le 3 juillet 2018
{: #1813_1516}

<table summary="Modifications effectuées depuis la version 1.8.13_1515">
<caption>Modifications depuis la version 1.8.13_1515</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Noyau</td>
<td>N/A</td>
<td>N/A</td>
<td>Optimisation de `sysctl` pour les charges de travail réseau hautes performances.</td>
</tr>
</tbody>
</table>


### Journal des modifications de noeud worker - Groupe de correctifs 1.8.13_1515, publié le 21 juin 2018
{: #1813_1515}

<table summary="Modifications effectuées depuis la version 1.8.13_1514">
<caption>Modifications depuis la version 1.8.13_1514</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Docker</td>
<td>N/A</td>
<td>N/A</td>
<td>Pour les types de machine non chiffrés, le disque secondaire est nettoyé en obtenant un nouveau système de fichiers lors du rechargement ou de la mise à jour du noeud worker.</td>
</tr>
</tbody>
</table>

### Journal des modifications pour la version 1.8.13_1514, publié le 19 juin 2018
{: #1813_1514}

<table summary="Modifications effectuées depuis la version 1.8.11_1512">
<caption>Modifications depuis la version 1.8.11_1512</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubernetes</td>
<td>v1.8.11</td>
<td>v1.8.13</td>
<td>Voir les [notes sur l'édition de Kubernetes![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/kubernetes/releases/tag/v1.8.13).</td>
</tr>
<tr>
<td>Configuration de Kubernetes</td>
<td>N/A</td>
<td>N/A</td>
<td>Ajout de PodSecurityPolicy dans l'option --admission-control pour le serveur d'API Kubernetes du cluster et configuration du cluster pour prendre en charge les politiques de sécurité de pod. Pour plus d'informations, voir [Configuration de politiques de sécurité de pod](cs_psp.html).</td>
</tr>
<tr>
<td>IBM Cloud Provider</td>
<td>v1.8.11-126</td>
<td>v1.8.13-176</td>
<td>Mise à jour pour prendre en charge l'édition Kubernetes 1.8.13.</td>
</tr>
<tr>
<td>Client OpenVPN</td>
<td>N/A</td>
<td>N/A</td>
<td>Ajout de <code>livenessProbe</code> dans le déploiement du <code>vpn</code> du client OpenVPN qui s'exécute dans l'espace de nom <code>kube-system</code>.</td>
</tr>
</tbody>
</table>


### Journal des modifications de noeud worker - Groupe de correctifs 1.8.11_1512, publié le 11 juin 2018
{: #1811_1512}

<table summary="Modifications effectuées depuis la version 1.8.11_1511">
<caption>Modifications depuis la version 1.8.11_1511</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Mise à jour du noyau</td>
<td>4.4.0-116</td>
<td>4.4.0-127</td>
<td>Mise à jour des images de noeud worker avec la mise à jour du noyau pour [CVE-2018-3639 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-3639).</td>
</tr>
</tbody>
</table>


### Journal des modifications de noeud worker - Groupe de correctifs 1.8.11_1511, publié le 18 mai 2018
{: #1811_1511}

<table summary="Modifications effectuées depuis la version 1.8.11_1510">
<caption>Modifications depuis la version 1.8.11_1510</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubelet</td>
<td>N/A</td>
<td>N/A</td>
<td>Correctif pour résoudre un bogue qui se produisait lorsque vous utilisiez le plug-in de stockage par blocs.</td>
</tr>
</tbody>
</table>

### Journal des modifications de noeud worker - Groupe de correctifs 1.8.11_1510, publié le 16 mai 2018
{: #1811_1510}

<table summary="Modifications effectuées depuis la version 1.8.11_1509">
<caption>Modifications depuis la version 1.8.11_1509</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubelet</td>
<td>N/A</td>
<td>N/A</td>
<td>Les données que vous stockez dans le répertoire racine `kubelet` sont désormais sauvegardées dans un disque secondaire plus volumineux de la machine du noeud worker.</td>
</tr>
</tbody>
</table>


### Journal des modifications pour la version 1.8.11_1509, publié le 19 avril 2018
{: #1811_1509}

<table summary="Modifications effectuées depuis la version 1.8.8_1507">
<caption>Modifications depuis la version 1.8.8_1507</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubernetes</td>
<td>v1.8.8</td>
<td>v1.8.11	</td>
<td><p>Voir les [notes sur l'édition de Kubernetes![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/kubernetes/releases/tag/v1.8.11). Cette édition traite les vulnérabilités [CVE-2017-1002101 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-1002101) et [CVE-2017-1002102 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-1002102).</p><p>Désormais les éléments `secret`, `configMap`, `downwardAPI` et les volumes projetés sont montés en mode lecture seule. Auparavant, les applications pouvaient écrire des données dans ces volumes, mais le système pouvait les rétablir automatiquement. Si vos applications s'appuient sur ce comportement peu fiable en matière de sécurité, modifiez-les en conséquence.</p></td>
</tr>
<tr>
<td>Image de conteneur Pause</td>
<td>3.0</td>
<td>3.1</td>
<td>Supprime les processus zombie orphelins hérités.</td>
</tr>
<tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>v1.8.8-86</td>
<td>v1.8.11-126</td>
<td>Les services `NodePort` et `LoadBalancer` prennent désormais en charge la [conservation de l'adresse IP source du client](cs_loadbalancer.html#node_affinity_tolerations) en définissant l'élément `service.spec.externalTrafficPolicy` sur `Local`.</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>Correction de la configuration de tolérance des [noeuds de périphérie](cs_edge.html#edge) pour les clusters plus anciens.</td>
</tr>
</tbody>
</table>

<br />


### Journal des modifications pour la version 1.7 (non prise en charge)
{: #17_changelog}

Passez en revue les modifications suivantes.

#### Journal des modifications de noeud worker - Groupe de correctifs 1.7.16_1514, publié le 11 juin 2018
{: #1716_1514}

<table summary="Modifications effectuées depuis la version 1.7.16_1513">
<caption>Modifications depuis la version 1.7.16_1513</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Mise à jour du noyau</td>
<td>4.4.0-116</td>
<td>4.4.0-127</td>
<td>Mise à jour des images de noeud worker avec la mise à jour du noyau pour [CVE-2018-3639 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2018-3639).</td>
</tr>
</tbody>
</table>

#### Journal des modifications de noeud worker - Groupe de correctifs 1.7.16_1513, publié le 18 mai 2018
{: #1716_1513}

<table summary="Modifications effectuées depuis la version 1.7.16_1512">
<caption>Modifications depuis la version 1.7.16_1512</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubelet</td>
<td>N/A</td>
<td>N/A</td>
<td>Correctif pour résoudre un bogue qui se produisait lorsque vous utilisiez le plug-in de stockage par blocs.</td>
</tr>
</tbody>
</table>

#### Journal des modifications de noeud worker - Groupe de correctifs 1.7.16_1512, publié le 16 mai 2018
{: #1716_1512}

<table summary="Modifications effectuées depuis la version 1.7.16_1511">
<caption>Modifications depuis la version 1.7.16_1511</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubelet</td>
<td>N/A</td>
<td>N/A</td>
<td>Les données que vous stockez dans le répertoire racine `kubelet` sont désormais sauvegardées dans un disque secondaire plus volumineux de la machine du noeud worker.</td>
</tr>
</tbody>
</table>

#### Journal des modifications pour la version 1.7.16_1511, publié le 19 avril 2018
{: #1716_1511}

<table summary="Modifications effectuées depuis la version 1.7.4_1509">
<caption>Modifications depuis la version 1.7.4_1509</caption>
<thead>
<tr>
<th>Composant</th>
<th>V. précédente</th>
<th>V. en cours</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Kubernetes</td>
<td>v1.7.4</td>
<td>v1.7.16	</td>
<td><p>Voir les [Notes sur l'édition de Kubernetes![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/kubernetes/kubernetes/releases/tag/v1.7.16). Cette édition traite les vulnérabilités [CVE-2017-1002101 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-1002101) et [CVE-2017-1002102 ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-1002102).</p><p>Désormais les éléments `secret`, `configMap`, `downwardAPI` et les volumes projetés sont montés en mode lecture seule. Auparavant, les applications pouvaient écrire des données dans ces volumes, mais le système pouvait les rétablir automatiquement. Si vos applications s'appuient sur ce comportement peu fiable en matière de sécurité, modifiez-les en conséquence.</p></td>
</tr>
<td>{{site.data.keyword.Bluemix_notm}} Provider</td>
<td>v1.7.4-133</td>
<td>v1.7.16-17</td>
<td>Les services `NodePort` et `LoadBalancer` prennent désormais en charge la [conservation de l'adresse IP source du client](cs_loadbalancer.html#node_affinity_tolerations) en définissant l'élément `service.spec.externalTrafficPolicy` sur `Local`.</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>Correction de la configuration de tolérance des [noeuds de périphérie](cs_edge.html#edge) pour les clusters plus anciens.</td>
</tr>
</tbody>
</table>
