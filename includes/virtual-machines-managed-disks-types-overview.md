---
title: Fichier Include
description: Fichier Include
services: virtual-machines
author: roygara
ms.service: virtual-machines
ms.topic: include
ms.date: 01/22/2019
ms.author: rogarana
ms.custom: include file
ms.openlocfilehash: 8a067474fb172d4ff7a7fdf7eb6d24536bd2d017
ms.sourcegitcommit: 9aa9552c4ae8635e97bdec78fccbb989b1587548
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/20/2019
ms.locfileid: "56443330"
---
# <a name="what-disk-types-are-available-in-azure"></a>Quels sont les types de disque disponibles dans Azure ?

Azure Managed Disks propose actuellement quatre types de disque, trois mis à la disposition générale (GA) et un en préversion. Ces quatre types de disque répondent à des scénarios clients qui leur sont propres.

## <a name="disk-comparison"></a>Comparaison des disques

Le tableau suivant offre une comparaison des niveaux SSD Ultra (préversion), SSD Premium, SSD Standard et HDD pour les disques managés afin de vous aider dans votre choix.

|   | SSD Ultra (préversion)   | SSD Premium   | SSD Standard   | HDD Standard   |
|---------|---------|---------|---------|---------|
|Type de disque   |SSD   |SSD   |SSD   |HDD   |
|Scénario   |Charges de travail gourmandes en E/S, telles que le système SAP HANA, les bases de données de niveau supérieur (par exemple, SQL et Oracle), et autres charges de travail très lourdes en transactions.   |Charges de travail de production et sensibles aux performances   |Serveurs web, applications d’entreprise peu utilisées et Dev/Test   |Sauvegarde, non critique, accès peu fréquent   |
|Taille du disque   |65 536 gibioctet (Gio) (préversion)   |4 095 Gio (GA), 32 767 Gio (préversion)    |4 095 Gio (GA), 32 767 Gio (préversion)   |4 095 Gio (GA), 32 767 Gio (préversion)   |
|Débit max.   |2 000 Mio/s (préversion)   |250 Mio/s (GA), 750 Mio/s (préversion)   |60 Mio/s (GA), 500 Mio/s (préversion)   |60 Mio/s (GA), 500 Mio/s (préversion)   |
|Nb max. d’E/S par seconde   |160 000 (préversion)   |7 500 (GA), 20 000 (préversion)   |500 (GA), 2 000 (préversion)   |500 (GA), 2 000 (préversion)   |

## <a name="ultra-ssd-preview"></a>SSD Ultra (préversion)

Les disques Ultra SSD d’Azure (préversion) fournissent un stockage de disque avec un haut débit, un nombre d’IOPS élevé et une faible latence homogène pour les machines virtuelles IaaS Azure. Entre autres avantages, Ultra SSD permet de changer dynamiquement les performances de disque en fonction de vos charges de travail sans avoir à redémarrer les machines virtuelles. Les disques SSD Ultra sont adaptés aux charges de travail qui consomment beaucoup de données comme SAP HANA, les bases de données de niveau supérieur et les charges de travail avec un grand nombre de transactions. Les disques SSD Ultra peuvent uniquement être utilisés en tant que disques de données. Nous vous recommandons d’utiliser des disques SSD Premium comme disques de système d’exploitation.

### <a name="performance"></a>Performances

Lorsque vous approvisionnez un disque Ultra, vous pouvez configurer de manière indépendante la capacité et les performances du disque. Les disques SSD Ultra se déclinent en plusieurs tailles fixes de 4 Gio à 64 Tio, et présentent un modèle de configuration de performances flexible qui vous permet de configurer les IOPS et le débit de manière indépendante.

Voici certaines fonctionnalités clés des disques Ultra SSD :

- Capacité du disque : La capacité des disques SSD Ultra s'échelonne de 4 Gio 64 Tio.
- IOPS du disque : Les disques SSD Ultra prennent en charge des limites d’IOPS de 300 IOPS/Gio, avec un maximum de 160 000 IOPS par disque. Pour atteindre le nombre d’IOPS provisionné, vérifiez que le nombre d’IOPS du disque sélectionné est inférieur au nombre d’IOPS de la machine virtuelle. Le nombre minimal d’IOPS du disque est 100.
- Débit du disque : Avec les disques SSD Ultra, la limite de débit d’un seul disque est de 256 Kio/s pour chaque IOPS approvisionnée, avec un maximum de 2000 Mbits/s par disque (où 1 Mbit/s = 10^6 octets par seconde). Le débit minimal du disque est 1 Mio.

### <a name="disk-size"></a>Taille du disque

