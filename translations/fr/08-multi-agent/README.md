# Modèles de conception multi-agents

Dès que vous commencez à travailler sur un projet impliquant plusieurs agents, vous devez prendre en compte le modèle de conception multi-agents. Cependant, il n'est pas toujours évident de savoir quand passer à un système multi-agents et quels en sont les avantages.  

## Introduction

Dans cette leçon, nous cherchons à répondre aux questions suivantes :

- Quels sont les scénarios où les systèmes multi-agents sont applicables ?  
- Quels sont les avantages d'utiliser des multi-agents plutôt qu'un agent unique effectuant plusieurs tâches ?  
- Quels sont les éléments constitutifs pour implémenter le modèle de conception multi-agents ?  
- Comment pouvons-nous avoir une visibilité sur les interactions entre plusieurs agents ?  

## Objectifs d'apprentissage

Après cette leçon, vous devriez être capable de :

- Identifier les scénarios où les multi-agents sont applicables.  
- Reconnaître les avantages d'utiliser des multi-agents par rapport à un agent unique.  
- Comprendre les éléments constitutifs nécessaires pour implémenter le modèle de conception multi-agents.  

Quelle est la vision d'ensemble ?

*Les systèmes multi-agents sont un modèle de conception qui permet à plusieurs agents de collaborer pour atteindre un objectif commun.*

Ce modèle est largement utilisé dans divers domaines, notamment la robotique, les systèmes autonomes et l'informatique distribuée.

## Scénarios où les systèmes multi-agents sont applicables

Quels sont donc les scénarios adaptés à l'utilisation de multi-agents ? La réponse est qu'il existe de nombreux cas où l'emploi de plusieurs agents est bénéfique, notamment dans les situations suivantes :

- **Charges de travail importantes** : Les charges de travail importantes peuvent être divisées en tâches plus petites et attribuées à différents agents, permettant un traitement en parallèle et une exécution plus rapide. Un exemple classique est le traitement de grandes quantités de données.
- **Tâches complexes** : Les tâches complexes, comme les charges de travail importantes, peuvent être décomposées en sous-tâches plus petites et attribuées à différents agents, chacun se spécialisant dans un aspect spécifique de la tâche. Un bon exemple est celui des véhicules autonomes où différents agents gèrent la navigation, la détection des obstacles et la communication avec d'autres véhicules.
- **Expertise variée** : Différents agents peuvent avoir des expertises variées, leur permettant de gérer différents aspects d'une tâche de manière plus efficace qu'un agent unique. Par exemple, dans le domaine de la santé, des agents peuvent gérer les diagnostics, les plans de traitement et la surveillance des patients.

## Avantages d'utiliser des multi-agents par rapport à un agent unique

Un système à agent unique peut fonctionner correctement pour des tâches simples, mais pour des tâches plus complexes, l'utilisation de plusieurs agents offre plusieurs avantages :

- **Spécialisation** : Chaque agent peut se spécialiser dans une tâche spécifique. L'absence de spécialisation dans un système à agent unique peut entraîner une confusion lorsqu'il est confronté à une tâche complexe. Par exemple, il pourrait finir par effectuer une tâche pour laquelle il n'est pas le mieux adapté.
- **Évolutivité** : Il est plus facile de faire évoluer un système en ajoutant des agents supplémentaires plutôt qu'en surchargeant un agent unique.
- **Tolérance aux pannes** : Si un agent tombe en panne, les autres peuvent continuer à fonctionner, assurant ainsi la fiabilité du système.

Prenons un exemple : réserver un voyage pour un utilisateur. Un système à agent unique devrait gérer tous les aspects du processus de réservation, de la recherche de vols à la réservation d'hôtels et de voitures de location. Cela nécessiterait que l'agent unique dispose d'outils pour gérer toutes ces tâches, ce qui pourrait conduire à un système complexe et monolithique, difficile à maintenir et à faire évoluer. Un système multi-agents, en revanche, pourrait avoir différents agents spécialisés dans la recherche de vols, la réservation d'hôtels et la location de voitures. Cela rendrait le système plus modulaire, plus facile à maintenir et évolutif.

