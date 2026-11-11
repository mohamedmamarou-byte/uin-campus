# UIN-Campus

Système de gestion académique de l'Université Islamique du Niger (UIN). Projet fil rouge du cours de Programmation Orientée Objet en C++ moderne.

La version actuelle (0.1.0) est le **squelette** du projet : l'arborescence, la configuration des outils, et un premier programme qui affiche le titre et la version.

## Fonctionnalités prévues

- Gestion des étudiants, enseignants, filières et unités d'enseignement (UE)
- Inscriptions et saisie des notes (entre 0 et 20)
- Calcul des moyennes par UE et de la moyenne générale
- Attribution des crédits et production des bulletins

## Prérequis

- Linux (testé sous Ubuntu)
- Un compilateur C++23 avec `<print>` : GCC 14 ou plus
- CMake 3.25 ou plus et Ninja

Installation sous Ubuntu :

```
sudo apt update
sudo apt install build-essential gcc-14 g++-14 \
                 clang clangd clang-format clang-tidy lldb gdb \
                 cmake ninja-build valgrind cppcheck git
```

## Versions des outils utilisées

- g++ 15.2.0
- clang++ 21.1.8
- cmake 4.2.3
- ninja 1.13.2
- gdb 17.1
- git 2.53.0

## Construire et exécuter

Version de développement (avec AddressSanitizer et UBSan) :

```
cmake --preset debug
cmake --build --preset debug
./build/debug/uin-campus
```

Version optimisée :

```
cmake --preset release
cmake --build --preset release
./build/release/uin-campus
```

Résultat attendu :

```
Le programme est interactif : il demande le nom d'un étudiant et ses notes, refuse les saisies invalides, puis affiche la moyenne, la mention et la décision.

Exemple de session :

```
UIN-Campus 0.1.0 — Calcul de la moyenne d'un étudiant

- Nom de l'étudiant : Aïssata Moussa
- Nombre de notes (1 à 30) : 3
-   Note 1 : 12,5
-   Note 2 : 25
-   La note doit être comprise entre 0 et 20.
-   Note 2 : 14
-   Note 3 : 16

----------------------------------------
- Étudiant                  Aïssata Moussa
- Nombre de notes                        3
- Moyenne                            14.17
- Mention                             Bien
- Décision                          Validé
----------------------------------------
```
```

## Structure du projet

```
uin-campus/
├── CMakeLists.txt        description de la construction
├── CMakePresets.json     configurations debug et release
├── .clang-format         règles de mise en forme du code
├── .clang-tidy           règles d'analyse du code
├── .gitignore            fichiers ignorés par Git
├── include/uincampus/    en-têtes (.hpp)
├── src/                  implémentations (.cpp)
├── app/                  programme principal (main.cpp)
└── tests/                tests unitaires (à venir)
```

## Qualité du code

Mettre en forme le code :

```
clang-format -i include/uincampus/*.hpp src/*.cpp app/*.cpp
```

Analyser le code :

```
clang-tidy -p build/debug src/*.cpp app/*.cpp
```

Le preset `debug` active les sanitizers, qui détectent à l'exécution les erreurs mémoire et les comportements indéfinis.

Remarque : clang-tidy signale un avertissement sur `main` (`bugprone-exception-escape`), parce que `std::println` peut en théorie lancer une exception. Ce point sera traité avec la gestion des erreurs.

## Feuille de route

Le projet grandit avec le cours :

- Classes `Etudiant`, `UE` et `Note`
- Gestion de la mémoire (copie et déplacement)
- Hiérarchie `Personne`, `Etudiant`, `Enseignant`
- Calcul de moyenne polymorphe
- Validation et gestion des erreurs
- Statistiques, persistance CSV/JSON, tests et intégration continue

## Auteur

Mamarou Sadou Mohamed Almoctar — Université Islamique du Niger, Faculté des Sciences et Techniques, Département Informatique. Année universitaire 2026-2027.
