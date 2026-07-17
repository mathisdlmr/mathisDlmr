# Heyyyy, moi c'est Mathis Delmaere 👋

**<img src="./miscellaneous/green-dot.gif" width="20" height="20" style="vertical-align:middle;"/> Disponible pour un stage de fin d'études à partir de février 2027**
> [!TIP]
> **Domaines recherchés**
> - Infrastructure
> - SRE
> - Backend *(design patterns, résilience, scalabilité)*
> - DevOps

---

Salut ! Moi c'est **Mathis Delmaere**, étudiant en génie informatique à l'**Université de Technologie de Compiègne (UTC)**, filière **Ingénierie des Systèmes Informatiques (ISI)** (Promo 2022).

Je code majoritairement pour apprendre, découvrir de nouvelles technos et systèmes informatiques (backend, infra ou réseau), ou pour des associations de mon école.

> [!NOTE]
> Les projets présentés ici s'approchent majoritairement du développement web/full stack, car ce sont des projets plus simples à mettre en avant, et car c'est dans ce secteur que j'ai eu l'occasion de réaliser le plus de projets en cours ou en association.
>
> Cependant, ma vraie passion réside dans les domaines suivants : **Infra, Monitoring, Backend, SRE, DevOps**.
>
> Le projet qui représente le mieux ça, c'est mon homelab **[k3s-project](#projet-phare--homelab-kubernetes-auto-hébergé-k3s-project)**, détaillé plus bas dans ce README.

---

## Sommaire

