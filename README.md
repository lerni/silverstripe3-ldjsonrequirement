# SilverStripe 3 Composer installable patch to add Requirements::ldJsonScript
This allows you to add script tags with type `application/ld+json` as you need for structured data (schema.org). This patch and a custom Requirements_Backend allows you to add those to template like `<% require ldJsonScript($JobPostingSchema) %>`. An easy way to generate those is `spatie/schema-org`.

## Requirements
* SilverStripe ~3.7 (just tested with that)

## Installation
Use [composer](https://getcomposer.org/):
`composer require lerni/silverstripe3-ldjsonrequirement`