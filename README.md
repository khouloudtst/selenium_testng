🧪 TodoMVC Angular — QA Automation Project
📋 Description du projet
Ce projet a pour objectif de tester l'application TodoMVC Angular, une application web permettant de gérer une liste de tâches (Todo).
L'application permet notamment de :
•	Ajouter une tâche
•	Modifier une tâche
•	Marquer une tâche comme terminée
•	Réactiver une tâche terminée
•	Filtrer les tâches
•	Supprimer une tâche
•	Supprimer les tâches terminées
•	Afficher le nombre de tâches restantes
TodoMVC est un projet de référence proposant une même application implémentée avec différents frameworks JavaScript, dont Angular. (GitHub)
Application testée :
https://todomvc.com/examples/angular/dist/browser/#/all
________________________________________
🎯 Objectifs du projet QA
L'objectif est de mettre en place une stratégie de tests permettant de vérifier :
1.	Le bon fonctionnement des fonctionnalités principales.
2.	Le comportement de l'application après différentes actions utilisateur.
3.	La gestion des cas nominaux et des cas d'erreur.
4.	La non-régression des fonctionnalités existantes.
5.	L'automatisation des tests fonctionnels.
6.	L'intégration des tests dans une pipeline CI/CD.
________________________________________
🧪 Périmètre fonctionnel
1. Gestion des tâches
Ajouter une tâche
L'utilisateur doit pouvoir saisir une nouvelle tâche dans le champ :
What needs to be done?
Exemple :
Acheter du lait
Après validation, la tâche doit apparaître dans la liste.
Modifier une tâche
L'utilisateur peut double-cliquer sur une tâche existante afin de la modifier.
Exemple :
Ancienne tâche
       ↓
Double-click
       ↓
Nouvelle tâche
L'application indique d'ailleurs explicitement que l'édition se fait par double-clic. (todomvc.com)
Compléter une tâche
L'utilisateur peut sélectionner la checkbox associée à une tâche.
Résultat attendu :
☐ Acheter du lait

        ↓

☑ Acheter du lait
La tâche est alors considérée comme terminée.
Supprimer une tâche
L'utilisateur doit pouvoir supprimer une tâche existante.
________________________________________
🔎 Filtres
L'application permet de filtrer les tâches selon leur état.
All
Affiche toutes les tâches :
All
Active
Affiche uniquement les tâches non terminées :
Active
Completed
Affiche uniquement les tâches terminées :
Completed
________________________________________
🧹 Clear completed
Le bouton :
Clear completed
permet de supprimer toutes les tâches terminées.
Exemple :
Task 1  ☑
Task 2  ☑
Task 3  ☐

Clear completed

↓

Task 3  ☐
________________________________________
🧪 Stratégie de tests
Tests fonctionnels
Les principaux tests fonctionnels sont :
ID	Test	Résultat attendu
TC001	Ajouter une tâche	La tâche apparaît dans la liste
TC002	Ajouter plusieurs tâches	Toutes les tâches apparaissent
TC003	Ajouter une tâche vide	La tâche vide n'est pas ajoutée
TC004	Compléter une tâche	La tâche passe à l'état Completed
TC005	Réactiver une tâche	La tâche revient à Active
TC006	Modifier une tâche	Le nouveau texte est enregistré
TC007	Supprimer une tâche	La tâche disparaît
TC008	Filtrer Active	Seules les tâches actives apparaissent
TC009	Filtrer Completed	Seules les tâches terminées apparaissent
TC010	Filtrer All	Toutes les tâches apparaissent
TC011	Clear completed	Toutes les tâches terminées sont supprimées
TC012	Plusieurs tâches	Le compteur est correctement mis à jour
________________________________________
🧪 Tests de non-régression
Après chaque modification de l'application, les tests suivants peuvent être exécutés :
Login / accès application
        ↓
Ajouter Todo
        ↓
Modifier Todo
        ↓
Compléter Todo
        ↓
Filtrer Todo
        ↓
Supprimer Todo
        ↓
Clear completed
L'objectif est de vérifier qu'une modification n'a pas cassé une fonctionnalité existante.
________________________________________
🤖 Automatisation
Technologies utilisées
Le projet d'automatisation peut être réalisé avec :
•	Java
•	Selenium WebDriver
•	TestNG
•	Cucumber
•	Gherkin
•	Maven
•	Git
•	GitLab CI/CD ou Jenkins
•	Allure Reports
Architecture proposée :
TodoMVC QA Automation
│
├── src
│   ├── test
│   │   ├── java
│   │   │   ├── pages
│   │   │   ├── stepDefinitions
│   │   │   ├── runners
│   │   │   └── utils
│   │   │
│   │   └── resources
│   │       ├── features
│   │       └── config
│
├── pom.xml
├── testng.xml
├── README.md
└── .gitignore
________________________________________
🏗️ Design Pattern
Le projet utilise le pattern :
Page Object Model — POM
Chaque page ou composant de l'application possède une classe dédiée.
Exemple :
TodoPage.java
Cette classe contient :
•	Les locators
•	Les actions utilisateur
•	Les méthodes permettant d'interagir avec l'application
Exemple :
public class TodoPage {

    private WebDriver driver;

    public TodoPage(WebDriver driver) {
        this.driver = driver;
    }

    public void addTodo(String todo) {
        // saisir et valider une tâche
    }

    public void completeTodo(String todo) {
        // compléter une tâche
    }

