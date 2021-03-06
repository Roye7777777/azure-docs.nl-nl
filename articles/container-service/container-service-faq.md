---
title: Azure Container Service - veelgestelde vragen | Microsoft Docs
description: Antwoorden op veelgestelde vragen over Azure Container Service, die het eenvoudiger maakt om een cluster van virtuele machines voor het uitvoeren van Docker-container-apps, te maken, configureren en beheren.
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Mesos, Azure, Kubernetes
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/21/2017
ms.author: danlep
translationtype: Human Translation
ms.sourcegitcommit: 2a381431acb6436ddd8e13c69b05423a33cd4fa6
ms.openlocfilehash: c28391b752c071161796421aee63402899d2a0a4


---
# <a name="frequently-asked-questions-azure-container-service"></a>Veelgestelde vragen: Azure Container Service


## <a name="orchestrators"></a>Orchestrators

### <a name="which-container-orchestrators-do-you-support-on-azure-container-service"></a>Welke containerorchestrators worden ondersteund door Azure Container Service? 

Er is ondersteuning voor open-source DC/OS, Docker Swarm en Kubernetes. Zie het [overzicht](container-service-intro.md) voor meer informatie.
 
### <a name="do-you-support-docker-swarm-mode"></a>Wordt de Docker Swarm-modus ondersteund? 

Swarm-modus wordt momenteel niet ondersteund, maar we zijn er wel mee bezig. 

### <a name="does-azure-container-service-support-windows-containers"></a>Biedt Azure Container Service ondersteuning voor Windows-containers?  

Momenteel worden Linux-containers alleen ondersteund met alle orchestrators. De ondersteuning voor Windows-containers met Kubernetes is momenteel beschikbaar als preview.

### <a name="do-you-recommend-a-specific-orchestrator-in-azure-container-service"></a>Welke orchestrator in Azure Container Service wordt aanbevolen? 
In het algemeen bevelen we geen specifieke orchestrators aan. Als u ervaring hebt met een van de ondersteunde orchestrators, kunt u die ervaring toepassen op Azure Container Service. Gegevenstrends suggereren echter dat DC/OS goed werkt voor big data- en IoT-workloads, dat Kubernetes geschikt is voor cloudworkloads en dat Docker Swarm bekendstaat om de integratie met Docker-hulpprogramma's en de toegankelijkheid.

Als uw situatie erom vraagt, kunt u ook aangepaste containeroplossingen bouwen en beheren met andere Azure-services. Deze services zijn onder andere [Virtual Machines](../virtual-machines/virtual-machines-linux-azure-overview.md), [Service Fabric](../service-fabric/service-fabric-overview.md), [Web Apps](../app-service-web/app-service-web-overview.md) en [Batch](../batch/batch-technical-overview.md).  

### <a name="what-is-the-difference-between-azure-container-service-and-acs-engine"></a>Wat is het verschil tussen Azure Container Service en ACS Engine? 
Azure Container Service is een Azure-service met SLA en functies in Azure Portal, Azure-opdrachtregelprogramma's en Azure-API's. Met de service kunt u clusters die standaardprogramma's voor containerorchestratie uitvoeren, snel implementeren en beheren met een relatief klein aantal configuratie-opties. 

