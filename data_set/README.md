# The information of our test cases
We will describe Splendor's two test datasets in detail here.

# The first data set 
The purpose of the first dataset is to test the precision of Splendor to find vulnerabilities in target programs with different coding styles. We selected five test cases for testing, which are introduced in the following.

## 1. osCommerce
We chose osCommerce[3] 2.3.3.4 for testing because it is the most effective test project for RIPS[1] work (61% of the vulnerabilities discovered by RIPS come from this project). This project uses the direct query database query model which can analyze the database read and write locations by string analysis directly.

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


## 2. phpBB
phpBB[2] is a very famous CMS written by PHP.



## 3.Corebos
Corebose is a relatively large CMS project (over a million rows), and we tested this project both to demonstrate the performance of our tools on large projects and to test the ability to find anchor points.


## 4.PunBB


## 5.CatfishCMS


## Reference
[1] Dahse, Johannes and Thorsten Holz. “Static Detection of Second-Order Vulnerabilities in Web Applications.” USENIX Security Symposium (2014).<br>
[2] Eriksson, Benjamin, Giancarlo Pellegrino and Andrei Sabelfeld. “Black Widow: Blackbox Data-driven Web Scanning.” 2021 IEEE Symposium on Security and Privacy (SP) (2021): 1125-1142. <br>
[3] osCommerce https://www.oscommerce.com/ <br>
[4] phpBB https://www.phpbb.com/ <br>
[5] Corebose https://corebos.org/ <br>
[6] PunBB https://punbb.informer.com/<br>
[7] ThinkPHP https://github.com/top-think/think
