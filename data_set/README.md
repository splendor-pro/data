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
Corebose is a relatively large CMS project (over a million lines of PHP code), and we tested this project both to demonstrate the performance of our tools on large projects and to test the ability to find anchor points.

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

# 2. The first data set
The purpose of the second dataset is to evaluate the ability of our work to construct database schema and discover vulnerabilities in an automated way in a large number of projects. We have constructed the database schema and scanned 1202 projects in over 4k PHP projects, which contain a total of 609,639 files and 68,672,580 lines of PHP code. The specific list is as follows.

| **id** | **name**                                                            | **files** | **lineno** |
|--------|---------------------------------------------------------------------|-----------|------------|
| 1      | sftnow-master                                                       | 692       | 63281      |
| 2      | CuteOneP-master                                                     | 78        | 2592       |
| 3      | c3crm-master                                                        | 1093      | 279557     |
| 4      | CacoCloud-master                                                    | 58        | 3202       |
| 5      | webERP-master                                                       | 870       | 272988     |
| 6      | kateglo-master                                                      | 185       | 31380      |
| 7      | with-related-behavior-master                                        | 10        | 684        |
| 8      | yoyow-wecenter-master                                               | 1009      | 138494     |
| 9      | 20190511_awd_docker-master                                          | 338       | 38644      |
| 10     | racktables-contribs-master                                          | 57        | 16863      |
| 11     | webird-master                                                       | 99        | 5558       |
| 12     | framework-master                                                    | 163       | 11700      |
| 13     | SemanticScuttle-master                                              | 210       | 20276      |
| 14     | openeclass-master                                                   | 1058      | 213333     |
| 15     | yii2-cookbook-3-ru-master                                           | 450       | 14249      |
| 16     | Seo-Panel-master                                                    | 1820      | 243128     |
| 17     | TieBaRobot-master                                                   | 16        | 925        |
| 18     | Startblog-master                                                    | 270       | 34869      |
| 19     | PHPFusion-Andromeda                                                 | 950       | 119613     |
| 20     | SlimJim-master                                                      | 40        | 3824       |
| 21     | xcxcms-master                                                       | 973       | 151361     |
| 22     | naofo.de-master                                                     | 5         | 862        |
| 23     | zf-oauth2-master                                                    | 23        | 1183       |
| 24     | dokku-alt-manager-master                                            | 33        | 1145       |
| 25     | HackMe-File-Upload-Challenges-master                                | 92        | 11103      |
| 26     | phpgrid-custom-crm-master                                           | 12        | 383        |
| 27     | country-nationality-list-master                                     | 3         | 2248       |
| 28     | Studen-Graduation-Project-master                                    | 128       | 18238      |
| 29     | Quill-main                                                          | 48        | 4498       |
| 30     | vendo-master                                                        | 6         | 145        |
| 31     | tbmsg-master                                                        | 24        | 1170       |
| 32     | dendrogram-master                                                   | 20        | 1245       |
| 33     | review-master                                                       | 38        | 2843       |
| 34     | api-master                                                          | 5329      | 415561     |
| 35     | useradmin-master                                                    | 62        | 3943       |
| 36     | RaspberryPints-master                                               | 57        | 4109       |
| 37     | Volumio-WebUI-master                                                | 321       | 18601      |
| 38     | openid-component-master                                             | 51        | 12574      |
| 39     | wheatbin-master                                                     | 659       | 59828      |
| 40     | link-preview-master                                                 | 41        | 1578       |
| 41     | education-online-master                                             | 10535     | 476151     |
| 42     | Projectfork-master                                                  | 725       | 67334      |
| 43     | archwiki-master                                                     | 6912      | 1024942    |
| 44     | pdo-event-store-master                                              | 51        | 6381       |
| 45     | altocms-master                                                      | 716       | 109672     |
| 46     | extension_builder-master                                            | 111       | 11539      |
| 47     | CommentPush-master                                                  | 14        | 4355       |
| 48     | Online-Banking-system-master                                        | 56        | 2891       |
| 49     | openSIS-Classic-master                                              | 903       | 366294     |
| 50     | flusio-main                                                         | 442       | 38320      |
| 51     | Zebra_Pagination-master                                             | 4         | 516        |
| 52     | friendica-addons-develop                                            | 1831      | 101501     |
| 53     | opengovplatform-beta-master                                         | 1168      | 372018     |
| 54     | PHP-MVC-Blog-System-master                                          | 23        | 457        |
| 55     | sftnow-master                                                       | 692       | 63281      |
| 56     | webERP-master                                                       | 870       | 272988     |
| 57     | kateglo-master                                                      | 185       | 31380      |
| 58     | with-related-behavior-master                                        | 10        | 684        |
| 59     | yoyow-wecenter-master                                               | 1009      | 138494     |
| 60     | 20190511_awd_docker-master                                          | 338       | 38644      |
| 61     | racktables-contribs-master                                          | 57        | 16863      |
| 62     | webird-master                                                       | 99        | 5558       |
| 63     | SemanticScuttle-master                                              | 210       | 20276      |
| 64     | openeclass-master                                                   | 1058      | 213333     |
| 65     | yii2-cookbook-3-ru-master                                           | 248       | 7623       |
| 66     | Seo-Panel-master                                                    | 1820      | 243128     |
| 67     | TieBaRobot-master                                                   | 16        | 925        |
| 68     | Startblog-master                                                    | 270       | 34869      |
| 69     | PHPFusion-Andromeda                                                 | 950       | 119613     |
| 70     | SlimJim-master                                                      | 40        | 3824       |
| 71     | xcxcms-master                                                       | 972       | 151358     |
| 72     | naofo.de-master                                                     | 5         | 862        |
| 73     | zf-oauth2-master                                                    | 23        | 1183       |
| 74     | dokku-alt-manager-master                                            | 33        | 1145       |
| 75     | HackMe-File-Upload-Challenges-master                                | 92        | 11103      |
| 76     | phpgrid-custom-crm-master                                           | 12        | 383        |
| 77     | Studen-Graduation-Project-master                                    | 128       | 18238      |
| 78     | Quill-main                                                          | 48        | 4498       |
| 79     | vendo-master                                                        | 6         | 145        |
| 80     | tbmsg-master                                                        | 24        | 1170       |
| 81     | dendrogram-master                                                   | 20        | 1245       |
| 82     | review-master                                                       | 38        | 2843       |
| 83     | useradmin-master                                                    | 62        | 3943       |
| 84     | RaspberryPints-master                                               | 57        | 4109       |
| 85     | Volumio-WebUI-master                                                | 321       | 18601      |
| 86     | openid-component-master                                             | 51        | 12574      |
| 87     | wheatbin-master                                                     | 659       | 59828      |
| 88     | education-online-master                                             | 10456     | 460026     |
| 89     | Projectfork-master                                                  | 725       | 67334      |
| 90     | pdo-event-store-master                                              | 51        | 6381       |
| 91     | extension_builder-master                                            | 111       | 11539      |
| 92     | Online-Banking-system-master                                        | 56        | 2891       |
| 93     | openSIS-Classic-master                                              | 903       | 366294     |
| 94     | flusio-main                                                         | 442       | 38118      |
| 95     | Zebra_Pagination-master                                             | 4         | 516        |
| 96     | friendica-addons-develop                                            | 1831      | 101501     |
| 97     | opengovplatform-beta-master                                         | 1168      | 371889     |
| 98     | PHP-MVC-Blog-System-master                                          | 23        | 457        |
| 99     | appleseed-master                                                    | 647       | 51635      |
| 100    | SecretSanta-master                                                  | 128       | 8297       |
| 101    | orcamentos-master                                                   | 51        | 3472       |
| 102    | remp-master                                                         | 980       | 54610      |
| 103    | cakeStrap-master                                                    | 849       | 151445     |
| 104    | SEBLOD-master                                                       | 615       | 71052      |
| 105    | Loris-main                                                          | 289       | 33782      |
| 106    | angularjs-cakephp-sample-master                                     | 42        | 1091       |
| 107    | iran-locality-database-master                                       | 3         | 2675       |
| 108    | Bitcoin-mining-proxy-master                                         | 20        | 2164       |
| 109    | acl-master                                                          | 57        | 4575       |
| 110    | cloudsuite-master                                                   | 2818      | 191870     |
| 111    | IDDD_Samples_PHP-master                                             | 418       | 26177      |
| 112    | rememberme-master                                                   | 28        | 1422       |
| 113    | mysql_monitor-master                                                | 19        | 1904       |
| 114    | yesnophp-master                                                     | 551       | 91900      |
| 115    | cell-blog-master                                                    | 126       | 5168       |
| 116    | Dswjcms-master                                                      | 704       | 126582     |
| 117    | seckill-master                                                      | 16        | 550        |
| 118    | laravel-shop-reviews-master                                         | 37        | 577        |
| 119    | Wikibase-master                                                     | 2408      | 200092     |
| 120    | yii2-2.0.3-annotated-master                                         | 1130      | 95011      |
| 121    | phpmixbill-master                                                   | 481       | 125490     |
| 122    | Zend-Framework-Skeleton-master                                      | 4424      | 545089     |
| 123    | codeigniter-paypal-ipn-master                                       | 13        | 1815       |
| 124    | bugkick-master                                                      | 2430      | 533446     |
| 125    | amango-master                                                       | 810       | 155384     |
| 126    | meiupic-master                                                      | 216       | 16609      |
| 127    | CodeIgniter-Standard-Project-master                                 | 197       | 26644      |
| 128    | address-smart-parse-master                                          | 2         | 170        |
| 129    | FruxePi-master                                                      | 258       | 38222      |
| 130    | emlauncher-master                                                   | 97        | 6940       |
| 131    | ThinkService-master                                                 | 660       | 55683      |
| 132    | xiunobbs4.0-master                                                  | 101       | 15595      |
| 133    | corebos-master                                                      | 19384     | 1535113    |
| 134    | bzfshop-master                                                      | 806       | 110713     |
| 135    | yiicms-master                                                       | 193       | 8821       |
| 136    | whmcs-shadowsocks-plugin-master                                     | 12        | 2142       |
| 137    | formcreator-master                                                  | 240       | 37585      |
| 138    | open-social-media-monitoring-master                                 | 2428      | 212754     |
| 139    | Roundcube-CardDAV-master                                            | 4         | 1373       |
| 140    | cms-master                                                          | 680       | 46105      |
| 141    | php-framework-benchmark-master                                      | 14393     | 1607307    |
| 142    | xataface-master                                                     | 1196      | 196252     |
| 143    | windframework-master                                                | 201       | 11665      |
| 144    | waimai-master                                                       | 225       | 29349      |
| 145    | forum-master                                                        | 52        | 3863       |
| 146    | XoopsCore-master                                                    | 1834      | 147873     |
| 147    | Crew-master                                                         | 2053      | 204984     |
| 148    | liveprof-ui-master                                                  | 116       | 11193      |
| 149    | sqli-labs-php7-master                                               | 97        | 6740       |
| 150    | CTF-Web-Challenges-master                                           | 16        | 621        |
| 151    | CookieCatcher-master                                                | 5         | 270        |
| 152    | OpenIB-master                                                       | 790       | 62529      |
| 153    | abantecart-src-master                                               | 2511      | 266359     |
| 154    | MovieContentFilter-master                                           | 47        | 2582       |
| 155    | phpsqlitecms-master                                                 | 73        | 11011      |
| 156    | FluxCP-master                                                       | 432       | 31852      |
| 157    | bpush-master                                                        | 46        | 3283       |
| 158    | dolphin.pro-master                                                  | 1936      | 181399     |
| 159    | opencart-ce-master                                                  | 662       | 64079      |
| 160    | ona-master                                                          | 284       | 66492      |
| 161    | PHP_Code_Challenge-master                                           | 57        | 643        |
| 162    | Tbo-master                                                          | 44        | 4183       |
| 163    | GreenCMS-master                                                     | 326       | 40276      |
| 164    | yubikey-val-master                                                  | 27        | 2590       |
| 165    | ASTPP-master                                                        | 865       | 288398     |
| 166    | xivapi.com-master                                                   | 236       | 51186      |
| 167    | Orion-master                                                        | 298       | 48369      |
| 168    | API-master                                                          | 51        | 5011       |
| 169    | GamePanelX-V3-master                                                | 233       | 29929      |
| 170    | pouet2.0-master                                                     | 143       | 18833      |
| 171    | china-distpicker-master                                             | 5         | 199        |
| 172    | web-master                                                          | 150       | 8317       |
| 173    | ocStore-master                                                      | 955       | 71584      |
| 174    | webcalendar-master                                                  | 179       | 41430      |
| 175    | Coinwink-master                                                     | 1317      | 74886      |
| 176    | ZnoteAAC-master                                                     | 108       | 14696      |
| 177    | k2-master                                                           | 208       | 49459      |
| 178    | torrentflux-master                                                  | 513       | 88473      |
| 179    | open-school-CE-master                                               | 3176      | 688954     |
| 180    | phalcon-module-skeleton-master                                      | 48        | 1650       |
| 181    | kompromat-master                                                    | 2         | 136        |
| 182    | cms-master                                                          | 2365      | 159493     |
| 183    | Z-Push-contrib-master                                               | 232       | 41204      |
| 184    | swoole-im-master                                                    | 144       | 9927       |
| 185    | graphp-master                                                       | 70        | 3543       |
| 186    | w7-rangine-project-document-master                                  | 130       | 8696       |
| 187    | php-yubico-master                                                   | 14        | 1082       |
| 188    | beansbooks-master                                                   | 1204      | 106908     |
| 189    | Jshop_mall-master                                                   | 1138      | 163992     |
| 190    | nginad-master                                                       | 610       | 92218      |
| 191    | openITCOCKPIT-master                                                | 1402      | 203373     |
| 192    | GotCms-master                                                       | 3176      | 220576     |
| 193    | SQLBuilder-master                                                   | 153       | 9794       |
| 194    | php-mysql-diff-master                                               | 20        | 2192       |
| 195    | 2Moons-master                                                       | 554       | 88102      |
| 196    | vulawdhub-master                                                    | 33479     | 3709762    |
| 197    | Tiny-Tiny-RSS-master                                                | 288       | 39760      |
| 198    | basercms-master                                                     | 2147      | 280461     |
| 199    | ss-panel-v3-mod-with-f2fpay-master                                  | 517       | 80952      |
| 200    | rox-master                                                          | 1236      | 102472     |
| 201    | EJDict-master                                                       | 7         | 107        |
| 202    | zig-master                                                          | 151       | 10733      |
| 203    | CE-Phoenix-master                                                   | 1373      | 62165      |
| 204    | castopod-develop                                                    | 852       | 52217      |
| 205    | flexi-auth-master                                                   | 96        | 18508      |
| 206    | lin-cms-tp5-master                                                  | 70        | 1833       |
| 207    | yii2-taggable-master                                                | 15        | 942        |
| 208    | payment-master                                                      | 2         | 136        |
| 209    | agora-invoicing-community-master                                    | 9757      | 847665     |
| 210    | Tpay_Svr-master                                                     | 8         | 3414       |
| 211    | Zebra_Session-master                                                | 3         | 275        |
| 212    | forget-db-master                                                    | 28        | 1283       |
| 213    | phphbaseadmin-master                                                | 174       | 38780      |
| 214    | Meneame-master                                                      | 1150      | 104893     |
| 215    | cakephp-oauth-server-master                                         | 17        | 846        |
| 216    | itdb-master                                                         | 214       | 62160      |
| 217    | omegaup-main                                                        | 545       | 101458     |
| 218    | lqycms-master                                                       | 412       | 39068      |
| 219    | webDiplomacy-master                                                 | 423       | 55728      |
| 220    | litecart-master                                                     | 390       | 37432      |
| 221    | BiliRoaming-PHP-Server-main                                         | 32        | 1923       |
| 222    | zphpdemo-master                                                     | 159       | 6269       |
| 223    | CleverStyle-Framework-master                                        | 576       | 61991      |
| 224    | aowow-master                                                        | 306       | 63760      |
| 225    | weixin-order-master                                                 | 891       | 208732     |
| 226    | yii2-tree-manager-master                                            | 27        | 3052       |
| 227    | thinkphp5-demo-master                                               | 1708      | 185070     |
| 228    | reportico-master                                                    | 123       | 31877      |
| 229    | blog_code-master                                                    | 267       | 16913      |
| 230    | leadshop-master                                                     | 4519      | 465515     |
| 231    | newznab-tmux-master                                                 | 532       | 87696      |
| 232    | australianpostcodes-master                                          | 1         | 138        |
| 233    | PhalconCMS-master                                                   | 105       | 7141       |
| 234    | crud-php-simple-master                                              | 5         | 136        |
| 235    | fundraising-application-main                                        | 353       | 18501      |
| 236    | yii2-admin-master                                                   | 105       | 4022       |
| 237    | FormIgniter-master                                                  | 137       | 22633      |
| 238    | openvk-master                                                       | 139       | 11277      |
| 239    | f-admin-master                                                      | 102       | 3414       |
| 240    | lulucms-master                                                      | 2053      | 174735     |
| 241    | Training-master                                                     | 613       | 167147     |
| 242    | Halite-master                                                       | 343       | 28081      |
| 243    | pdo-master                                                          | 11        | 338        |
| 244    | itflow-master                                                       | 661       | 71052      |
| 245    | torrentpier-master                                                  | 226       | 139939     |
| 246    | WebRtcXSS-master                                                    | 323       | 49072      |
| 247    | hashtag-pull-master                                                 | 5         | 887        |
| 248    | godot-asset-library-master                                          | 36        | 3374       |
| 249    | jegarn-master                                                       | 104       | 6534       |
| 250    | slim-born-master                                                    | 23        | 510        |
| 251    | gw2spidy-master                                                     | 1793      | 167032     |
| 252    | zotprime-master                                                     | 2485      | 272698     |
| 253    | symfony1-1.4                                                        | 2134      | 166409     |
| 254    | Social-Network-master                                               | 312       | 31772      |
| 255    | php.googleplusapi-master                                            | 15        | 1115       |
| 256    | cartulary-master                                                    | 1314      | 148079     |
| 257    | zf-boilerplate-master                                               | 2989      | 256199     |
| 258    | nForum-master                                                       | 109       | 13334      |
| 259    | a2billing-master                                                    | 532       | 115857     |
| 260    | raspberrypi-weather-station-master                                  | 12        | 874        |
| 261    | chyrp-master                                                        | 126       | 24626      |
| 262    | blogdemo2-master                                                    | 1672      | 163636     |
| 263    | wine-cellar-php-master                                              | 18        | 1627       |
| 264    | rartracker-master                                                   | 54        | 9225       |
| 265    | Tieba_Sign-master                                                   | 81        | 5262       |
| 266    | BigTree-CMS-master                                                  | 1637      | 106575     |
| 267    | BookedScheduler-master                                              | 1761      | 192614     |
| 268    | Vub_ENV-master                                                      | 3944      | 448681     |
| 269    | erp_opensource-master                                               | 5725      | 1030021    |
| 270    | engine-master                                                       | 2898      | 202852     |
| 271    | Phraseanet-master                                                   | 2350      | 185734     |
| 272    | wuzhicms-master                                                     | 1065      | 133656     |
| 273    | photo-map-master                                                    | 15        | 771        |
| 274    | youbbs-master                                                       | 102       | 9834       |
| 275    | pagon-master                                                        | 14        | 421        |
| 276    | evolution-master                                                    | 3551      | 301594     |
| 277    | rede-social-master                                                  | 399       | 30086      |
| 278    | Typesetter-master                                                   | 380       | 86077      |
| 279    | una-master                                                          | 19502     | 2465104    |
| 280    | yii2-master                                                         | 950       | 104125     |
| 281    | searchku-master                                                     | 673       | 70864      |
| 282    | php-ddd-skeleton-master                                             | 237       | 6703       |
| 283    | CTF_Web_docker-master                                               | 1224      | 131087     |
| 284    | blog-master                                                         | 28        | 2138       |
| 285    | meta-environment-master                                             | 14        | 571        |
| 286    | Database-to-PlantUML-master                                         | 15        | 579        |
| 287    | BWVS-master                                                         | 64        | 2177       |
| 288    | BlogMVC-master                                                      | 521       | 30138      |
| 289    | oxideshop_ce-master                                                 | 2899      | 342095     |
| 290    | theyworkforyou-master                                               | 421       | 78389      |
| 291    | openBI-main                                                         | 86        | 17105      |
| 292    | red-master                                                          | 1222      | 187756     |
| 293    | hyperf-chat-main                                                    | 225       | 9839       |
| 294    | Centurion-master                                                    | 2841      | 228022     |
| 295    | openwrt-on-android-master                                           | 6812      | 643632     |
| 296    | wowarmory-master                                                    | 103       | 18660      |
| 297    | swoft-im-master                                                     | 154       | 6022       |
| 298    | dataserver-master                                                   | 224       | 52465      |
| 299    | hd.rustem-master                                                    | 303       | 31852      |
| 300    | easyswoole_panel-master                                             | 28        | 1396       |
| 301    | Pichome-master                                                      | 817       | 102859     |
| 302    | storytlr-master                                                     | 547       | 50554      |
| 303    | schoolcms-master                                                    | 676       | 120247     |
| 304    | likeshop-master                                                     | 17426     | 699045     |
| 305    | app-dev                                                             | 10055     | 1947481    |
| 306    | cakephp-rest-plugin-master                                          | 12        | 1510       |
| 307    | larke-admin-main                                                    | 122       | 9706       |
| 308    | ATutor-master                                                       | 6046      | 400530     |
| 309    | website-master                                                      | 215       | 18564      |
| 310    | atom-qa-2.x                                                         | 3915      | 325795     |
| 311    | xbmc-video-server-master                                            | 238       | 6790       |
| 312    | joomla-framework-master                                             | 710       | 89720      |
| 313    | xiunobbs-main                                                       | 90        | 13301      |
| 314    | elefant-master                                                      | 657       | 66344      |
| 315    | Luminance-master                                                    | 523       | 62857      |
| 316    | Ourls-master                                                        | 6         | 284        |
| 317    | wafer2-quickstart-php-master                                        | 708       | 71293      |
| 318    | CDash-master                                                        | 813       | 82678      |
| 319    | wp-project-manager-master                                           | 278       | 26281      |
| 320    | msautocreate-master                                                 | 4         | 387        |
| 321    | yii-user-master                                                     | 83        | 5828       |
| 322    | webzash-master                                                      | 164       | 18178      |
| 323    | web2project-master                                                  | 591       | 100980     |
| 324    | dexonline-master                                                    | 700       | 73240      |
| 325    | mail_fishing-master                                                 | 219       | 25298      |
| 326    | chive-master                                                        | 1343      | 237735     |
| 327    | city-master                                                         | 2         | 98         |
| 328    | prado-master                                                        | 1215      | 90475      |
| 329    | nofw-master                                                         | 22        | 1251       |
| 330    | nested-set-behavior-master                                          | 8         | 1606       |
| 331    | LetsBBS-master                                                      | 219       | 29295      |
| 332    | NorthStarC2-master                                                  | 32        | 2354       |
| 333    | readerself-master                                                   | 453       | 94902      |
| 334    | php-hmac-rest-api-master                                            | 17        | 459        |
| 335    | SuperNova-master                                                    | 426       | 49966      |
| 336    | FileZ-master                                                        | 590       | 99076      |
| 337    | notabenoid-master                                                   | 2084      | 745852     |
| 338    | wa4e-master                                                         | 482       | 66037      |
| 339    | goteo-master                                                        | 1342      | 101989     |
| 340    | laravel-multi-auth-admin-master                                     | 112       | 6704       |
| 341    | OWASP-mth3l3m3nt-framework-master                                   | 78        | 11640      |
| 342    | Kalkun-master                                                       | 373       | 38915      |
| 343    | dotProject-master                                                   | 662       | 141581     |
| 344    | rbac-master                                                         | 3882      | 327234     |
| 345    | phpbeginner_gmanage-master                                          | 45        | 3128       |
| 346    | ssrf-vuls-main                                                      | 1206      | 190713     |
| 347    | kanji-koohii-master                                                 | 706       | 61313      |
| 348    | pi-master                                                           | 5618      | 453431     |
| 349    | Zend-Framework--Doctrine-ORM--PHPUnit--Ant--Jenkins-CI--TDD--master | 2825      | 247846     |
| 350    | wildflower-master                                                   | 868       | 146631     |
| 351    | usvn-master                                                         | 2552      | 244175     |
| 352    | ss-panel-master                                                     | 56        | 1819       |
| 353    | CSGOWinBig-master                                                   | 26        | 1574       |
| 354    | continuouspipe-master                                               | 1709      | 70829      |
| 355    | lh-ehr-master                                                       | 4829      | 492516     |
| 356    | inventory-manager-master                                            | 11        | 382        |
| 357    | yoshop-master                                                       | 402       | 35532      |
| 358    | opendocman-master                                                   | 567       | 50661      |
| 359    | silex-simpleuser-master                                             | 16        | 2265       |
| 360    | Attack-Defense-Challenges-master                                    | 14958     | 1642715    |
| 361    | flourish-old-master                                                 | 143       | 50513      |
| 362    | Password-Manager-master                                             | 35        | 5264       |
| 363    | Link-Preview-master                                                 | 16        | 844        |
| 364    | orm-3.3-master                                                      | 14        | 1589       |
| 365    | TSSSaver-master                                                     | 9         | 1533       |
| 366    | OpenPNE3-master                                                     | 4238      | 338061     |
| 367    | ivozprovider-bleeding                                               | 2714      | 193414     |
| 368    | wikireader-master                                                   | 938       | 550094     |
| 369    | pdnsmanager-master                                                  | 43        | 2675       |
| 370    | tutorial-master                                                     | 8         | 142        |
| 371    | ant-master                                                          | 96        | 3628       |
| 372    | cms-2.0                                                             | 572       | 55687      |
| 373    | eva-engine-master                                                   | 921       | 60318      |
| 374    | simpleforum-master                                                  | 1211      | 142215     |
| 375    | cryptdb-master                                                      | 289       | 152764     |
| 376    | owaspbwa-master                                                     | 4655      | 800550     |
| 377    | X2CRM-master                                                        | 5026      | 1235084    |
| 378    | neoinvoice-master                                                   | 461       | 171555     |
| 379    | mysql-country-list-master                                           | 2         | 444        |
| 380    | swf-docs-generator-master                                           | 151       | 24873      |
| 381    | appengine-php-wordpress-starter-project-master                      | 1         | 43         |
| 382    | CMS-master                                                          | 332       | 51501      |
| 383    | phpstorm-workshop-docker                                            | 104       | 35908      |
| 384    | onethink-master                                                     | 261       | 32815      |
| 385    | yii2-zh-cn-master                                                   | 369       | 37613      |
| 386    | BjyAuthorize-master                                                 | 90        | 3503       |
| 387    | CRM-master                                                          | 505       | 50255      |
| 388    | data-migration-tool-2.4-develop                                     | 364       | 25356      |
| 389    | acg-faka-main                                                       | 2265      | 144483     |
| 390    | orangescrum-community-master                                        | 1268      | 275854     |
| 391    | wechatAlliance-master                                               | 222       | 10731      |
| 392    | How-to-Hack-Websites-master                                         | 19        | 438        |
| 393    | Tattle-master                                                       | 132       | 40670      |
| 394    | mini3-master                                                        | 18        | 409        |
| 395    | receive-payments-demos-master                                       | 6         | 225        |
| 396    | B-XSSRF-master                                                      | 6         | 409        |
| 397    | go-master                                                           | 58        | 10873      |
| 398    | forum-master                                                        | 274       | 12762      |
| 399    | zhihuSpider-master                                                  | 10        | 1628       |
| 400    | DolphinPHP-master                                                   | 715       | 74286      |
| 401    | namedmanager-master                                                 | 1321      | 161031     |
| 402    | dota2-api-master                                                    | 69        | 3661       |
| 403    | the-great-web-framework-shootout-master                             | 42        | 955        |
| 404    | PHPageBuilder-master                                                | 62        | 4359       |
| 405    | easyhadoop-master                                                   | 292       | 90680      |
| 406    | admin-2                                                             | 45        | 2388       |
| 407    | phpDhtSpider-master                                                 | 23        | 2450       |
| 408    | gnuboard5-master                                                    | 1319      | 207988     |
| 409    | kldns-3.0                                                           | 6344      | 494395     |
| 410    | represent-map-master                                                | 15        | 1780       |
| 411    | framework-master                                                    | 176       | 12272      |
| 412    | hackademic-master                                                   | 251       | 19907      |
| 413    | simpleinvoices-master                                               | 839       | 101109     |
| 414    | shopsys-master                                                      | 2693      | 137663     |
| 415    | LxdMosaic-master                                                    | 603       | 32465      |
| 416    | geo-master                                                          | 2         | 88         |
| 417    | XiaoTShop-master                                                    | 340       | 58660      |
| 418    | phanbook-master                                                     | 308       | 18723      |
| 419    | laravel-whatsapp-server-main                                        | 61        | 3003       |
| 420    | BaiduPanAutoReshare-master                                          | 13        | 1268       |
| 421    | Project-Pier-master                                                 | 927       | 103474     |
| 422    | Newscoop-master                                                     | 1593      | 316001     |
| 423    | rest-api-slim-php-master                                            | 69        | 2745       |
| 424    | network-weathermap-master                                           | 207       | 30591      |
| 425    | workflow-master                                                     | 80        | 2624       |
| 426    | easy-admin-master                                                   | 438       | 58912      |
| 427    | JammerCore-master                                                   | 331       | 35414      |
| 428    | Omeka-master                                                        | 2367      | 242003     |
| 429    | CI-AdminLTE-master                                                  | 305       | 37243      |
| 430    | rbac-master                                                         | 17        | 34131      |
| 431    | e107-master                                                         | 1410      | 243286     |
| 432    | tools-master                                                        | 1         | 2033       |
| 433    | yii2-framework-master                                               | 526       | 55171      |
| 434    | hyperf-admin-master                                                 | 161       | 14500      |
| 435    | the-events-calendar-master                                          | 1550      | 129214     |
| 436    | laconia-master                                                      | 48        | 1718       |
| 437    | oscommerce-master                                                   | 1203      | 47503      |
| 438    | ECMobile_PHP-master                                                 | 77        | 6827       |
| 439    | Yaf-Blog-master                                                     | 61        | 8369       |
| 440    | xiaohuanxiong-master                                                | 724       | 91740      |
| 441    | sentrifugo-master                                                   | 5129      | 871702     |
| 442    | wms-master                                                          | 448       | 84605      |
| 443    | omeka-s-master                                                      | 916       | 50419      |
| 444    | GMDprivateServer-master                                             | 191       | 7861       |
| 445    | tpAdmin-master                                                      | 951       | 123439     |
| 446    | PhishAPI-master                                                     | 83        | 15087      |
| 447    | pearProjectApi-master                                               | 364       | 46330      |
| 448    | faka-master                                                         | 2094      | 124408     |
| 449    | infinity-master                                                     | 813       | 63842      |
| 450    | opencorpora-master                                                  | 139       | 12660      |
| 451    | koseven-master                                                      | 512       | 31801      |
| 452    | php7-master                                                         | 463       | 6451       |
| 453    | rcmcarddav-master                                                   | 27        | 4084       |
| 454    | open_source_bms-master                                              | 55        | 2441       |
| 455    | nahamsec.training-main                                              | 50        | 2185       |
| 456    | airship-master                                                      | 277       | 32573      |
| 457    | openDCIM-master                                                     | 1266      | 244711     |
| 458    | anahita-master                                                      | 722       | 39550      |
| 459    | PASTE-master                                                        | 453       | 209638     |
| 460    | webmail-lite-master                                                 | 917       | 111212     |
| 461    | Uguu-master                                                         | 4         | 444        |
| 462    | processmaker-master                                                 | 10319     | 1256125    |
| 463    | icms2-master                                                        | 1781      | 128962     |
| 464    | startbbs-master                                                     | 316       | 31899      |
| 465    | engelsystem-main                                                    | 486       | 32926      |
| 466    | fashop-master                                                       | 355       | 32855      |
| 467    | wallacepos-master                                                   | 598       | 189255     |
| 468    | GroupCo-master                                                      | 48        | 1372       |
| 469    | jorani-master                                                       | 1701      | 105918     |
| 470    | blockscloud-master                                                  | 4952      | 378226     |
| 471    | laychat-master                                                      | 253       | 31916      |
| 472    | liveprof-master                                                     | 16        | 1293       |
| 473    | phalconeye-master                                                   | 1220      | 117195     |
| 474    | daloradius-master                                                   | 548       | 78497      |
| 475    | funshop-master                                                      | 351       | 16558      |
| 476    | WCF-master                                                          | 3011      | 246157     |
| 477    | blog-master                                                         | 174       | 19044      |
| 478    | OpenCATS-master                                                     | 351       | 89431      |
| 479    | laravel-admin-master                                                | 64        | 1719       |
| 480    | Greyhole-master                                                     | 94        | 12105      |
| 481    | poweradmin-master                                                   | 504       | 27273      |
| 482    | symfony1-master                                                     | 1029      | 67280      |
| 483    | goteo-legacy-master                                                 | 524       | 59810      |
| 484    | nines-master                                                        | 6         | 657        |
| 485    | FromMySqlToPostgreSql-master                                        | 4         | 1388       |
| 486    | ionize-master                                                       | 717       | 103602     |
| 487    | media-master                                                        | 94        | 7154       |
| 488    | givewp-master                                                       | 1018      | 100622     |
| 489    | redirection-master                                                  | 153       | 14186      |
| 490    | Making-Isometric-Real-time-Games-master                             | 16        | 1255       |
| 491    | xhprof.io-master                                                    | 23        | 2101       |
| 492    | apify-library-master                                                | 33        | 2465       |
| 493    | economizzer-master                                                  | 87        | 5019       |
| 494    | genetify-master                                                     | 12        | 1882       |
| 495    | ViMbAdmin-master                                                    | 370       | 26356      |
| 496    | wstmall-master                                                      | 703       | 123049     |
| 497    | ACI-master                                                          | 250       | 34587      |
| 498    | yzmcms-master                                                       | 165       | 18032      |
| 499    | wpcore-master                                                       | 438       | 41030      |
| 500    | vmoex-framework-master                                              | 213       | 9206       |
| 501    | jslate-master                                                       | 807       | 147735     |
| 502    | hotcrp-master                                                       | 418       | 104544     |
| 503    | zencart-158                                                         | 3626      | 297596     |
| 504    | TinyLara-master                                                     | 19        | 355        |
| 505    | vichan-master                                                       | 84        | 13319      |
| 506    | icingaweb2-module-director-master                                   | 723       | 68359      |
| 507    | TorrentMonitor-master                                               | 55        | 9849       |
| 508    | arc2-master                                                         | 113       | 20089      |
| 509    | laravel-backup-master                                               | 19        | 989        |
| 510    | leadshop-master                                                     | 4519      | 465540     |
| 511    | phpok-master                                                        | 632       | 103721     |
| 512    | ServerStatus-master                                                 | 6         | 256        |
| 513    | douchat-master                                                      | 173       | 29338      |
| 514    | SecureCodingDojo-main                                               | 46        | 3716       |
| 515    | mellivora-master                                                    | 129       | 9021       |
| 516    | angular-cellar-master                                               | 18        | 1627       |
| 517    | WackoPicko-master                                                   | 48        | 2510       |
| 518    | docker-lamp-master                                                  | 1         | 32         |
| 519    | subrion-master                                                      | 938       | 105246     |
| 520    | orangehrm-master                                                    | 2563      | 306045     |
| 521    | ecshop-master                                                       | 713       | 105806     |
| 522    | oauth2-php-master                                                   | 47        | 3359       |
| 523    | moeSS-master                                                        | 251       | 35946      |
| 524    | chronicle-master                                                    | 63        | 4287       |
| 525    | ROCBOSS-OLD-master                                                  | 141       | 24269      |
| 526    | yii2-nested-sets-master                                             | 30        | 1970       |
| 527    | fusioninventory-for-glpi-master                                     | 325       | 68847      |
| 528    | HackMe-SQL-Injection-Challenges-master                              | 85        | 9952       |
| 529    | yona-cms-master                                                     | 167       | 14491      |
| 530    | tudu-web-master                                                     | 1002      | 126768     |
| 531    | vufind-dev                                                          | 2427      | 181060     |
| 532    | ctf_challenges-main                                                 | 442       | 31589      |
| 533    | mini2-master                                                        | 2         | 157        |
| 534    | zf1-master                                                          | 2282      | 219838     |
| 535    | jin-chat-master                                                     | 30        | 2300       |
| 536    | algeria-cities-master                                               | 6         | 170279     |
| 537    | masscan-web-ui-master                                               | 16        | 965        |
| 538    | webasyst-framework-master                                           | 2102      | 220368     |
| 539    | crawler-master                                                      | 7         | 469        |
| 540    | Joomla-Component-Builder-master                                     | 1443      | 272873     |
| 541    | djjob-master                                                        | 5         | 626        |
| 542    | osTicket-1.7-master                                                 | 286       | 40044      |
| 543    | zpanelx-master                                                      | 1927      | 290416     |
| 544    | v2015-master                                                        | 9860      | 1041806    |
| 545    | WePloy-master                                                       | 3         | 471        |
| 546    | barcodebuddy-master                                                 | 103       | 10558      |
| 547    | ClassicPress-master                                                 | 1310      | 296622     |
| 548    | testenv-master                                                      | 142       | 1537       |
| 549    | manaphp-master                                                      | 802       | 40771      |
| 550    | finance-laravel-7.x                                                 | 257       | 9242       |
| 551    | yii2-usuario-master                                                 | 220       | 13696      |
| 552    | mageplus-master                                                     | 8926      | 676904     |
| 553    | slim4-skeleton-master                                               | 63        | 1976       |
| 554    | tcexam-develop                                                      | 320       | 95596      |
| 555    | easyadmin-master                                                    | 1603      | 169242     |
| 556    | sourcebans-pp-1.x                                                   | 313       | 51696      |
| 557    | btcloud-main                                                        | 37        | 1810       |
| 558    | statedecoded-master                                                 | 242       | 23034      |
| 559    | server-master                                                       | 11577     | 1308559    |
| 560    | app-master                                                          | 74        | 1874       |
| 561    | IXP-Manager-master                                                  | 1026      | 85775      |
| 562    | MateCat-master                                                      | 1346      | 92952      |
| 563    | diygw-master                                                        | 1485      | 159943     |
| 564    | laravel-database-encryption-master                                  | 36        | 1704       |
| 565    | qr-master                                                           | 326       | 46105      |
| 566    | loginregister-master                                                | 17        | 4199       |
| 567    | emlog-master                                                        | 119       | 17223      |
| 568    | core-master                                                         | 2090      | 196079     |
| 569    | ectouch-main                                                        | 1005      | 184064     |
| 570    | vue-admin-php-master                                                | 53        | 1896       |
| 571    | OSAdmin-master                                                      | 176       | 19183      |
| 572    | ADOdb-master                                                        | 146       | 35683      |
| 573    | ss-panel-v3-mod_Uim-alipay-wxpay-master                             | 154       | 16284      |
| 574    | hsmm-pi-master                                                      | 56        | 2229       |
| 575    | fabrik-master                                                       | 5659      | 442760     |
| 576    | Link-master                                                         | 20        | 398        |
| 577    | verydows-master                                                     | 188       | 21900      |
| 578    | providence-master                                                   | 10306     | 930786     |
| 579    | yii2-giiant-master                                                  | 97        | 6282       |
| 580    | pokemon-showdown-client-master                                      | 354       | 31175      |
| 581    | zperfmon-master                                                     | 134       | 20819      |
| 582    | ILIAS-release_7                                                     | 8005      | 1141950    |
| 583    | thinkphp-bjyblog-master                                             | 375       | 54096      |
| 584    | CodeIgniter-Aauth-master                                            | 16        | 2338       |
| 585    | zenphoto-master                                                     | 397       | 128938     |
| 586    | MCIR-master                                                         | 279       | 40420      |
| 587    | zf1-future-master                                                   | 2288      | 220795     |
| 588    | Gazelle-master                                                      | 980       | 88736      |
| 589    | ExpressionEngine-5.x                                                | 1634      | 238914     |
| 590    | Piwigo-master                                                       | 744       | 143865     |
| 591    | hisiphp-master                                                      | 323       | 42116      |
| 592    | laykefu-master                                                      | 234       | 34484      |
| 593    | livestreet-master                                                   | 190       | 32794      |
| 594    | Cloudlog-master                                                     | 656       | 62369      |



