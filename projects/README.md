# The Popular PHP Applications

## 1. 30 popular PHP CMS
Because the study is to figure out the trend of PHP database query model, we try to select the more representative PHP projects that appear in different time stages.
We chosen them from three kinds of sources: test projects from related papers of top tier conferences, projects with high Github star numbers (over 1k), and those that appear in some well-known lists.

### Table 1: The projects that access the DB using SQL query statements directly

| id | name       | year |   locs | source                      |
|----|------------|------|--------|-----------------------------|
|  1 | Collabtive | 2013 |  28721 | paper test case[5][6]       |
|  2 | ImpressCMS | 2008 | 506359 | wiki[10]                    |
|  3 | phpBB      | 2016 | 245873 | paper test case[2][3][6][7] |
|  4 | WeBid      | 2013 |  35872 | paper test case[3][6]       |
|  5 | HotCRP     | 2013 |  89122 | paper test case[2][7]       |
|  6 | osCommerce | 2011 |  47533 | paper test case[2][6][7]    |
|  7 | prestaShop | 2012 |  96145 | paper test case[7]          |
|  8 | WackoPicko | 2007 |   2510 | paper test case[7]         |
|  9 | myBloggie  | 2011 |   6843 | paper test case[3]          |
| 10 | WebChess   | 2012 |   4690 | paper test case[3]          |
| 11 | SchoolMate | 2013 |   6549 | paper test case[3]          |
| 12 | Zen-Cart   | 2011 | 193336 | paper test case[5][6]       |
| 13 | OpenConf   | 2009 |  22190 | paper test case[3]          |
| 14 | FAQForg    | 2010 |   1040 | paper test case[3]          |


### Table 2: The projects that use a DAL

| id | name             | year |    locs | source              |
|----|------------------|------|---------|---------------------|
| 15 | MantisBT         | 2011 |   73979 | paper test case[4]  |
| 16 | myBB             | 2012 |  135089 | paper test case[2]  |
| 17 | punBB            | 2011 |   31864 | wiki[11]            |
| 18 | Drupal           | 2011 |  815734 | 2022 top10 CMS[1]   |
| 19 | Joomla           | 2011 |  322897 | 2022 top10 CMS[1]   |
| 20 | Vanilla          | 2010 |  149873 | paper test case[7]  |
| 21 | Gallery          | 2011 |   26945 | paper test case[5]  |
| 22 | phpStan          | 2016 |  261254 | Github high star[8] |
| 23 | Monstra          | 2013 |   27531 | paper test case[6]  |
| 24 | Codiad           | 2003 |    7489 | paper test case[6]  |
| 25 | ExpressionEngine | 2019 | 3085020 | 2022 top10 CMS[1]   |
| 26 | Elgg             | 2017 |  617225 | paper test case[5]  |
| 27 | octoberCMS       | 2012 |   87572 | 2022 top10 CMS[1]   |
| 28 | Z-Blog           | 2015 |   45436 | Github high star[9] |
| 29 | CraftCMS         | 2013 |  815734 | 2022 top10 CMS[1]   |
| 30 | WordPress        | 2003 |  284505 | 2022 top10 CMS[1]   |

### Database access mode analysis on 30 PHP projects

<img src="https://user-images.githubusercontent.com/126662430/232279388-70c3cb16-0d84-4ad4-b497-50587e3917d3.png" width="60%" height="60%">

The circle dots represent items in Table 1 and the triangle dots represent items in Table 2.