Comparez cela à une agence de voyage gérée comme un petit commerce familial versus une agence gérée comme une franchise. Le petit commerce familial aurait un agent unique gérant tous les aspects du processus de réservation, tandis que la franchise aurait différents agents gérant différents aspects du processus.

## Éléments constitutifs pour implémenter le modèle de conception multi-agents

Avant de pouvoir implémenter le modèle de conception multi-agents, vous devez comprendre les éléments constitutifs qui le composent.

Prenons à nouveau l'exemple de la réservation d'un voyage pour un utilisateur. Dans ce cas, les éléments constitutifs incluraient :

- **Communication entre agents** : Les agents chargés de trouver des vols, de réserver des hôtels et de louer des voitures doivent communiquer et partager des informations sur les préférences et les contraintes de l'utilisateur. Vous devez décider des protocoles et des méthodes pour cette communication. Concrètement, cela signifie que l'agent chargé de trouver des vols doit communiquer avec l'agent chargé de réserver des hôtels pour s'assurer que l'hôtel est réservé pour les mêmes dates que le vol. Cela implique de décider *quels agents partagent des informations et comment ils les partagent*.
- **Mécanismes de coordination** : Les agents doivent coordonner leurs actions pour s'assurer que les préférences et les contraintes de l'utilisateur sont respectées. Par exemple, une préférence utilisateur pourrait être d'avoir un hôtel proche de l'aéroport, tandis qu'une contrainte pourrait être que les voitures de location ne sont disponibles qu'à l'aéroport. Cela signifie que vous devez décider *comment les agents coordonnent leurs actions*.
- **Architecture des agents** : Les agents doivent avoir une structure interne leur permettant de prendre des décisions et d'apprendre de leurs interactions avec l'utilisateur. Par exemple, l'agent chargé de trouver des vols doit être capable de décider quels vols recommander à l'utilisateur. Cela implique de déterminer *comment les agents prennent des décisions et apprennent de leurs interactions avec l'utilisateur*. Un exemple pourrait être qu'un agent utilise un modèle d'apprentissage automatique pour recommander des vols basés sur les préférences passées de l'utilisateur.
- **Visibilité des interactions multi-agents** : Vous devez avoir une visibilité sur la manière dont les agents interagissent entre eux. Cela nécessite des outils et des techniques pour suivre les activités et les interactions des agents. Cela peut inclure des outils de journalisation, de surveillance, de visualisation et des indicateurs de performance.
- **Modèles multi-agents** : Il existe différents modèles pour implémenter des systèmes multi-agents, comme des architectures centralisées, décentralisées ou hybrides. Vous devez choisir le modèle qui correspond le mieux à votre cas d'utilisation.
- **Humain dans la boucle** : Dans la plupart des cas, un humain interviendra dans le processus, et vous devez définir quand les agents doivent demander une intervention humaine. Cela peut inclure des demandes spécifiques, comme un utilisateur demandant un hôtel ou un vol particulier, ou des confirmations avant de finaliser une réservation.

## Visibilité des interactions multi-agents

Il est crucial d'avoir une visibilité sur la manière dont les agents interagissent entre eux. Cette visibilité est essentielle pour le débogage, l'optimisation et l'efficacité globale du système. Pour cela, vous devez disposer d'outils et de techniques permettant de suivre les activités et interactions des agents. Cela peut inclure des outils de journalisation, de surveillance, de visualisation et des indicateurs de performance.

Par exemple, dans le cas de la réservation d'un voyage, vous pourriez avoir un tableau de bord affichant le statut de chaque agent, les préférences et contraintes de l'utilisateur, ainsi que les interactions entre les agents. Ce tableau de bord pourrait montrer les dates de voyage de l'utilisateur, les vols recommandés par l'agent de vol, les hôtels recommandés par l'agent hôtelier et les voitures de location recommandées par l'agent de location. Cela vous offrirait une vue claire des interactions entre les agents et de la satisfaction des préférences et contraintes de l'utilisateur.

Voyons ces aspects plus en détail :

