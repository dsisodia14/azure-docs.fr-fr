---
title: Configuration d’alertes dans Azure Application Insights | Microsoft Docs
description: Tenez-vous informé des temps de réponse lents, des exceptions et des autres changements de performances ou d’utilisation de votre application web.
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm
ms.reviewer: lagayhar
ms.assetid: f8ebde72-f819-4ba5-afa2-31dbd49509a5
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.topic: conceptual
ms.date: 01/23/2019
ms.author: mbullwin
ms.openlocfilehash: 233ce5623195a9a661f67b5c3ded40e68c8eb33a
ms.sourcegitcommit: 8115c7fa126ce9bf3e16415f275680f4486192c1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54843512"
---
# <a name="set-alerts-in-application-insights"></a>Configuration d’alertes dans Application Insights
[Azure Application Insights][start] peut vous signaler les modifications des métriques de performances ou d’utilisation de votre application web. 

Application Insights analyse votre application en direct sur un [large éventail de plateformes][platforms] pour vous aider à diagnostiquer les problèmes de performances et comprendre les schémas d’utilisation.

Il existe trois types d’alertes :

* Les **alertes de métrique** indiquent quand une métrique dépasse une valeur seuil pendant une certaine période, comme les temps de réponse, le nombre d’exceptions, l’utilisation du processeur ou les affichages de page. 
* Les [**tests web**][availability] indiquent quand votre site est indisponible sur Internet ou répond lentement. [En savoir plus][availability].
* Les [**diagnostics proactifs**](../../azure-monitor/app/proactive-diagnostics.md) sont configurés automatiquement pour vous informer des modèles de performances exceptionnelles.

Dans cet article, nous allons nous concentrer sur les alertes métriques.

## <a name="set-a-metric-alert"></a>Définir une alerte métrique
Ouvrez le panneau des règles d’alerte, puis utilisez le bouton Ajouter. 

![Dans le panneau Règles d’alerte, cliquez sur Ajouter une alerte. Définissez votre application comme ressource à mesurer, fournissez un nom pour l’alerte et sélectionnez une métrique.](./media/alerts/01-set-metric.png)

* Définissez la ressource avant les autres propriétés. **Choisissez la ressource « (composants) »** si vous souhaitez définir des alertes sur les mesures de performances ou d'utilisation.
* Le nom que vous donnez à l’alerte doit être unique dans le groupe de ressources (pas uniquement dans votre application).
* Veillez à noter les unités dans lesquelles vous êtes invité à entrer la valeur seuil.
* Si vous cochez la case « Envoyer des e-mails aux propriétaires… », les alertes sont envoyées par e-mail à toutes les personnes ayant accès à ce groupe de ressources. Pour étendre cet ensemble de personnes, ajoutez-le au [groupe de ressources ou à l’abonnement](../../azure-monitor/app/resources-roles-access-control.md) (pas à la ressource).
* Si vous spécifiez « E-mails supplémentaires », les alertes sont envoyées à ces personnes ou groupes (que vous ayez ou non coché la case « Envoyer des e-mails aux propriétaires… »). 
* Définissez une [adresse de webhook](../../azure-monitor/platform/alerts-webhooks.md) si vous avez configuré une application web qui répondra aux alertes. Elle est appelée lorsque l’alerte est Activée ou Résolue. (Mais notez qu’à l’heure actuelle, les paramètres de requête ne sont pas transmis en tant que propriétés webhook.)
* Vous pouvez désactiver ou activer l'alerte avec les boutons en haut du panneau.

*Je ne vois pas apparaître le bouton Ajouter une alerte.* 

* Utilisez-vous un compte professionnel ? Vous pouvez définir des alertes si vous avez un accès propriétaire ou collaborateur à cette ressource d’application. Consultez le panneau Access Control. [En savoir plus sur le contrôle d’accès][roles].

> [!NOTE]
> Dans le panneau Alertes, vous pouvez constater qu’une alerte est déjà configurée : [Diagnostics proactifs](../../azure-monitor/app/proactive-failure-diagnostics.md). Cette alerte automatique surveille une métrique spécifique : le taux d’échec des demandes. Sauf si vous décidez de désactiver l’alerte proactive, vous n’avez pas besoin de définir votre propre alerte pour les taux d’échec des demandes. 
> 
> 

## <a name="see-your-alerts"></a>Consultez vos alertes
Vous recevez un e-mail lorsqu’une alerte bascule entre les états inactive et active. 

L’état actuel de chaque alerte est indiqué dans le panneau Règles d’alerte.

Il existe un résumé de l’activité récente dans la liste déroulante des alertes :

![Liste déroulante Alertes](./media/alerts/010-alert-drop.png)

L’historique des modifications d’état figure dans le journal d’activité :

