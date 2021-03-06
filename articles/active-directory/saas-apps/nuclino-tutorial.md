---
title: 'Tutoriel : Intégration d’Azure Active Directory à Nuclino | Microsoft Docs'
description: Découvrez comment configurer l’authentification unique entre Azure Active Directory et Nuclino.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 74bbab82-5581-4dcf-8806-78f77c746968
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2018
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 655ac490e528680f779eeca54899a022ddf3b89a
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56189551"
---
# <a name="tutorial-azure-active-directory-integration-with-nuclino"></a>Tutoriel : Intégration d’Azure Active Directory à Nuclino

Dans ce didacticiel, vous allez apprendre à intégrer Nuclino à Azure Active Directory (Azure AD).

L’intégration de Nuclino à Azure AD vous offre les avantages suivants :

- Dans Azure AD, vous pouvez contrôler qui a accès à Nuclino.
- Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Nuclino (par authentification unique) avec leur compte Azure AD.
- Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure

Pour en savoir plus sur l’intégration des applications SaaS à Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique auprès d’Azure Active Directory ?](../manage-apps/what-is-single-sign-on.md)

## <a name="prerequisites"></a>Prérequis

Pour configurer l'intégration d'Azure AD avec Nuclino, vous avez besoin des éléments suivants :

- Un abonnement Azure AD
- Un abonnement Nuclino pour lequel l’authentification unique est activée

> [!NOTE]
> Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.

Vous devez en outre suivre les recommandations ci-dessous :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario

Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :

1. Ajout de Nuclino à partir de la galerie
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-nuclino-from-the-gallery"></a>Ajout de Nuclino à partir de la galerie

Pour configurer l’intégration de Nuclino dans Azure AD, vous devez ajouter Nuclino depuis la galerie à votre liste d’applications SaaS gérées.

**Pour ajouter Nuclino à partir de la galerie, procédez comme suit :**

1. Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**. 

    ![Bouton Azure Active Directory][1]

2. Accédez à **Applications d’entreprise**. Accédez ensuite à **Toutes les applications**.

    ![Panneau Applications d’entreprise][2]

3. Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.

    ![Bouton Nouvelle application][3]

