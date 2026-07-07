# Heyyyy, moi c'est Mathis Delmaere 👋

Salut ! Moi c'est **Mathis Delmaere**, étudiant en génie informatique à l'**Université de Technologie de Compiègne (UTC)**, filière **Ingénierie des Systèmes Informatiques (ISI)** (Promo 2022)

Je code majoritairement pour apprendre, découvrir de nouvelles technos et systèmes informatiques (que ça soit niveau backend, infra ou réseau), ou encore pour des associations de mon école.

> [!NOTE]
> Les projets présentés ici s'approchent majoritairement du développement web/full stack, car ce sont des projets qui sont plus simples à mettre en avant, mais aussi car c'est dans ce secteur que j'ai eu l'occasion de réaliser le plus de projets en cours ou dans les associations.
>
> Cependant, ma vraie passion réside dans les domaines suivants : Infra, Monitoring, Backend, SRE, DevOps
>
> Pour un exemple de projet plus concret dans ces domaines je t'invite à regarder mon homelab [mathisdlmr/k3s-project](https://github.com/mathisdlmr/k3s-project)

---

# Une petite intro ?

A peine âgé de 10 ans, je passais déjà mon temps à jouer à minecraft, aller dans le fameux `%appdata%` pour custom mon jeu, installer des modpacks initialement pas du tout compatibles, commencer à toucher à Java et aux VMs pour essayer de comprendre comment fonctionnait le jouer et comment il tournait sur un PC.

La suite logique était d'ensuite construire mon propre PC pour faire tourner un Minecraft boosté dessus, commencer à mettre Linux dessus parce que c'est cool, commencer à faire du développement, puis décider que j'allais faire ça toute ma vie.

Au cours de mon parcours associatif et académique je me serai vraiment éclaté avec le développement web/mobile, mais j'avoue que je ne m'amuse plus autant dans ce milieu qu'avant. Depuis que j'ai découvert le **DevOps**, **l'Infra**, les **deisgn patterns** pour des backends scalables et résilients, et plus globalement tous les enjeux liés au **SRE**, j'ai l'impression d'avoir trouvé un terrain de jeu bien plus imposant et intéressant que le simple développement.

---

# 💼 Expérience professionnelle

### Ingénieur SRE DevOps - [Padoa](https://www.padoa.fr) *(Stage)*

Infra & DevOps dans une scale-up française de santé au travail
- **Kubernetes/ArgoCD** : maintenance et évolution des clusters kubernetes multi-environnements
- **Monitoring** : Grafana, Prometheus, Thanos
- **CI/CD** : GitHub Actions et pipelines de déploiement
- **Go** : développement d'outils internes (tooling infra)

---

# 🏫 Vie associative à l'UTC

### Integ Fev *(Printemps 2023)*

Reprise, debug et mise à jour (nouvelles features, nouveau design) d'une app mobile **Flutter** et d'un backend **Laravel** pour une intégration de 1,5 semaine.
L'application a été utilisée par une ~100aine d'étudiant.e.s et servait essentiellement à proposer des animations et gérer l'organisation de la semaine d'intégration.

---

### Integ *(Automne 2023)*

Reprise, debug et mise à jour (nouvelles features, nouveau design) d'une app mobile **Expo** et d'un backend Laravel pour une intégration de 2 semaines.
L'application a été utilisée par >1000 étudiant.e.s et comptait encore plus de fonctionnalités que celle de l'integ fev : réservation de repas, file d'attente virtuelle, réservation de navette, scanner de QR code, etc.

<p style="display: flex; gap: 20px; justify-content: center;">
<img src="./images/integ/integ1.jpg" height="200" alt="Screenshot de l'application de l'Intégration" />
<img src="./images/integ/integ2.jpg" height="200" alt="Screenshot de l'application de l'Intégration" />
<img src="./images/integ/integ3.jpg" height="200" alt="Screenshot de l'application de l'Intégration" />
<img src="./images/integ/integ4.jpg" height="200" alt="Screenshot de l'application de l'Intégration" />
<img src="./images/integ/integ5.jpg" height="200" alt="Screenshot de l'application de l'Intégration" />
<img src="./images/integ/integ6.jpg" height="200" alt="Screenshot de l'application de l'Intégration" />
</p>

_Ces screenshot sont issus de la version de l'application sur laquelle j'ai commencé à travailler, mais ce développement avait été effectué par Géo SAGLIO l'année précédent mon arrivée dans l'association_ 

---

### [Ski'UT](https://github.com/ski-utc) *(2024 -> 2025)*

