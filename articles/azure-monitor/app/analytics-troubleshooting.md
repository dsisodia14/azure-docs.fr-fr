---
title: Dépannage d’Analytics dans Azure Application Insights | Microsoft Docs
description: 'Des problèmes avec Application Insights Analytics ? Démarrer ici. '
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm
ms.assetid: 9bbd5859-3584-4d80-9b6d-d5910fa48baa
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.topic: conceptual
ms.date: 02/08/2019
ms.author: mbullwin
ms.openlocfilehash: ecf0638aa999208331603ac30ccf4eb17b3c4500
ms.sourcegitcommit: d1c5b4d9a5ccfa2c9a9f4ae5f078ef8c1c04a3b4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/08/2019
ms.locfileid: "55960681"
---
# <a name="troubleshoot-analytics-in-application-insights"></a>Dépannage d’Analytics dans Application Insights
Des problèmes avec [Application Insights Analytics](analytics.md)? Démarrer ici. Analytics est le puissant outil de recherche d’Azure Application Insights.

## <a name="limits"></a>limites
* Les résultats de requête sont actuellement limités à une seule semaine de données d’historique.
* Navigateurs que nous testons : dernières versions de Chrome, Microsoft Edge et d’Internet Explorer.

## <a name="known-incompatible-browser-extensions"></a>Extensions du navigateur incompatibles connues
* Ghostery

Désactivez l’extension ou utilisez un autre navigateur.

## <a name="e-a"></a> « Erreur inattendue »
![Ecran Erreur inattendue](media/analytics-troubleshooting/010.png)

Une erreur interne s'est produite lors de l'exception non prise en charge du runtime du portail.

* Nettoyez le cache du navigateur.

## <a name="e-b"></a>403... essayez de recharger
![403... essayez de recharger](media/analytics-troubleshooting/020.png)

Une erreur d’authentification s’est produite (lors de l’authentification ou pendant la génération du jeton d’accès). Le portail n’a peut-être aucun moyen de récupérer les données sans modifier les paramètres du navigateur.

* Vérifiez que [les cookies tiers sont activés](#cookies) dans le navigateur. 

## <a name="authentication"></a>403... vérifiez la zone de sécurité
![403... vérifiez la zone de sécurité](media/analytics-troubleshooting/030.png)

Une erreur d’authentification s’est produite (lors de l’authentification ou pendant la génération du jeton d’accès). Le portail n’a peut-être aucun moyen de récupérer les données sans modifier les paramètres du navigateur.

1. Vérifiez que [les cookies tiers sont activés](#cookies) dans le navigateur. 
2. Avez-vous utilisé un favori, un signet ou un lien enregistré pour ouvrir le portail Analytics ? Vous êtes-vous connecté avec des informations d’identification différentes de celles utilisées pour enregistrer le lien ?
3. Essayez d’utiliser une fenêtre de navigateur privée/anonyme (après avoir fermé toutes les fenêtres de ce type). Vous devrez fournir vos informations d’identification. 
4. Ouvrez une autre fenêtre de navigateur (standard) et accédez à [Azure](https://portal.azure.com). Déconnectez-vous. Ouvrez ensuite votre lien et connectez-vous avec les informations d’identification correctes.
5. Les utilisateurs Microsoft Edge et Internet Explorer peuvent également obtenir cette erreur lorsque les paramètres de la zone de confiance ne sont pas pris en charge.
   
    Vérifiez que le [portail Analytics](https://portal.azure.com) et le [portail Azure Active Directory](https://portal.azure.com) se trouvent dans la même zone de sécurité :
   
   * Dans Internet Explorer, ouvrez **Options Internet**, **Sécurité**, **Sites de confiance**, **Sites** :
     
     ![Boîte de dialogue Options Internet, ajout d’un site aux sites de confiance](media/analytics-troubleshooting/033.png)
     
     Dans la liste des sites Web, si une des URL suivantes est incluse, assurez-vous que les autres le sont également :
     
     https://analytics.applicationinsights.io<br/>
     https://login.microsoftonline.com<br/>
     https://login.windows.net

## <a name="e-d"></a>404 ... Ressource introuvable
![404... ressource introuvable](media/analytics-troubleshooting/040.png)

Une ressource d'application a été supprimée d'Application Insights et n'est plus disponible. Cela peut se produire si vous avez enregistré l’URL dans la page Analytics.

## <a name="e-e"></a>403 ... Aucune autorisation
![403... non autorisé](media/analytics-troubleshooting/050.png)

Vous n’êtes pas autorisé à ouvrir cette application dans Analytics.

* Avez-vous reçu le lien d’un tiers ? Si oui, demandez à cette personne de vérifier que vous figurez bien dans les [lecteurs ou contributeurs de ce groupe de ressources](../../azure-monitor/app/resources-roles-access-control.md).
* Avez-vous enregistré le lien en utilisant d’autres informations d’identification ? Ouvrez le [portail Azure](https://portal.azure.com), déconnectez-vous, puis essayez à nouveau d’ouvrir ce lien en fournissant les informations d’identification correctes.

## <a name="html-storage"></a>403 ... Stockage HTML5
Notre portail utilise HTML5 localStorage et sessionStorage.

* Chrome : Paramètres, Confidentialité, Paramètres de content.
* Internet Explorer : Options Internet, onglet Avancé, Sécurité, Activer le stockage DOM

![403... essayez d’activer le stockage HTML5](media/analytics-troubleshooting/060.png)

## <a name="e-g"></a>404 ... Abonnement introuvable
![404 ... Abonnement introuvable](media/analytics-troubleshooting/070.png)

L’URL n’est pas valide. 

* Ouvrez la ressource d’application dans le [portail Application Insights](https://portal.azure.com). Utilisez ensuite le bouton Analytics.

## <a name="e-h"></a>404... page inexistante
![404 ... Page inexistante](media/analytics-troubleshooting/080.png)

L’URL n’est pas valide.

* Ouvrez la ressource d’application dans le [portail Application Insights](https://portal.azure.com). Utilisez ensuite le bouton Analytics.

## <a name="cookies"></a>Activer les cookies tiers
  Consultez la page [Comment désactiver les cookies tiers](https://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), mais notez que nous devons les **activer** .


[!INCLUDE [app-insights-analytics-footer](../../../includes/app-insights-analytics-footer.md)]

