---
title: 'Tutoriel : Didacticiel : Intégration d’Azure Active Directory à LiquidFiles | Microsoft Docs'
description: Découvrez comment configurer l’authentification unique entre Azure Active Directory et LiquidFiles.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: cb517134-0b34-4a74-b40c-5a3223ca81b6
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 20a3144f2a8727420803034426106a29a7924727
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56167301"
---
# <a name="tutorial-azure-active-directory-integration-with-liquidfiles"></a>Didacticiel : Intégration d’Azure Active Directory à LiquidFiles

Dans ce didacticiel, vous allez apprendre à intégrer LiquidFiles avec Azure Active Directory (Azure AD).

L’intégration de LiquidFiles avec Azure AD vous offre les avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès à LiquidFiles.
- Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à LiquidFiles (via l’authentification unique) avec leur compte Azure AD.
- Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure.

Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prérequis

Pour configurer l’intégration d’Azure AD avec LiquidFiles, vous avez besoin des éléments suivants :

- Un abonnement Azure AD
- Un abonnement LiquidFiles pour lequel l’authentification unique est activée

> [!NOTE]
> Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.

Vous devez en outre suivre les recommandations ci-dessous :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :

1. Ajout de LiquidFiles à partir de la galerie
1. Configuration et test de l’authentification unique Azure AD

## <a name="adding-liquidfiles-from-the-gallery"></a>Ajout de LiquidFiles à partir de la galerie
Pour configurer l’intégration de LiquidFiles avec Azure AD, vous devez ajouter LiquidFiles à partir de la galerie à votre liste d’applications SaaS managées.

**Pour ajouter LiquidFiles à partir de la galerie, procédez comme suit :**

1. Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**. 

    ![Active Directory][1]

1. Accédez à **Applications d’entreprise**. Accédez ensuite à **Toutes les applications**.

    ![APPLICATIONS][2]
    
1. Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.

    ![APPLICATIONS][3]

1. Dans la zone de recherche, tapez **LiquidFiles**.

    ![Création d’un utilisateur de test Azure AD](./media/liquidfiles-tutorial/tutorial_liquidfiles_search.png)