- [Une petite intro ?](#une-petite-intro-)
- [Expérience professionnelle](#expérience-professionnelle)
- [Projet phare - Homelab k3s](#projet-phare--homelab-kubernetes-auto-hébergé-k3s-project)
- [Vie associative à l'UTC](#vie-associative-à-lutc)
- [Projets de cours](#projets-de-cours)
- [Hackathons](#hackathons)
- [Stack & Technos](#stack--technos)
- [Contact](#contact)

---

## Une petite intro ?

À peine âgé de 10 ans, je passais déjà mon temps à jouer à Minecraft, à aller dans le fameux `%appdata%` pour customiser mon jeu, à installer des modpacks à la base pas du tout compatibles entre eux, à toucher à Java et aux VMs pour essayer de comprendre comment fonctionnait le jeu et comment il tournait sur un PC.

La suite logique a été de construire mon propre PC pour faire tourner un Minecraft boosté dessus, de mettre Linux dessus parce que c'est cool, de commencer à faire du développement, puis de décider que j'allais faire ça toute ma vie.

Au cours de mon parcours associatif et académique, je me suis vraiment éclaté avec le développement web/mobile, mais j'avoue que je ne m'amuse plus autant dans ce milieu qu'avant. Depuis que j'ai découvert le **DevOps**, **l'infra**, les **design patterns** pour des backends scalables et résilients, et plus globalement tous les enjeux liés au **SRE**, j'ai l'impression d'avoir trouvé un terrain de jeu bien plus imposant et intéressant que le simple développement.

---

## <img src="./miscellaneous/briefcase.svg" width="22" height="22" style="vertical-align:middle; margin-right: 6" alt=""/> Expérience professionnelle

### Ingénieur SRE DevOps - [Padoa](https://www.padoa.fr) *(Stage : Septembre 2025 → Février 2026)*

Infra & DevOps dans une scale-up française de santé au travail.

- **Kubernetes / ArgoCD** : maintenance et évolution de clusters Kubernetes multi-environnements (staging/prod), gestion des déploiements GitOps
- **Monitoring** : mise en place et exploitation de dashboards Grafana, requêtes Prometheus, agrégation long-terme avec Thanos
- **CI/CD** : écriture et maintenance de pipelines GitHub Actions
- **Go** : développement d'outils internes de tooling infra

### Et d'autres choses...

* Tuteur soutient étudiant en mathématiques et informatique · UTC, Compiègne : Septembre 2023 → Juin 2025
* Stagiaire opérateur sur ligne · Chanel, Compiègne: Février 2023 → Mars 2023
* Réalisation de sites webs en Freelance : Janvier 2023 → Mars 2023

---

## <img src="./miscellaneous/server.svg" width="22" height="22" style="vertical-align:middle; margin-right: 6" alt=""/> Projet phare - Homelab Kubernetes auto-hébergé (k3s-project)

Un cluster **k3s** que j'administre de bout en bout depuis novembre 2025 : c'est le terrain de jeu où j'applique concrètement tout ce qui touche à l'infra, au réseau et au SRE, et où je fais tourner en prod plusieurs des projets associatifs présentés plus bas.

![Photo du Cluster](./images/k3s/cluster.jpg)

**Repo complet (GitOps, à cloner et explorer librement) : [mathisdlmr/k3s-project](https://github.com/mathisdlmr/k3s-project)**

### Architecture - HA géographique

Le cluster k3s HA tourne sur **3 mini-PC (NUC)** répartis sur **2 logements différents**, interconnectés via un mesh **Tailscale** (VPN) : Cilium fait passer son réseau **VXLAN** inter-pods à travers ce tunnel, et l'**etcd** assure le consensus distribué avec des snapshots automatiques toutes les 6h. Bien évidemment, Longhorn a également été setup de sorte à repliquer les volumes sur chaque nodes afin de toujours pouvoir accéder au stockage, même si un node tombe.

PS : _Initialement les 3 NUCs étaient chez mes parents, d'où la photo ci-dessus, mais j'en ai ensuite embarqué 2 dans mon logement à Compiègne_

Depuis mon PC, un **HAProxy local** fait du round-robin sur les 3 control-planes pour un accès HA à l'API server : si un noeud tombe, `kubectl`, ArgoCD et tout mes autres services continuent de fonctionner sans interruption.

### Setup - Approche DevOps

Pour le cluster, j'ai opté pour une approche DevOps, entièrement reproductible en quelques minutes.

Le cluster est dans un premier temps créé par Ansible, qui tourne sur mon ordinateur portable, et setup chacun des NUCs pour les préparer à être une node (sécurisée)

![Configuration des nodes](./images/k3s/setup/1-node-configuration.png)

Une fois l'installation terminée, on obtient cette architecture : 

![Architecture après la configuration des nodes](./images/k3s/setup/1-nodes-configured.png)

Pour continuer le setup, on va installer une application ArgoCD qui va pouvoir reprendre la main sur le ArgoCD installé par Ansible, et se charger de déployer tout le reste du repo par l'intermédiaire de l'application `meta`

![ArgoCD Setup](./images/k3s/setup/2-argocd-setup.png)

Finalement, il ne nous reste plus qu'à récupérer tous les secrets. Pour ça on créé alors un secret kubernetes `infisical-universal-auth-credentials` qui permet à External Secrets Operator de s'identifier auprès de Infisical, pour ensuite pouvoir recréer tous les secrets du repo (login, tunnel cloudflare, ...)

![Re-création des secrets](./images/k3s/setup/3-recreate-secrets.png)

Et voilà le cluster est remonté de A à Z ! 

Les services sont alors accessibles en ligne depuis le nom de domaine `https://mdlmr.fr/*`. Et pour avoir un peu plus de visibilité sur comment ça se passe à ce niveau, voilà un dernier schéma ;)

![Flow d'une requête](./images/k3s/setup/4-request-flow.png)

### Maintenance - CI/CD et GitOps

Le cluster est piloté par **ArgoCD** selon un pattern *app-of-apps* multi-niveaux (avec des sync-waves pour garantir l'ordre de déploiement : ArgoCD lui-même et ses CRDs d'abord, puis l'infra, puis le monitoring, puis les apps, et par **Renovate** qui ouvre automatiquement les PRs de mise à jour des charts Helm et des images Docker (auto-merge sur les mises à jour mineures, revue manuelle sur les majeures).

Un workflow GitHub Actions, **Argo Diff Preview**, génère le diff complet des manifests (Helm rendu + Kustomize) et le poste en commentaire de chaque PR. Pratique pour visualiser l'impact avant de merger :)

<p style="display: flex; gap: 20px; justify-content: center;">
  <img src="./images/k3s/pr-1.png" height="300" alt="Renovate + ArgoDiff Preview" />
  <img src="./images/k3s/pr-2.png" height="300" alt="Renovate + ArgoDiff Preview" />
</p>

### Observabilité complète

Stack **Prometheus + Grafana + Loki + Alloy + Tempo** : les backends applicatifs (Ski'UT en tête) sont instrumentés en **OpenTelemetry** et envoient leurs traces directement dans Tempo.

Logs, métriques et traces sont donc centralisés sur la stack de Grafana Labs, avec Grafana comme point d'entrée unique.

Par curiosité j'ai également prévu de tester les techno suivantes dans les prochains mois : Mimir, Victoria Metrics, Fluentd, Elasticsearch, Kibana, Datadog

### Résultats concrets

En janvier 2026, ce cluster a encaissé en prod les pics de charge du mini-jeu de réservation Ski'UT - **en moyenne autour de 150 reqs/s, allant jusqu'à 200 reqs/s** - absorbés grâce à un cache Cloudflare configuré sur le storage (principalement des images, du CSS et JSS), Traefik en DaemonSet devant le cluster, et un load-balancing ajusté par un HPA pouvant monter de 1 à 3 containers Backend en cas de forte charge.

![Réservation des places Ski'UT 2026](./images/k3s/shotgun-skiut.png)

En temps normal, le serveur héberge aussi mes services persos (TodoList, Affine en Notion-like, Immich pour les photos, mon portfolio...).

---

## <img src="./miscellaneous/users.svg" width="22" height="22" style="vertical-align:middle; margin-right: 6" alt=""/> Vie associative à l'UTC

> [!TIP]
> Les projets sont dans l'ordre chronologique, plus vous descendez mieux c'est ;)

### Integ Fev *(Printemps 2024)*

Reprise, debug et mise à jour (nouvelles fonctionnalités, nouveau design) d'une app mobile **Flutter** et d'un backend **Laravel** pour une intégration de 1,5 semaine. L'application a été utilisée par une centaine d'étudiant.e.s et servait à proposer des animations et gérer l'organisation de la semaine d'intégration.

---

### Integ *(Automne 2024)*

Reprise, debug et mise à jour d'une app mobile **Expo** et d'un backend Laravel pour une intégration de 2 semaines. L'application a été utilisée par plus de 1000 étudiant.e.s et comptait encore plus de fonctionnalités que celle de l'Integ Fev : réservation de repas, file d'attente virtuelle, réservation de navette, scanner de QR code, etc.

<p style="display: flex; gap: 20px; justify-content: center;">
<img src="./images/integ/integ1.jpg" height="200" alt="Screenshot de l'application de l'Intégration" />
<img src="./images/integ/integ2.jpg" height="200" alt="Screenshot de l'application de l'Intégration" />
<img src="./images/integ/integ3.jpg" height="200" alt="Screenshot de l'application de l'Intégration" />
<img src="./images/integ/integ4.jpg" height="200" alt="Screenshot de l'application de l'Intégration" />
<img src="./images/integ/integ5.jpg" height="200" alt="Screenshot de l'application de l'Intégration" />
<img src="./images/integ/integ6.jpg" height="200" alt="Screenshot de l'application de l'Intégration" />
</p>

_Ces screenshots sont issus de la version de l'application sur laquelle j'ai commencé à travailler ; le développement initial avait été effectué par Géo SAGLIO l'année précédant mon arrivée dans l'association._

---

### [Ski'UT](https://github.com/ski-utc) *(Mars 2024 → Fév. 2025)*

Développement de A à Z (avec mon colocataire de l'époque, Eric BJARSTAL) d'une application mobile **Expo** et d'un backend **Laravel** pour gérer l'organisation d'un voyage au ski pour ~500 étudiant.e.s et proposer des animations tout au long de la semaine.

- **Backend** : [ski-utc/server-skiut-2026](https://github.com/ski-utc/server-skiut-2026) - serveur Laravel/Filament pour toute l'organisation du voyage (réservations, planning, navettes…)
- **App mobile** : [ski-utc/app-skiut-2026](https://github.com/ski-utc/app-skiut-2026) - app Expo avec défis, planning, anecdotes, plan du domaine, navettes, notifications push, export/anonymisation RGPD, etc.

<p style="display: flex; gap: 20px; justify-content: center;">
<img src="./images/skiut2025/skiut2.png" height="200" alt="Screenshot de l'application de Skiut 2025" />
<img src="./images/skiut2025/skiut3.png" height="200" alt="Screenshot de l'application de Skiut 2025" />
<img src="./images/skiut2025/skiut4.png" height="200" alt="Screenshot de l'application de Skiut 2025" />
<img src="./images/skiut2025/skiut5.png" height="200" alt="Screenshot de l'application de Skiut 2025" />
<img src="./images/skiut2025/skiut6.png" height="200" alt="Screenshot de l'application de Skiut 2025" />
</p>

<a href="./files/skiut2025.pdf">Voir la présentation du projet</a>

---

### [Ski'UT V2](https://github.com/ski-utc) *(Mars 2025 → Fév. 2026)*

Redéveloppement du projet, cette fois seul, pour le stabiliser et le rendre pérenne :

- CI/CD sur le frontend et le backend (dockerisation + pipeline de tests unitaires backend, ESLint + Prettier frontend)
- Déploiement du backend dans des containers Docker auto-hébergés sur mon cluster Kubernetes personnel *(→ voir la section [Homelab k3s](#-projet-phare--homelab-kubernetes-auto-hébergé-k3s-project) ci-dessus)*
- Intégration de métriques et de traces dans le backend, récupérées par l'agent Alloy du cluster
- Rédaction de documentation pour expliquer le fonctionnement du projet et les bonnes pratiques à suivre

<p style="display: flex; gap: 20px; justify-content: center;">
<img src="./images/skiut2026/skiut1.png" height="200" alt="Screenshot de l'application de Skiut 2026" />
<img src="./images/skiut2026/skiut2.png" height="200" alt="Screenshot de l'application de Skiut 2026" />
<img src="./images/skiut2026/skiut3.png" height="200" alt="Screenshot de l'application de Skiut 2026" />
<img src="./images/skiut2026/skiut4.png" height="200" alt="Screenshot de l'application de Skiut 2026" />
<img src="./images/skiut2026/skiut5.png" height="200" alt="Screenshot de l'application de Skiut 2026" />
<img src="./images/skiut2026/skiut6.png" height="200" alt="Screenshot de l'application de Skiut 2026" />
</p>

Le projet a par la suite entièrement tourné sur mon cluster Kubernetes.

---

### [Le Pic'Asso](https://github.com/picasso-utc) *(Printemps 2025, Automne 2026)*

Bar et foyer étudiant de l'UTC. J'y ai d'abord travaillé sur la maintenance des systèmes informatiques et le développement de nouvelles fonctionnalités pour les équipes de trésorerie et pour les animations (Printemps 2025), puis j'y reviens à partir de l'Automne 2026 pour reprendre et fiabiliser l'ensemble des projets :

- **Ocktopus** - [picasso-utc/ocktopus](https://github.com/picasso-utc/ocktopus) : backend Laravel/Filament pour l'organisation de l'association et les services de trésorerie + API pour l'app mobile
- **Bach** - [picasso-utc/bach](https://github.com/picasso-utc/bach) : borne de paiement en React installée sur des Raspberry Pi, avec badgeuse NFC pour les cartes étudiantes et intégration Weezpay
- Reprise de la documentation, mise à jour des projets, migration des Raspberry Pi 3 vers des Raspberry Pi 5 pour les bornes de vente et l'écran de diffusion

<p style="display: flex; gap: 20px; justify-content: center;">
<img src="./images/pic/ocktopus1.png" height="180" alt="Screenshot de l'interface admin du Pic" />
<img src="./images/pic/ocktopus2.png" height="180" alt="Screenshot de l'interface admin du Pic" />
</p>

**TODO : screenshot des bornes de paiement + de l'app mobile**

---

### [SiMDE](https://assos.utc.fr/simde/) *(Printemps 2025, Printemps 2026)*

Service Informatique de la Maison des Étudiants - hébergement et infra pour les >100 associations de la fédération BDE-UTC.

- **UTCats** : webapp Filament pour la gestion des CATs - [mathisdlmr/UTCats](https://github.com/mathisdlmr/UTCats)
- Debug et développement sur des projets d'infrastructure (majoritairement privés)
- Participation à la migration **nginx/Apache → auto-hébergement k8s**, pour faire passer des applications historiquement en PHP vers du Node.js

---

### Président du Pic'Asso *(Février 2026 → Juillet 2026)*

Élu à la présidence du Pic'Asso, le bar et foyer étudiant de l'UTC, pour un 6 mois à la tête d'une équipe de 25 personnes.

- Interlocuteur direct avec la présidence du BDE, l'administration de l'école, le service hygiène et sécurité (SHS) et le service incendie
- Pilotage de projets sur les locaux : réflexion, demandes de subvention, suivi des travaux
- Réflexion et actions sur les enjeux RSE, le savoir-vivre ensemble, la non-discrimination et la lutte contre les VSS
- Accompagnement individuel des membres de l'association pour s'assurer de leur bien-être et de la bonne marche du foyer
- Organisation d'événements quasi hebdomadaires, chacun avec son propre dossier de sécurité
- Supervision de la logistique (~1000L de bière, 125 sandwichs et 250 viennoiseries par semaine, 400 canettes de soft) et des relations fournisseurs associées
- Entretien des locaux et des systèmes informatiques, soutien sur la communication de l'association, etc.

---

## <img src="./miscellaneous/graduation-cap.svg" width="22" height="22" style="vertical-align:middle; margin-right: 6" alt=""/> Projets de cours

> [!TIP]
> La grande majorité des repos embarquent un Makefile et/ou un Dockerfile. N'hésite pas à les essayer !

| Matière | Année | Projet | Description | Stack | Lien |
|---|---|---|---|---|---|
| **API Init, Introduction à Linux** | Automne 2023 | Space Invaders | Jeu Space Invaders dans le terminal | `Bash` | [mathisdlmr/Space-Invaders](https://github.com/mathisdlmr/Space-Invaders) |
| **IC05, Analyse critique des données numériques** | Printemps 2024 | Scraper de Letterboxd | Scraper Letterboxd → PostgreSQL, puis nettoyage et analyse des données via Python | `Python` · `PostgreSQL` | [mathisdlmr/ic05](https://github.com/mathisdlmr/ic05) |
| **NF18, Conception de BDD (non-)relationnelles** | Printemps 2024 | Projet de BDD | BDD d'un aéroport en relationnel puis non-relationnel, implémentée dans PostgreSQL | `PostgreSQL` · `Python` | [mathisdlmr/nf18](https://github.com/mathisdlmr/nf18) |
| **SR04, Réseaux** | Automne 2024 | Travail de recherche | Recherche sur l'IoT pour la santé | `BLE` · `Zigbee` · `AMQP` · `MQTT` · `CoAP` | [voir plus bas ⤵](#sr04) |
| **SR10, Introduction au développement web** | Printemps 2025 | Plateforme de recrutement | Webapp style LinkedIn - gestion d'offres, candidatures, organisations, avec rôles admin/recruteur/candidat | `Express.js` · `EJS` · `SQLite` | [mathisdlmr/sr10](https://github.com/mathisdlmr/sr10) |
| **IA02, Résolution de problèmes par algorithme** | Printemps 2025 | Résolution du morpion par algorithme | Implémentation d'un MCTS pour résoudre le jeu du morpion | `Python` | [mathisdlmr/ia02](https://github.com/mathisdlmr/ia02) |
| **TX, projet** | Automne 2025 | Plateforme de gestion | Webapp Filament pour le programme de tutorat de l'UTC | `Laravel` · `Filament` | [mathisdlmr/Tutut](https://github.com/mathisdlmr/Tutut) |
| **SR03, Architecture des applications web** | Printemps 2026 | Chat multi-utilisateurs en WebSocket | Application de chat avec panel admin, rooms temporaires, messages vocaux, photos et fichiers | `Spring Boot` · `React` · `WebSocket` | [mathisdlmr/sr03](https://github.com/mathisdlmr/sr03) |
| **SR05, Systèmes répartis** | Printemps 2026 | Loup-garou distribué | Jeu du loup-garou décentralisé implémentant exclusion mutuelle distribuée et snapshots (horloges vectorielles) | `Go` | [mathisdlmr/sr05](https://github.com/mathisdlmr/sr05) |

---

### IC05

<a href="./files/ic05.pdf">Voir le rapport du projet</a>

---

### SR04

<a href="./files/sr04-presentation.pdf">Voir la présentation du projet</a> | <a href="./files/sr04-rapport.pdf">Voir le rapport du projet</a>

---

### IA02

<p style="display: flex; gap: 20px; justify-content: center;">
  <img src="./images/ia02/ia02-3.gif" height="200" alt="Démo d'un MCTS" />
</p>
<p style="display: flex; gap: 20px; justify-content: center;">
  <img src="./images/ia02/ia02-1.png" height="200" alt="Élément de gameplay IA02" />
  <img src="./images/ia02/ia02-2.png" height="200" alt="Élément de gameplay IA02" />
</p>

---

### TX

<p style="display: flex; gap: 20px; justify-content: center;">
  <img src="./images/tutut/tutut1.png" height="200" alt="Élément de l'interface de Tut'ut" />
  <img src="./images/tutut/tutut2.png" height="200" alt="Élément de l'interface de Tut'ut" />
</p>

**TODO : ajouter des screenshots supplémentaires ici**

---

### SR03

<p style="display: flex; gap: 20px; justify-content: center;">
<img src="./images/sr03/sr03-1.png" height="180" alt="Élément de l'interface du projet de SR03" />
<img src="./images/sr03/sr03-2.png" height="180" alt="Élément de l'interface du projet de SR03" />
<img src="./images/sr03/sr03-3.png" height="180" alt="Élément de l'interface du projet de SR03" />
<img src="./images/sr03/sr03-4.png" height="180" alt="Élément de l'interface du projet de SR03" />
</p>

→ La majorité du projet porte sur la sécurité de l'application ainsi que l'utilisation de WebSockets.

---

### SR05

<a href="./files/sr05.pdf">Voir la présentation du projet</a>

---

### Annexe : PHITECO

_Au-delà des cours en informatique, j'ai suivi de nombreux autres cours dans le domaine des sciences cognitives ainsi que sur le lien entre technique et cognition. En parallèle de mon diplôme de génie informatique, je suis la mineure [PHITECO](https://sites.google.com/site/mineurphiteco/) (PHIlosophie, TEchnique et COgnition)._

> PHITECO propose des éléments scientifiques, philosophiques et pratiques pour comprendre la manière dont les technologies transforment nos façons de penser, de percevoir, de raisonner, d'agir et d'interagir. Le mineur permet à l'étudiant-ingénieur d'être introduit aux grands enjeux, théoriques et pratiques, des sciences cognitives.

---

## <img src="./miscellaneous/laptop.svg" width="22" height="22" style="vertical-align:middle; margin-right: 6" alt=""/> Hackathons

### CultureXP *(Février 2025 - GottaGoHack, Epitech)*

App mobile de gamification culturelle : carte de lieux culturels (via OpenStreetMap), quêtes, podcasts (via PodcastIndex), livres (via Google Books API), boutique d'achat avec l'XP gagnée. Un projet développé en 48h.

**Stack** : `Expo` · `React Native` · `TypeScript`
→ [mathisdlmr/CultureXP](https://github.com/mathisdlmr/CultureXP)

<a href="./files/culturexp.pdf">Voir la présentation du projet</a>

---

### Aide-un-étudiant *(Juillet 2025 - UTC x mc2i)* - <img src="./miscellaneous/yellow-trophy.svg" width="16" height="16" style="vertical-align:-2px;" alt=""/> 1er prix

Plateforme d'entraide locale entre étudiants : prêt d'objets, échange de services, partage de connaissances. Pensée accessibilité et éco-conception (Server Components, requêtes Prisma optimisées, rendu statique, Score d'Impact Positif).

**Stack** : `Next.js` · `TypeScript` · `Prisma` · `TailwindCSS` · `NextAuth.js`
→ [mathisdlmr/hackhaton-utc-mc2i](https://github.com/mathisdlmr/hackhaton-utc-mc2i)

<a href="./files/aide-un-etu.pdf">Voir la présentation du projet</a>

---

## <img src="./miscellaneous/gears.svg" width="22" height="22" style="vertical-align:middle; margin-right: 6" alt=""/> Stack & Technos

### Langages de programmation

<p style="display: flex; gap: 20px;">
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/python/python-original.svg" height="40" alt="Python" />
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/php/php-original.svg" height="40" alt="PHP" />
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/javascript/javascript-original.svg" height="40" alt="JavaScript" />
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/typescript/typescript-original.svg" height="40" alt="TypeScript" />
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/go/go-original.svg" height="40" alt="Go" />
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/bash/bash-original.svg" height="40" alt="Bash" />
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/java/java-original.svg" height="40" alt="Java" />
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/c/c-original.svg" height="40" alt="C" />
</p>

### Frameworks & Bibliothèques Web

<p style="display: flex; gap: 20px;">
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/react/react-original.svg" height="40" alt="React / React Native" />
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/nextjs/nextjs-original.svg" height="40" alt="Next.js" />
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/laravel/laravel-original.svg" height="40" alt="Laravel" />
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/nodejs/nodejs-original.svg" height="40" alt="Node.js" />
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/spring/spring-original.svg" height="40" alt="Spring Boot" />
<img src="https://seekicon.com/free-icon-download/expo_1.png" height="40" alt="Expo" />
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/flutter/flutter-original.svg" height="40" alt="Flutter" />
</p>

### DevOps & Infrastructure

<p style="display: flex; gap: 20px;">
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/bash/bash-original.svg" height="40" alt="Bash" />
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/git/git-original.svg" height="40" alt="Git" />
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/docker/docker-original.svg" height="40" alt="Docker" />
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/kubernetes/kubernetes-plain.svg" height="40" alt="Kubernetes" />
<img src="https://www.redhat.com/rhdc/managed-files/helm.svg" height="40" alt="Helm" />
<img src="https://cdn.prod.website-files.com/5f10ed4c0ebf7221fb5661a5/5f2ba11e378c8f49e8b28486_argo.png" height="40" alt="ArgoCD" />
<img src="https://miro.medium.com/v2/resize:fit:1400/1*7qk0-4XwCKWQO0GU5Hu39w.png" height="40" alt="GitHub Actions" />
<img src="https://forge.inrae.fr/uploads/-/system/project/avatar/6031/gitlab-ci.png" height="40" alt="GitLab CI" />
</p>

### Observabilité

<p style="display: flex; gap: 20px;">
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/prometheus/prometheus-original.svg" height="40" alt="Prometheus" />
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/grafana/grafana-original.svg" height="40" alt="Grafana" />
<img src="https://grafana.com/media/docs/loki/logo-grafana-loki.png" height="40" alt="Loki" />
<img src="https://grafana.com/media/docs/alloy/alloy_icon.png" height="40" alt="Alloy" />
<img src="https://thanos.io/icon-dark.png" height="40" alt="Thanos" />
</p>

### Bases de données

<p style="display: flex; gap: 20px;">
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/sqlite/sqlite-original.svg" height="40" alt="SQLite" />
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/mysql/mysql-original.svg" height="40" alt="MySQL" />
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/postgresql/postgresql-original.svg" height="40" alt="PostgreSQL" />
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/mongodb/mongodb-original.svg" height="40" alt="MongoDB" />
</p>

### Cloud & Réseau

<p style="display: flex; gap: 20px;">
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/cloudflare/cloudflare-original.svg" height="40" alt="Cloudflare" />
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/traefikproxy/traefikproxy-original.svg" height="40" alt="Traefik" />
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/nginx/nginx-original.svg" height="40" alt="Nginx" />
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/apache/apache-original.svg" height="40" alt="Apache" />
<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/terraform/terraform-original.svg" height="40" alt="Terraform" />
<img src="https://raw.githubusercontent.com/cert-manager/cert-manager/ae6723401bd1bef1c00bd3c46a52c15387cd05ba/logo/logo.svg" height="40" alt="Cert-Manager" />
</p>

_Prochainement : ESO, Longhorn, Ansible, EFK eph, Fluentd, Kibana, Cilium, Mimir_

---

## <img src="./miscellaneous/envelope.svg" width="22" height="22" style="vertical-align:middle; margin-right: 6" alt=""/> Contact

- **Email** : [mathis.dlmr@gmail.com](mailto:mathis.dlmr@gmail.com)
- **LinkedIn** : [linkedin.com/in/mathis-delmaere-6a6325325](https://www.linkedin.com/in/mathis-delmaere-6a6325325/)
- **GitHub** : [github.com/mathisdlmr](https://github.com/mathisdlmr)
- **Localisation / mobilité** : à l'international ou en France en travaillant avec des acteurs internationaux
- **Langues** : Français (natif), Anglais (C1)

---

Merci d'être passé·e par ici !