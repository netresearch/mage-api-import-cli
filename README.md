# Magento API import CLI script

Provides a PHP script for interaction with the [ApiImport](https://github.com/danslo/ApiImport) module for Magento.

## Synopsis

    $> import --help
    import [OPTIONS] TYPE CSV_FILE
    
    Invokes the import of ApiImport according to TYPE for the CSV_FILE
    
    Arguments:
    TYPE      Type of the import entities - possible types are:
                categories
                products
                customers
                attribute-sets
                attributes
                attribute-associations
    CSV_FILE  Path to the CSV file containing the entities
    
    Options:
    -b BEHAVIOUR  Behaviour  - can be 'append', 'replace' or 'delete' and
                  (only for the attribute*-types) 'delete_if_not_exist'
                  Defaults to 'replace'
    -d DELIMITER  The csv delimiter (defaults to ;)
    -e ENCLOSURE  Text enclosure (defaults to "
    -s ESCAPE     Escape char (defaults to \)
    -i INDEXES    Rebuild the given (comma separated) or all indexes -
                  valid indexes are:
                    all
                    catalog_product_attribute
                    catalog_product_price
                    catalog_url
                    catalog_product_flat
                    catalog_category_flat
                    catalog_category_product
                    catalogsearch_fulltext
                    cataloginventory_stock
                    tag_summary
    -c PATH       Change dir to PATH prior to the import (root path of a
                  magento installation)

## Examples

    # Import products
    $> import products var/import/products.csv
    # Delete products in a csv:
    $> import -b delete products var/import/products.csv
    # Execute from another directory than a magento project root
    $> import -c /path/to/magento/installation products var/import/products.csv

In [example-data](example-data) you can find example CSV files that were generated out of Akeneo sample data exports. To try each of them, run the following commands:

    $> import attribute-sets example-data/attribute_sets.csv
    Imported 14 attribute-sets
    $> import attributes example-data/attributes.csv
    Imported 55 attributes
    $> import attribute-associations example-data/attribute_associations.csv
    Imported 300 attribute-associations
    $> import categories example-data/categories.csv
    Begin import of "catalog_category" with "replace" behavior
    Checked rows: 0, checked entities: 140, invalid rows: 0, total errors: 0
    Import has been done successfuly.
    $> import -i all products example-data/products.csv
    Begin import of "catalog_product" with "replace" behavior
    Checked rows: 0, checked entities: 126, invalid rows: 0, total errors: 0
    Import has been done successfuly.
    Product Attributes index was rebuilt successfully in 00:00:00
    Product Prices index was rebuilt successfully in 00:00:00
    Catalog URL Rewrites index was rebuilt successfully in 00:00:02
    Product Flat Data index was rebuilt successfully in 00:00:01
    Category Flat Data index was rebuilt successfully in 00:00:00
    Category Products index was rebuilt successfully in 00:00:00
    Catalog Search Index index was rebuilt successfully in 00:00:00
    Stock Status index was rebuilt successfully in 00:00:00
    Tag Aggregation Data index was rebuilt successfully in 00:00:00
    
## Installation

    curl -sL "https://raw.githubusercontent.com/netresearch/mage-api-import-cli/master/import" -o /usr/local/bin/import
    chmod +x /usr/local/bin/import