1. Dans le volet de résultats, sélectionnez **LiquidFiles**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.

    ![Création d’un utilisateur de test Azure AD](./media/liquidfiles-tutorial/tutorial_liquidfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec LiquidFiles sur un utilisateur de test nommé « Britta Simon ».

Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur LiquidFiles équivalent à l’utilisateur dans Azure AD. En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur LiquidFiles associé doit être établie.

Dans LiquidFiles, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur **Nom d’utilisateur** pour établir la relation.

Pour configurer et tester l’authentification unique Azure AD avec LiquidFiles, vous devez suivre les indications des sections suivantes :

1. **[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.
1. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.
1. **[Création d’un utilisateur de test LiquidFiles](#creating-a-liquidfiles-test-user)** pour avoir un équivalent de Britta Simon dans LiquidFiles lié à la représentation de l’utilisateur Azure AD.
1. **[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** : permet à Britta Simon d’utiliser l’authentification unique Azure AD.
1. **[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application LiquidFiles.

**Pour configurer l’authentification unique Azure AD avec LiquidFiles, procédez comme suit :**

1. Dans le portail Azure, sur la page d’intégration de l’application **LiquidFiles**, cliquez sur **Authentification unique**.

    ![Configurer l'authentification unique][4]

1. Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.
 
    ![Configurer l'authentification unique](./media/liquidfiles-tutorial/tutorial_liquidfiles_samlbase.png)

1. Dans la section **Domaine et URL LiquidFiles**, procédez comme suit :

    ![Configurer l'authentification unique](./media/liquidfiles-tutorial/tutorial_liquidfiles_url.png)

    a. Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<YOUR_SERVER_URL>/saml/init`

    b. Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<YOUR_SERVER_URL>`

    c. b. Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<YOUR_SERVER_URL>/saml/consume`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettez à jour ces valeurs avec l’URL de connexion, l’identificateur et l’URL de réponse réels. Pour obtenir ces valeurs, contactez [l’équipe de support technique LiquidFiles](https://www.liquidfiles.com/support.html). 
 
1. Dans la section **Certificat de signature SAML**, copiez la valeur **THUMBPRINT** du certificat.

    ![Configurer l'authentification unique](./media/liquidfiles-tutorial/tutorial_liquidfiles_certificate.png) 

1. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l'authentification unique](./media/liquidfiles-tutorial/tutorial_general_400.png)

1. Dans la section **Configuration de LiquidFiles**, cliquez sur **Configurer LiquidFiles** pour ouvrir la fenêtre **Configurer l’authentification unique**. Copiez l’**URL de déconnexion et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.

    ![Configurer l'authentification unique](./media/liquidfiles-tutorial/tutorial_liquidfiles_configure.png)
 
1. Connectez-vous à votre site d’entreprise LiquidFiles en tant qu’administrateur.

1. Dans le menu **Administration > Configuration**, cliquez sur **Single Sign-On (Authentification unique)**.

1. Dans la page **Single Sign-On Configuration** (Configuration de l’authentification unique), procédez comme suit :

    ![Configurer l'authentification unique](./media/liquidfiles-tutorial/tutorial_single_01.png)

    a. Pour **Single Sign On Method** (Méthode d’authentification unique), sélectionnez **SAML 2**.

    b. Dans la zone de texte **IDP Login URL** (URL de connexion de fournisseur d’identité), collez la valeur de **l’URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.

    c. Dans la zone de texte **IDP Logout URL** (URL de déconnexion de fournisseur d’identité), collez la valeur de **l’URL de déconnexion** que vous avez copiée à partir du portail Azure.

    d. Dans la zone de texte **IDP Cert Fingerprint** (Empreinte du certificat IDP), collez la valeur **THUMBPRINT** que vous avez copiée à partir du portail Azure.

    e. Dans la zone de texte Name Identifier Format (Format d’identificateur de nom), entrez la valeur **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.

    f. Dans la zone de texte Authn Context (Contexte d’authentification), tapez la valeur **urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport**.

    g. Cliquez sur **Enregistrer**.  

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.  Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas. Pour en savoir plus sur la fonctionnalité de documentation incorporée, accédez à : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.

![Créer un utilisateur Azure AD][100]

**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**

1. Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.

    ![Création d’un utilisateur de test Azure AD](./media/liquidfiles-tutorial/create_aaduser_01.png) 

1. Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/liquidfiles-tutorial/create_aaduser_02.png) 

1. Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/liquidfiles-tutorial/create_aaduser_03.png) 

1. Dans la boîte de dialogue **Utilisateur**, procédez comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/liquidfiles-tutorial/create_aaduser_04.png) 

    a. Dans la zone de texte **Nom**, entrez **BrittaSimon**.

    b. Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.

    c. Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.

    d. Cliquez sur **Créer**.
 
### <a name="creating-a-liquidfiles-test-user"></a>Création d’un utilisateur de test LiquidFiles

L’objectif de cette section est de créer un utilisateur nommé Britta Simon dans LiquidFiles. Demandez à votre administrateur de serveur LiquidFiles de vous ajouter en tant qu’utilisateur avant de vous connecter à votre application LiquidFiles.

### <a name="assigning-the-azure-ad-test-user"></a>Affectation de l’utilisateur de test Azure AD

Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à LiquidFiles.

![Affecter des utilisateurs][200] 

**Pour affecter Britta Simon à LiquidFiles, procédez comme suit :**

1. Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.

    ![Affecter des utilisateurs][201] 

1. Dans la liste des applications, sélectionnez **LiquidFiles**.

    ![Configurer l'authentification unique](./media/liquidfiles-tutorial/tutorial_liquidfiles_app.png) 

1. Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

1. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

1. Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.

1. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

1. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.

Lorsque vous cliquez sur la vignette LiquidFiles dans le volet d’accès, vous êtes connecté automatiquement à votre application LiquidFiles.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory](tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/liquidfiles-tutorial/tutorial_general_01.png
[2]: ./media/liquidfiles-tutorial/tutorial_general_02.png
[3]: ./media/liquidfiles-tutorial/tutorial_general_03.png
[4]: ./media/liquidfiles-tutorial/tutorial_general_04.png

[100]: ./media/liquidfiles-tutorial/tutorial_general_100.png

[200]: ./media/liquidfiles-tutorial/tutorial_general_200.png
[201]: ./media/liquidfiles-tutorial/tutorial_general_201.png
[202]: ./media/liquidfiles-tutorial/tutorial_general_202.png
[203]: ./media/liquidfiles-tutorial/tutorial_general_203.png

