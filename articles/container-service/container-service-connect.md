---
title: Verbinding maken met een Azure Container Service-cluster | Microsoft Docs
description: Vanaf een externe computer verbinding maken met een Kubernetes-, DC/OS- of Docker Swarm-cluster in Azure Container Service
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Kubernetes, DC/OS, Azure
ms.assetid: ff8d9e32-20d2-4658-829f-590dec89603d
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/21/2017
ms.author: rogardle
translationtype: Human Translation
ms.sourcegitcommit: 2a381431acb6436ddd8e13c69b05423a33cd4fa6
ms.openlocfilehash: 45d399b72f8d037fb828d9ad22bbd3543847feb3
ms.lasthandoff: 02/22/2017


---
# <a name="connect-to-an-azure-container-service-cluster"></a>Verbinding maken met een Azure Container Service-cluster
Nadat u een Azure Container Service-cluster hebt gemaakt, moet u het cluster verbinden om workloads te kunnen implementeren en beheren. In dit artikel wordt beschreven hoe u vanaf een externe computer verbinding maakt met de hoofd-VM van het cluster. 

De Kubernetes-, DC/OS- en Docker Swarm-clusters stellen lokale HTTP-eindpunten beschikbaar. Bij Kubernetes wordt dit eindpunt veilig beschikbaar gesteld op internet en kunt u het rechtstreeks openen door op een machine met een internetverbinding het opdrachtregelprogramma `kubectl` uit te voeren. 

Voor DC/OS en Docker Swarm moet u een veilige shell-tunnel (SSH) naar een intern systeem maken. Wanneer de tunnel is ingesteld, kunt u opdrachten uitvoeren die gebruikmaken van de HTTP-eindpunten en kunt u de webinterface van het cluster vanuit uw lokale systeem bekijken. 


## <a name="prerequisites"></a>Vereisten

* Een Kubernetes-, DC/OS- of Swarm-cluster, [geïmplementeerd in Azure Container Service](container-service-deployment.md).
* SSH RSA-bestand met persoonlijke sleutel die overeenkomt met de openbare sleutel die tijdens de implementatie is toegevoegd aan het cluster. Met deze opdrachten wordt ervan uitgegaan dat de persoonlijke SSH-sleutel zich bevindt in `$HOME/.ssh/id_rsa` op uw computer. Zie deze instructies voor [OS X en Linux](../virtual-machines/virtual-machines-linux-mac-create-ssh-keys.md) of [Windows](../virtual-machines/virtual-machines-linux-ssh-from-windows.md) voor meer informatie. Als de SSH-verbinding niet werkt, moet u mogelijk [uw SSH-sleutels opnieuw instellen](../virtual-machines/virtual-machines-linux-troubleshoot-ssh-connection.md).

## <a name="connect-to-a-kubernetes-cluster"></a>Verbinding maken met een Kubernetes-cluster

Volg deze stappen om `kubectl` op uw computer te installeren en te configureren.

> [!NOTE] 
> Op Linux of OS X moet u de opdrachten in deze sectie mogelijk uitvoeren met `sudo`.
> 

### <a name="install-kubectl"></a>Kubectl installeren
Eén manier om dit hulpprogramma te installeren, is met de Azure CLI 2.0-opdracht `az acs kubernetes install-cli`. Als u deze opdracht wilt uitvoeren, moet de meest recente versie van Azure CLI 2.0 zijn [geïnstalleerd](/cli/azure/install-az-cli2) en moet u zijn aangemeld bij een Azure-account (`az login`).

```azurecli
# Linux or OS X
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

U kunt de nieuwste client ook rechtstreeks downloaden vanaf de [Kubernetes-releasepagina](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md). Zie [Installing and Setting up kubectl](https://kubernetes.io/docs/user-guide/prereqs/) (kubectl installeren en instellen) voor meer informatie.

### <a name="download-cluster-credentials"></a>Clusterreferenties downloaden
Nadat `kubectl` is geïnstalleerd, kopieert u de clusterreferenties naar uw machine. Eén manier om de referenties te verkrijgen, is met de opdracht `az acs kubernetes get-credentials`. Geef de naam van de resourcegroep en de naam van de containerserviceresource als volgt door:


```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

Hiermee worden de clusterreferenties gedownload in `$HOME/.kube/config`, waar `kubectl` ze verwacht.