|Taille de disque (Gio)  |Nombre limite d’IOPS  |Débit limite (Mbits/s)  |
|---------|---------|---------|
|4     |1,200         |300         |
|8     |2 400         |600         |
|16     |4 800         |1,200         |
|32     |9 600         |2 000         |
|64     |19 200         |2 000         |
|128     |38 400         |2 000         |
|256     |76 800         |2 000         |
|512     |80 000         |2 000         |
|1 024 à 65 536 (dans cette plage, les tailles augmentent par incréments de 1 Tio)     |160 000         |2 000         |

### <a name="preview-scope-and-limitations"></a>Limitations et étendue de la préversion

Dans la préversion, les disques Ultra SSD présentent les caractéristiques suivantes :

- Ils sont pris en charge dans la région USA Est 2 dans une seule zone de disponibilité  
- Ils peuvent être utilisés seulement avec des zones de disponibilité (les groupes à haute disponibilité et les déploiements de machine virtuelle individuelle en dehors des zones n’ont pas la possibilité d’attacher un disque Ultra)
- Ils sont pris en charge seulement sur les machines virtuelles ES/DS v3
- Ils sont disponibles seulement comme des disques de données et prennent en charge uniquement une taille de secteur physique de 4 k  
- Ils peuvent être créés seulement comme des disques vides  
- Actuellement, ils peuvent être déployés uniquement à l’aide de modèles Azure Resource Manager, de l’interface CLI et du SDK Python.
- Ils ne prennent pas encore en charge les instantanés de disque, les images de machine virtuelle, les groupes à haute disponibilité, les groupes de machines virtuelles identiques et Azure Disk Encryption.
- Ils ne prennent pas encore en charge l’intégration à la Sauvegarde Azure ou à Azure Site Recovery.
- Comme pour la  [plupart des préversions](https://azure.microsoft.com/support/legal/preview-supplemental-terms/), cette fonctionnalité ne doit pas être utilisée pour les charges de travail de production avant la mise en disponibilité générale.

## <a name="premium-ssd"></a>SSD Premium

Les disques SSD Premium Azure offrent une prise en charge très performante et une faible latence pour les machines virtuelles avec des charges de travail qui utilisent beaucoup d’entrée/sortie (E/S). Pour tirer parti de la vitesse et des performances des disques de stockage Premium, vous pouvez migrer les disques de machines virtuelles existantes vers des disques SSD Premium. Les disques SSD Premium sont adaptés aux applications de production critiques.

### <a name="disk-size"></a>Taille du disque

Les tailles signalées par un astérisque sont actuellement en préversion.

| Tailles de disque SSD Premium  | P4               | P6               | P10             | P15 | P20              | P30              | P40              | P50              | P60*              | P70*              | P80*              |
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------|------------------|------------------|------------------|------------------|
| Taille du disque (Gio)           | 32             | 64             | 128            | 256  | 512            | 1 024    | 2 048     | 4 095    | 8 192     | 16 384     | 32 767     |
| IOPS par disque       | Jusqu’à 120 | Jusqu’à 240              | Jusqu’à 500              | Jusqu’à 1 100 | Jusqu’à 2 300              | Jusqu’à 5 000              | Jusqu’à 7 500             | Jusqu’à 7 500              | Jusqu’à 12 500              | Jusqu’à 15 000              | Jusqu’à 20 000              |
| Débit par disque | Jusqu’à 25 Mio/s | Jusqu’à 50 Mio/s | Jusqu’à 100 Mio/s | Jusqu’à 125 Mio/s | Jusqu’à 150 Mio/s | Jusqu’à 200 Mio/s | Jusqu’à 250 Mio/s | Jusqu’à 250 Mio/s| Jusqu’à 480 Mio/s | Jusqu’à 750 Mio/s | Jusqu’à 750 Mio/s |

## <a name="standard-ssd"></a>SSD Standard

Les disques SSD Azure Standard constituent une option de stockage économique optimisée pour les charges de travail nécessitant des performances cohérentes à des niveaux d’IOPS bas. Les disques SSD Standard offrent une bonne expérience de niveau d’entrée pour ceux qui souhaitent migrer vers le cloud, en particulier si vous rencontrez des problèmes de variation avec les charges de travail exécutées sur vos solutions HDD locales. Les disques SSD standard offrent une meilleure disponibilité, cohérence, fiabilité et latence par rapport aux disques HDD. Les disques SSD Standard sont adaptés aux serveurs web, serveurs d’applications avec peu d’IOPS, applications d’entreprise peu utilisées et charges de travail Dev/Test.

### <a name="disk-size"></a>Taille du disque

Les tailles signalées par un astérisque sont actuellement en préversion.

| Tailles de disque SSD Standard  | E10               | E15               | E20             | E30 | E40              | E50              | E60*              | E70*              | E80*              |
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------|------------------|------------------|
| Taille du disque (Gio)           | 128             | 256             | 512            | 1 024  | 2 048            | 4 095     | 8 192     | 16 384     | 32 767    |
| IOPS par disque       | Jusqu’à 500              | Jusqu’à 500              | Jusqu’à 500              | Jusqu’à 500 | Jusqu’à 500              | Jusqu’à 500              | Jusqu’à 500             | Jusqu’à 500              | Jusqu’à 1 300              | Jusqu’à 2 000              | Jusqu’à 2 000              |
| Débit par disque | Jusqu’à 60 Mio/s | Jusqu’à 60 Mio/s | Jusqu’à 60 Mio/s | Jusqu’à 60 Mio/s | Jusqu’à 60 Mio/s | Jusqu’à 60 Mio/s | Jusqu’à 60 Mio/s | Jusqu’à 60 Mio/s| Jusqu’à 300 Mio/s |  Jusqu’à 500 Mio/s | Jusqu’à 500 Mio/s |

## <a name="standard-hdd"></a>HDD Standard

Les disques HDD standard Azure offrent une prise en charge fiable et économique des disques des machines virtuelles exécutant des charges de travail non sensibles aux latences. Il prend également en charge les objets blob, les tables, les files d’attente et les fichiers. Dans le cadre d’un stockage Standard, les données sont stockées sur des disques durs. Lorsque vous utilisez des machines virtuelles, vous pouvez utiliser des disques SSD et HDD Standard pour les scénarios Dev/Test et les charges de travail moins critiques. Le stockage Standard est disponible dans toutes les régions Azure.

### <a name="disk-size"></a>Taille du disque

Les tailles signalées par un astérisque sont actuellement en préversion.

| Type de disque Standard  | S4               | S6               | S10             | S15 | S20              | S30              | S40              | S50              | S60*              | S70*              | S80*              |
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------|------------------|------------------|------------------|------------------|
| Taille du disque en Gio          | 32             | 64             | 128            | 256  | 512            | 1 024    | 2 048     | 4 095    | 8 192     | 16 384     | 32 767     |
| IOPS par disque       | Jusqu’à 500              | Jusqu’à 500              | Jusqu’à 500              | Jusqu’à 500 | Jusqu’à 500              | Jusqu’à 500              | Jusqu’à 500             | Jusqu’à 500              | Jusqu’à 1 300              | Jusqu’à 2 000              | Jusqu’à 2 000              |
| Débit par disque | Jusqu’à 60 Mio/s | Jusqu’à 60 Mio/s | Jusqu’à 60 Mio/s | Jusqu’à 60 Mio/s | Jusqu’à 60 Mio/s | Jusqu’à 60 Mio/s | Jusqu’à 60 Mio/s | Jusqu’à 60 Mio/s| Jusqu’à 300 Mio/s | Jusqu’à 500 Mio/s | Jusqu’à 500 Mio/s |

## <a name="billing"></a>Facturation

Lorsque vous utilisez des disques managés, les considérations de facturation suivantes s’appliquent :

- Type de disque
- Taille des disques managés
- Instantanés
- Transferts de données sortantes
- Nombre de transactions

**Taille des disques managés** : les disques managés sont facturés selon la taille provisionnée. Azure fait correspondre la taille provisionnée (arrondie à la valeur supérieure) à la taille de disque offerte la plus proche. Pour plus d’informations sur les tailles de disque proposées, consultez les tableaux précédents. Chaque disque correspond à une offre de taille de disque configurée prise en charge, et est facturé en conséquence. Par exemple, si vous avez provisionné un disque SSD Standard de 200 Gio, celui-ci correspond à l’offre de taille de disque E15 (256 Gio). La facturation de n’importe quel disque configuré est calculée au prorata horaire sur la base du tarif mensuel de l’offre de stockage Premium. Par exemple, si vous provisionnez un disque E10 et le supprimez au bout de 20 heures, l’offre E10 vous est facturée au prorata de 20 heures. Le montant facturé est indépendant de la quantité de données écrites sur le disque.

**Instantanés** : Les instantanés facturés en fonction de la taille utilisée. Par exemple, si vous créez une capture instantanée d’un disque managé avec une capacité approvisionnée de 64 Gio et une taille des données utilisées réelle de 10 Gio, l'instantané est facturé uniquement pour la taille des données utilisées de 10 Gio.