### Reference
[1] Top 10 Best PHP CMS In 2022: [https://devrims.com/blog/best-php-cms-platforms/](https://www.plesk.com/blog/various/top-10-php-cms-platforms-for-developers-in-2020/) <br>
[2] Dahse, Johannes and Thorsten Holz. “Simulation of Built-in PHP Features for Precise Static Code Analysis.” Network and Distributed System Security Symposium (2014). <br>
[3] Alhuzali, Abeer, Rigel Gjomemo, Birhanu Eshete and Venkat Venkatakrishnan. “NAVEX: Precise and Scalable Exploit Generation for Dynamic Web Applications.” USENIX Security Symposium (2018). <br>
[4] Kassar, Feras Al, Giulia Clerici, Luca Compagna, Davide Balzarotti and Fabian Yamaguchi. “Testability Tarpits: the Impact of Code Patterns on the Security Testing of Web Applications.” Proceedings 2022 Network and Distributed System Security Symposium (2022): n. pag. <br>
[5] Li, Penghui, Wei Meng, Kangjie Lu and Changhua Luo. “On the Feasibility of Automated Built-in Function Modeling for PHP Symbolic Execution.” Proceedings of the Web Conference 2021 (2021): n. pag. <br>
[6] Luo, Changhua, Penghui Li and Wei Meng. “TChecker: Precise Static Inter-Procedural Analysis for Detecting Taint-Style Vulnerabilities in PHP Applications.” Proceedings of the 2022 ACM SIGSAC Conference on Computer and Communications Security (2022): n. pag. <br>
[7] Eriksson, Benjamin, Giancarlo Pellegrino and Andrei Sabelfeld. “Black Widow: Blackbox Data-driven Web Scanning.” 2021 IEEE Symposium on Security and Privacy (SP) (2021): 1125-1142. <br>
[8] phpStan: https://github.com/phpstan/phpstan <br>
[9] Z-Blog: ttps://github.com/zblogcn <br>
[10] ImpressCMS: https://en.wikipedia.org/wiki/ImpressCMS <br>
[11] PunBB: https://en.wikipedia.org/wiki/PunBB <br>

## 2. Awesome-CMS for rebuttal
In order to better illustrate the generality of DAL usage, in the rebuttal we decided to include a new dataset, i.e. to analyze the database query patterns of 45 PHP projects in awesome-cms.

| id   | name                                                         | read model                                                   | write model                                                  |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 1    | [**Anchor CMS**](https://github.com/anchorcms/anchor-cms)    | anchor-cms-master/anchor/libraries/auth.php<br>User::where('username','=',\$username)<br>->where('status','=','active')<br>->fetch(); | anchor/libraries/update.php<br>Query::*table*(\$table)<br>->where('key','=','last_update_check')<br>->update(['value'=>\$today]); |
| 2    | [**AsgardCms**](https://github.com/AsgardCms/Platform)       | Modules/Media/Http/Controllers/Api/MediaController.php<br>DB::*table*('media__imageables')<br>->where('imageable_id',\$request->get('entity_id'))<br>->whereZone(\$request->get('zone'))<br>->whereImageableType(\$request->get('entity'))<br>->first(); | Modules/Media/Http/Controllers/Api/MediaController.php<br>DB::*table*('media__imageables')<br>->whereId(\$id)<br>->update(['order'=>\$order]);<br><br> |
| 3    | [**Azuriom**](https://github.com/Azuriom/Azuriom)            |                                                              |                                                              |
| 4    | [**Bolt**](https://github.com/bolt/project)                  | src/Storage/Repository.php<br>\$result=\$qb->where\(\$this->getAlias().'.id=:id')<br>->setParameter('id',\$id)<br>->execute()<br>->fetch(); | src/Storage/Repository.php<br>\$qb->insert(\$this->getTableName());<br>\$querySet->append(\$qb);<br>\$this->persist(\$querySet,$entity,['id']);<br>\$result=\$querySet->execute(); |
| 5    | [**Bootstrap CMS**](https://github.com/BootstrapCMS/CMS)     | app/Http/Controllers/PostController.php<br>\$comments=\$post->comments()->orderBy('id','desc')->get();<br> | app/Http/Controllers/PostController.php<br>\$post=PostRepository::*find*(\$id);<br>\$post->update(\$input);<br> |
| 6    | [**Borgert CMS**](https://github.com/odirleiborgert/borgert-cms) | borgert-cms-master/app/Http/Controllers/Blog/SitemapController.php<br>\$categorys=Categorys::where('status',1)->get();<br><br><br><br><br> | borgert-cms-master/app/Http/Controllers/Blog/CommentController.php<br>Comments::create([<br>'post_id'=>\$id,<br>'name'=>\$request->name, <br>'email'=>\$request->email,<br>'description'=>\$request->comment,<br>'status'=>0,<br>]); |
| 7    | [**Cockpit CMS**](https://github.com/COCOPi/cockpit)         | cockpit-master/lib/MongoLite/Collection.php<br>\$sql='SELECT id,document FROM\`'.<br>\$this->name.'\`WHERE document_criteria("'.<br>\$this->database->registerCriteriaFunction(\$criteria).<br>'",document)';<br>\$stmt=\$conn->query(\$sql); | cockpit-master/lib/MongoLite/Collection.php<br>\$sql="INSERT INTO\`{\$table}\`({\$fields})VALUES({\$values})";<br>\$res=\$this<br>->database<br>->connection<br>->exec(\$sql); |
| 8    | [**Contao**](https://github.com/contao/core)                 | core-bundle/src/Resources/contao/drivers/DC_Table.php<br>\$objRow=\$this<br>->Database<br>->prepare("SELECT * FROM".$this->strTable."WHEREid=?")<br>->limit(1)<br><br><br> | core-bundle/src/Resources/contao/drivers/DC_Table.php<br>\$objUndoStmt=\$this<br>->Database<br>->prepare("INSERT INTO tl_undo(pid,tstamp,fromTable,query,affectedRows,data)VALUES(?,?,?,?,?,?)")<br>->execute(\$this->User->id,time(),\$this->strTable,<br>'DELETEFROM'.\$this->strTable.'WHEREid='.\$this->intId,<br>\$affected,serialize(\$data)); |
| 9    | [**Contenta CMS**](https://github.com/contentacms/contenta_jsonapi) | web/modules/contrib/crop/src/CropStorage.php<br>\$query=\$this->database->select('crop_field_data','cfd');<br><br><br> | web/core/lib/Drupal/Core/Entity/Sql/SqlContentEntityStorage.php<br>\$this->database->update(\$table_name)<br>->fields(['deleted'=>1])<br>->condition('bundle',\$field_definition->getTargetBundle())<br>->execute(); |
| 10   | [**Craft CMS**](https://github.com/craftcms/cms)             | src/services/Assets.php<br>\$query=\$this->_createFolderQuery()<br>->where([<br>'and',<br>['like','path',\$parentFolder->path.'%',false],<br>['volumeId'=>\$parentFolder->volumeId],<br>['not',['parentId'=>null]],<br>]); | src/services/Drafts.php<br>Db::*insert*(Table::DRAFTS,[<br>'sourceId'=>\$sourceId,<br>'creatorId'=>\$creatorId,<br>'name'=>\$name,<br>'notes'=>\$notes,<br>'trackChanges'=>\$trackChanges,<br>],false,\$this->db); |
| 11   | [**Croogo**](https://github.com/croogo/croogo)               |                                                              |                                                              |
| 12   | [**Drupal**](https://github.com/drupal/drupal)               |                                                              |                                                              |
| 13   | [**ExpressionEngine**](https://github.com/ExpressionEngine/ExpressionEngine) |                                                              |                                                              |
| 14   | [**Flextype**](https://github.com/flextype/flextype)         |                                                              |                                                              |
| 15   | [**Fork CMS**](https://github.com/forkcms/forkcms)           |                                                              |                                                              |
| 16   | [**FUEL CMS**](https://github.com/daylightstudio/FUEL-CMS)   |                                                              |                                                              |
| 17   | [**Grav**](https://github.com/getgrav/grav)                  |                                                              |                                                              |
| 18   | [**Joomla!**](https://github.com/joomla/joomla-cms)          |                                                              |                                                              |
| 19   | [**Kirby**](https://github.com/getkirby/starterkit)          |                                                              |                                                              |
| 20   | [**KunstmaanBundlesCMS**](https://github.com/Kunstmaan/KunstmaanBundlesCMS) |                                                              |                                                              |
| 21   | [**Lavalite**](https://github.com/LavaLite/cms)              |                                                              |                                                              |
| 22   | [**Magento**](https://github.com/magento/magento2)           |                                                              |                                                              |
| 23   | [**MediaWiki**](https://github.com/wikimedia/mediawiki)      |                                                              |                                                              |
| 24   | [**Microweber**](https://github.com/microweber/microweber)   |                                                              |                                                              |
| 25   | [**MODX** ](https://github.com/modxcms/revolution)           |                                                              |                                                              |
| 26   | [**October**](https://github.com/octobercms/october)         |                                                              |                                                              |
| 27   | [**Pagekit**](https://github.com/pagekit/pagekit)            |                                                              |                                                              |
| 28   | [**Pimcore Platform**](https://github.com/pimcore/pimcore)   |                                                              |                                                              |
| 29   | [**Processwire**](https://github.com/processwire/processwire) |                                                              |                                                              |
| 30   | [**PyroCMS**](https://github.com/pyrocms/pyrocms)            |                                                              |                                                              |
| 31   | [**REDAXO**](https://github.com/redaxo/redaxo)               |                                                              |                                                              |
| 32   | [**Redaxscript**](https://github.com/redaxmedia/redaxscript) |                                                              |                                                              |
| 33   | [**Roadiz**](https://github.com/roadiz/roadiz)               |                                                              |                                                              |
| 34   | [**Serendipity**](https://github.com/s9y/Serendipity)        |                                                              |                                                              |
| 35   | [**SilverStripe**](https://github.com/silverstripe/silverstripe-framework) |                                                              |                                                              |
| 36   | [**Textpattern CMS**](https://github.com/textpattern/textpattern) |                                                              |                                                              |
| 37   | [**Thelia**](https://github.com/thelia/thelia)               |                                                              |                                                              |
| 38   | [**Twill**](https://github.com/area17/twill)                 |                                                              |                                                              |
| 39   | [**TypiCMS**](https://github.com/TypiCMS/Base)               |                                                              |                                                              |
| 40   | [**TYPO3**](https://github.com/TYPO3/TYPO3.CMS)              |                                                              |                                                              |
| 41   | [**Unite CMS**](https://github.com/unite-cms/unite-cms)      |                                                              |                                                              |
| 42   | [**Winter CMS**](https://github.com/wintercms/winter)        |                                                              |                                                              |
| 43   | [**WonderCMS**](https://github.com/robiso/WonderCMS)         |                                                              |                                                              |
| 44   | [**WordPress**](https://github.com/WordPress/WordPress)      |                                                              |                                                              |
| 45   | [**XOOPS**](https://github.com/XOOPS/XoopsCore)              |                                                              |                                                              |






