---
title: Déployer Kubernetes sur Azure Stack à l’aide d’Azure Active Directory (Azure AD) | Microsoft Docs
description: Découvrez comment déployer Kubernetes sur Azure Stack à l’aide d’Azure Active Directory (Azure AD).
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2019
ms.author: mabrigg
ms.reviewer: waltero
ms.lastreviewed: 01/16/2019
ms.openlocfilehash: b7214230d55831fa33d547ecf9e65051aa5bb4d9
ms.sourcegitcommit: e51e940e1a0d4f6c3439ebe6674a7d0e92cdc152
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/08/2019
ms.locfileid: "55891451"
---
# <a name="deploy-kubernetes-to-azure-stack-using-azure-active-directory"></a>Déployer Kubernetes sur Azure Stack à l’aide d’Azure Active Directory

*S’applique à : systèmes intégrés Azure Stack et Kit de développement Azure Stack*

> [!Note]  
> Kubernetes sur Azure Stack est en préversion. Le scénario Azure Stack déconnecté n'est actuellement pas pris en charge par la préversion.

Vous pouvez suivre les étapes décrites dans cet article pour déployer et configurer les ressources pour Kubernetes lorsque vous utilisez Azure Active Directory (Azure AD) comme service de gestion des identités en une seule et même opération.

## <a name="prerequisites"></a>Prérequis

Pour commencer, assurez-vous que vous disposez des autorisations appropriées et que votre Azure Stack est prêt.

1. Vérifiez que vous pouvez créer des applications dans votre client Azure Active Directory (Azure AD). Ces autorisations sont nécessaires pour le déploiement de Kubernetes.

    Pour obtenir des instructions sur la vérification de vos autorisations, voir [Vérifier les autorisations Azure Active Directory](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal).

