# Laravel-Vue SPA + Tailwind CSS

> Forked from [cretueusebiu/laravel-vue-spa](https://github.com/cretueusebiu/laravel-vue-spa)

The main difference between this repository and the original is that this one uses Tailwind CSS instead of Bootstrap.

![Image of Laravel-Vue SPA + Tailwind CSS](https://repository-images.githubusercontent.com/193556327/a1d35f80-9746-11e9-884b-6b1fa8318cfb)

## Features

- [Laravel 5.8](https://laravel.com/docs/5.8) 
- Vue + VueRouter + Vuex + VueI18n + ESlint
- Pages with dynamic import and custom layouts
- Login, register, email verification and password reset
- Authentication with JWT
- Socialite integration
- [Tailwind CSS](https://tailwindcss.com/) + Font Awesome 5

## Installation

- `composer create-project --prefer-dist shriker/laravel-vue-spa-tailwind`
- Edit `.env` and set your database connection details
- (When installed via git clone or download, run `php artisan key:generate` and `php artisan jwt:secret`)
- `php artisan migrate`
- `npm install`

## Usage

#### Development

```bash
# build and watch
npm run watch

# serve with hot reloading
npm run hot
```

#### Production

```bash
npm run production
```

## Email Verification

To enable email verification make sure that your `App\User` model implements the `Illuminate\Contracts\Auth\MustVerifyEmail` contract.

## Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.
