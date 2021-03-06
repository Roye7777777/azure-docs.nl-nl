1. Meld u aan bij [Azure Portal][Azure portal].
2. Klik in het linkernavigatievenster van de portal achtereenvolgens op **Nieuw**, **Bedrijfsintegratie** en **Relay**.
3. Voer in het dialoogvenster **Naamruimte maken** een naam in voor de naamruimte. In het systeem wordt onmiddellijk gecontroleerd of de naam beschikbaar is.
4. Kies in het veld **Abonnement** een Azure-abonnement waarin u de naamruimte maakt.
5. Kies in het veld **[Resourcegroep](../articles/azure-resource-manager/resource-group-portal.md)** een bestaande resourcegroep waarin de naamruimte zal zijn opgenomen of maak een nieuwe resourcegroep.      
6. Kies in **Locatie** het land of regio waarin uw naamruimte moet worden gehost.
   
    ![Een naamruimte maken][create-namespace]
7. Klik op **Create**. Uw naamruimte wordt nu gemaakt en ingeschakeld. Na enkele minuten stelt het systeem resources ter beschikking voor uw account.

### <a name="obtain-the-management-credentials"></a>De beheerreferenties ophalen
1. Klik in de lijst met naamruimten op de zojuist gemaakte naam voor de naamruimte.
2. Klik in de naamruimte-blade op **Beleid voor gedeelde toegang**.
3. Klik in de blade **Beleid voor gedeelde toegang** op **RootManageSharedAccessKey**.
   
    ![verbinding-gegevens][connection-info]
4. Klik in het blade **Beleid: RootManageSharedAccessKey** op de knop Kopiëren naast **Verbindingsreeks–primaire sleutel** om de verbindingsreeks naar het klembord te kopiëren voor later gebruik. Plak deze waarde in Kladblok of een andere tijdelijke locatie.
   
    ![connection-string][connection-string]

5. Herhaal de vorige stap: het kopiëren en plakken van de waarde voor de **Primaire sleutel** voor een tijdelijke locatie zodat u deze later kunt gebruiken.  

<!--Image references-->

[create-namespace]: ./media/relay-create-namespace-portal/create-namespace.png
[connection-info]: ./media/relay-create-namespace-portal/connection-info.png
[connection-string]: ./media/relay-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com


<!--HONumber=Feb17_HO2-->


