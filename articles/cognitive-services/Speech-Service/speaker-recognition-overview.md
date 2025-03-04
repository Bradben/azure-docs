---
title: Speaker Recognition overview - Speech service
titleSuffix: Azure Cognitive Services
description: Speaker Recognition provides algorithms that verify and identify speakers by their unique voice characteristics using voice biometry. Speaker Recognition is used to answer the question “who is speaking?”. This article is an overview of the benefits and capabilities of the Speaker Recognition service.
services: cognitive-services
author: eric-urban
manager: nitinme
ms.service: cognitive-services
ms.subservice: speech-service
ms.topic: conceptual
ms.date: 09/02/2020
ms.author: eur
ms.custom: cog-serv-seo-aug-2020, ignite-fall-2021
keywords: speaker recognition, voice biometry
---

# What is Speaker Recognition?

Speaker Recognition can help determine who is speaking in an audio clip. The service can verify and identify speakers by their unique voice characteristics using voice biometry. 

You provide audio training data for a single speaker, which creates an enrollment profile based on the unique characteristics of the speaker's voice. You can then cross-check audio voice samples against this profile to verify that the speaker is the same person (speaker verification), or cross-check audio voice samples against a *group* of enrolled speaker profiles to see if it matches any profile in the group (speaker identification).

> [!IMPORTANT]
> Microsoft limits access to Speaker Recognition. You can apply for access through the [Azure Cognitive Services Speaker Recognition Limited Access Review](https://aka.ms/azure-speaker-recognition). For more information, please visit [Limited access for Speaker Recognition](/legal/cognitive-services/speech-service/speaker-recognition/limited-access-speaker-recognition).

## Speaker Verification

Speaker Verification streamlines the process of verifying an enrolled speaker identity with either passphrases or free-form voice input. For example, you can use it for customer identity verification in call centers or contact-less facility access.

### How does Speaker Verification work?

:::image type="content" source="media/speaker-recognition/speaker-rec.png" alt-text="Speaker Verification flowchart.":::

Speaker verification can be either text-dependent or text-independent. **Text-dependent** verification means speakers need to choose the same passphrase to use during both enrollment and verification phases. **Text-independent** verification means speakers can speak in everyday language in the enrollment and verification phrases.

For **text-dependent** verification, the speaker's voice is enrolled by saying a passphrase from a set of predefined phrases. Voice features are extracted from the audio recording to form a unique voice signature, while the chosen passphrase is also recognized. Together, the voice signature and the passphrase are used to verify the speaker. 

**Text-independent** verification has no restrictions on what the speaker says during enrollment, besides the initial activation phrase to activate the enrollment. It doesn't have any restrictions on the audio sample to be verified, as it only extracts voice features to score similarity. 

The APIs are not intended to determine whether the audio is from a live person or an imitation/recording of an enrolled speaker. 

## Speaker Identification

Speaker Identification is used to determine an unknown speaker’s identity within a group of enrolled speakers. Speaker Identification enables you to attribute speech to individual speakers, and unlock value from scenarios with multiple speakers, such as:

* Support solutions for remote meeting productivity 
* Build multi-user device personalization

### How does Speaker Identification work?

Enrollment for speaker identification is **text-independent**, which means that there are no restrictions on what the speaker says in the audio, besides the initial activation phrase to activate the enrollment. Similar to Speaker Verification, the speaker's voice is recorded in the enrollment phase, and the voice features are extracted to form a unique voice signature. In the identification phase, the input voice sample is compared to a specified list of enrolled voices (up to 50 in each request).

## Data security and privacy

Speaker enrollment data is stored in a secured system, including the speech audio for enrollment and the voice signature features. The speech audio for enrollment is only used when the algorithm is upgraded, and the features need to be extracted again. The service does not retain the speech recording or the extracted voice features that are sent to the service during the recognition phase. 

You control how long data should be retained. You can create, update, and delete enrollment data for individual speakers through API calls. When the subscription is deleted, all the speaker enrollment data associated with the subscription will also be deleted. 

As with all of the Cognitive Services resources, developers who use the Speaker Recognition service must be aware of Microsoft's policies on customer data. You should ensure that you have received the appropriate permissions from the users for Speaker Recognition. You can find more details in [Data and privacy for Speaker Recognition](/legal/cognitive-services/speech-service/speaker-recognition/data-privacy-speaker-recognition). For more information, see the [Cognitive Services page](https://azure.microsoft.com/support/legal/cognitive-services-compliance-and-privacy/) on the Microsoft Trust Center. 

## Common questions and solutions

| Question | Solution |
|---------|----------|
| What scenarios can Speaker Recognition be used for? | Call center customer verification, voice-based patient check-in, meeting transcription, multi-user device personalization|
| What is the difference between Identification and Verification? | Identification is the process of detecting which member from a group of speakers is speaking. Verification is the act of confirming that a speaker matches a known, or **enrolled** voice.|
| What's the difference between text-dependent and text-independent verification? | Text-dependent verification requires a specific pass-phrase for both enrollment and recognition. Text-independent verification requires a longer voice sample that must start with a particular activation phrase for enrollment, but anything can be spoken, including during recognition.|
| What languages are supported? | English, French, Spanish, Chinese, German, Italian, Japanese, and Portuguese |
| What Azure regions are supported? | Speaker Recognition is a preview service, and currently only available in the West US region.|
| What audio formats are supported? | Mono 16 bit, 16 kHz PCM-encoded WAV |
| **Accept** and **Reject** responses aren't accurate, how do you tune the threshold? | Since the optimal threshold varies highly with scenarios, the service decides whether to accept or reject based on a default threshold of 0.5. You should override the default decision and fine tune the result based on your own scenario. |
| Can you enroll one speaker multiple times? | Yes, for text-dependent verification, you can enroll a speaker up to 50 times. For text-independent verification or speaker identification, you can enroll with up to 300 seconds of audio. |
| What data is stored in Azure? | Enrollment audio is stored in the service until the voice profile is [deleted](./get-started-speaker-recognition.md#deleting-voice-profile-enrollments). Recognition audio samples are not retained or stored. |

## Next steps

> [!div class="nextstepaction"]
> [Speaker Recognition quickstart](./get-started-speaker-recognition.md) 
