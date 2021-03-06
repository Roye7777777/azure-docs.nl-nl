---
title: "Privé-Docker-containerregister in Azure | Microsoft Docs"
description: Kennismaking met de Azure Container Registry-service, waarmee u cloudgebaseerde, beheerde en persoonlijke Docker-registers kunt maken.
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: ee2b652b-fb7c-455b-8275-b8d4d08ffeb3
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/14/2016
ms.author: stevelas
translationtype: Human Translation
ms.sourcegitcommit: f299cff22d00a1c765a32838647818d18f3df85d
ms.openlocfilehash: 44bfd57feecc45e037717a35b64dd8e4bfb6a1b3

---
# <a name="what-is-azure-container-registry"></a>Wat is Azure Container Registry?
> [!NOTE]
> Container Registry is momenteel in de preview-versie.


Azure Container Registry is een beheerde service voor [Docker-registers](https://docs.docker.com/registry/) gebaseerd op de open-source Docker Registry v2. Maak en onderhoud Azure-containerregisters om uw persoonlijke installatiekopieën voor [Docker-containers](https://www.docker.com/what-docker) op te slaan en te beheren. Gebruik containerregisters in Azure met uw bestaande pijplijnen voor containerontwikkeling en -implementatie en profiteer van de expertise in de Docker-community.

Voor achtergrondinformatie over Docker en containers raadpleegt u:

* [Gebruikershandleiding voor Docker](https://docs.docker.com/engine/userguide/)
* [Aankondiging Azure Container Registry-preview](https://azure.microsoft.com/blog/azure-container-registry-preview/) 

## <a name="key-concepts"></a>Belangrijkste concepten
* **Register**: maak een of meerdere containerregisters in uw Azure-abonnement. Elk register wordt ondersteund door een standaard-Azure-[opslagaccount](../storage/storage-introduction.md) op dezelfde locatie. Maak een register op dezelfde Azure-locatie als uw implementaties om te profiteren van lokale opslag dichtbij in het netwerk van uw containerinstallatiekopieën. 

  Registers worden in een hoofddomein geplaatst op basis van de [Azure Active Directory-tenant](../active-directory/active-directory-howto-tenant.md) van het abonnement. Als u bijvoorbeeld een organisatieaccount hebt in het Contoso-domein, heeft uw volledig gekwalificeerde registernaam een indeling zoals `myregistry-contoso.azurecr.io`. 
  
  U kunt [toegang beheren](container-registry-authentication.md) tot een containerregister met behulp van een [service-principal](../active-directory/active-directory-application-objects.md) ondersteund door Azure Active Directory of een opgegeven beheeraccount. Voer de standaardopdracht `docker login` uit om deze te verifiëren met een register. 

* **Opslagplaats**: een register bevat een of meer opslagplaatsen. Dit zijn groepen met containerinstallatiekopieën. Azure Container Registry ondersteunt naamruimten voor opslagplaatsen op meerdere niveaus. Met deze functie kunt u verzamelingen van installatiekopieën maken die gerelateerd zijn aan een specifieke app, of verzamelingen apps die gerelateerd zijn aan specifieke ontwikkelingsteams of operationele teams. Bijvoorbeeld:
  
  * `myregistry-contoso.azurecr.io/aspnetcore:1.0.1` staat voor een bedrijfsbrede installatiekopie
  * `myregistry-contoso.azurecr.io/warrantydept/dotnet-build` staat voor een installatiekopie die wordt gebruikt om .NET-apps te maken die op de garantieafdeling worden gedeeld
  * `myregistry-contoso.azrecr.io/warrantydept/customersubmissions/web` staat voor een webinstallatiekopie, opgenomen in de app voor klantinzendingen die eigendom is van de garantieafdeling

* **Installatiekopie**: installatiekopieën worden opgeslagen in een opslagplaats. Elke installatiekopie is een alleen-lezenmomentopname van een Docker-container. Azure-containerregisters kunnen zowel Windows- als Linux-installatiekopieën bevatten. U beheert de namen van de installatiekopieën voor al uw containerimplementaties. Gebruik standaard-[Docker-opdrachten](https://docs.docker.com/engine/reference/commandline/) om installatiekopieën naar een opslagplaats te pushen of een installatiekopie uit een opslagplaats op te halen. 

* **Container**: een container definieert een softwaretoepassing en de afhankelijkheden opgenomen in een compleet bestandssysteem inclusief code, runtime, systeemwerkset en bibliotheken. U kunt Docker-containers uitvoeren op basis van Windows- of Linux-installatiekopieën die u ophaalt uit een containerregister. Containers die op een enkele machine worden uitgevoerd, delen de kernel van het besturingssysteem. Docker-containers zijn volledig overdraagbaar naar alle grote distributies van Linux, Mac en Windows.

## <a name="use-cases"></a>Gebruiksvoorbeelden
Haal installatiekopieën op vanuit een Azure-containerregister en push ze naar verschillende implementatiedoelen:

* **Schaalbare indelingssystemen** die toepassingen in een container beheren voor verschillende hostclusters, waaronder [DC/OS](https://docs.mesosphere.com/), [Docker Swarm](https://docs.docker.com/swarm/) en [Kubernetes](http://kubernetes.io/docs/).
* **Azure-services** die het bouwen en uitvoeren van toepassingen op schaal ondersteunen, waaronder [Container Service](../container-service/index.md), [App Service](/app-service/index.md), [Batch](../batch/index.md) en [Service Fabric](../service-fabric/index.md). 

Ontwikkelaars kunnen ook naar een containerregister pushen als onderdeel van een ontwikkelingswerkstroom met containers. Bijvoorbeeld naar een containerregister vanuit doorlopende integratie- implementatieprogramma's als [Visual Studio Team Services](https://www.visualstudio.com/docs/overview) of [Jenkins](https://jenkins.io/).





## <a name="next-steps"></a>Volgende stappen
* [Een containerregister maken met Azure Portal](container-registry-get-started-portal.md)
* [Een containerregister maken met de Azure-CLI](container-registry-get-started-azure-cli.md)
* [Uw eerste installatiekopie pushen met de Docker-CLI](container-registry-get-started-docker-cli.md)
* Raadpleeg [deze zelfstudie](../container-service/container-service-setup-ci-cd.md) voor informatie over hoe u een doorlopende integratie- en implementatiewerkstroom maakt met Visual Studio Team Services, Azure Container Service en Azure Container Registry.
* Als u een privé-Docker-register in Azure wilt instellen (zonder een openbaar eindpunt), raadpleegt u [Uw eigen privé-Docker-register in Azure implementeren](../virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md).



<!--HONumber=Jan17_HO4-->


