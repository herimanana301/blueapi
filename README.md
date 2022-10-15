API Version 1.1

Cette documentation explique comment enregistrer, configurer et développer votre application afin que vous puissiez utiliser nos API avec succès.


1. Créer une application

Pour que votre application puisse accéder à nos API, vous devez enregistrer votre application à l'aide du Dashboard de l'application. L'inscription crée un ID d'application qui nous permet de savoir qui vous êtes, nous aide à distinguer votre application des autres applications..

   Vous devrez créer une nouvelle application 

   Une fois que vous avez créé votre application, vous obtiendrez votre app_id et app_secret

2. Log in With

Se connecter avec le système est un moyen rapide et pratique pour les utilisateurs de créer des comptes et de se connecter à votre application. Notre système de connexion permet deux scénarios, l'authentification et la demande d'autorisations pour accéder aux données des utilisateurs. Vous pouvez utiliser le système Connexion simplement pour l'authentification ou pour l'authentification et l'accès aux données.

   1. Pour démarrer le processus de connexion OAuth, vous devez utiliser un lien pour votre application comme celui-ci:
```
    <a href="https://bluepix.fr/api/oauth?app_id=YOUR_APP_ID">Log in With BluePix</a>
```

   
   L'utilisateur sera redirigé vers la page Se connecter avec comme celle-ci
    
   ![alt text](https://bluepix.fr/content/themes/bluepix3.6/images/screenshots/login_with.png)
    
    
   2. Une fois que l'utilisateur a accepté votre application, l'utilisateur sera redirigé vers l'URL de redirection de votre application avec auth_key comme ça:
    
```
    https://mydomain.com/my_redirect_url.php?auth_key=AUTH_KEY
```

   Ce auth_key valable uniquement pour une utilisation unique, donc une fois que vous l'avez utilisé, vous ne pourrez plus l'utiliser et générer un nouveau code, vous devrez rediriger l'utilisateur vers la connexion avec le lien à nouveau.

3. Access Token

Une fois que vous avez obtenu l'approbation de l'utilisateur de votre application Connectez-vous avec la fenêtre et que vous êtes revenu avec le auth_key ce qui signifie que vous êtes maintenant prêt à récupérer les données de nos API et pour démarrer ce processus, vous devrez autoriser votre application et obtenir le access_token et vous pouvez suivre nos étapes pour savoir comment l'obtenir.

   1. Pour obtenir un jeton d'accès, envoyez une requête HTTP GET au point de terminaison suivant comme celui-ci:
```
    <?php
    $app_id = "YOUR_APP_ID"; // your app id
    $app_secret = "YOUR_APP_SECRET"; // your app secret
    $auth_key = $_GET['auth_key']; // the returned auth key from previous step

    $get = file_get_contents("https://bluepix.fr/api/authorize?app_id=$app_id&app_secret=$app_secret&auth_key=$auth_key");

    $json = json_decode($get, true);
    if(!empty($json['access_token'])) {
        $access_token = $json['access_token']; // your access token
    }
    ?>
```
   Ce access_token valide uniquement pour une 1 heure , donc une fois qu'il est devenu invalide, vous devrez en générer un nouveau en redirigeant l'utilisateur vers la connexion avec le lien à nouveau.

4. APIs

Une fois que vous obtenez votre access_token Vous pouvez maintenant récupérer des informations de notre système via des requêtes HTTP GET qui prennent en charge les paramètres suivants

Endpoint 	                     Description
api/get_user_info 	           get user info



Vous pouvez récupérer les informations utilisateur comme celle-ci
```
if(!empty($json['access_token'])) {
   $access_token = $json['access_token']; // your access token
   $get = file_get_contents("https://bluepix.fr/api/get_user_info?access_token=$access_token");
}
```
Le résultat sera:
```
{
    "user_info": {
        "user_id": "",
        "user_name": "",
        "user_email": "",
        "user_firstname": "",
        "user_lastname": "",
        "user_gender": "",
        "user_birthdate": "",
        "user_picture": "",
        "user_cover": "",
        "user_registered": "",
        "user_verified": "",
        "user_biography": "",
        "user_website": ""
    }
}
```