4. Dans la zone de recherche, tapez **Nuclino**, sélectionnez **Nuclino** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.

    ![Nuclino dans la liste des résultats](./media/nuclino-tutorial/tutorial_nuclino_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD

Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Nuclino avec un utilisateur de test appelé « Britta Simon ».

Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Nuclino équivalent dans Azure AD. En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur Nuclino associé doit être établie.

Pour configurer et tester l'authentification unique Azure AD avec Nuclino, vous devez suivre les indications des sections suivantes :

1. **[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.
3. **[Créer un utilisateur de test Nuclino](#create-a-nuclino-test-user)** pour avoir dans Nuclino un équivalent de Britta Simon lié à la représentation Azure AD associée.
4. **[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.
5. **[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Nuclino.

**Pour configurer l'authentification unique Azure AD avec Nuclino, procédez comme suit :**

1. Dans le Portail Azure, sur la page d’intégration de l’application **Nuclino**, cliquez sur **Authentification unique**.

    ![Lien Configurer l’authentification unique][4]

2. Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.

    ![Boîte de dialogue Authentification unique](./media/nuclino-tutorial/tutorial_nuclino_samlbase.png)

3. Dans la section **Domaines et URL Nuclino**, suivez les étapes ci-dessous si vous souhaitez configurer l’application en mode initié par **IDP** :

    ![Informations d’authentification unique dans Domaine et URL Nuclino](./media/nuclino-tutorial/tutorial_nuclino_url1.png)

    a. Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://api.nuclino.com/api/sso/<UNIQUE-ID>/metadata`

    b. Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://api.nuclino.com/api/sso/<UNIQUE-ID>/acs`

    > [!NOTE]
    > Il ne s’agit pas de valeurs réelles. Mettez à jour ces valeurs avec l’identificateur et l’URL de réponse réels à partir de la section **Authentification**, expliquée plus loin dans ce didacticiel.

4. Si vous souhaitez configurer l’application en **mode démarré par le fournisseur de service**, cochez **Afficher les paramètres d’URL avancés**, puis effectuez les étapes suivantes :

    ![Informations d’authentification unique dans Domaine et URL Nuclino](./media/nuclino-tutorial/tutorial_nuclino_url2.png)

    Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://app.nuclino.com/<UNIQUE-ID>/login`

    > [!NOTE]
    > Cette valeur n’est pas la valeur réelle. Mettez à jour cette valeur avec l’URL d’authentification réelle. Pour obtenir cette valeur, contactez [l’équipe du support Nuclino](mailto:contact@nuclino.com).

5. L’application Nuclino attend les assertions SAML dans un format spécifique. Configurez les revendications suivantes pour cette application. Vous pouvez gérer les valeurs de ces attributs à partir de la section « **Attributs utilisateur** » sur la page d’intégration des applications. La capture d’écran suivante montre un exemple :

    ![Configurer l'authentification unique](./media/Nuclino-tutorial/tutorial_attribute.png)

6. Dans la section **Attributs utilisateur**, cliquez sur **Afficher et modifier tous les autres attributs utilisateur** pour développer les attributs. Dans chacun des attributs affichés, procédez comme suit :

    | Nom de l'attribut | Valeur de l’attribut |
    | ---------------| --------------- |
    | first_name | user.givenname |
    | last_name | user.surname |

    a. Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.

    ![Configure Single Sign-On](./media/nuclino-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/nuclino-tutorial/tutorial_attribute_05.png)

    b. Dans la zone de texte **Nom**, indiquez le **nom d’attribut** pour cette ligne.

    c. Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.

    d. Cliquez sur **OK**.

7. Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.

    ![Lien Téléchargement de certificat](./media/nuclino-tutorial/tutorial_nuclino_certificate.png)

8. Cliquez sur le bouton **Enregistrer** .

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/nuclino-tutorial/tutorial_general_400.png)

9. Dans la section **Configuration de Nuclino**, cliquez sur **Configurer Nuclino** pour ouvrir la fenêtre **Configurer l’authentification**. Copiez l’**ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**

    ![Configuration de Nuclino](./media/nuclino-tutorial/tutorial_nuclino_configure.png)

10. Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Nuclino en tant qu’administrateur.

11. Cliquez sur l’**icône**.

    ![Configuration de Nuclino](./media/nuclino-tutorial/configure1.png)

12. Cliquez sur l’**authentification unique Azure AD** et sélectionnez **Paramètres d’équipe** dans la liste déroulante.

    ![Configuration de Nuclino](./media/nuclino-tutorial/configure2.png)

13. Sélectionnez **Authentification** à partir du volet de navigation gauche.

    ![Configuration de Nuclino](./media/nuclino-tutorial/configure3.png)

14. Dans la section **Authentication**, procédez comme suit :

    ![Configuration de Nuclino](./media/nuclino-tutorial/configure4.png)

    a. Sélectionnez **Authentification unique SAML (SSO)**.

    b. Copiez **la valeur d’URL ACS (vous devez la copier et la coller dans votre fournisseur d’authentification unique)** et collez-la dans la zone de texte **URL de réponse** de la section **Domaine et URL Nuclino** dans le portail Azure.

    c. Copiez **l’ID d’entité (vous devez la copier et la coller dans votre fournisseur d’authentification unique)** et collez-la dans la zone de texte **Identificateur** de la section **Domaine et URL Nuclino** dans le portail Azure.

    d. Dans la zone de texte **URL d’authentification unique**, collez **l’URL du service d’authentification unique SAML** que vous avez copiée sur le portail Azure.

    e. Dans la zone de texte **ID d’entité**, collez la valeur **ID d’entité SAML** que vous avez copiée à partir du Portail Azure.

    f. Ouvrez votre **Certificat (Base64)** téléchargé dans le Bloc-notes. Copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **Certificat public**.

    g. Cliquez sur **ENREGISTRER LES MODIFICATIONS**.

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD

L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.

   ![Créer un utilisateur de test Azure AD][100]

**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**

1. Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.

    ![Bouton Azure Active Directory](./media/nuclino-tutorial/create_aaduser_01.png)

2. Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/nuclino-tutorial/create_aaduser_02.png)

3. Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.

    ![Bouton Ajouter](./media/nuclino-tutorial/create_aaduser_03.png)

4. Dans la boîte de dialogue **Utilisateur**, procédez comme suit :

    ![Boîte de dialogue Utilisateur](./media/nuclino-tutorial/create_aaduser_04.png)

    a. Dans la zone **Nom**, tapez **BrittaSimon**.

    b. Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.

    c. Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.

    d. Cliquez sur **Créer**.

### <a name="create-a-nuclino-test-user"></a>Créer un utilisateur de test Nuclino

L'objectif de cette section est de créer un utilisateur appelé Britta Simon dans Nuclino. Nuclino prend en charge l’approvisionnement juste-à-temps, option activée par défaut. Vous n’avez aucune opération à effectuer dans cette section. S’il n’existe pas déjà, un utilisateur est créé lors d’une tentative d’accès à Nuclino.

> [!Note]
> Si vous devez créer un utilisateur manuellement, contactez  [l’équipe de support technique Nuclino](mailto:contact@nuclino.com).

### <a name="assign-the-azure-ad-test-user"></a>Affecter l’utilisateur de test Azure AD

Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Nuclino.

![Attribuer le rôle utilisateur][200]

**Pour affecter Britta Simon à Nuclino, procédez comme suit :**

1. Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.

    ![Affecter des utilisateurs][201]

2. Dans la liste des applications, sélectionnez **Nuclino**.

    ![Lien Nuclino dans la liste des applications](./media/nuclino-tutorial/tutorial_nuclino_app.png)  

3. Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.

    ![Lien « Utilisateurs et groupes »][202]

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Volet Ajouter une attribution][203]

5. Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.

### <a name="test-single-sign-on"></a>Tester l’authentification unique

Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.

Lorsque vous cliquez sur la vignette Nuclino dans le volet d’accès, vous devez être connecté automatiquement à votre application Nuclino.
Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](../user-help/active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory](tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/nuclino-tutorial/tutorial_general_01.png
[2]: ./media/nuclino-tutorial/tutorial_general_02.png
[3]: ./media/nuclino-tutorial/tutorial_general_03.png
[4]: ./media/nuclino-tutorial/tutorial_general_04.png

[100]: ./media/nuclino-tutorial/tutorial_general_100.png

[200]: ./media/nuclino-tutorial/tutorial_general_200.png
[201]: ./media/nuclino-tutorial/tutorial_general_201.png
[202]: ./media/nuclino-tutorial/tutorial_general_202.png
[203]: ./media/nuclino-tutorial/tutorial_general_203.png
