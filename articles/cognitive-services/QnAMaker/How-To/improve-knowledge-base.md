---
title: Amélioration d’une base de connaissances - QnA Maker
titleSuffix: Azure Cognitive Services
description: ''
author: diberry
manager: nitinme
displayName: active learning, suggestion, dialog prompt, train api, feedback loop, autolearn, auto-learn, user setting, service setting, services setting
ms.service: cognitive-services
ms.subservice: qna-maker
ms.topic: article
ms.date: 01/29/2019
ms.author: diberry
ms.openlocfilehash: 6feb521aa47ca813b3067451c8c77111deb60e73
ms.sourcegitcommit: 90cec6cccf303ad4767a343ce00befba020a10f6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/07/2019
ms.locfileid: "55874003"
---
# <a name="use-active-learning-to-improve-knowledge-base"></a>Utiliser un entraînement actif pour améliorer la base de connaissances

L’apprentissage actif vous permet d’améliorer la qualité de votre base de connaissances en suggérant d’autres questions à votre paire de question/réponse basées sur les soumissions d’utilisateurs. Après avoir passé en revue ces suggestions, ajoutez-les aux questions existantes ou rejetez-les. 

Votre base de connaissances ne change pas automatiquement. Vous devez accepter les suggestions afin que toute modification prenne effet. Ces suggestions ajoutent des questions, mais elles ne modifient pas les questions existantes pas plus qu’elles ne les suppriment.

## <a name="active-learning"></a>Apprentissage actif

QnA Maker apprend de nouvelles variantes de question à l’aide des commentaires implicites et explicites.
 
* Commentaires implicites : l’outil de classement comprend lorsqu’une question d’utilisateur a plusieurs réponses dont les scores sont très proches et la considère comme un commentaire. 
* Commentaires explicites : si plusieurs réponses avec peu de variations dans les scores sont retournées à partir de la base de connaissances, l’application cliente demande à l’utilisateur quelle question est appropriée. Les commentaires explicites de l’utilisateur sont envoyés à QnA Maker avec l’API Train. 

Les deux méthodes fournissent à l’outil de classement des requêtes similaires qui sont ordonnées en cluster.

Lorsque des requêtes similaires sont ordonnées en cluster, QnA Maker suggère les questions de l’utilisateur au concepteur de la base de connaissances pour qu’il les accepte ou les rejette.

## <a name="how-active-learning-works"></a>Fonctionnement de l’apprentissage actif

L’apprentissage actif est déclenché en fonction des scores des principales réponses retournées par QnA Maker pour une requête donnée. Si les différences de scores s’inscrivent dans une petite plage, la requête est considérée comme une _suggestion_ possible pour chacune des réponses possibles. 

Toutes les suggestions sont regroupées par similarité, et les principales suggestions pour les questions alternatives sont affichées en fonction de la fréquence des requêtes particulières des utilisateurs finals. L’apprentissage actif offre les meilleures suggestions possible dans les cas où les points de terminaison reçoivent une quantité raisonnable de différentes requêtes d’utilisation.

## <a name="upgrade-version-to-use-active-learning"></a>Mise à niveau d’une version pour utiliser l’apprentissage actif