    public void deleteTodo(String todo) {
        // supprimer une tâche
    }
}
________________________________________
🥒 BDD avec Cucumber
Les scénarios peuvent être écrits en langage Gherkin.
Exemple :
Feature: Todo management

  Scenario: Add a new todo
    Given User is on the TodoMVC application
    When User adds a new todo "Acheter du lait"
    Then The todo "Acheter du lait" should be displayed
________________________________________
🧪 Exemple de scénario
TC001 — Ajouter une tâche
Précondition
L'utilisateur est sur la page TodoMVC.
Étapes
1.	Ouvrir l'application.
2.	Cliquer sur le champ Todo.
3.	Saisir :
Acheter du lait
4.	Appuyer sur Enter.
Résultat attendu
La tâche :
Acheter du lait
est affichée dans la liste.
________________________________________
🔄 CI/CD
Les tests automatisés peuvent être exécutés automatiquement après chaque git push.
Exemple de pipeline
Developer
    │
    │ git push
    ↓
GitLab
    │
    ↓
GitLab Runner
    │
    ├── Checkout
    │
    ├── Build
    │
    ├── Run automated tests
    │
    ├── Generate Allure Report
    │
    └── Publish results
Une autre possibilité consiste à utiliser Jenkins avec un Jenkinsfile.
________________________________________
📊 Reporting
Les résultats des tests peuvent être générés avec :
Allure Report
Exemple :
Total tests      : 20
Passed           : 18
Failed           : 2
Skipped          : 0
Les rapports permettent notamment d'identifier :
•	Les tests réussis
•	Les tests échoués
•	Les étapes exécutées
•	Les erreurs
•	Les screenshots en cas d'échec
________________________________________
🐞 Gestion des anomalies
Lorsqu'une anomalie est détectée, elle doit être documentée avec :
Titre
Impossible de supprimer une tâche
Environnement
Browser : Chrome
OS      : Windows
Version : ...
Préconditions
Une tâche existe dans la liste.
Étapes de reproduction
1. Ouvrir TodoMVC
2. Ajouter une tâche
3. Cliquer sur Delete
Résultat attendu
La tâche est supprimée.
Résultat obtenu
La tâche reste affichée.
Evidence
Ajouter :
•	Screenshot
•	Logs
•	Vidéo si nécessaire
•	Rapport automatisé
________________________________________
📁 Structure recommandée du projet
todomvc-qa-automation/
│
├── src/
│   └── test/
│       ├── java/
│       │   ├── pages/
│       │   │   └── TodoPage.java
│       │   │
│       │   ├── stepDefinitions/
│       │   │   └── TodoStepDefinitions.java
│       │   │
│       │   ├── runners/
│       │   │   └── TestRunner.java
│       │   │
│       │   └── utils/
│       │       ├── DriverFactory.java
│       │       └── ConfigReader.java
│       │
│       └── resources/
│           ├── features/
│           │   └── todo.feature
│           │
│           └── config/
│               └── config.properties
│
├── pom.xml
├── testng.xml
├── Jenkinsfile
├── .gitlab-ci.yml
├── .gitignore
└── README.md
________________________________________
🚀 Installation
Prérequis
Installer :
•	Java JDK
•	Maven
•	Git
•	Chrome
•	IDE : IntelliJ IDEA ou Eclipse
Vérifier Java :
java -version
Vérifier Maven :
mvn -version
Vérifier Git :
git --version
________________________________________
▶️ Exécution des tests
Exécuter tous les tests :
mvn test
Exécuter les tests avec TestNG :
mvn test -DsuiteXmlFile=testng.xml
________________________________________
📈 Évolutions possibles
Le projet peut être enrichi avec :
•	Selenium Grid
•	Docker
•	Playwright
•	API testing
•	Parallel execution
•	Cross-browser testing
•	Allure Report
•	Jenkins
•	GitLab CI/CD
•	Screenshots automatiques
•	Retry des tests flaky
•	Data Driven Testing
•	Parameterized Testing
________________________________________
🎯 Compétences QA démontrées
Ce projet permet de démontrer les compétences suivantes :
Functional Testing
•	Analyse des exigences
•	Création des cas de test
•	Tests fonctionnels
•	Tests de régression
•	Tests négatifs
Automation Testing
•	Selenium WebDriver
•	Java
•	TestNG
•	Cucumber
•	Gherkin
•	Page Object Model
•	WebDriverWait
•	Assertions
DevOps / CI-CD
•	Git
•	GitLab
•	GitLab CI/CD
•	Jenkins
•	Maven
•	Allure
Méthodologie
•	Agile / Scrum
•	BDD
•	Shift Left Testing
•	Continuous Testing
________________________________________
📚 Références
•	TodoMVC : https://todomvc.com/
•	Application Angular TodoMVC : https://todomvc.com/examples/angular/dist/browser/#/all
•	Repository TodoMVC : https://github.com/tastejs/todomvc
TodoMVC fournit une spécification comportementale commune pour ses différentes implémentations, notamment autour de l'ajout, de l'édition, du changement d'état, des filtres, du routage et de la persistance. (GitHub)
________________________________________
👩‍💻 Author
QA Automation Engineer
Project : TodoMVC Angular — Web Automation Testing
Technologies :
Java | Selenium | TestNG | Cucumber | Maven
Git | GitLab CI/CD | Jenkins | Allure

