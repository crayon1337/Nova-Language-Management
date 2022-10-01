# Laravel Nova Langauge Management

A tool for Laravel Nova to implement dynamic languages. The whole idea of this package is to rewrite the configuration files of several localization packages based on your inputs.

NOTE: This package does not support Nova 4 right now. We are working on making it available soon enough.

## Installation

Use the package manager [composer](https://pip.pypa.io/en/stable/) to install this tool.

```bash
composer require crayon/nova-language-management
```

## Usage
Import the NovaLanguageEditor class at the top of your NovaServiceProvider like below:
```php
use Crayon\NovaLanguageEditor\NovaLanguageEditor;
```

Open up NovaServiceProvider and register the tool in the tools method

```php
/**
 * Get the tools that should be listed in the Nova sidebar.
 *
 * @return array
 */
public function tools()
{
    NovaLanguageEditor::make();
}
```
### Permissions
```php
    NovaLanguageEditor::make()->canSee(fn($request) => $request->user()->isSuperAdmin()),
```

## Clarification

This tool is  uses \
[Nova Translatable](https://github.com/optimistdigital/nova-translatable)\
[Macamara Laravel Localization](https://github.com/mcamara/laravel-localization)\
[Nova Translation Editor](https://github.com/bernhardh/nova-translation-editor)

If you do not have them installed it will install them for you. Also, make sure to publish the configuration files:

```bash
php artisan vendor:publish --provider="Mcamara\LaravelLocalization\LaravelLocalizationServiceProvider"
php artisan vendor:publish --tag="nova-translatable-config"
php artisan vendor:publish --provider="Bernhardh\NovaTranslationEditor\ToolServiceProvider"
```

### Migration
Publish language_lines (Nova Translation Editor) migration
```bash
php artisan vendor:publish --provider="Spatie\TranslationLoader\TranslationServiceProvider" --tag="migrations"
```

```bash
php artisan migrate
```

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## Screenshots
![Nova language management](https://i.imgur.com/BXESFKc.png)

## License
[MIT](https://choosealicense.com/licenses/mit/)