- **Outils de journalisation et de surveillance** : Vous souhaitez enregistrer chaque action effectuée par un agent. Une entrée de journal peut contenir des informations sur l'agent ayant effectué l'action, l'action elle-même, l'heure de l'action et son résultat. Ces informations peuvent ensuite être utilisées pour le débogage, l'optimisation, etc.
- **Outils de visualisation** : Les outils de visualisation peuvent vous aider à comprendre les interactions entre les agents de manière plus intuitive. Par exemple, vous pourriez avoir un graphique montrant le flux d'informations entre les agents, ce qui pourrait vous aider à identifier les goulets d'étranglement ou inefficacités.
- **Indicateurs de performance** : Les indicateurs de performance peuvent vous aider à mesurer l'efficacité du système multi-agents. Par exemple, vous pourriez suivre le temps nécessaire pour terminer une tâche, le nombre de tâches accomplies par unité de temps, ou encore la précision des recommandations faites par les agents.

## Modèles multi-agents

Explorons quelques modèles concrets que nous pouvons utiliser pour créer des applications multi-agents. Voici quelques modèles intéressants à considérer :

### Discussion de groupe

Ce modèle est utile lorsque vous souhaitez créer une application de discussion de groupe où plusieurs agents peuvent communiquer entre eux. Les cas d'utilisation typiques incluent la collaboration en équipe, le support client et les réseaux sociaux.

Dans ce modèle, chaque agent représente un utilisateur dans la discussion de groupe, et les messages sont échangés entre les agents via un protocole de messagerie. Les agents peuvent envoyer des messages à la discussion de groupe, recevoir des messages de celle-ci et répondre à d'autres agents.

Ce modèle peut être implémenté via une architecture centralisée où tous les messages transitent par un serveur central, ou via une architecture décentralisée où les messages sont échangés directement.

![Discussion de groupe](../../../translated_images/multi-agent-group-chat.82d537c5c8dc833abbd252033e60874bc9d00df7193888b3377f8426449a0b20.fr.png)

### Transmission de tâches

Ce modèle est utile lorsque vous souhaitez créer une application où plusieurs agents peuvent se transmettre des tâches.

Les cas d'utilisation typiques incluent le support client, la gestion des tâches et l'automatisation des flux de travail.

Dans ce modèle, chaque agent représente une tâche ou une étape d'un flux de travail, et les agents peuvent transmettre des tâches à d'autres agents en fonction de règles prédéfinies.

![Transmission de tâches](../../../translated_images/multi-agent-hand-off.ed4f0a5a58614a8a3e962fc476187e630a3ba309d066e460f017b503d0b84cfc.fr.png)

### Filtrage collaboratif

Ce modèle est utile lorsque vous souhaitez créer une application où plusieurs agents peuvent collaborer pour faire des recommandations aux utilisateurs.

L'intérêt d'avoir plusieurs agents collaborant est que chaque agent peut avoir une expertise différente et contribuer au processus de recommandation de diverses manières.

Prenons un exemple où un utilisateur souhaite une recommandation sur la meilleure action à acheter en bourse :

- **Expertise sectorielle** : Un agent pourrait être expert dans un secteur spécifique.
- **Analyse technique** : Un autre agent pourrait être spécialisé dans l'analyse technique.
- **Analyse fondamentale** : Un autre agent encore pourrait exceller dans l'analyse fondamentale. En collaborant, ces agents peuvent fournir une recommandation plus complète à l'utilisateur.

![Recommandation](../../../translated_images/multi-agent-filtering.719217d169391ddb118bbb726b19d4d89ee139f960f8749ccb2400efb4d0ce79.fr.png)

## Scénario : Processus de remboursement

Considérons un scénario où un client cherche à obtenir un remboursement pour un produit. Plusieurs agents peuvent être impliqués dans ce processus, mais distinguons les agents spécifiques à ce processus et les agents généraux pouvant être utilisés dans d'autres contextes.

**Agents spécifiques au processus de remboursement** :

Voici quelques agents qui pourraient être impliqués dans le processus de remboursement :

- **Agent client** : Représente le client et est responsable d'initier le processus de remboursement.
- **Agent vendeur** : Représente le vendeur et est chargé de traiter le remboursement.
- **Agent de paiement** : Représente le processus de paiement et est responsable de rembourser le paiement du client.
- **Agent de résolution** : Représente le processus de résolution et est chargé de résoudre les problèmes éventuels pendant le processus de remboursement.
- **Agent de conformité** : Représente le processus de conformité et veille à ce que le processus de remboursement respecte les réglementations et politiques en vigueur.

**Agents généraux** :

