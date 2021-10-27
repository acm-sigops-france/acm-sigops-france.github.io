---
layout: post
title: "C’est un événement : un papier français accepté à SOSP 2021 !"
date: 2021-10-26 09:00:00 -0000
comments: false
---

Il s’agit de « J-NVM: Off-heap Persistent Objects in Java » par Anatole Lefort et al. de l’équipe de SAMOVAR, dirigée par Gaël Thomas à Télécom SudParis (TSP). Le papier porte sur l’intégration de la mémoire persistante avec un langage de programmation de haut niveau. Cela pose en particulier le problème du ramasse-miettes (RM); les solutions existantes sont, soit transparentes mais d’une grande lourdeur, soit explicites mais mal intégrées. La nouvelle approche de Lefort et al. utilise des objets mandataires, afin que les objets persistants échappent au RM tout en s’intégrant de façon transparente. C’est une solution légère et élégante, et de plus efficace, comme le montrent les résultats expérimentaux.

[SOSP](https://sosp2021.mpi-sws.org) est LA conférence phare de la communauté système internationale. C’est à SOSP qu’ont été introduites les grandes innovations marquantes en systèmes qui sont à la base de toutes les architectures modernes. Dans un décompte rapide des numéros précédents, nous retrouvons 24 papiers écrits par des lauréats du Prix Turing. La conférence n’a lieu que tous les deux ans. Il s’agit du canal de publication le plus prestigieux en systèmes, sans sessions parallèles. Une publication à SOSP exige, à la fois créativité, mise en œuvre réelle et expérimentation, et rigueur dans l’écriture. Devant sa haute sélectivité, il y a une forte auto-censure à la soumission.

Le succès du groupe de Gaël Thomas est d’autant plus remarquable que la conférence est complètement trustée par les grandes universités américaines (et plus récemment asiatiques). Les papiers européens sont très rares, en provenance généralement des EPFL, ETHZ, Cambridge ou Microsoft Research. À notre connaissance, et si l'on exclut le collaborateur français occasionnel, il n’y a eu précédemment que deux papiers français depuis la création de SOSP en 1967: Bétourné et al. en 1969, Abrossimov et al. en 1989. 

La communauté informatique française toute entière doit féliciter les auteurs à la hauteur de l’exploit. 


# J-NVM: Off-heap Persistent Objects in Java
Java est un langage communément utilisé par les acteurs majeurs de l'internet pour mettre en œuvre des bases de données larges échelles et des grands systèmes d'analyse de données (Cassandra, Infinispan, Spark, Hadoop, Kafka, Flink, HBase etc...). Comme l'un des principaux goulots d'étranglement de ces systèmes est la vitesse d'accès au support de stockage, il est essentiel qu'ils puissent utiliser efficacement les mémoires persistantes : des supports de stockages quasiment aussi rapide que les mémoires volatiles et de l'ordre de 1000 fois plus rapides que les disques SATA SSD. Malheureusement, utiliser efficacement les mémoires persistantes en Java est difficile. Java, comme de nombreux langages de haut niveau, gère automatiquement la libération de la mémoire avec un ramasse-miettes, et les algorithmes actuels sont totalement incapables de passer à l'échelle de ces mémoires avec leur 128GB à 1TB d'espace.

Dans leur travail, Lefort et al. proposent de revisiter la façon de concevoir les objets Java à l'ère des mémoires persistantes. Ils proposent un principe de découplage qui consiste à séparer la structure de données d'un objet persistant de l'objet volatile qui le représente dans le langage Java. À l'aide de ce principe de découplage, ils peuvent accéder à la mémoire persistante quasi à vitesse native tout en évitant d'augmenter la pression sur le ramasse-miettes puisque les structures de données sont stockées en dehors de la mémoire Java.

À partir de ce principe de découpage, Lefort et al. propose J-NVM, un système complet constitué d'un moteur d'exécution offrant des abstractions simples pour le programmeur, de bibliothèques offrant des structures de données classiques persistantes, et d'un générateur de code permettant de séparer automatiquement les structures de données des objets qui les représentent. L'évaluation de leur système avec la base de donnée Infinispan, avec le banc d'essai TPC-B et avec des micro-évaluations montrent que J-NVM, comparé aux meilleures solutions de l'état de l'art, multiplie par au moins 10 les performances dans la plupart des cas, et que J-NVM permet d'accéder à la mémoire persistante avec des vitesses proches de la mémoire volatile (seulement 50% de ralentissement).

Pour plus de détails, la vidéo de la présentation à SOSP est [disponible en ligne](https://www.youtube.com/watch?v=6RcV9PSsub8) et l'article [disponible sur le site de l'ACM](https://dl.acm.org/doi/10.1145/3477132.3483579).
