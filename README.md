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
    -c PATH       Execute the import within the given PATH (root path of a
                  magento installation)

## Examples

    # Import products
    $> import products var/import/products.csv
    # Delete products in a csv:
    $> import -b delete products var/import/products.csv
    # Execute from another directory than a magento project root
    $> import -c /path/to/magento/installation products var/import/products.csv

## Installation

    curl -sL "https://raw.githubusercontent.com/netresearch/mage-api-import-cli/master/import" -o /usr/local/bin/import
    chmod +x /usr/local/bin/import