U kunt `scp` ook gebruiken om het bestand veilig te kopiëren van `$HOME/.kube/config` op de hoofd-VM naar uw lokale machine. Bijvoorbeeld:

```console
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

Als u met Windows werkt, moet u gebruikmaken van Bash op Ubuntu in Windows, de PuTTy-client voor het veilig kopiëren van bestanden of een vergelijkbaar hulpprogramma.



### <a name="use-kubectl"></a>Kubectl gebruiken

Zodra `kubectl` is geconfigureerd, kunt u de verbinding testen door de knooppunten in uw cluster weer te geven:

```console
kubectl get nodes
```

U kunt andere `kubectl`-opdrachten proberen. Zo zou u bijvoorbeeld het Kubernetes Dashboard kunnen weergeven. Daartoe voert u eerst een proxy uit naar de API-server van Kubernetes:

```console
kubectl proxy
```

De gebruikersinterface van Kubernetes is nu beschikbaar via `http://localhost:8001/ui`.

Raadpleeg de [Snelstartgids van Kubernetes](http://kubernetes.io/docs/user-guide/quick-start/) voor meer informatie.

## <a name="connect-to-a-dcos-or-swarm-cluster"></a>Verbinding maken met een DC/OS- of Swarm-cluster

Als u de CD/OS- en Docker Swarm-clusters wilt gebruiken die door Azure Container Service zijn geïmplementeerd, volgt u deze instructies om een veilige shell-tunnel (SSH) vanuit uw lokale Linux-, OS X- of Windows-systeem te maken. 

> [!NOTE]
> Deze instructies zijn gericht op tunnelling van TCP-verkeer via SSH. U kunt ook een interactieve SSH-sessie starten met een van de interne clusterbeheersystemen, maar dit wordt niet aanbevolen. Wanneer er rechtstreeks in een intern systeem wordt gewerkt, ontstaat het risico dat er onbedoeld configuratiewijzigingen worden doorgevoerd.  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-os-x"></a>Een SSH-tunnel maken in Linux of OS X
Het eerste wat u doet wanneer u een SSH-tunnel in Linux of OS X maakt, is het lokaliseren van de openbare DNS-naam van masters met gelijke taakverdeling. Volg deze stappen:


1. Blader in [Azure Portal](https://portal.azure.com) naar de resourcegroep die uw containerservicecluster bevat. Vouw de resourcegroep uit zodat elke resource wordt weergegeven. 

2. Klik op de resource van de containerservice en vervolgens op **Overzicht**. Onder **Essentials** wordt de **Hoofd-FQDN** van het cluster weergegeven. Bewaar deze naam voor later gebruik. 

    ![Openbare DNS-naam](media/pubdns.png)

    U kunt ook de opdracht `az acs show` voor de containerservice uitvoeren. Zoek naar de eigenschap **Master Profile:fqdn** in de uitvoer van de opdracht.

3. Open nu een shell en voer de opdracht `ssh` uit door de volgende waarden op te geven: 

    **LOCAL_PORT** is de TCP-poort aan de servicezijde van de tunnel waarmee verbinding moet worden gemaakt. Voor Swarm stelt u deze in op 2375. Voor DC/OS stelt u deze in op 80.  
    **REMOTE_PORT** is de naam van het eindpunt dat u beschikbaar wilt maken. Voor Swarm gebruikt u poort 2375. Gebruik poort 80 voor DC/OS.  
    **USERNAME** de naam is van de gebruiker die is opgegeven tijdens de implementatie van het cluster.  
    **DNSPREFIX** het DNS-voorvoegsel is dat is opgegeven tijdens de implementatie van het cluster.  
    **REGION** de regio is waarin uw resourcegroep zich bevindt.  
    **PATH_TO_PRIVATE_KEY** [OPTIONEEL] is het pad naar de persoonlijke sleutel die overeenkomt met de openbare sleutel die u hebt opgegeven bij het maken van het cluster. Gebruik deze optie met de vlag `-i`.

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com 
    ```
    > [!NOTE]
    > De poort voor de SSH-verbinding is 2200 en niet de standaardpoort 22. In een cluster met meerdere hoofd-VM's is dit de verbindingspoort naar de eerste hoofd-VM.
    > 



Zie de voorbeelden voor DC/OS en Swarm in de volgende secties.    

### <a name="dcos-tunnel"></a>DC/OS-tunnel
Als u een tunnel voor DC/OS-eindpunten wilt openen, voert u een opdracht als deze uit:

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> U kunt een andere lokale poort dan poort 80 opgeven, bijvoorbeeld poort 8888. Sommige web-UI-koppelingen werken echter niet wanneer u deze poort gebruikt.

Nu hebt u vanaf de lokale computer via de volgende URL's toegang tot de DC/OS-eindpunten (ervan uitgaande dat de lokale poort 80 is):

* DC/OS: `http://localhost:80/`
* Marathon: `http://localhost:80/marathon`
* Mesos: `http://localhost:80/mesos`

U kunt ook de REST API's voor elke toepassing via deze tunnel bereiken.

### <a name="swarm-tunnel"></a>Swarm-tunnel
Wanneer u een tunnel naar het Swarm-eindpunt wilt openen, voert u een opdracht als deze uit:

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```

U kunt nu uw omgevingsvariabele DOCKER_HOST als volgt instellen. U kunt uw Docker-opdrachtregelinterface blijven gebruiken zoals u dat normaal doet.

```bash
export DOCKER_HOST=:2375
```

### <a name="create-an-ssh-tunnel-on-windows"></a>Een SSH-tunnel maken in Windows
Er zijn meerdere opties voor het maken van SSH-tunnels in Windows. In deze sectie wordt beschreven hoe u PuTTY gebruikt om de tunnel te maken.

1. [Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) naar uw Windows-systeem.

2. Voer de toepassing uit.

3. Voer een hostnaam in die bestaat uit de naam van de cluserbeheerdergebruiker en de openbare DNS-naam van de eerste master in het cluster. De **hostnaam** ziet er ongeveer zo uit: `adminuser@PublicDNSName`. Voer 2200 in bij **Poort**.

    ![PuTTY-configuratie 1](media/putty1.png)

4. Selecteer **SSH > Verificatie**. Voeg een pad aan uw persoonlijke-sleutelbestand (.ppk-indeling) toe voor verificatie. U kunt een hulpprogramma als [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) gebruiken om dit bestand te genereren vanuit de SSH-sleutel waarmee het cluster is gemaakt.

    ![PuTTY-configuratie 2](media/putty2.png)

5. Selecteer **SSH > Tunnels** en configureer de volgende doorgestuurde poorten:

    * **Bronpoort:** gebruik 80 voor DC/OS of 2375 voor Swarm.
    * **Doelpoort:** gebruik localhost:80 voor DC/OS of localhost:2375 voor Swarm.

    Het volgende voorbeeld is geconfigureerd voor DC/OS, maar ziet er ongeveer hetzelfde uit voor Docker Swarm.

    > [!NOTE]
    > Poort 80 mag niet in gebruik zijn wanneer u deze tunnel maakt.
    > 

    ![PuTTY-configuratie 3](media/putty3.png)

6. Wanneer u klaar bent, klikt u op **Sessie > Opslaan** om de verbindingsconfiguratie op te slaan.

7. Klik op **Openen** als u verbinding wilt maken met de PuTTY-sessie. Wanneer u verbinding maakt, kunt u de poortconfiguratie in het PuTTY-gebeurtenislogboek zien.

    ![PuTTY-gebeurtenislogboek](media/putty4.png)

Nadat u de tunnel voor DC/OS hebt geconfigureerd, hebt u toegang tot het gerelateerde eindpunt op:

* DC/OS: `http://localhost/`
* Marathon: `http://localhost/marathon`
* Mesos: `http://localhost/mesos`

Nadat u de tunnel voor Docker Swarm hebt geconfigureerd, opent u de Windows-instellingen om een systeemomgevingsvariabele te configureren met de naam `DOCKER_HOST` en de waarde `:2375`. Daarna kunt u het Swarm-cluster openen via de Docker CLI.

## <a name="next-steps"></a>Volgende stappen
Containers in het cluster implementeren en beheren:

* [Werken met de Azure Container Service en Kubernetes](container-service-kubernetes-ui.md)
* [Werken met de Azure Container Service en DC/OS](container-service-mesos-marathon-rest.md)
* [Werken met de Azure Container Service en Docker Swarm](container-service-docker-swarm.md)


