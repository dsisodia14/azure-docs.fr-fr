---
title: Déployer Azure Cognitive Services sur Azure Stack | Microsoft Docs
description: Découvrez comment déployer Azure Cognitive Services sur Azure Stack.
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
ms.date: 12/11/2018
ms.author: mabrigg
ms.reviewer: guanghu
ms.lastreviewed: 12/11/2018
ms.openlocfilehash: 1ccbe8b268725cf3d0747486a20e0597d023662e
ms.sourcegitcommit: e51e940e1a0d4f6c3439ebe6674a7d0e92cdc152
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/08/2019
ms.locfileid: "55890601"
---
# <a name="deploy-azure-cognitive-services-to-azure-stack"></a>Déployer Azure Cognitive Services sur Azure Stack

*S’applique à : systèmes intégrés Azure Stack et Kit de développement Azure Stack*

> [!Note]  
> Azure Cognitive Services sur Azure Stack est disponible en préversion.

Vous pouvez utiliser Azure Cognitive Services avec prise en charge des conteneurs sur Azure Stack. La prise en charge des conteneurs dans Azure Cognitive Services vous permet d’utiliser les mêmes API puissantes que celles disponibles dans Azure. L’utilisation des conteneurs vous offre une flexibilité quant à l’emplacement où vous déployez et hébergez les services délivrés dans des [conteneurs Docker](https://www.docker.com/what-container). La prise en charge des conteneurs est désormais disponible en préversion pour quelques solutions Azure Cognitive Services, dont des composants de [Vision par ordinateur](https://docs.microsoft.com/azure/cognitive-services/computer-vision/home), [Visage](https://docs.microsoft.com/azure/cognitive-services/face/overview), [Analyse de texte](https://docs.microsoft.com/azure/cognitive-services/text-analytics/overview) et [Language Understanding](https://docs.microsoft.com/azure/cognitive-services/luis/luis-container-howto) (LUIS).

La conteneurisation est une méthode de distribution de logiciels dans laquelle une application ou un service, y compris ses dépendances et sa configuration, est empaqueté(e) en tant qu’image conteneur. Avec peu ou aucune modification, vous pouvez déployer une image sur un hôte de conteneur. Chaque conteneur est isolé des autres conteneurs et du système d’exploitation sous-jacent. Le système proprement dit a uniquement les composants nécessaires pour exécuter votre image. Un hôte de conteneur a un encombrement inférieur à celui d’une machine virtuelle. De plus, vous pouvez créer des conteneurs à partir d’images pour les tâches à court terme et les supprimer quand vous n’en avez plus besoin.

## <a name="use-containers-with-cognitive-services-on-azure-stack"></a>Utiliser des conteneurs avec Cognitive Services sur Azure Stack

- **Contrôle des données**  
  Autorisez les utilisateurs de votre application à contrôler leurs données lors de l’utilisation de Cognitive Services. Vous pouvez distribuer Cognitive Services aux utilisateurs de l’application qui ne peuvent pas envoyer de données vers le cloud public ou Azure mondial.

- **Contrôle des mises à jour des modèles**  
  Fournissez aux utilisateurs de votre application la version et la mise à jour des modèles déployés dans leur solution.

- **Architecture portable**  
  Facilitez la création d'une architecture d'application portable afin de pouvoir déployer votre solution sur le cloud public, sur un cloud privé local ou à la périphérie. Vous pouvez déployer votre conteneur sur Azure Kubernetes Service, Azure Container Instances ou un cluster Kubernetes dans Azure Stack. Pour plus d’informations, consultez [Déployer Kubernetes sur Azure Stack](https://docs.microsoft.com/azure/azure-stack/user/azure-stack-solution-template-kubernetes-deploy).

- **Haut débit et faible latence**  
   Offrez aux utilisateurs de votre application la possibilité de mettre à l’échelle avec des pics de trafic pour un débit élevé et une faible latence. Activez Cognitive Services pour une exécution dans Azure Kubernetes Service physiquement proche de leur logique d’application et de leurs données.

Avec Azure Stack, déployez des conteneurs Cognitive Services dans un cluster Kubernetes avec vos conteneurs d’application pour une haute disponibilité et une mise à l’échelle élastique. Vous pouvez développer votre application en combinant Cognitive services avec des composants reposant sur App Services, Functions, Stockage Blob, ou des bases de données SQL ou mySQL. 

Pour plus d’informations sur les conteneurs Cognitive Services, consultez [Prise en charge des conteneurs dans Azure Cognitive Services](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-container-support).

## <a name="deploy-the-azure-face-api"></a>Déployer l’API Visage Azure

Cet article décrit comment déployer l’API Visage Azure sur un cluster Kubernetes sur Azure Stack. Vous pouvez adopter la même approche pour déployer d’autres conteneurs Cognitive Services sur un cluster Kubernetes Azure Stack.

## <a name="prerequisites"></a>Prérequis

Avant de commencer, vous devrez :

1.  Demander l’accès au registre de conteneurs pour extraire des images conteneurs Visage à partir d’Azure Cognitive Services Container Registry. Pour plus d’informations, accédez à la section [Demander l’accès au registre de conteneurs privé](https://docs.microsoft.com/azure/cognitive-services/face/face-how-to-install-containers#request-access-to-the-private-container-registry).

2.  Préparer un cluster Kubernetes sur Azure Stack. Vous pouvez suivre les instructions fournies dans l’article [Déployer Kubernetes sur Azure Stack](azure-stack-solution-template-kubernetes-deploy.md).

## <a name="create-azure-resources"></a>Créer des ressources Azure

Créez une ressource Cognitive Services sur Azure pour afficher un aperçu des conteneurs Visage, LUIS ou Reconnaître le texte, respectivement. Vous devrez utiliser la clé d’abonnement et l’URL de point de terminaison de la ressource pour instancier les conteneurs Cognitive Services.

1.  Créez une ressource Azure dans le portail Azure. Si vous souhaitez afficher un aperçu des conteneurs Visage, vous devez d’abord créer une ressource Visage correspondante dans le portail Azure. Pour plus d’informations, consultez [Démarrage rapide : Créer un compte Cognitive Services dans le portail Azure](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account).

    >  [!Note]  
    >  La ressource Visage ou Vision par ordinateur doit utiliser le niveau tarifaire F0.

2.  Obtenez l’URL de point de terminaison et la clé d’abonnement pour la ressource Azure. Une fois la ressource Azure créée, vous devez utiliser la clé d’abonnement et l’URL de point de terminaison de cette ressource pour instancier le conteneur Visage, LUIS ou Reconnaître le texte correspondant pour l’aperçu.

## <a name="create-a-kubernetes-secret"></a>Créer un secret Kubernetes 

Utilisez la commande de création de secret Kubectl pour accéder au registre de conteneurs privé. Remplacez **&lt;username&gt;** par le nom d’utilisateur et **&lt;password&gt;** par le mot de passe fourni dans les informations d’identification envoyées par l’équipe Azure Cognitive Services.

```bash  
    kubectl create secret docker-registry <secretName> \
        --docker-server='containerpreview.azurecr.io' \
        --docker-username='<username>' \
        --docker-password='<password>' 
```

## <a name="prepare-a-yaml-configure-file"></a>Préparer un fichier de configuration YAML

Vous allez utiliser le fichier de configuration YAML pour simplifier le déploiement du service cognitif sur le cluster Kubernetes.

Voici un exemple de fichier de configuration YAML pour déployer le service Visage sur Azure Stack :

```Yaml  
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: <deploymentName>
spec:
  replicas: <replicaNumber>
  template:
    metadata:
      labels:
        app: <appName>
    spec:
      containers:
      - name: <containersName>
        image: <ImageLocation>
        env: 
        - name: EULA
          value: accept 
        - name: Billing
          value: <billingURL> 
        - name: apikey
          value: <apiKey>
        tty: true
        stdin: true
        ports:
        - containerPort: 5000 
      imagePullSecrets:
        - name: <secretName>
---
apiVersion: v1
kind: Service
metadata:
  name: <LBName>
spec:
  type: LoadBalancer
  ports:
  - port: 5000
    targetPort : 5000
    name: <PortsName>
  selector:
    app: <appName>
```

Dans ce fichier de configuration YAML, utilisez le secret que vous avez utilisé pour obtenir les images conteneurs du service cognitif à partir d’Azure Container Registry. Vous utilisez le fichier de secret pour déployer un réplica spécifique du conteneur. Vous créez également un équilibreur de charge pour vous assurer que les utilisateurs peuvent accéder à ce service en externe.

Détails concernant les principaux champs :

| Champ | Notes |
| --- | --- |
| replicaNumber | Définit les réplicas d’instances initiaux à créer. Vous pourrez effectuer une mise à l’échelle après le déploiement. |
| ImageLocation | Indique l’emplacement de l’image conteneur de service cognitif spécifique dans ACR. Par exemple, le service Visage : `aicpppe.azurecr.io/microsoft/cognitive-services-face` |
| BillingURL |URL de point de terminaison notée à l’étape [Créer une ressource Azure](#create-azure-resources). |
| ApiKey | Clé d’abonnement notée à l’étape [Créer une ressource Azure](#create-azure-resources). |
| SecretName | Nom du secret noté à l'étape Créer un secret pour accéder au registre de conteneurs privé |

## <a name="deploy-the-cognitive-service"></a>Déployer le service cognitif

Utilisez la commande suivante pour déployer les conteneurs de service cognitif :

```bash  
    Kubectl apply -f <yamlFineName>
```
Utilisez la commande suivante pour superviser le déploiement : 
```bash  
    Kubectl get pod – watch
```

## <a name="test-the-cognitive-service"></a>Tester le service cognitif

Accédez à la [spécification OpenAPI](https://swagger.io/docs/specification/about/) (anciennement Swagger), qui décrit les opérations prises en charge par un conteneur instancié à partir de l’URI relatif **/swagger** pour ce conteneur. Par exemple, l’URI suivant permet d’accéder à la spécification OpenAPI pour le conteneur Analyse des sentiments instancié dans l’exemple précédent :

```HTTP  
http:<External IP>:5000/swagger
```

Vous pouvez obtenir l’adresse IP externe à l’aide de la commande suivante : 

```bash  
    Kubectl get svc <LoadBalancerName>
```

## <a name="try-the-services-with-python"></a>Essayer les services avec Python

Vous pouvez essayer de valider les services cognitifs sur votre système Azure Stack en exécutant quelques scripts Python simples. Il existe des exemples de guide de démarrage rapide Python officiels pour [Vision par ordinateur](https://docs.microsoft.com/azure/cognitive-services/computer-vision/home), [Visage](https://docs.microsoft.com/azure/cognitive-services/face/overview), [Analyse de texte](https://docs.microsoft.com/azure/cognitive-services/text-analytics/overview) et [Language Understanding](https://docs.microsoft.com/azure/cognitive-services/luis/luis-container-howto) (LUIS) pour référence.

Deux points doivent être pris en compte lors de l’exécution de l’application Python sur les services exécutés sur des conteneurs : 
1. Les services cognitifs dans le conteneur n’ont pas besoin de sous-clés pour l’authentification, mais nous devons quand même entrer une chaîne comme espace réservé pour satisfaire le SDK. 
2. Remplacez base_URL par l’adresse IP réelle du point de terminaison de service. 

Voici un exemple de script Python qui utilise le SDK Python des services Visage pour détecter et encadrer des visages dans une image. 

```Python  
import cognitive_face as CF

# Cognitive Services in container do not need sub keys for authentication
# Keep the invalid key to satisfy the SDK inputs requirement. 
KEY = '0'  #  (keeping the quotes in place).
CF.Key.set(KEY)

# Get your actual Ip Address of service endpoint of your cognitive service on Azure Stack
BASE_URL = 'http://<svc IP Address>:5000/face/v1.0/'  
CF.BaseUrl.set(BASE_URL)

# You can use this example JPG or replace the URL below with your own URL to a JPEG image.
img_url = 'https://raw.githubusercontent.com/Microsoft/Cognitive-Face-Windows/master/Data/detection1.jpg'
faces = CF.face.detect(img_url)
print(faces)

```

## <a name="next-steps"></a>Étapes suivantes

[Guide pratique pour installer et exécuter des conteneurs d’API Vision par ordinateur](https://docs.microsoft.com/azure/cognitive-services/computer-vision/computer-vision-how-to-install-containers)

[Guide pratique pour installer et exécuter des conteneurs d’API Visage](https://docs.microsoft.com/azure/cognitive-services/face/face-how-to-install-containers)

[Guide pratique pour installer et exécuter des conteneurs d’API Analyse de texte](https://docs.microsoft.com/azure/cognitive-services/text-analytics/how-tos/text-analytics-how-to-install-containers)

[Guide pratique pour installer et exécuter des conteneurs LUIS (Language Understanding)](https://docs.microsoft.com/azure/cognitive-services/luis/luis-container-howto)
