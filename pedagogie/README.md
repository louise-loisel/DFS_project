# Tests fonctionnels avec Selenium

## Un peu de théorie
### Définitions

> Un test fonctionnel est le test qui servira à tester automatiquement toutes les fonctionnalités d’une application. Par exemple, vous pourrez avoir à tester qu'un membre peut bien s'inscrire, se connecter, se déconnecter…
Généralement, un test fonctionnel est associé à une User Story et teste son bon déroulement avant l'étape de vérification manuelle.

> Selenium est une suite d’outils permettant de faire des tests fonctionnels d’une application web (et uniquement web) de façon automatique. 

> Il permet donc d'écrire, de manière plus ou moins assistée, des scripts dont l'exécution réalisera automatiquement des actions dans un navigateur web : visiter une page, cliquer sur un lien, remplir un formulaire, etc. et de récupérer les résultats de ces actions.

### Intérêts de ces tests
> Assurer sereinement les évolutions de l'application : Les tests fonctionnels permettent de s’assurer, de façon automatique, que les modifications/évolutions effectuées n’impactent pas les autres fonctionnalités du site.

> Découverte d’une application inconnue : Les tests fonctionnels  représentent une documentation précise du projet qui permet à quiconque arrivant en cours de route sur celui ci de comprendre rapidement de quoi il s’agit. 

Rapidité : Les tests automatiques sont beaucoup plus rapides que les tests manuels

Adaptable : Ils permettent de s’adapter aux langages de code mais aussi au niveau des tests : à beaucoup de navigateurs et systèmes d’exploitation

Reproductible : Ils sont reproductibles à tous moments

Analysable : analyse des résultats de tests facile et sans erreur humaine


### Quand doit on écrire ces tests ?

Les tests fonctionnels peuvent s’implémenter à différents moments du projet :
avant d'implémenter une nouvelle fonctionnalité (TDD)
juste après avoir implémenté une nouvelle fonctionnalité
au moment où l’on découvre une anomalie
Une bonne manière de commencer est de vous assurer que toutes les pages de votre site web ne retournent pas de code status 500 !


### Comment faire nos tests?
Voici la liste des étapes qu'il faut respecter a minima pour effectuer un test fonctionnel :

Créer un client HTTP.

Effectuer une requête HTTP sur la page que nous devons tester.

S'assurer que les éléments sur la page testée sont bien présents (écrire des assertions).

Dans tous les cas, les assertions qu'il faudra écrire seront toujours liées aux besoins exprimés avant le développement.

Note : Vous n'avez pas besoin de connaître le code de l'application en détail pour tester fonctionnellement une application. C'est donc un test dit "boîte noire". A contrario, Les tests unitaires, eux, sont dits "boîtes blanches" car vous avez besoin de lire le code de l'application pour les effectuer. 

### Les outils
Avant de se plonger plus précisément dans certaines des méthodes de test fonctionnel, voici les différents familles et éléments à comprendre :

