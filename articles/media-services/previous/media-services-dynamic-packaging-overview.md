---
title: Vue d’ensemble de l’empaquetage dynamique Azure Media Services | Microsoft Docs
description: Cette rubrique donne une vue d'ensemble de l'empaquetage dynamique.
author: Juliako
manager: femila
editor: ''
services: media-services
documentationcenter: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2019
ms.author: juliako
ms.openlocfilehash: 987928d98752d5f32255b94a5e0177a20c12daf3
ms.sourcegitcommit: e69fc381852ce8615ee318b5f77ae7c6123a744c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/11/2019
ms.locfileid: "55989080"
---
# <a name="dynamic-packaging"></a>l’empaquetage dynamique

Vous pouvez utiliser Microsoft Azure Media Services pour distribuer de nombreux formats de fichiers sources multimédias, formats de streaming de contenu multimédia et formats de protection de contenu à diverses technologies clientes (par exemple, iOS, XBOX, Silverlight, Windows 8). Ces clients comprennent différents protocoles. Par exemple, iOS nécessite un format HTTP Live Streaming (HLS) V4, tandis que Silverlight et Xbox nécessitent le format Smooth Streaming. Si vous voulez transmettre un ensemble de fichiers MP4 (ISO Base Media 14496-12) ou de fichiers Smooth Streaming à vitesse de transmission adaptative, à des clients qui utilisent le format MPEG DASH, HLS ou Smooth Streaming, nous vous recommandons de tirer profit de l'empaquetage dynamique Media Services.

Avec l'empaquetage dynamique, il vous suffit de créer un élément multimédia contenant un ensemble de fichiers MP4 ou de fichiers Smooth Streaming à vitesse de transmission adaptative. Ensuite, en fonction du format spécifié dans le manifeste ou la demande de fragment, le serveur de streaming à la demande s'assure que vous recevez le flux conforme au protocole choisi. Par conséquent, il vous suffit de stocker et de payer les fichiers dans un seul format de stockage. Le service Media Services se charge de créer et de fournir la réponse appropriée en fonction des demandes des clients.

Le diagramme suivant illustre le flux traditionnel d'encodage et d'empaquetage statique.

![Encodage statique](./media/media-services-dynamic-packaging-overview/media-services-static-packaging.png)

Le diagramme suivant illustre le flux d'empaquetage dynamique.

![Encodage dynamique](./media/media-services-dynamic-packaging-overview/media-services-dynamic-packaging.png)

## <a name="common-scenario"></a>Scénario courant
1. Téléchargez un fichier d'entrée (appelé fichier mezzanine). Par exemple, H.264, MP4 ou WMV (pour obtenir la liste des formats pris en charge, consultez [Formats pris en charge par Media Encoder Standard](media-services-media-encoder-standard-formats.md)).
2. Encodez votre fichier mezzanine en ensembles de fichiers MP4 à vitesse de transmission adaptative H.264.
3. Publiez l'élément multimédia qui contient l'ensemble de fichiers MP4 à vitesse de transmission adaptative en créant le localisateur à la demande.
4. Générez les URL de streaming pour accéder à votre contenu et le diffuser en continu.

## <a name="preparing-assets-for-dynamic-streaming"></a>Préparation des éléments multimédias pour un streaming dynamique
Pour préparer un élément multimédia à un streaming dynamique, vous disposez des options suivantes :

- [Chargez un fichier maître](media-services-dotnet-upload-files.md).
- [Utilisez l’encodeur Media Encoder Standard pour produire des ensembles de fichiers MP4 à vitesse de transmission adaptative H.264](media-services-dotnet-encode-with-media-encoder-standard.md).
- [Diffusez votre contenu](media-services-deliver-content-overview.md).

## <a name="audio-codecs-supported-by-dynamic-packaging"></a>Codecs audio pris en charge par l’empaquetage dynamique

L’empaquetage dynamique prend en charge les fichiers MP4 (ou les fichiers Smooth Streaming) qui contiennent des données audio encodées avec [AAC](https://en.wikipedia.org/wiki/Advanced_Audio_Coding) (AAC-LC, HE-AAC v1, HE-AAC v2), [Dolby Digital Plus](https://en.wikipedia.org/wiki/Dolby_Digital_Plus) (Enhanced AC-3 ou E-AC3) ou [ DTS](https://en.wikipedia.org/wiki/DTS_%28sound_system%29) (DTS Express, DTS LBR, DTS HD, HD DTS sans perte).

> [!Note]
> L’empaquetage dynamique ne prend pas en charge les fichiers qui contiennent des données audio [Dolby Digital](https://en.wikipedia.org/wiki/Dolby_Digital) (AC3) (il s’agit d’un codec hérité).

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

