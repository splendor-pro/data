# The information of our test cases
We will describe Splendor's two test datasets in detail here.

# The first data set 
The purpose of the first dataset is to test the precision of Splendor to find vulnerabilities in target programs with different coding styles. We selected five test cases for testing, which are introduced in the following.

## 1. osCommerce
We chose osCommerce 2.3.3.4 for testing because it is the most effective test project for RIPS work (61% of the vulnerabilities discovered by RIPS come from this project). This project uses the direct query database query model which can analyze the database read and write locations by string analysis directly.

- read model: 
```php
$sql_file = new upload('sql_file');
read_from = $sql_file->filename;
tep_db_query("insert into " . TABLE_CONFIGURATION ."values(null, 'Last Database Restore', 'DB_RESTORE', '" 
              .$read_from . "', 'Last database restore file', '6', '0', null, now(), '', '')");
```

- write model:
```php
$conf_query = tep_db_query("select configuration_id, configuration_title, configuration_value, use_function from " 
              . TABLE_CONFIGURATION . " where configuration_group_id = '" . (int)$gID . "'");
```

