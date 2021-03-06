---
title: Exemples de notebooks Jupyter
titleSuffix: Azure Machine Learning service
description: Recherchez des exemples de notebooks Jupyter pour explorer Azure Machine Learning service en Python.
services: machine-learning
ms.service: machine-learning
ms.subservice: core
ms.topic: sample
author: sdgilley
ms.author: sgilley
ms.reviewer: sgilley
ms.date: 12/04/2018
ms.custom: seodec18
ms.openlocfilehash: 12da1b20c5e4e6299445b8ec8ec90eeec6711e2c
ms.sourcegitcommit: 7f7c2fe58c6cd3ba4fd2280e79dfa4f235c55ac8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/25/2019
ms.locfileid: "56805516"
---
# <a name="use-jupyter-notebooks-to-explore-azure-machine-learning-service"></a>Utiliser des notebooks Jupyter pour explorer Azure Machine Learning service

Par souci pratique, nous avons développé une série de notebooks Jupyter Python que vous pouvez utiliser pour explorer Azure Machine Learning service. 

Découvrez comment utiliser le service en suivant la documentation de ce site et personnaliser les notebooks en fonction de vos besoins. 

Utilisez l’un des chemins ci-dessous pour exécuter un serveur de notebooks avec ces exemples de notebooks.  Une fois que le serveur est en cours d’exécution, recherchez des notebooks de tutoriels dans le dossier des **tutoriels** ou explorez les différentes fonctionnalités dans le dossier **how-to-utilisation-azureml**.


## <a name="try-azure-notebooks-free-jupyter-notebooks-in-the-cloud"></a>Essayez Azure Notebooks : Notebooks Jupyter gratuits dans le cloud

La prise en main d’Azure Notebooks est simple. Le [kit SDK Azure Machine Learning pour Python](https://aka.ms/aml-sdk) est déjà installé et configuré dans [Azure Notebooks](https://notebooks.azure.com/). L’installation et les futures mises à jour sont gérées automatiquement par le biais des services Azure.
  
[!INCLUDE [aml-azure-notebooks](../../../includes/aml-azure-notebooks.md)]


## <a name="use-a-data-science-virtual-machine-dsvm"></a>Utiliser Data Science Virtual Machine (DSVM)

Le [SDK Azure Machine Learning pour Python](https://aka.ms/aml-sdk) et le serveur de notebooks sont déjà installés et configurés dans une machine DSVM. 

Après avoir [créé une machine DSVM](how-to-configure-environment.md#dsvm), effectuez les étapes suivantes sur la machine DSVM pour exécuter les notebooks.

[!INCLUDE [aml-dsvm-server](../../../includes/aml-dsvm-server.md)]


## <a name="use-your-own-jupyter-notebook-server"></a>Utiliser votre propre serveur de notebooks Jupyter

Utilisez ces étapes pour créer une instance locale de serveur de notebooks Jupyter sur votre ordinateur.

[!INCLUDE [aml-your-server](../../../includes/aml-your-server.md)]

Les instructions de démarrage rapide permettent d’installer les packages nécessaires pour exécuter les notebooks de démarrage rapide et de tutoriel.  D’autres exemples de notebooks peuvent nécessiter l’installation de composants supplémentaires.  Pour plus d’informations sur ces composants, consultez [Installer le Kit SDK Azure Machine Learning pour Python](https://docs.microsoft.com/python/api/overview/azure/ml/install).

<a name="automated-ml-setup"></a>

## <a name="automated-machine-learning-setup"></a>Configuration de Machine Learning automatisé 

_Les étapes suivantes s’appliquent uniquement aux notebooks du dossier **how-to-use-azureml/automated-machine-learning**._

Vous pouvez utiliser l’une des options ci-dessus, ou bien installer l’environnement et créer un espace de travail simultanément, en suivant les instructions ci-dessous. 

1. Installez [Mini-conda](https://conda.io/miniconda.html). Choisissez la version 3.7 ou ultérieure. Suivez les invites pour procéder à l’installation. 
   >[!NOTE]
   >Vous pouvez utiliser une installation existante de conda, du moment que sa version est égale ou supérieure à 4.4.10. Pour afficher la version, utilisez `conda -V`. Vous pouvez mettre à jour une version de conda avec la commande `conda update conda`. Il n’est pas nécessaire d’installer mini-conda.

1. Téléchargez les exemples de notebooks [GitHub](https://github.com/Azure/MachineLearningNotebooks/tree/master/how-to-use-azureml/automated-machine-learning
) sous la forme d’un fichier zip, puis extrayez le contenu dans un répertoire local. Les notebooks du machine learning automatisé se trouvent dans le dossier `how-to-use-azureml/automated-machine-learning`.

1. Configurez un nouvel environnement Conda. 
   1. Ouvrez une invite Conda sur votre ordinateur local.
   
   1. Accédez aux fichiers que vous avez extraits sur votre ordinateur local.
   
   1. Ouvrez le dossier **automated-machine-learning**.
   
   1. Exécutez `automl_setup.cmd` dans l’invite Conda pour Windows, ou le fichier `.sh` pour votre système d’exploitation. L’exécution dure environ 10 minutes.

      Le script d’installation :
      + Crée un nouvel environnement Conda
      + Installe les packages nécessaires
      + Configure le widget
      + Démarre un notebook Jupyter
      
   >[!NOTE]
   > Le script prend le nom de l’environnement Conda comme paramètre facultatif. Par défaut, le nom de l’environnement Conda est `azure_automl`. La commande exacte varie selon le système d’exploitation. C’est utile si vous créez un nouvel environnement ou si vous faites une mise à niveau vers une nouvelle version. Par exemple, vous pouvez utiliser « automl_setup.cmd azure_automl_sandbox » pour créer un environnement nommé « azure_automl_sandbox ». 
      
1. Une fois l’exécution du script terminée, vous voyez la page d’accueil Jupyter Notebook dans votre navigateur.

1. Accédez à l’emplacement où vous avez enregistré les notebooks. 

1. Ouvrez le dossier automated-machine-learning, puis ouvrez le notebook **configuration.ipynb**. 

1. Exécutez les cellules du notebook pour inscrire le fournisseur de ressources Machine Learning Services et créer un espace de travail.

Vous êtes maintenant prêt à exécuter les notebooks enregistrés sur votre ordinateur local.


## <a name="next-steps"></a>Étapes suivantes

Explorez le [dépôt de notebooks GitHub pour Azure Machine Learning service](https://aka.ms/aml-notebooks).

Essayez ces tutoriels :
+ [Entraîner un modèle de classification d’images avec MNIST](tutorial-train-models-with-aml.md)

+ [Préparer des données et utiliser le machine learning automatisé pour entraîner un modèle de régression avec le jeu de données NYC Taxi](tutorial-data-prep.md)
