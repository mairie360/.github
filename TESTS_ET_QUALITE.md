# 🧪 **Tests et Assurance Qualité**

Ce document définit les bonnes pratiques et processus à suivre pour garantir la **qualité**, la **fiabilité** et la **stabilité** du code au sein du projet **Mairie360**.

---

## 🎯 **Objectifs**

L’assurance qualité vise à :
- Détecter les erreurs le plus tôt possible.
- Garantir un code robuste, lisible et maintenable.
- Préserver la cohérence entre les différents modules.
- Assurer la conformité avec les exigences fonctionnelles et techniques.

---

## 🧩 **1. Types de tests**

### ✅ **Tests unitaires**
- Vérifient le bon fonctionnement d’une **unité de code isolée** (fonction, classe, composant…).
- Permettent de détecter rapidement les régressions.

**Bonnes pratiques :**
- Un test par cas d’usage.
- Utiliser des **noms explicites** pour les tests.
- Couvrir les cas normaux, limites et erreurs attendues.

---

### 🔗 **Tests d’intégration**
- Vérifient que plusieurs modules fonctionnent correctement **ensemble**.
- S’assurent que les dépendances (API, base de données, services externes) interagissent comme prévu.

**Bonnes pratiques :**
- Simuler les dépendances externes via des **mocks**.
- Tester les flux de données réels entre modules.

---

### 🧠 **Tests fonctionnels**
- Vérifient que les fonctionnalités répondent bien aux **exigences utilisateurs**.
- Souvent réalisés via une interface ou un outil automatisé (ex : Cypress, Playwright).

**Bonnes pratiques :**
- Basés sur les **critères d’acceptation** définis dans les issues GitHub.
- Scénarios rédigés dans un langage compréhensible par tous (ex : Gherkin).

---

### 💻 **Tests manuels**
- Réalisés par les développeurs ou testeurs sur des environnements **staging**.
- Permettent de valider le comportement visuel, l’ergonomie et les interactions complexes.

**Bonnes pratiques :**
- Documenter les étapes de test dans l’issue ou la PR.
- Signaler tout comportement inattendu avant la mise en production.

---

## ⚙️ **2. Intégration Continue (CI)**

Chaque module **Mairie360** doit être relié à une **pipeline CI** (GitHub Actions, GitLab CI, etc.) pour :
- Lancer automatiquement les tests unitaires et d’intégration.
- Vérifier la qualité du code via des outils d’analyse statique (ESLint, PHPStan, etc.).
- Empêcher la fusion de code tant que les tests ne sont pas passés ✅.

---

## 📈 **3. Mesure de la couverture de tests**

La **couverture de tests** indique le pourcentage de code exécuté lors des tests.
Objectif recommandé : **> 80 % de couverture** pour les modules critiques.


---

## 🔍 **4. Revue de qualité avant fusion**

Avant de fusionner une branche dans `main` :
- Tous les tests doivent passer.
- Le code doit être **relisible, documenté et cohérent**.
- La PR doit être **validée par au moins un reviewer**.
- Les changements doivent être **justifiés et traçables**.

---

## 🧱 **5. Validation post-déploiement**

Après chaque déploiement en **staging** ou **production** :
- Effectuer un **test de non-régression** sur les principales fonctionnalités.
- Vérifier les **performances** et la **stabilité**.
- Recueillir les **retours utilisateurs** pour identifier d’éventuels problèmes.

---

## 🪄 **6. Bonnes pratiques générales**

- Toujours **tester avant de merger**.
- **Ne pas ignorer les tests** en cas d’échec CI.
- Favoriser les **tests automatisés reproductibles**.
- Documenter tout scénario de test spécifique.
- Corriger immédiatement les **bugs critiques** détectés.

---

## 🧾 **Résumé du flux qualité**

1️⃣ Écrire les tests unitaires lors du développement.
2️⃣ Valider l’intégration et les dépendances.
3️⃣ Soumettre une PR avec **tests et résultats**.
4️⃣ Vérifier la CI avant fusion.
5️⃣ Tester en staging.
6️⃣ Déployer et valider en production.

---

🎉 **Grâce à ce processus, Mairie360 garantit un code fiable, évolutif et conforme aux exigences des collectivités locales.**