[ACS Engine](http://github.com/Azure/acs-engine) is een open source-project waarmee hoofdgebruikers de clusterconfiguratie op elk niveau kunnen aanpassen. Deze mogelijkheid om de configuratie van de infrastructuur en de software te wijzigen, betekent dat we geen SLA voor ACS Engine bieden. Ondersteuning is beschikbaar via het open-source project op GitHub in plaats van via officiële Microsoft-kanalen. 

## <a name="cluster-management"></a>Clusterbeheer

### <a name="how-do-i-create-ssh-keys-for-my-cluster"></a>Hoe kan ik SSH-sleutels maken voor mijn cluster?

U kunt standaardprogramma's op uw besturingssysteem gebruiken om een sleutelpaar met openbare en privé-SSH RSA-sleutel te maken voor verificatie met de virtuele Linux-machines voor uw cluster. Raadpleeg de stappen voor [OS X en Linux](../virtual-machines/virtual-machines-linux-mac-create-ssh-keys.md) of [Windows](../virtual-machines/virtual-machines-linux-ssh-from-windows.md). 

Als u [Azure CLI 2.0-opdrachten](container-service-create-acs-cluster-cli.md) gebruikt om een Container Service-cluster te implementeren, kunnen de SSH-sleutels automatisch worden gegenereerd voor uw cluster.

### <a name="how-do-i-create-a-service-principal-for-my-kubernetes-cluster"></a>Hoe kan ik een service-principal maken voor mijn Kubernetes-cluster?

Voor het maken van een Kubernetes-cluster in Azure Container Service zijn ook een id en wachtwoord nodig voor de service-principal van Azure Active Directory nodig. Zie [Over de service-principal voor een Kubernetes-cluster](container-service-kubernetes-service-principal.md) voor meer informatie.


Als u [Azure CLI 2.0-opdrachten](container-service-create-acs-cluster-cli.md) gebruikt om een Kubernetes-cluster te implementeren, kunnen de referenties van de service-principal automatisch worden gegenereerd voor uw cluster.


### <a name="how-do-i-increase-the-number-of-masters-after-a-cluster-is-created"></a>Hoe kan ik het aantal masters verhogen nadat een cluster is gemaakt? 
Nadat het cluster is gemaakt, staat het aantal masters vast en kan dit niet worden gewijzigd. We raden u aan om bij het maken van het cluster meerdere masters te selecteren voor hogere beschikbaarheid.


### <a name="how-do-i-increase-the-number-of-agents-after-a-cluster-is-created"></a>Hoe kan ik het aantal agents verhogen nadat een cluster is gemaakt? 
U kunt het aantal agents in het cluster schalen via Azure Portal of met opdrachtregelprogramma's. Zie [Scale an Azure Container Service cluster](container-service-scale.md) (Een Azure Container Service-cluster schalen).


### <a name="what-are-the-urls-of-my-masters-and-agents"></a>Wat zijn de URL's van mijn masters en agents? 
De URL's van clusterresources in Azure Container Service zijn gebaseerd op het DNS-naamvoorvoegsel dat u opgeeft en de naam van de Azure-regio die u hebt gekozen voor implementatie. De volledig gekwalificeerde domeinnaam (FQDN) van het hoofdknooppunt ziet er bijvoorbeeld als volgt uit:

``` 
DNSnamePrefix.AzureRegion.cloudapp.azure.net
```

U vindt veelgebruikte URL's voor uw cluster in Azure Portal, Azure Resource Explorer of andere Azure-hulpprogramma's.
 
### <a name="where-do-i-find-the-ssh-connection-string-to-my-cluster"></a>Waar vind ik de SSH-verbindingsreeks naar mijn cluster?

U vindt de verbindingsreeks in Azure Portal of met behulp van Azure-opdrachtregelprogramma's. 

1. Navigeer in de portal naar de resourcegroep voor de clusterimplementatie.  

2. Klik op **Overzicht** en dan op de koppeling voor **Implementaties** onder **Essentials**. 

3. Op de blade **Implementatiegeschiedenis** klikt u op de implementatie met een naam die begint met **microsoft-acs** gevolgd door een implementatiedatum. Voorbeeld: microsoft-acs-201701310000.  

4. Op de pagina **Samenvatting**, onder **Uitvoer**, worden enkele clusterkoppelingen gegeven.<provided></provided> **SSHMaster0** biedt een SSH-verbindingsreeks naar de eerste master in uw Container Service-cluster. 

Zoals eerder vermeld, kunt u ook Azure-hulpprogramma's gebruiken om de FQDN van de master te vinden. Maak een SSH-verbinding met de master met behulp van de FQDN van de master en de gebruikersnaam die u hebt opgegeven bij het maken van het cluster. Bijvoorbeeld:

```bash
ssh userName@masterFQDN –A –p 22 
```

Zie [Verbinding maken met een Azure Container Service-cluster](container-service-connect.md) voor meer informatie.




## <a name="next-steps"></a>Volgende stappen

* [Meer informatie](container-service-intro.md) over Azure Container Service.
* Implementeer een Container Service-cluster met de [portal](container-service-deployment.md) of [Azure CLI 2.0](container-service-create-acs-cluster-cli.md).


<!--HONumber=Feb17_HO4-->


