---
title: Fichier Include
description: Fichier Include
services: application-insights
author: mrbullwinkle
ms.service: application-insights
ms.topic: include
ms.date: 06/21/2018
ms.author: mbullwin
ms.custom: include file
ms.openlocfilehash: 6b9b40c457766573be0d72cb7f4ebe2328a070f5
ms.sourcegitcommit: 25936232821e1e5a88843136044eb71e28911928
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/04/2019
ms.locfileid: "54026262"
---
Il existe certaines limites au nombre de mesures et d’événements par application (c'est-à-dire, par clé d'instrumentation). Les limites varient selon le [plan de tarification](https://azure.microsoft.com/pricing/details/application-insights/) que vous choisissez.

| Ressource | Limite par défaut | Remarque
| --- | --- | --- |
| Total des données par jour | 100 Go | Vous pouvez réduire les données en définissant une limite. Si vous avez besoin de davantage de données, vous pouvez augmenter la limite dans le portail, jusqu’à 1 000 Go. Pour une capacité supérieure à 1 000 Go, envoyez un e-mail à AIDataCap@microsoft.com.
| Limitation | 32 000 événements par seconde | La limite est mesurée par minute.
| Conservation des données | 90 jours | Cette ressource est pour [Recherche](../articles/azure-monitor/app/diagnostic-search.md), [Analytics](../articles/azure-monitor/app/analytics.md) et [Metrics Explorer](../articles/azure-monitor/app/metrics-explorer.md).
| Rétention des résultats détaillés du [test de disponibilité à plusieurs étapes](../articles/azure-monitor/app/monitor-web-app-availability.md#multi-step-web-tests) | 90 jours | Cette ressource fournit des résultats détaillés de chaque étape.
| Taille d’événement maximale | 64 K | 
| Longueur des noms de propriétés et de mesures | 150 | Consultez les [schémas par type](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/EndpointSpecs/Schemas/Docs/).
| Longueur de chaîne de valeur de propriété | 8 192 | Consultez les [schémas par type](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/EndpointSpecs/Schemas/Docs/).
| Longueur des messages de trace et d’exception | 10 000 | Consultez les [schémas par type](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/EndpointSpecs/Schemas/Docs/).
| Nombre de [tests de disponibilité](../articles/azure-monitor/app/monitor-web-app-availability.md) par application | 100 |
| Rétention de données [Profileur](../articles/azure-monitor/app/profiler.md) | 5 jours |
| Données [Profileur](../articles/azure-monitor/app/profiler.md) envoyées par jour | 10 Go |

Pour plus d’informations, consultez [Tarification et quotas dans Application Insights](../articles/azure-monitor/app/pricing.md).