L’apprentissage actif est pris en charge dans la version 4.4.0 du runtime et dans les versions ultérieures. Si votre base de connaissances a été créée dans une version antérieure, [mettez à niveau votre runtime](troubleshooting-runtime.md#how-to-get-latest-qnamaker-runtime-updates) pour utiliser cette fonctionnalité. 

## <a name="best-practices"></a>Bonnes pratiques

Pour prendre connaissance des meilleures pratiques lors de l’utilisation de l’apprentissage actif, consultez la rubrique [Bonnes pratiques](../Concepts/best-practices.md#active-learning).

## <a name="score-proximity-between-knowledge-base-questions"></a>Proximité des scores entre les questions de la base de connaissances

Lorsque le niveau de confiance du score d’une question est élevé, par exemple 80 %, la plage des scores pris en compte pour l’apprentissage actif est large, environ 10 %. À mesure que le score de confiance diminue, par exemple 40 %, la plage des scores décroît également et passe à environ 4 %. 

L’algorithme permettant de déterminer la proximité n’est pas un calcul simple. Les plages indiquées dans les exemples précédents ne sont censées être fixes, mais doivent servir de guide pour comprendre l’impact de l’algorithme uniquement.

## <a name="turn-on-active-learning"></a>Activation de l’apprentissage actif

L’apprentissage actif est désactivé par défaut. Activez-le pour afficher les suggestions de questions. 

1. Pour activer l’apprentissage actif, cliquez sur votre **Nom**, puis accédez à [**Paramètres du service**](https://www.qnamaker.ai/UserSettings) dans le portail QnA Maker, dans l’angle supérieur droit.  

    ![Activation de l’apprentissage actif dans la page des paramètres du service](../media/improve-knowledge-base/Endpoint-Keys.png)


1. Recherchez le service QnA Maker, puis activez la stratégie **Apprentissage actif**. 

    [![Activation de l’apprentissage actif dans la page des paramètres du service](../media/improve-knowledge-base/turn-active-learning-on-at-service-setting.png)](../media/improve-knowledge-base/turn-active-learning-on-at-service-setting.png#lightbox)

    Une fois que la stratégie **Apprentissage actif** est activée, la base de connaissances suggère de nouvelles questions à intervalles réguliers en fonction des questions soumises par l’utilisateur. Vous pouvez désactiver la stratégie **Apprentissage actif** en basculant de nouveau le paramètre.

## <a name="add-active-learning-suggestion-to-knowledge-base"></a>Ajout d’une suggestion d’apprentissage actif à la base de connaissances

1. Pour afficher les suggestions de questions, dans la page **Edit knowledge base** (Modifier la base de connaissances), sélectionnez **Afficher les suggestions**. 

    [![Activation/Désactivation du bouton Afficher les Suggestions de la page des paramètres du service](../media/improve-knowledge-base/show-suggestions-button.png)](../media/improve-knowledge-base/show-suggestions-button.png#lightbox)

1. Filtrez la base de connaissances contenant des paires de question/réponse pour afficher uniquement les suggestions en sélectionnant **Filter by Suggestions** (Filtrer par suggestions).

    [![Dans la page des paramètres du service, filtrage par suggestions pour afficher uniquement ces paires de question/réponse](../media/improve-knowledge-base/filter-by-suggestions.png)](../media/improve-knowledge-base/filter-by-suggestions.png#lightbox)

1.  Chaque section de question présentant des suggestions affiche les nouvelles questions avec une coche, `✔`, pour les accepter ou avec un symbole `x` pour rejeter les suggestions. Sélectionnez la coche pour ajouter la question. 

    [![Activation de l’apprentissage actif dans la page des paramètres du service](../media/improve-knowledge-base/accept-active-learning-suggestions.png)](../media/improve-knowledge-base/accept-active-learning-suggestions.png#lightbox)

    Vous pouvez ajouter ou supprimer _toutes les suggestions_ en sélectionnant **Ajouter tout** ou **Reject all** (Rejeter tout).

1. Sélectionnez **Save and Train** (Enregistrer et effectuer l’apprentissage) pour enregistrer les modifications apportées à la base de connaissances.


## <a name="determine-best-choice-when-several-questions-have-similar-scores"></a>Identification du meilleur choix lorsque plusieurs questions ont des scores similaires

Lorsque le score d’une question est trop proche de celui d’autres questions, le développeur de l’application cliente peut demander des précisions.

### <a name="use-the-top-property-in-the-generateanswer-request"></a>Utilisation de la propriété principale dans la requête GenerateAnswer

Lorsque vous soumettez une question à QnA Maker pour obtenir une réponse, le corps JSON permet de retourner plusieurs réponses principales :

```json
{
    "question": "wi-fi",
    "isTest": false,
    "top": 3
}
```

Lorsque l’application cliente (par exemple, un bot conversationnel) reçoit la réponse, les 3 questions principales sont retournées :

```json
{
    "answers": [
        {
            "questions": [
                "Wi-Fi Direct Status Indicator"
            ],
            "answer": "**Wi-Fi Direct Status Indicator**\n\nStatus bar icons indicate your current Wi-Fi Direct connection status:  \n\nWhen your device is connected to another device using Wi-Fi Direct, '$  \n\n+ •+ ' Wi-Fi Direct is displayed in the Status bar.",
            "score": 74.21,
            "id": 607,
            "source": "Bugbash KB.pdf",
            "metadata": []
        },
        {
            "questions": [
                "Wi-Fi - Connections"
            ],
            "answer": "**Wi-Fi**\n\nWi-Fi is a term used for certain types of Wireless Local Area Networks (WLAN). Wi-Fi communication requires access to a wireless Access Point (AP).",
            "score": 74.15,
            "id": 599,
            "source": "Bugbash KB.pdf",
            "metadata": []
        },
        {
            "questions": [
                "Turn Wi-Fi On or Off"
            ],
            "answer": "**Turn Wi-Fi On or Off**\n\nTurning Wi-Fi on makes your device able to discover and connect to compatible in-range wireless APs.  \n\n1.  From a Home screen, tap ::: Apps > e Settings .\n2.  Tap Connections > Wi-Fi , and then tap On/Off to turn Wi-Fi on or off.",
            "score": 69.99,
            "id": 600,
            "source": "Bugbash KB.pdf",
            "metadata": []
        }
    ]
}
```

### <a name="client-application-follow-up-when-questions-have-similar-scores"></a>Suivi de l’application cliente lorsque les questions présentent des scores similaires

L’application cliente affiche toutes les questions avec une option permettant à l’utilisateur de sélectionner la question qui représente le mieux son intention. 

Une fois que l’utilisateur a sélectionné l’une des questions existantes, ses commentaires sont envoyés à l’API [Train](http://www.aka.ms/activelearningsamplebot) de QnA Maker pour poursuivre la boucle des commentaires d’apprentissage actif. 

```http
POST https://<QnA-Maker-resource-name>.azurewebsites.net/qnamaker/knowledgebases/<knowledge-base-ID>/train
Authorization: EndpointKey <endpoint-key>
Content-Type: application/json
{"feedbackRecords": [{"userId": "1","userQuestion": "<question-text>","qnaId": 1}]}
```

En savoir plus sur l’utilisation de l’apprentissage actif avec un [exemple de bot Azure en C#](https://github.com/Microsoft/BotBuilder-Samples/tree/master/experimental/csharp_dotnetcore/qnamaker-activelearning-bot)

## <a name="next-steps"></a>Étapes suivantes
 
> [!div class="nextstepaction"]
> [Utiliser l’API QnA Maker](https://westus.dev.cognitive.microsoft.com/docs/services/5a93fcf85b4ccd136866eb37/operations/5ac266295b4ccd1554da75ff)
