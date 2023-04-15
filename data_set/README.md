# The information of our test cases
We will describe Splendor's two test datasets in detail here.

# 1. The first data set 
The purpose of the first dataset is to test the precision of Splendor to find vulnerabilities in target programs with different coding styles. We selected five test cases for testing, which are introduced in the following.

## 1.1. osCommerce
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


## 1.2. phpBB
phpBB[4] is a very famous CMS written by PHP. We tested it because the Black Widow[2] performed well on phpBB 2.0.23.

- read mode 
```php
$sql = "SELECT * FROM " . FORUMS_TABLE . " WHERE forum_id IN ($from_id, $to_id)";
$result = $db->sql_query($sql);
```

- write model
```php
$sql = "INSERT INTO " . CATEGORIES_TABLE . " (cat_title, cat_order) VALUES ('" . str_replace("\'", "''", $HTTP_POST_VARS['categoryname']) . "',  $next_order)";
        $result = $db->sql_query($sql);
```



## 1.3.Corebos
Corebose is a relatively large CMS project (over a million rows), and we tested this project both to demonstrate the performance of our tools on large projects and to test the ability to find anchor points.

- read model 
```php
$sql2 = 'select * from vtiger_def_org_share where editstatus=0';
$result2 = $adb->pquery($sql2, array());
```

- write model
```php
$sql7='update vtiger_def_org_share set permission=? where tabid=? and ruleid=?';
$adb->pquery($sql7, array($permission, $tabid, $ruleid));
```


## 1.4. PunBB
PunBB [6] is a typical project that uses the Non-chain Query Model mentioned in our paper. We use this project as a representative demonstration of Splendor's ability to discover read and write locations in this type of database query model.

- read model
```php
$query = array(
  'SELECT' => 'sc.search_data',
  'FROM' => 'search_cache AS sc',
  'WHERE' => 'sc.id='.$search_id.' AND
  sc.ident=\''.$forum_db->escape($ident).'\''
  );
$result = $forum_db->query_build($query) or error(__FILE__, __LINE__);
```

- write model
```php
$query = array(
  'INSERT' => 'poster, poster_id, poster_ip, message,
hide_smilies, posted, topic_id',
  'INTO' => 'punbb_posts',
  'VALUES' => $forum_db->escape($post_info['poster']),
  $post_info['poster_id'],
  $forum_db->escape(get_remote_address()),
  $forum_db->escape($post_info['message']),
  $post_info['hide_smilies'],
  $post_info['posted'],
  $post_info['topic_id']
  );
$forum_db->query_build($query) or error(__FILE__, __LINE__);
```

## 1.5. CatfishCMS
Catfish is a CMS system developed using ThinkPHP[7], a well-known PHP development framework. The framework is typical of using the Chain Query Model as a database query model.

- read model 
```php
$data = ['uid' => Session::get($this->session_prefix.'user_id'),
         'pid' => Request::instance()->post('pid'),
         'jname' => Request::instance()->post('name'),
         'jvalue' => Request::instance()->post('jval'),
         'times' => $time];
Db::name('terminal')->insert($data);
```
- write model
```php
$fields = '*';
$data = Db::name('terminal')->field($fields)->select();
```

## Reference
[1] Dahse, Johannes and Thorsten Holz. “Static Detection of Second-Order Vulnerabilities in Web Applications.” USENIX Security Symposium (2014).<br>
[2] Eriksson, Benjamin, Giancarlo Pellegrino and Andrei Sabelfeld. “Black Widow: Blackbox Data-driven Web Scanning.” 2021 IEEE Symposium on Security and Privacy (SP) (2021): 1125-1142. <br>
[3] osCommerce https://www.oscommerce.com/ <br>
[4] phpBB https://www.phpbb.com/ <br>
[5] Corebose https://corebos.org/ <br>
[6] PunBB https://punbb.informer.com/<br>
[7] ThinkPHP https://github.com/top-think/think
