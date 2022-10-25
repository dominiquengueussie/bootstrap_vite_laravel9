COMMENT INSTALLER BOOTSTRAP DANS LARAVEL VITE
Installez une nouvelle application laravel, alors dirigez-vous vers le terminal, tapez la commande et créez une nouvelle application laravel.
COMMANDDE: composer create-project --prefer-dist laravel/laravel:^9.0 laravel9-bootstrap5-vite
Étape 2 : Installez l'interface utilisateur de Laravel pour Bootstrap 5
Ensuite, vous devez exécuter la commande ci-dessous dans votre terminal
composer require laravel/ui
Étape 3 : Configuration de l'échafaudage d'authentification avec Bootstrap 5
php artisan ui bootstrap --auth
 Étape 4 : Installer les dépendances NPM
Exécutez la commande suivante pour installer les dépendances frontend :
npm install
Étape 5 : Importez le chemin Bootstrap 5 de vite.config.js
Tout d'abord, vous devez modifier vite.config.js et ajouter le chemin bootstrap 5 et supprimer resources/css/app.css

import { defineConfig } from 'vite';
import laravel from 'laravel-vite-plugin';
import path from 'path'

export default defineConfig({
    plugins: [
        laravel([
            'resources/js/app.js',
        ]),
    ],
    resolve: {
        alias: {
            '~bootstrap': path.resolve(__dirname, 'node_modules/bootstrap'),
        }
    },
});

Étape 6 : Mettre à jour bootstrap.js
Nous devons utiliser import à la place de require.

import loadash from 'lodash'
window._ = loadash


import * as Popper from '@popperjs/core'
window.Popper = Popper

import 'bootstrap'


/**
 * We'll load the axios HTTP library which allows us to easily issue requests
 * to our Laravel back-end. This library automatically handles sending the
 * CSRF token as a header based on the value of the "XSRF" token cookie.
 */

import axios from 'axios'
window.axios = axios

window.axios.defaults.headers.common['X-Requested-With'] = 'XMLHttpRequest';

/**
 * Echo exposes an expressive API for subscribing to channels and listening
 * for events that are broadcast by Laravel. Echo and event broadcasting
 * allows your team to easily build robust real-time web applications.
 */

// import Echo from 'laravel-echo';

// window.Pusher = require('pusher-js');

// window.Echo = new Echo({
//     broadcaster: 'pusher',
//     key: process.env.MIX_PUSHER_APP_KEY,
//     cluster: process.env.MIX_PUSHER_APP_CLUSTER,
//     forceTLS: true
// });

Étape 7 : Importer Bootstrap 5 SCSS dans le dossier JS
Vous devez maintenant importer le chemin SCSS bootstrap 5 dans vos  ressources/js/app.js  ou  resources/js/bootstrap.js

ressources/js/app.js
import './bootstrap';
import '../sass/app.scss'

Étape 8 : Remplacez mix() par la directive @vite Blade
Lorsque vous utilisez Vite, vous devrez utiliser la  directive @vite  Blade au lieu de l'   assistant mix() . supprimez l'assistant de mixage et ajoutez  la directive @vite  .

<link rel="stylesheet" href="{{ mix('css/app.css') }}">
<script src="{{ mix('js/app.js') }}" defer></script>

utiliser  la  directive @vite
@vite(['resources/js/app.js'])

UN EXEMPLE DANS LE FICHIER vues/mises en page/app.blade

<!doctype html>
<html lang="{{ str_replace('_', '-', app()->getLocale()) }}">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- CSRF Token -->
    <meta name="csrf-token" content="{{ csrf_token() }}">

    <title>{{ config('app.name', 'Laravel') }}</title>

    <!-- Fonts -->
    <link rel="dns-prefetch" href="//fonts.gstatic.com">
    <link href="https://fonts.googleapis.com/css?family=Nunito" rel="stylesheet">

    @vite(['resources/js/app.js'])

</head>

Étape 9 : Exécution de la commande Vite pour créer un fichier d'actif
Vous devez  exécuter la commande build npm  pour créer l'asset bootstrap 5.

npm run build

Étape 10 : Démarrez le serveur local AVEC UN PHP ARTISAN SERVE

