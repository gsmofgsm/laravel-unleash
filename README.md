# Laravel Unleash

[![Codacy Badge](https://api.codacy.com/project/badge/Grade/56b0c6402eca49169cbeb3f404c2bff9)](https://app.codacy.com/manual/mikefrancis/laravel-unleash?utm_source=github.com&utm_medium=referral&utm_content=mikefrancis/laravel-unleash&utm_campaign=Badge_Grade_Dashboard)
[![Packagist](https://img.shields.io/packagist/v/mikefrancis/laravel-unleash)](https://packagist.org/packages/mikefrancis/laravel-unleash) [![Build Status](https://github.com/mikefrancis/laravel-unleash/workflows/CI/badge.svg)](https://github.com/mikefrancis/laravel-unleash/actions?query=workflow%3ACI) [![codecov](https://codecov.io/gh/mikefrancis/laravel-unleash/branch/master/graph/badge.svg)](https://codecov.io/gh/mikefrancis/laravel-unleash)

An [Unleash](https://unleash.github.io) client for Laravel.

## Installation

```bash
composer require mikefrancis/laravel-unleash
```

Export package config:

```bash
php artisan vendor:publish --provider="MikeFrancis\LaravelUnleash\ServiceProvider"
```

## Configuration

Documentation for configuration can be found in [config/unleash.php](https://github.com/mikefrancis/laravel-unleash/blob/master/config/unleash.php).

## Usage

```php
use \MikeFrancis\LaravelUnleash\Unleash;

$unleash = app(Unleash::class);

if ($unleash->isFeatureEnabled('myAwesomeFeature')) {
  // Congratulations, you can see this awesome feature!
}

if ($unleash->isFeatureDisabled('myAwesomeFeature')) {
  // Check back later for more features!
}

$feature = $unleash->getFeature('myAwesomeFeature');

$allFeatures = $unleash->getFeatures();

$availableFeatures = $unleash->getAvailableFeaturesCollection(); // collection of feature name enabled true/false pair
```

### Facades

You can use the `Unleash` facade:

```php
use Unleash;

if (Unleash::isFeatureEnabled('myAwesomeFeature')) {
  // Congratulations, you can see this awesome feature!
}

if (Unleash::isFeatureDisabled('myAwesomeFeature')) {
  // Check back later for more features!
}

$feature = Unleash::getFeature('myAwesomeFeature');

$allFeatures = Unleash::getFeatures();
```

or use the generically named `Feature` facade:

```php
use Feature;

if (Feature::enabled('myAwesomeFeature')) {
  // Congratulations, you can see this awesome feature!
}

if (Feature::disabled('myAwesomeFeature')) {
  // Check back later for more features!
}

$feature = Feature::get('myAwesomeFeature');

$allFeatures = Feature::all();
```

### Dynamic Arguments

If your strategy relies on dynamic data at runtime, you can pass additional arguments to the feature check functions:

```php
use \MikeFrancis\LaravelUnleash\Unleash;
use Config;

$unleash = app(Unleash::class);

$allowList = config('app.allow_list');

if ($unleash->isFeatureEnabled('myAwesomeFeature', $allowList)) {
  // Congratulations, you can see this awesome feature!
}

if ($unleash->isFeatureDisabled('myAwesomeFeature', $allowList)) {
  // Check back later for more features!
}
```

### Blade

Blade directive for checking if a feature is **enabled**:

```php
@featureEnabled('myAwesomeFeature')
Congratulations, you can see this awesome feature!
@endfeatureEnabled
```

Or if a feature is **disabled**:

```php
@featureDisabled('myAwesomeFeature')
Check back later for more features!
@endfeatureDisabled
```

You cannot currently use dynamic strategy arguments with Blade template directives.