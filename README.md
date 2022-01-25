# vue-weather-app

This app is created with Vue.js and uses the openweathermap.com API. In order to run this app from the source code, a developer must create an account on openweathermap.com and then create an API Key.

## Screenshots

<img width="959" alt="Screen Shot 2022-01-25 at 4 16 13 PM" src="https://user-images.githubusercontent.com/77586218/151065525-50ae5b12-8807-4b69-bdbf-7e13e86f683c.png">

## Steps to create an OpenWeatherMap API Key

    1. Go to openweathermap.com and create an account
    2. Go to API Keys and create a new key
    3. Copy and pased the key into a .env file as the variable:

    ```
    VUE_APP_MY_ENV_VARIABLE
    ```

    4. Save the .env file

## Steps to run the app via npm scripts

    1. Run the npm script serve

    2. The app will appear on localhost:3000

## Steps to run the app with Docker

    1. Open docker
    2. Go to the terminal and run command

    ```
    $docker-compose up -d --build
    ```

    3. The app will appear on localhost:3000
