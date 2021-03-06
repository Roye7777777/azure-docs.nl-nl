# Overzicht
## [Wat is Cloud Services?](cloud-services-choose-me.md)
## [Configuratiebestanden en verpakking van een cloudservice](cloud-services-model-and-package.md)

# Aan de slag
## [Voorbeeld van .NET-cloudservice](cloud-services-dotnet-get-started.md)
## [Voorbeeld van Python voor Visual Studio-cloudservice](cloud-services-python-ptvs.md)
## [Een hybride HPC-cluster configureren met Microsoft HPC Pack](cloud-services-setup-hybrid-hpcpack-cluster.md)

# Procedures
## Plannen
### [Grootte van virtuele machines](cloud-services-sizes-specs.md)
### [Updates](cloud-services-update-azure-service.md)

## Ontwikkelen
### [PHP-web- en -werkrollen maken](../cloud-services-php-create-web-role.md)
### [Een Node.js-toepassing bouwen en implementeren](cloud-services-nodejs-develop-deploy-app.md)
### [Een Node.js-webtoepassing bouwen met Express](cloud-services-nodejs-develop-deploy-express-app.md)
### Storage en Visual Studio
#### [Blob Storage en verbonden services](../storage/vs-storage-cloud-services-getting-started-blobs.md)
#### [Queue Storage en verbonden services](../storage/vs-storage-cloud-services-getting-started-queues.md)
#### [Table Storage en verbonden services](../storage/vs-storage-cloud-services-getting-started-tables.md)
### Pakketten configureren voor doorlopend bouwen en implementeren
#### [Visual Studio Team Services en Git](cloud-services-continuous-delivery-use-vso-git.md)
#### [Visual Studio Team Services](cloud-services-continuous-delivery-use-vso.md)
#### [TFS en Team Build](cloud-services-dotnet-continuous-delivery.md)
### [Verkeersregels voor een rol configureren](cloud-services-enable-communication-role-instances.md)
### [Levenscyclusgebeurtenissen van cloudservices verwerken](cloud-services-role-lifecycle-dotnet.md)
### [Socket.io (Node.js)](cloud-services-nodejs-chat-app-socketio.md)
### [Bellen met behulp van Twilio (.NET)](../partner-twilio-cloud-services-dotnet-phone-call-web-role.md)
### [New Relic](../store-new-relic-cloud-services-dotnet-application-performance-management.md)

### Opstarttaken configureren
#### [Opstarttaken maken](cloud-services-startup-tasks.md)
#### [Veelvoorkomende opstarttaken](cloud-services-startup-tasks-common.md)
#### [Een taak gebruiken om .NET op een cloudservicerol te installeren](cloud-services-dotnet-install-dotnet.md)

### Extern bureaublad configureren
#### [Visual Studio](cloud-services-role-enable-remote-desktop.md)
#### [Node.js](cloud-services-nodejs-enable-remote-desktop.md)
#### [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)

## Implementeren
### Een cloudservice maken en implementeren in Portal
#### [Portal](cloud-services-how-to-create-deploy-portal.md)
#### [Klassieke portal](cloud-services-how-to-create-deploy.md)
### [Een lege cloudservicecontainer maken in PowerShell](cloud-services-powershell-create-cloud-container.md)
### Een aangepaste domeinnaam configureren
#### [Portal](cloud-services-custom-domain-name-portal.md)
#### [Klassieke portal](cloud-services-custom-domain-name.md)
### [Een cloudservice-implementatie klaarzetten (Node.js)](cloud-services-nodejs-stage-application.md)
### [Verbinding maken met een aangepaste domeincontroller](cloud-services-connect-to-custom-domain.md)

## Services beheren
### Veelvoorkomende beheertaken
#### [Portal](cloud-services-how-to-manage-portal.md)
#### [Klassieke portal](cloud-services-how-to-manage.md)
### Cloudservice configureren
#### [Portal](cloud-services-how-to-configure-portal.md)
#### [Klassieke portal](cloud-services-how-to-configure.md)
### [Een cloudservice beheren met Azure Automation](automation-manage-cloud-services.md)
### Automatisch schalen configureren
#### [Portal](cloud-services-how-to-scale-portal.md)
#### [Klassieke portal](cloud-services-how-to-scale.md)
### [Python gebruiken om Azure-resources te beheren](cloud-services-python-how-to-use-service-management.md)

