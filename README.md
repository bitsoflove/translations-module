# pyro_translations-module
Generic streams translations module for PyroCMS 3.1 and up
(using [react-handsontable](https://github.com/handsontable/react-handsontable))

## Installation

- `composer require bitsoflove/pyro_translations-module`
- `php artisan module:install translations`

## Configuration

First, you'll have to publish the config file:
- `php artisan addon:publish bitsoflove.module.translations`

By default, after installing this module, every admin will be able to translate all streams.
To allow only a subset of that list, update the published config file accordingly:

```
<?php return [

    'middleware' => [
        // list any middlewares you want to use here
        // you can use middleware to manipulate this config on the fly

        //TranslationsModuleMiddleware::class,
    ],

    'streams' => [

        /**
         * Possible values:
         *
         * 'all' or an array of EntryModel classes
         */
        'models' => [
            [
                'model' => YourModel::class,
                'fields' => ['title'], // just allow translation of the title field
                'default' => true,
            ],
            [
                'model' => YourSecondModel::class,
                'fields' => [], // all fields
                'default' => false,
            ],
        ],

        'locales' => [
            'default' => config('streams::locales.default'),

            'supported' => array_keys(
                config('streams::locales.supported')
            ),
        ],
    ]
];
```
## Developing
1. Instead of using 'composer require', manually add the following entry to the composer 'require' list: `"bitsoflove/translations-module": "dev-master"`
2. Add this repository to the composer repositories list (to ensure you'll fetch the repo)
```
    "repositories": [
        {
            "url": "https://github.com/bitsoflove/pyro_translations-module.git",
            "type": "git"
        }
    ],
```
3. `composer install`

Then:
- `php artisan module:install translations`
- `cd core/bitsoflove/translations-module`
- `cp .env.example.js .env.js`
- Change the [proxy](https://github.com/bitsoflove/pyro_translations-module/blob/master/.env.example.js#L4) property in `.env.js` to the host of your local pyro application
- `npm install`
- `npm run dev`
```