L’enregistreur de test : Il permet d’enregistrer les actions faites dans l’application sous forme de scénarios. On peut faire des ajouts de commandes pour rendre le test plus complet.
Les players de test permettent de jouer les tests. On peut trouver des players locaux (qui s’executent sur la machine de l’utilisateur), ou des players serveurst, tournant sur des machines liées au projet ou non (et qui ne bloquent pas l’utilisateur.
Les frameworks sont des outils d’écriture de tests. La plupart des langages sont couverts par un ou des frameworks de tests.Les drivers permettent le lien entre les navigateurs et les players.Sur les players locaux, ils sont généralement intégrés, mais dans le cadre de Selenium webdriver (le serveur de tests le plus répandu) ils sont à installer indépendamment.

### Zoom sur Selenium



Selenium met à disposition 4 outils principaux :

##### Selenium IDE
Selenium IDE est une extension de Mozilla Firefox et Chrome qui va permettre d’enregistrer, éditer et débugger des tests en un clic pour une suite d’actions que l’on va effectuer sur le navigateur.

Une fois la capture terminée, Selenium IDE nous permet de générer cette capture sous forme de script. Différents langages sont proposés tels que : Python, JAVA, C#...

##### Selenium WebDriver (ou Selenium 3)
Selenium WebDriver est une API, disponible dans plusieurs langages (Java, C#, Python, Ruby) et qui va utiliser le fichier fourni par Sélénium IDE. Il permet de reproduire un navigateur souhaité (Chrome/Firefox...) avec une version bien précise.  

##### Selenium Grid
Selenium Grid est un serveur qui permet d’effectuer des tests en parallèle sur des navigateurs différents, et éventuellement sur des machines différentes et environnements différents.

##### Selenium Client API

Permet d’écrire des tests en Java, C#, Ruby, JavaScript, R et Python. Les tests vont communiquer avec Selenium grâce à des méthodes de Selenium Client API.


## Cas pratique : Testons l’interface utilisateur (UI)

### Tester de façon simple avec Selenium IDE
#### Exemple simple en langage Ruby
On veut tester l’application très simple “cooking_battle”. Pour se faire nous allons utiliser Selenium IDE. Vous devez donc installer l’extension sur Chrome ou Firefox. Une fois un test lancé vous allez jouer le rôle de l’utilisateur. Selenium va enregistrer vos actions et les traduire en test. Tout d’abord, hébergeons localement la cooking battle :
Téléchargez le dossier cooking_battle du dossier source. Celui ci est codé en Ruby et utilise le framework Ruby on rails. Nous allons donc devoir les installer dans un premier temps.

Vérifier que vous avez bien Ruby sur le terminal :
ruby -v
Si non, allez télécharger Ruby.
Une fois cela fait, installez rails via la commande :
‘gem install rails‘
Puis placez vous dans votre dossier cooking_battle et lancez l’application web via la commande :
‘rails server’

> Si le message suivant s’affiche
>‘Your Ruby version is X.X.X, but your Gemfile specified Y.Y.Y’ 
> Ouvrez Gemfiles avec un éditeur de texte, et remplacer sur la ligne concernant Ruby : Y.Y.Y par X.X.X
> Pour que cette modification soit prise en compte, il faut lancer la commande suivante:
> ‘Bundle install’
> Vous pouvez enfin lancer votre serveur !
> ‘rails server’


L’application est maintenant disponible sur l’adresse :
http://localhost:3000/

Lancez l’extension Selenium IDE en créant un projet et un test sur l’adresse http://localhost:3000/
Interagissez avec les pages puis stoppez la capture. Vous allez voir dans votre fenêtre Selenium IDE la traduction de vos actions en test. Vous pouvez ouvrir le log pour voir le succès ou non du test. Vous pouvez également modifier la target d’un test/ajouter un test/ supprimez un test.

#### Exemple plus complet en exportation Java

L’avantage avec la suite Selenium, c’est que l’on peut adapter à beaucoup de langages. Nous avons vu avec Ruby, nous alors maintenant voir avec une exportation de test en java. Le principe initial est le même.

Cette fois-ci, on ne sera pas en localhost mais sur un site hébergé. Le code est cependant disponible dans sources/consomarseille. Il s’agit d’un site vitrine avec quelques liens internes et externes.

Lancez l’extension Selenium IDE en créant un projet et un test sur l’adresse : 
http://agastache.ovh1.ec-m.fr/dfs/
Interagissez avec les pages puis stoppez la capture de la même manière que dans la première partie.

Une fois la capture réalisée, vous pouvez exporter votre simulation dans le langage désiré : dans notre nous l’exporterons en java.

Vous devriez obtenir cela :

import ...
public class AccueilproduitlocauxaccueilTest {
  private WebDriver driver;
  private Map<String, Object> vars;
  JavascriptExecutor js;
  @Before
  public void setUp() {
    driver = new FirefoxDriver();
    js = (JavascriptExecutor) driver;
    vars = new HashMap<String, Object>();
  }
  @After
  public void tearDown() {
    driver.quit();
  }
  @Test
  public void accueilproduitlocauxaccueil() {
    // Test name: accueil_produitlocaux_accueil
    driver.get("http://agastache.ovh1.ec-m.fr/dfs/index.html");
    driver.manage().window().setSize(new Dimension(1108, 714));
    driver.findElement(By.linkText("PRODUITS LOCAUX")).click();
    driver.findElement(By.linkText("Paniers Bio")).click();
    js.executeScript("window.scrollTo(0,672)");
    driver.findElement(By.linkText("ACCUEIL")).click();
  }



Remarques:
En regardant ce code, la première chose que nous voyons, c'est que tout passe par l'utilisation de la classe org.openqa.selenium.WebDriver. Il s'agit de l'interface qui nous permet de manipuler la page Web.

Pratiquement tout notre test consiste à trouver un élément de la page, avec la méthode findElement(), et appeler une méthode sur cet élément pour simuler une action de l'utilisateur. Les éléments sont sélectionnés par leur id, mais d'autres modes sont possibles : par classe CSS ou par balise notamment.

D’autres méthodes existent pour modéliser le comportement utilisateur sur le navigateur, notamment en utilisant la classe selenium de l’API.

Pour le moment nous avons seulement mimé l’interaction de l’utilisateur sur l’interface web. Si on run ce test, tout devrait passer. 

Nous allons maintenant ajouter les vérifications que nous voulons effectuer dans nos tests.

Attente du chargement de page
Avant de tester une page, nous devons nous assurer que le serveur a fini de l'envoyer. Selenium offre plusieurs moyens d'attendre que la page soit disponible. 

Le premier est d'attendre le chargement de la page complète :

‘selenium.waitForPageToLoad("30000");  //utilisation de la classe’
‘com.thoughtworks.selenium.Selenium’

Le second d’attendre au plus 30 sec :

‘driver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);//utilisation de la classe du webDriver’


Vérification du contenu 

Vous pouvez maintenant réaliser vos propres tests, en créant des méthodes en utilisant celles importées avec selenium IDE. 
Par exemple, créons une méthode pour vérifier le contenu d’un élément :

 'private void checkElement(String elementId, String expected) {
        assertThat(driver.findElement(By.id(elementId)).getText(), is(expected));
    }'

Ou encore, nous pouvons par exemple tester que le titre de la page d’accueil soit bien “ConsoMarseille”

' public void test_titre_accueil () {
    driver.get("http://agastache.ovh1.ec-m.fr/dfs/index.html");
    driver.manage().window().setSize(new Dimension(1108, 714));
    WebElement titre = driver.findElement(By.id("titre"));
    assert (titre.getText(), is("ConsoMarseille"));
  }'

C’est à vous de définir ce qui est important de tester sur chacune de vos pages.

Vous pouvez vous amusez en téléchargeant les fichiers présents dans le code source, ou si vous voulez aller plus loin voici quelques références : 

https://atatorus.developpez.com/tutoriels/java/test-application-web-avec-selenium/
selenium ruby tuto browserstack
https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Cross_browser_testing/Your_own_automation_environment