Développement de A à Z (avec mon colocataire de l'époque, Eric BJARSTAL) d'une application mobile **Expo** et d'un backend **Laravel** pour gérer l'organisation d'un voyage au ski pour ~500 étudiant.e.s et proposer des animations tout au long de la semaine
* **Backend** [ski-utc/server-skiut-2026](https://github.com/ski-utc/server-skiut-2026) : Serveur Laravel/Filament pour toute l'organisation du voyage (réservations, planning, navettes…)
* **App mobile** : [ski-utc/app-skiut-2026](https://github.com/ski-utc/app-skiut-2026) : App Expo avec défis, planning, anecdotes, plan du domaine, navettes, notifications push, export/anonymisation RGPD, etc.

<p style="display: flex; gap: 20px; justify-content: center;">
<img src="./images/skiut2025/skiut2.png" height="200" alt="Screenshot de l'application de Skiut 2025" />
<img src="./images/skiut2025/skiut3.png" height="200" alt="Screenshot de l'application de Skiut 2025" />
<img src="./images/skiut2025/skiut4.png" height="200" alt="Screenshot de l'application de Skiut 2025" />
<img src="./images/skiut2025/skiut5.png" height="200" alt="Screenshot de l'application de Skiut 2025" />
<img src="./images/skiut2025/skiut6.png" height="200" alt="Screenshot de l'application de Skiut 2025" />
</p>

<a href="./files/skiut2025.pdf" download>Télécharger la présentation du projet</a>

---

### [Ski'UT V2](https://github.com/ski-utc) *(2025 -> 2026)*

Redéveloppement sur mon projet de l'époque, cette fois seul, pour stabiliser le projet et le rendre pérenne : 
* CI/CD sur le frontend et le backend
  * Dockerization + Pipeline de tests unitaires pour le backend
  * ESLint + Prettier pour le frontend 
* Déploiement du backend dans des containers docker auto-hébergés sur mon serveur kubernetes personnel
* Intégration de métriques et de traces dans le backend, récupérés par la suite par l'agent Alloy dans le cluster
* Rédaction de documentation pour expliquer le fonctionnement du projet et donner des bonnes pratiques à suivre

<p style="display: flex; gap: 20px; justify-content: center;">
<img src="./images/skiut2026/skiut1.png" height="200" alt="Screenshot de l'application de Skiut 2026" />
<img src="./images/skiut2026/skiut2.png" height="200" alt="Screenshot de l'application de Skiut 2026" />
<img src="./images/skiut2026/skiut3.png" height="200" alt="Screenshot de l'application de Skiut 2026" />
<img src="./images/skiut2026/skiut4.png" height="200" alt="Screenshot de l'application de Skiut 2026" />
<img src="./images/skiut2026/skiut5.png" height="200" alt="Screenshot de l'application de Skiut 2026" />
<img src="./images/skiut2026/skiut6.png" height="200" alt="Screenshot de l'application de Skiut 2026" />
</p>

Le projet a par la suite entièrement tourné sur mon serveur kubernetes, et a tenu des pics de charge à >10k reqs/sec lors de certaines réservations à des évènements.
Pour çela le projet a grandement profité d'une infrastructure réseau mature avec Cloudflare -> Tunnel Cloudfalre -> Traefik in-cluster -> Load balancing sur 2 containers Docker avec un HPA en cas de grosse charge

<p style="display: flex; gap: 20px; justify-content: center;">
<img src="./images/skiut2026/shotgun.png" height="300" alt="Screenshot du shotgun de Skiut 2026" />
</p>

---

### [Le Pic'Asso](https://github.com/picasso-utc) *(Printemps 2025)*

Bar et foyer étudiant de l'UTC dans lequel j'ai travaillé à la maintenance des systèmes informatique utilisés et au développement de nouvelles features pour les équipes de trésorerie et pour des animations

* **Ocktopus** [picasso-utc/ocktopus](https://github.com/picasso-utc/ocktopus) : Backend Laravel/Filament pour l'organisation de l'association et les services de trésorerie + API pour l'app mobile
* **Bach** [picasso-utc/bach](https://github.com/picasso-utc/bach) : Borne de paiement en React installée sur des Raspberry Pi, avec badgeuse NFC pour les cartes étudiantes et intégration Weezpay

<p style="display: flex; gap: 20px; justify-content: center;">
<img src="./images/pic/ocktopus1.png" height="180" alt="Screenshot de l'interface admin du Pic" />
<img src="./images/pic/ocktopus2.png" height="180" alt="Screenshot de l'interface admin du Pic" />
</p>

TODO : screenshot des bornes

---

### [SiMDE](https://assos.utc.fr/simde/) *(Printemps 2025, Printemps 2026)*

Service Informatique de la Maison des Étudiants - hébergement et infra pour les >100 associations de la fédération BDE-UTC.

- **UTCats** : webapp Filament pour la gestion des CATs - [mathisdlmr/UTCats](https://github.com/mathisdlmr/UTCats)
- Debug et développement sur des projets d'infrastructure (majoritairement privés)
- Participation à la migration **nginx/Apache -> auto-hébergement k8s** pour passer d'applications uniquement en PHP vers du NodeJS

---

### [Le Pic'Asso](https://github.com/picasso-utc) *(Automne 2026 ?)*

Retour au Pic'Asso pour
* Refaire de la documentation,
* Remettre tous les projets à jours
* Effectuer la migration des raspberry 3 vers 5 utilisés pour les bornes de vente et écran de diffusion
* Développer de A à Z l'app mobile qui irait se brancher sur l'API du Backend : [mathisdlmr/app-pic](https://github.com/mathisdlmr/app-pic) : Application mobile du Pic'Asso, développée de A à Z

TODO : screenshot de l'app

---

# 📚 Projets de cours

> La grande majorité des repo embarquent Makefile et/ou Dockerfile. N'hésite pas à les essayer !

| Matière | Année | Projet | Description | Stack | Lien |
|---|---|---|---|---|---|
| **SR05, Systèmes répartis** | Printemps 2026 | Loup-garou distribué | Jeu du loup-garou décentralisé implémentant exclusion mutuelle distribuée et snapshots (horloges vectorielles) | `Go` | [mathisdlmr/sr05](https://github.com/mathisdlmr/sr05) |
| **SR03, Architecture des app web** | Printemps 2026 | Chat multi-utilisateurs en WebSocket| Application de chat avec panel admin, rooms temporaires, messages vocaux, photos et fichiers | `Spring Boot` · `React` · `WebSocket` | [mathisdlmr/sr03](https://github.com/mathisdlmr/sr03) |
| **TX, projets** | Automne 2025 | Plateforme de gestion | Webapp Filament pour le programme de tutorat de l'UTC | `Laravel` · `Filament` | [mathisdlmr/Tutut](https://github.com/mathisdlmr/Tutut) |
| **IA02, Résolution de Problèmes par algo** | Printemps 2025 | Résolution du Morpion par Algo | Implémentation d'un MCTS pour résoudre le problème du jeu du morpion | `Python` | [mathisdlmr/ia02](https://github.com/mathisdlmr/ia02) |
| **SR10, Introduction au dev web** | Printemps 2025 | Plateforme de recrutement | Webapp style LinkedIn - gestion d'offres, candidatures, organisations, avec rôles admin/recruteur/candidat | `Express.js` · `EJS` · `SQLite` | [mathisdlmr/sr10](https://github.com/mathisdlmr/sr10) |
| **SR04, Réseaux** | Automne 2024 | Travail de recherche | Recherche sur l'IoT pour la santé | `BLE` · `Zigbee` · `AMQP` · `MQTT` · `CoAP` | ... |
| **NF18, Conception de BDD (non-)relationnelles** | Printemps 2024 | Projet de BDD | BDD d'un aéroport en relationnel puis non-relationnel implémentée dans PostgreSQL | `PostgreSQL` · `Python` | [mathisdlmr/nf18](https://github.com/mathisdlmr/nf18) |
| **IC05, Analyse critique des données numériques** | Printemps 2024 | Scrapper de Letterboxd | Scrapper Letterboxd -> PostgreSQL puis nettoyage et analyse des données via Python | `Python` · `PostgreSQL` | [mathisdlmr/ic05](https://github.com/mathisdlmr/ic05) |
| **API Init, Introduction à Linux** | Automne 2023 | Space Invaders | Jeu Space Invaders dans le terminal | `Bash` | [mathisdlmr/Space-Invaders](https://github.com/mathisdlmr/Space-Invaders) |

---

### SR05

<a href="./files/sr05.pdf" download>Télécharger la présentation du projet</a>

---

### SR03

<p style="display: flex; gap: 20px; justify-content: center;">
<img src="./images/sr03/sr03-1.png" height="180" alt="Element de l'interface du projet de SR03" />
<img src="./images/sr03/sr03-2.png" height="180" alt="Element de l'interface du projet de SR03" />
<img src="./images/sr03/sr03-3.png" height="180" alt="Element de l'interface du projet de SR03" />
<img src="./images/sr03/sr03-4.png" height="180" alt="Element de l'interface du projet de SR03" />
</p>

-> La majorité du projet porte sur la sécurité de l'application ainsi que l'utilisation de WebSockets.

---

### TX

<p style="display: flex; gap: 20px; justify-content: center;">
  <img src="./images/tutut/tutut1.png" height="200" alt="Element de l'interface de Tut'ut" />
  <img src="./images/tutut/tutut2.png" height="200" alt="Element de l'interface de Tut'ut" />
</p>

TODO : ajouter des screens ici

---

### IA02

<p style="display: flex; gap: 20px; justify-content: center;">
  <img src="./images/ia02/ia02-3.gif" height="200" alt="Démo d'un MCTS" />
</p>
<p style="display: flex; gap: 20px; justify-content: center;">
  <img src="./images/ia02/ia02-1.png" height="200" alt="Element de gameplay IA02" />
  <img src="./images/ia02/ia02-2.png" height="200" alt="Element de gameplay IA02" />
</p>

---

### SR04

<a href="./files/sr04-presentation.pdf" download>Télécharger la présentation du projet</a> | <a href="./files/sr04-rapport.pdf" download>Télécharger le rapport du projet</a>

---

### IC05

<a href="./files/ic05.pdf" download>Télécharger le rapport du projet</a>

---


_Au delà des cours dans le domaine de l'informatique, j'ai suivi de nombreux autres cours dans le domain des sciences cognitives ainsi que du lien entre technique et cognition. J'ai alors, en parallèle de mon diplôme de génie informatique, la mineure [PHITECO](https://sites.google.com/site/mineurphiteco/) (PHIlosophie, TEchnique et COgnition)._

> PHITECO propose des éléments scientifiques, philosophiques et pratiques pour comprendre la manière dont les technologies transforment nos façons de penser, de percevoir, de raisonner, d’agir et  d’interagir – bref, nos activités cognitives, telles qu'elles sont étudiées par les sciences cognitives et par la philosophie. Le mineur PHITECO permet ainsi à l'étudiant-ingénieur d'être introduit aux grands enjeux, théoriques et pratiques, des sciences cognitives

---

# 🚀 Hackathons

### CultureXP *(Février 2025 - GottaGoHack, Epitech)*

App mobile de gamification culturelle : carte de lieux culturels (via OpenStreetMap), quêtes, podcasts (via PodcastIndex), livres (via GoogleAPO), boutique d'achat avec l'XP. Un projet développé en 48h

**Stack** : `Expo` · `React Native` · `TypeScript`
-> [mathisdlmr/CultureXP](https://github.com/mathisdlmr/CultureXP)

<a href="./files/culturexp.pdf" download>Télécharger la présentation du projet</a>

---

### Aide-un-étudiant *(Juillet 2025 - UTC x mc2i)* - 🏆 1er prix

Plateforme d'entraide locale entre étudiants : prêt d'objets, échange de services, partage de connaissances. Pensée accessibilité et éco-conception (Server Components, requêtes Prisma optimisées, rendu statique, Score d'Impact Positif).

**Stack** : `Next.js` · `TypeScript` · `Prisma` · `TailwindCSS` · `NextAuth.js`
-> [mathisdlmr/hackhaton-utc-mc2i](https://github.com/mathisdlmr/hackhaton-utc-mc2i)

<a href="./files/aide-un-etu.pdf" download>Télécharger la présentation du projet</a>

---

# 🏠 Projets personnels

### k3s-project - Homelab k3s HA

Cluster k3s haute disponibilité déployé sur 3 Ordinateurs NUC

**Objectif** : apprendre les pratiques DevOps/SRE en conditions réelles, tout en hébergeant mes projets et en servant d'infra de secours pour les gros événements étudiants.

**Ce qui tourne dessus** : ArgoCD, Traefik, cert-manager, Cloudflared, Longhorn, Grafana, Prometheus, Loki, Alloy, Affine, Immich…

**Cas d'usage réel** : en janvier 2026, le cluster a hébergé le backend du mini-jeu de réservation Ski'UT, avec caching Cloudflare configuré à la main, pour absorber les pics à **10-15k req/s**. En temps normal le cluster héberge mes propres services de TodoList, Notion-Like (Affine), hébergement de photos (Immich), hébergement web...

-> [mathisdlmr/k3s-project](https://github.com/mathisdlmr/k3s-project)

---

# ⚙️ Stack & Technos

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

_Prochainement : Longhorn, ceph, Fluentd, kibana, tempo, victoria metrics_

---

# 📬 Contact

- 📧 **Email** : [mathis.dlmr@gmail.com](mailto:mathis.dlmr@gmail.com)
- 💼 **LinkedIn** : [linkedin.com/in/mathis-delmaere-6a6325325](https://www.linkedin.com/in/mathis-delmaere-6a6325325/)

---

Merci d'être passé·e par ici !