1. Générez une paire de clés publique et privée SSH pour vous connecter à la machine virtuelle Linux sur Azure Stack. Vous aurez besoin de la clé publique lors de la création du cluster.

    Pour obtenir des instructions sur la génération d’une clé, voir [Génération d’une clé SSH](https://github.com/msazurestackworkloads/acs-engine/blob/master/docs/ssh.md#ssh-key-generation).

1. Vérifiez que vous avez un abonnement valide dans votre portail de client Azure Stack et que vous disposez d’un nombre suffisant d’adresses IP publiques pour ajouter de nouvelles applications.

    Vous ne pouvez pas déployer le cluster sur un abonnement **Administrateur** Azure Stack. Vous devez utiliser un abonnement **Utilisateur**. 

1. Si Cluster Kubernetes ne figure pas dans votre Place de marché, contactez votre administrateur Azure Stack.

## <a name="create-a-service-principal"></a>Créer un principal du service

Créer un principal de service dans Azure. Le principal de service offre à votre application l’accès aux ressources Azure Stack.

1. Connectez-vous au [portail Azure](http://portal.azure.com) global.

1. Vérifiez que vous vous êtes connecté à l’aide du locataire Azure AD associé à l’instance Azure Stack. Vous pouvez changer d’identification en cliquant sur l’icône de filtre dans la barre d’outils Azure.

    ![Sélectionner votre locataire AD](media/azure-stack-solution-template-kubernetes-deploy/tenantselector.png)

1. Créez une application Azure AD.

    a. Sélectionnez **Azure Active Directory** > **Inscriptions des applications** > **Nouvelle inscription d’application**.

    b. Entrez le **nom** de l’application.

    c. Sélectionnez **Application web/API**.

    d. Entrez l’**URL de connexion** `http://localhost`.

    c. Cliquez sur **Créer**.

1. Notez l’**ID d’application**. Vous aurez besoin de l’ID lors de la création du cluster. L’ID est référencé en tant qu’**ID client du principal de service**.

1. Sélectionnez **Paramètres** > **Clés**.

    a. Entrez la **Description**.

    b. Pour **Expire**, sélectionnez **N’expire jamais**.

    c. Sélectionnez **Enregistrer**. Notez la chaîne de clé. Vous aurez besoin de la chaîne de clé lors de la création du cluster. La clé est référencée comme **Secret client du principal de service**.

## <a name="give-the-service-principal-access"></a>Accorder l’accès au principal de service

Accordez l’accès à votre abonnement au principal de service afin qu’il puisse créer des ressources.

1.  Connectez-vous au [portail Azure Stack](https://portal.local.azurestack.external/).

1. Sélectionnez **Tous les services** > **Abonnements**.

1. Sélectionnez l’abonnement créé par votre opérateur pour utiliser le cluster Kubernetes.

1. Sélectionnez **Contrôle d’accès (IAM)**  > **Ajouter une attribution de rôle**.

1. Sélectionnez le rôle **Contributeur**.

1. Sélectionnez le nom de l’application créée pour votre principal de service. Vous devrez peut-être taper le nom dans la zone de recherche.

1. Cliquez sur **Enregistrer**.

## <a name="deploy-kubernetes"></a>Déployer Kubernetes

1. Ouvrez le [portail Azure Stack](https://portal.local.azurestack.external).

1. Sélectionnez **Créer une ressource** > **Calcul** > **Cluster Kubernetes**. Cliquez sur **Créer**.

    ![Déployer un modèle de solution](media/azure-stack-solution-template-kubernetes-deploy/01_kub_market_item.png)

### <a name="1-basics"></a>1. Concepts de base

1. Dans le volet Créer un cluster Kubernetes, sélectionnez **Bases**.

    ![Déployer un modèle de solution](media/azure-stack-solution-template-kubernetes-deploy/02_kub_config_basic.png)

1. Sélectionnez votre ID **d’abonnement**.

1. Entrez le nom d’un nouveau groupe de ressources ou sélectionnez un groupe de ressources existant. Le nom de la ressource doit être alphanumérique et en minuscules.

1. Sélectionnez **l’emplacement** du groupe de ressources. Il s’agit de la région que vous avez choisie pour votre installation Azure Stack.

### <a name="2-kubernetes-cluster-settings"></a>2. Paramètres de cluster Kubernetes

1. Dans le volet Créer un cluster Kubernetes, sélectionnez **Kubernetes Cluster Settings** (Paramètres de cluster Kubernetes).

    ![Déployer un modèle de solution](media/azure-stack-solution-template-kubernetes-deploy/03_kub_config_settings-aad.png)

1. Entrez le **nom de l’utilisateur administrateur de la machine virtuelle Linux**. Nom d’utilisateur pour les machines virtuelles Linux qui font partie du cluster Kubernetes et de DVM.

1. Entrez la **Clé publique SSH** utilisée pour l’autorisation sur toutes les machines Linux, créée en même temps que le cluster Kubernetes et DVM.

1. Entrez le **Préfixe DNS du profil principal** qui est unique pour la région. Il doit s’agir d’un nom unique pour la région, tel que `k8s-12345`. Nous vous recommandons d’essayer de choisir le même préfixe que celui du nom du groupe de ressources.

    > [!Note]  
    > Pour chaque cluster, utilisez un préfixe DNS de profil principal nouveau et unique.

1. Sélectionnez la valeur du champ **Kubernetes Master Pool Profile Count** (Nombre de profils de pool maître Kubernetes). Il s’agit du nombre de nœuds dans le pool maître. Elle peut être comprise entre 1 et 7. Cette valeur doit être un nombre impair.

1. Sélectionnez la valeur du champ **The VMSize of the Kubernetes master VMs** (Taille des machines virtuelles maîtres Kubernetes).

1. Sélectionnez la valeur du champ **Kubernetes Node Pool Profile Count** (Nombre de profils de pool de nœuds Kubernetes). Il s’agit du nombre d’agents dans le cluster. 

1. Sélectionnez la valeur du champ **Storage Profile** (Profil de stockage). Vous pouvez choisir **Blob Disk** (Disque de blob) ou **Managed Disk** (Disque managé). Cette opération spécifie la taille des machines virtuelles de nœud Kubernetes. 

1. Sélectionnez **Azure AD** comme **système d’identité Azure Stack** pour votre installation Azure Stack. 

1. Entrez **l’ID client du principal de service**. Celui-ci est utilisé par le fournisseur cloud d’Azure Kubernetes. Il s’agit de l’ID client identifié en tant qu’ID d’application lorsque vous avez créé votre principal de service.

1. Entrez le **Secret client du principal du service** que vous avez créé au moment de la création de votre principal de service.

1. Entrez la **version du fournisseur cloud d’Azure Kubernetes**. Il s’agit de la version du fournisseur d’Azure Kubernetes. Azure Stack publie une build Kubernetes personnalisée pour chaque version d’Azure Stack.

### <a name="3-summary"></a>3. Résumé

1. Sélectionnez Résumé. Le panneau affiche un message de validation concernant vos paramètres de configuration de cluster Kubernetes.

    ![Déployer un modèle de solution](media/azure-stack-solution-template-kubernetes-deploy/04_preview.png)

2. Passez vos paramètres en revue.

3. Sélectionnez **OK** pour déployer votre cluster.

> [!TIP]  
>  Si vous avez des questions concernant votre déploiement, vous pouvez poster votre question ou lire la réponse si quelqu’un y a déjà répondu sur le [Forum Azure Stack](https://social.msdn.microsoft.com/Forums/azure/home?forum=azurestack).


## <a name="next-steps"></a>Étapes suivantes

[Se connecter à votre cluster](azure-stack-solution-template-kubernetes-deploy.md#connect-to-your-cluster)