### [Patches voor gastbesturingssysteem](cloud-services-guestos-msrc-releases.md)
### Buitengebruikstelling van gastbesturingssysteem
#### [Stopzetting van beleid](cloud-services-guestos-retirement-policy.md)
#### [Kennisgeving van buitengebruikstelling van serie 1](cloud-services-guestos-family1-retirement.md)
### [Releasenieuws voor gastbesturingssysteem](cloud-services-guestos-update-matrix.md)
### [Overzichtskaart van configuratie van Cloud Services-rollen voor XPath](cloud-services-role-config-xpath.md)

## Certificaten beheren
### [Cloud Services en beheercertificaten](cloud-services-certs-create.md)
### SSL configureren 
#### [Portal](cloud-services-configure-ssl-certificate-portal.md)
#### [Klassieke portal](cloud-services-configure-ssl-certificate.md)

## Controleren
### [Cloud Services controleren](cloud-services-how-to-monitor.md)
### [Prestaties testen](../vs-azure-tools-performance-profiling-cloud-services.md)
#### [Testen met Visual Studio Profiler](cloud-services-performance-testing-visual-studio-profiler.md)
### Diagnostische gegevens inschakelen
#### [PowerShell](cloud-services-diagnostics-powershell.md)
#### [.NET](cloud-services-dotnet-diagnostics.md)
#### [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)
### [Prestatiemeteritems gebruiken in Azure Diagnostics](cloud-services-dotnet-diagnostics-performance-counters.md)
### [Diagnostische gegevens opslaan en weergeven in Azure Storage](cloud-services-dotnet-diagnostics-storage.md)
### [Een cloudservice volgen met de diagnosefunctie](cloud-services-dotnet-diagnostics-trace-flow.md)
### [Diagnostische gegevens verzenden naar App Insights](cloud-services-dotnet-diagnostics-applicationinsights.md)

## Problemen oplossen
### Fouten opsporen 
#### [Fouten opsporen op afstand inschakelen met continue levering](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md)
#### [Opties voor een cloudservice](../vs-azure-tools-debugging-cloud-services-overview.md)
#### [Lokale cloudservice met Visual Studio](../vs-azure-tools-debug-cloud-services-virtual-machines.md)
#### [Gepubliceerde cloudservice met Visual Studio](../vs-azure-tools-intellitrace-debug-published-cloud-services.md)
### [Toewijzing van cloudservice is mislukt](cloud-services-allocation-failures.md)
### [Veelvoorkomende oorzaken voor het recyclen van cloudservicerollen](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md)
### [Standaard TEMP-map is te klein voor de rol](cloud-services-troubleshoot-default-temp-folder-size-too-small-web-worker-role.md)
### [Veelvoorkomende implementatieproblemen](cloud-services-troubleshoot-deployment-problems.md)
### [Rol is niet gestart](cloud-services-troubleshoot-roles-that-fail-start.md)
### [Richtlijnen voor herstel](cloud-services-disaster-recovery-guidance.md)
### [Veelgestelde vragen over Cloud Services](cloud-services-faq.md)

# Naslaginformatie
## [.csdef XMLSchema](https://msdn.microsoft.com/library/azure/ee758711)
## [.cscfg XMLSchema](https://msdn.microsoft.com/library/azure/ee758710)
## [REST](https://msdn.microsoft.com/library/azure/ee460812)

# Bronnen
## [Prijzen](https://azure.microsoft.com/pricing/details/cloud-services/)
## [MSDN-forum](https://social.msdn.microsoft.com/Forums/en-us/home?forum=windowsazuredevelopment)
## [Video's](https://azure.microsoft.com/documentation/videos/index/?services=cloud-services)
## [Service-updates](https://azure.microsoft.com/updates/?product=cloud-services&updatetype=&platform=)
## [Leertraject](https://azure.microsoft.com/documentation/learning-paths/cloud-services/)


<!--HONumber=Feb17_HO3-->