![Dans le panneau Vue d’ensemble, cliquez sur Paramètres, puis sur Journaux d'audit.](./media/alerts/09-alerts.png)

## <a name="how-alerts-work"></a>Fonctionnement des alertes
* Une alerte possède trois états : « Jamais activé », « Activé » et « Résolu ». L’état Activé signifie que la condition spécifiée était vraie lors de la dernière évaluation.
* Une notification est générée lorsqu'une alerte change d'état. (Si la condition d'alerte était déjà vraie lorsque vous avez créé l'alerte, il est possible que vous ne receviez pas de notification tant que la condition n’est pas fausse.)
* Chaque notification génère un message électronique si vous avez coché la case E-mails ou fourni des adresses de messagerie électronique. Vous pouvez également consulter la liste déroulante Notifications.
* Une alerte est évaluée chaque fois qu’une mesure arrive, mais pas autrement.
* L’évaluation agrège la mesure de la période précédente, puis la compare à la valeur de seuil pour déterminer le nouvel état.
* La période que vous choisissez spécifie la durée pendant laquelle les mesures sont agrégées. Cela n’affecte pas la fréquence à laquelle l’alerte est évaluée, mais cela dépend de la fréquence d’arrivée des mesures.
* Si aucune donnée n’arrive pour une mesure particulière pendant un certain temps, l’écart a des effets différents sur l’évaluation de l’alerte et sur les graphiques dans Metrics Explorer. Dans Metrics Explorer, si aucune donnée n’apparaît plus longtemps que l’intervalle d’échantillonnage du graphique, le graphique affiche la valeur 0. Cependant, une alerte basée sur la même métrique n’est pas réévaluée et l’état de l’alerte reste inchangé. 
  
    Lorsque les données arrivent par la suite, le graphique revient à une valeur différente de zéro. L’alerte est évaluée en fonction des données disponibles pour la période spécifiée. Si le nouveau point de données est le seul disponible dans la période, l’agrégat repose uniquement sur ce point.
* Une alerte peut osciller fréquemment entre les états alerte et intègre même si vous définissez une longue période. Cela peut se produire si la valeur de la mesure est placée autour du seuil. Le seuil est cohérent : la transition vers l’état alerte se produit à la même valeur que la transition vers l’état intègre.

## <a name="what-are-good-alerts-to-set"></a>Quelles sont les alertes à définir ?
Cela dépend de votre application. Pour commencer, il est préférable de ne pas définir un trop grand nombre de métriques. Prenez le temps d’examiner vos graphiques de métriques pendant l’exécution de votre application, pour mieux comprendre comment elle se comporte normalement. Cet exercice vous aide à trouver des moyens d’améliorer ses performances. Définissez ensuite des alertes qui vous indiquent lorsque les métriques quittent la zone normale. 

Les alertes les plus appréciées sont les suivantes :

* Les [mesures de navigateur][client], surtout les **temps de chargement des pages** de navigateur, sont efficaces pour les applications web. Si votre page contient de nombreux scripts, vous devez rechercher d’éventuelles **exceptions du navigateur**. Pour obtenir ces métriques et alertes, vous devez configurer la [surveillance de page web][client].
* Le **temps de réponse de serveur** pour le côté serveur des applications web. Outre la définition des alertes, gardez un œil sur cette métrique pour voir si elle varie de façon importante avec un taux de demandes élevé. Une telle variation peut indiquer que votre application manque de ressources. 
* **Exceptions du serveur** - pour les afficher, vous devrez peut-être effectuer une [installation supplémentaire](../../azure-monitor/app/asp-net-exceptions.md).

N’oubliez pas que les [diagnostics de taux d’échec proactifs](../../azure-monitor/app/proactive-failure-diagnostics.md) analysent automatiquement le taux selon lequel votre application répond aux demandes avec des codes d’échec.

## <a name="who-receives-the-classic-alert-notifications"></a>Qui reçoit les notifications d’alerte (classiques) ?

Cette section ne s’applique qu’aux alertes classiques et vous aidera à optimiser vos notifications d’alertes pour vous assurer que seuls les destinataires de votre choix reçoivent les notifications. Pour mieux comprendre la différence entre les [alertes classiques](../platform/alerts-classic.overview.md) et les nouvelles alertes, reportez-vous à l’[article de présentation des alertes](../platform/alerts-overview.md). Pour contrôler la notification d’alerte dans l’expérience des nouvelles alertes, utilisez les [groupes d’actions](../platform/action-groups.md).

* Nous recommandons l’utilisation de destinataires spécifiques pour les notifications d’alertes classiques.

* Pour les alertes liées aux métriques Application Insights (notamment les métriques de disponibilité), l’option **bulk/group** check-box, si elle est activée, envoie des alertes aux utilisateurs ayant des rôles de propriétaire, contributeur ou lecteur dans l’abonnement. En effet, _tous_ les utilisateurs ayant accès à la ressource Application Insights sont dans la portée et recevront des notifications. 

> [!NOTE]
> Si vous utilisez actuellement l’option **bulk/group** et que vous la désactivez, vous ne pourrez pas annuler la modification.

Utilisez les nouvelles alertes d’expérience/alertes en temps réel si vous devez avertir les utilisateurs en fonction de leurs rôles. Avec les [groupes d’actions](../platform/action-groups.md), vous pouvez configurer des notifications par e-mail aux utilisateurs ayant n’importe quel rôle contributeur/propriétaire/lecteur (sans que ces rôles soient combinés en une même option).

## <a name="automation"></a>Automatisation
* [Utiliser PowerShell pour automatiser la configuration d’alertes](../../azure-monitor/app/powershell-alerts.md)
* [Utiliser les webhooks pour automatiser la réponse aux alertes](../../azure-monitor/platform/alerts-webhooks.md)

## <a name="video"></a>Vidéo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="see-also"></a>Voir aussi
* [Tests web de disponibilité](../../azure-monitor/app/monitor-web-app-availability.md)
* [Automatiser la configuration d’alertes](../../azure-monitor/app/powershell-alerts.md)
* [Diagnostics proactifs](../../azure-monitor/app/proactive-diagnostics.md) 

<!--Link references-->

[availability]: ../../azure-monitor/app/monitor-web-app-availability.md
[client]: ../../azure-monitor/app/javascript.md
[platforms]: ../../azure-monitor/app/platforms.md
[roles]: ../../azure-monitor/app/resources-roles-access-control.md
[start]: ../../azure-monitor/app/app-insights-overview.md

