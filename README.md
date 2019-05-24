# SilverStripe 3 Composer installable patch to add Requirements::ldJsonScript
This patch allows to add script tags with type `application/ld+json` to SS 3.x as you need for structured data [schema.org](https://schema.org/). In tandem with a custom you than can add any schema easily. A comfortable way to generate those json blobs is [spatie/schema-org](https://github.com/spatie/schema-org).

## How it works
It adds a patch since Requirements is a standard php class (no SS_Object)
https://gist.github.com/lerni/582f500d3d9223ada4b7e9c155189b77

Register a custom Requirements_Backend like:
https://gist.github.com/lerni/42a656c8a337754c33de0179762d1898
```
Requirements:
  backend: 'Requirements_BackendEnhancement'
```

Map what you like to expose in your Model like:
```
    use Spatie\SchemaOrg\Schema;

    public function LocalBusiness() {
        $schema = Schema::localBusiness()
            ->name($this->Title)
            ->email($this->EMail)
            ->contactPoint(
                Schema::contactPoint()
                    ->areaServed('Worldwide'));

        $schema->setProperty('@id', $this->Anchor());

        return $schema->toScript();
    }
```

An in Template include it where appropriate.
```
    <% require ldJsonScript($LocalBusiness) %>
```

## Requirements
* SilverStripe ~3.7 (just tested with that)

## Installation
Use [composer](https://getcomposer.org/):
`composer require lerni/silverstripe3-ldjsonrequirement`