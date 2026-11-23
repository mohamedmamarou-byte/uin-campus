# UIN-Campus

Système de gestion académique de l'Université Islamique du Niger (UIN). Projet fil rouge du cours de Programmation Orientée Objet en C++ moderne.

La version actuelle (0.1.0) est un programme interactif qui établit le **relevé d'un étudiant** : saisie contrôlée des notes et des coefficients, moyennes simple et pondérée, statistiques (minimum, maximum, écart-type), nombre d'UE validées et mention.

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
./build/debug/app/uin-campus
```

Version optimisée :

```
cmake --preset release
cmake --build --preset release
./build/release/app/uin-campus
```

Options de la ligne de commande :

```
./build/debug/app/uin-campus --aide
./build/debug/app/uin-campus --version
```

Installation locale de la version optimisée :

```
cmake --install build/release --prefix ~/.local
~/.local/bin/uin-campus --version
```

## Résultat attendu

Le programme est interactif : il demande le nom de l'étudiant, le nombre d'UE, puis la note et le coefficient de chaque UE, et affiche le relevé.

Exemple de session (le coefficient 18 est refusé, car il doit être compris entre 1 et 10) :

```
UIN-Campus 0.1.0 — Relevé d'un étudiant

Nom de l'étudiant : Mohamed
Nombre d'UE (1 à 30) : 2
 Note de l'UE 1 : 17
 Coefficient de l'UE 1 : 18
 La valeur doit être comprise entre 1 et 10.
 Coefficient de l'UE 1 : 2
 Note de l'UE 2 : 16
 Coefficient de l'UE 2 : 2

--------------------------------------------
Étudiant                             Mohamed
Moyenne pondérée                       16.50
Moyenne simple                         16.50
Note min / max                 16.00 / 17.00
Écart-type                              0.50
UE validées                            2 / 2
Mention                            Très bien
--------------------------------------------
```

La commande `--version` affiche les informations de construction (le compilateur et la configuration dépendent de ta machine) :

```
UINCampus 0.1.0 — GCC 15.2.0 — C++ (202302) — Debug
```

## Structure du projet

```
uin-campus/
├── CMakeLists.txt        description de la construction (racine)
├── CMakePresets.json     configurations debug et release
├── .clang-format         règles de mise en forme du code
├── .clang-tidy           règles d'analyse du code
├── .gitignore            fichiers ignorés par Git
├── include/uincampus/    en-têtes (.hpp), dont uincampus.hpp (en-tête parapluie)
├── src/                  implémentations (.cpp), CMakeLists.txt et config.hpp.in
├── app/                  programme principal (main.cpp) et son CMakeLists.txt
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