Ces agents peuvent être utilisés dans d'autres parties de votre entreprise.

- **Agent d'expédition** : Représente le processus d'expédition et est chargé de renvoyer le produit au vendeur. Cet agent peut être utilisé à la fois pour le processus de remboursement et pour l'expédition générale d'un produit après un achat, par exemple.
- **Agent de retour d'expérience** : Représente le processus de collecte des retours d'expérience et est chargé de recueillir les retours du client. Ces retours peuvent être collectés à tout moment, pas seulement pendant le processus de remboursement.
- **Agent d'escalade** : Représente le processus d'escalade et est chargé de transmettre les problèmes à un niveau de support supérieur. Ce type d'agent peut être utilisé dans n'importe quel processus nécessitant une escalade.
- **Agent de notification** : Représente le processus de notification et est chargé d'envoyer des notifications au client à différentes étapes du processus de remboursement.
- **Agent d'analyse** : Représente le processus d'analyse et est chargé d'analyser les données relatives au processus de remboursement.
- **Agent d'audit** : Représente le processus d'audit et est chargé de vérifier que le processus de remboursement est correctement exécuté.
- **Agent de reporting** : Représente le processus de reporting et est chargé de générer des rapports sur le processus de remboursement.
- **Agent de connaissance** : Représente le processus de gestion des connaissances et est chargé de maintenir une base de connaissances sur le processus de remboursement. Cet agent peut être informé à la fois sur les remboursements et sur d'autres aspects de votre entreprise.
- **Agent de sécurité** : Représente le processus de sécurité et est chargé de garantir la sécurité du processus de remboursement.
- **Agent de qualité** : Représente le processus de qualité et est chargé d'assurer la qualité du processus de remboursement.

Il y a beaucoup d'agents listés ci-dessus, à la fois pour le processus de remboursement spécifique et pour les agents généraux pouvant être utilisés dans d'autres parties de votre entreprise. Cela devrait vous donner une idée de la manière de décider quels agents utiliser dans votre système multi-agents.

## Exercice

Quel serait un bon exercice pour cette leçon ?

Concevez un système multi-agents pour un processus de support client. Identifiez les agents impliqués dans le processus, leurs rôles et responsabilités, et comment ils interagissent entre eux. Prenez en compte à la fois les agents spécifiques au processus de support client et les agents généraux pouvant être utilisés dans d'autres parties de votre entreprise.

> Réfléchissez avant de lire la solution ci-dessous, vous pourriez avoir besoin de plus d'agents que vous ne le pensez.

> TIP : Pensez aux différentes étapes du processus de support client et prenez également en compte les agents nécessaires à tout système.

## Solution

[Solution](./solution/solution.md)

## Questions de révision

Question : Quand devriez-vous envisager d'utiliser des multi-agents ?

- [] A1 : Lorsque vous avez une charge de travail légère et une tâche simple.  
- [] A2 : Lorsque vous avez une charge de travail importante.  
- [] A3 : Lorsque vous avez une tâche simple.  

[Solution du quiz](./solution/solution-quiz.md)

## Résumé

Dans cette leçon, nous avons exploré le modèle de conception multi-agents, y compris les scénarios où les multi-agents sont applicables, les avantages d'utiliser des multi-agents par rapport à un agent unique, les éléments constitutifs pour implémenter le modèle de conception multi-agents, et comment avoir une visibilité sur les interactions entre les agents.

## Ressources supplémentaires

- [Autogen design patterns](https://microsoft.github.io/autogen/stable/user-guide/core-user-guide/design-patterns/intro.html)  
- [Agentic design patterns](https://www.analyticsvidhya.com/blog/2024/10/agentic-design-patterns/)  
```

**Avertissement** :  
Ce document a été traduit à l'aide de services de traduction automatisés basés sur l'intelligence artificielle. Bien que nous nous efforcions d'assurer l'exactitude, veuillez noter que les traductions automatisées peuvent contenir des erreurs ou des inexactitudes. Le document original dans sa langue d'origine doit être considéré comme la source faisant autorité. Pour des informations critiques, il est recommandé de recourir à une traduction humaine professionnelle. Nous déclinons toute responsabilité en cas de malentendus ou d'interprétations erronées résultant de l'utilisation de cette traduction.