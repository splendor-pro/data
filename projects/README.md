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
In order to better illustrate the generality of DAL usage, in the rebuttal we decided to include a new dataset, to analyze the database query models of 45 PHP projects in awesome-cms. we found that 28 of them can find the database operation triples from the code base.
1. [**Anchor CMS**](https://github.com/anchorcms/anchor-cms)

   * Read Model

     ```php
     //anchor-cms-master/anchor/libraries/auth.php
     User::where('username','=',$username)->where('status','=','active')->fetch();
     ```

     

   * Write Model

     ```php
     //anchor/libraries/update.php
     Query::table($table)
     ->where('key','=','last_update_check')
     ->update(['value'=>$today]);
     ```

     

2. [**AsgardCms**](https://github.com/AsgardCms/Platform)

   * Read Model

     ```php
     //Modules/Media/Http/Controllers/Api/MediaController.php
     DB::table('media__imageables')
     ->where('imageable_id',$request->get('entity_id'))
     ->whereZone($request->get('zone'))
     ->whereImageableType($request->get('entity'))
     ->first();
     ```

     

   * Write Model

     ```php
     //Modules/Media/Http/Controllers/Api/MediaController.php
     DB::table('media__imageables')->whereId($id)->update(['order'=>$order]);
     ```

     

3. [**Azuriom[todo]**](https://github.com/Azuriom/Azuriom)

   * Read Model

     ```php
     
     ```

     

   * Write Model

     ```php
     
     ```

     

4. [**Bolt**](https://github.com/bolt/project)

   * Read Model

     ```php
     //src/Storage/Repository.php
     $result=$qb->where($this->getAlias().'.id=:id')
     ->setParameter('id',$id)
     ->execute()
     ->fetch();
     ```

     

   * Write Model

     ```php
     //src/Storage/Repository.php
     $qb->insert($this->getTableName());
     $querySet->append($qb);
     $this->persist($querySet,$entity,['id']);
     $result=$querySet->execute();
     ```

     

5. [**Bootstrap CMS**](https://github.com/BootstrapCMS/CMS)

   * Read Model

     ```php
     //app/Http/Controllers/PostController.php
     $comments=$post->comments()->orderBy('id','desc')->get();
     ```

     

   * Write Model

     ```php
     //app/Http/Controllers/PostController.php
     $post=PostRepository::find($id);
     $post->update($input);
     ```

     

6. [**Borgert CMS**](https://github.com/odirleiborgert/borgert-cms)

   * Read Model

     ```php
     //borgert-cms-master/app/Http/Controllers/Blog/SitemapController.php
     $categorys=Categorys::where('status',1)->get();
     ```

     

   * Write Model

     ```php
     //borgert-cms-master/app/Http/Controllers/Blog/CommentController.php
     Comments::create([
       'post_id'=>$id,
       'name'=>$request->name,
       'email'=>$request->email,
       'description'=>$request->comment,
       'status'=>0,
       ]);
     ```

     

     

7. [**Cockpit CMS**](https://github.com/COCOPi/cockpit)

   * Read Model

     ```php
     //cockpit-master/lib/MongoLite/Collection.php
     $sql='SELECT id,document FROM`'.$this->name.
       	 '`WHERE document_criteria("'.$this->database->registerCriteriaFunction($criteria).'",document)';
     $stmt=$conn->query($sql);
     ```

     

   * Write Model

     ```php
     //cockpit-master/lib/MongoLite/Collection.php
     $sql="INSERT INTO`{$table}`({$fields})VALUES({$values})";
     $res=$this->database->connection->exec($sql);
     ```

   

8. [**Contao**](https://github.com/contao/core)

   * Read Model

     ```php
     //core-bundle/src/Resources/contao/drivers/DC_Table.php
     $objRow=$this->Database->prepare("SELECT * FROM".$this->strTable."WHEREid=?")
     ->limit(1)
     ->execute($this->intId);
     ```

     

   * Write Model

     ```php
     //core-bundle/src/Resources/contao/drivers/DC_Table.php
     $objUndoStmt=$this->Database->prepare("INSERT INTO tl_undo(pid,tstamp,fromTable,query,affectedRows,data)VALUES(?,?,?,?,?,?)")
     ->execute($this->User->id,time(),$this->strTable,'DELETE FROM'.$this->strTable.
               'WHERE id='.$this->intId,$affected,serialize($data));
     ```

     

9. [**Contenta CMS**](https://github.com/contentacms/contenta_jsonapi)

   * Read Model

     ```php
     //web/modules/contrib/crop/src/CropStorage.php
     $query=$this->database->select('crop_field_data','cfd');
     ```

     

   * Write Model

     ```php
     //web/core/lib/Drupal/Core/Entity/Sql/SqlContentEntityStorage.php
     $this->database->update($table_name)
     ->fields(['deleted'=>1])
     ->condition('bundle',$field_definition->getTargetBundle())
     ->execute();
     ```

     

10. [**Craft CMS**](https://github.com/craftcms/cms)

    * Read Model

      ```php
      //src/services/Assets.php
      $query=$this->_createFolderQuery()
      ->where([
             'and',
             ['like','path',$parentFolder->path.'%',false],
             ['volumeId'=>$parentFolder->volumeId],
             ['not',['parentId'=>null]],
             ]);
      ```

      

    * Write Model

      ```php
      //src/services/Drafts.php
      Db::insert(Table::DRAFTS,[
      'sourceId'=>$sourceId,
      'creatorId'=>$creatorId,
      'name'=>$name,
      'notes'=>$notes,
      'trackChanges'=>$trackChanges,
      ],false,$this->db);
      ```

      

11. [**Croogo**](https://github.com/croogo/croogo)

    * Read Model

      ```php
      //croogo-master/Users/src/Controller/Admin/UsersController.php
      $user=$this->Users
      ->find()
      ->where(['username'=>$username])
      ->orWhere(['email'=>$username])
      ->first();
      ```

      

    * Write Model

      ```php
      //croogo-master/Users/src/Controller/UsersController.php
      $user=$this->Users->newEntity();
      $this->set('user',$user);
      ```

      

12. [**Drupal**](https://github.com/drupal/drupal)

    * Read Model

      ```php
      
      ```

      

    * Write Model

      ```php
      
      ```

      

13. [**ExpressionEngine**](https://github.com/ExpressionEngine/ExpressionEngine)

    * Read Model

      ```php
      //system/ee/ExpressionEngine/Addons/channel/upd.channel.php
      ee()->db->select('module_id')->from('modules');
      ```

      

    * Write Model

      ```php
      //system/ee/ExpressionEngine/Addons/channel/upd.channel.php
      
      $data=array(
      'module_name'=>'Channel',
      'module_version'=>$this->version,
      'has_cp_backend'=>'n'
      );
      
      ee()->db->insert('modules',$data);
      ```

      

14. [**Flextype**](https://github.com/flextype/flextype)

    * Read Model

      

    * Write Model

      

15. [**Fork CMS**](https://github.com/forkcms/forkcms)

    * Read Model

      ```php
      //frontend/core/engine/user.php
      $settings=(array)$db->getPairs(
      'SELECT us.name,us.value
      FROM users_settingsASus
      WHERE us.user_id=?',
      array($userId)
      ```

      

      

    * Write Model

      ```php
      //frontend/modules/faq/engine/model.php
      $db->execute(
      'UPDATE faq_questions
      SET num_usefull_yes=num_usefull_yes+1
      WHERE id=?',
      array((int)$id)
      ```

      

16. [**FUEL CMS**](https://github.com/daylightstudio/FUEL-CMS)

    * Read Model

      

    * Write Model

      

17. [**Grav**](https://github.com/getgrav/grav)

    * Read Model

      

    * Write Model

      

18. [**Joomla!**](https://github.com/joomla/joomla-cms)

    * Read Model

      ```php
      //administrator/components/com_admin/postinstall/languageaccess340.php
      $query = $db->getQuery(true)
      ->select($db->quoteName('access'))
      ->from($db->quoteName('#__languages'))
      ->where($db->quoteName('access') . ' = ' . $db->quote('0'));
      ```

      

    * Write Model

      ```php
      //libraries/legacy/table/menu/type.php
      $query->clear()
      ->update('#__menu')
      ->set('menutype='.$this->_db->quote($this->menutype))
      ->where('menutype='.$this->_db->quote($table->menutype));
      $this->_db->setQuery($query);
      $this->_db->execute();
      ```

      

      

19. [**Kirby**](https://github.com/getkirby/starterkit)

    * Read Model

      ```php
      
      ```

      

    * Write Model

      ```php
      
      ```

      

20. [**KunstmaanBundlesCMS**](https://github.com/Kunstmaan/KunstmaanBundlesCMS)

    * Read Model

      ```php
      //src/Kunstmaan/TranslatorBundle/Repository/TranslationRepository.php
      
      $qb->select('t')
      ->from('KunstmaanTranslatorBundle:Translation','t')
      ->andWhere('t.status!=:statusstring')
      ->setParameter('statusstring',Translation::STATUS_DISABLED)
      ->orderBy('t.domain','ASC')
      ->addOrderBy('t.keyword','ASC');
      ```

      

    

    * Write Model

      ```php
      //src/Kunstmaan/TranslatorBundle/Repository/TranslationRepository.php
      
      $this->createQueryBuilder('t')
      ->update('KunstmaanTranslatorBundle:Translation','t')
      ->set('t.flag','NULL')
      ->getQuery()
      ->execute();
      ```

      

21. [**Lavalite**](https://github.com/LavaLite/cms)

    * Read Model

    

    * Write Model

      

22. [**Magento**](https://github.com/magento/magento2)

    * Read Model

    

    * Write Model

      

23. [**MediaWiki**](https://github.com/wikimedia/mediawiki)

    * Read Model

      ```php
      //maintenance/populateInterwiki.php
      
      $row=$dbw->selectRow(
                'interwiki',
                '1',
                ['iw_prefix'=>$prefix],
                __METHOD__
                );
      ```

      

    * Write Model

      ```php
      //maintenance/populateInterwiki.php
      
      $dbw->insert(
            'interwiki',
            [
            'iw_prefix'=>$prefix,
            'iw_url'=>$d['url'],
            'iw_local'=>1
            ],
            __METHOD__,
            ['IGNORE']
            );
      ```

      

      

24. [**Microweber**](https://github.com/microweber/microweber)

    * Read Model

    

    * Write Model

      

25. [**MODX**](https://github.com/modxcms/revolution)

    * Read Model

    

    * Write Model

      

26. [**October**](https://github.com/octobercms/october)

    * Read Model

    

    * Write Model

27. [**Pagekit**](https://github.com/pagekit/pagekit)

    * Read Model

    

    * Write Model

28. [**Pimcore Platform**](https://github.com/pimcore/pimcore)

    * Read Model

      ```php
      //models/User/AbstractUser/Dao.php
      $data=$this->db->fetchRow('SELECT*FROMusersWHERE`type`=?ANDid=?',[$this->model->getType(),$id]);
      ```

    * Write Model

      ```php
      //models/User/AbstractUser/Dao.php
      $this->db->update('users',$data,['id'=>$this->model->getId()]);
      ```

      

29. [**Processwire**](https://github.com/processwire/processwire)

    * Read Model

    

    * Write Model

30. [**PyroCMS**](https://github.com/pyrocms/pyrocms)

    * Read Model

    

    * Write Model

31. [**REDAXO**](https://github.com/redaxo/redaxo)

    * Read Model

    

    * Write Model

      

32. [**Redaxscript**](https://github.com/redaxmedia/redaxscript)

    * Read Model

      ```php
      //includes/Controller/Recover.php
      $userModel = new Model\User();
      $userModel
      			->query()
      			->where(
      			[
      				'email' => $postArray['email'],
      				'status' => 1
      			])
      			->findMany() ? : null;
      	}
      ```

      

    * Write Model

      ```php
      //includes/Admin/Controller/Article.php
      $articleModel = new Admin\Model\Article();
      return $articleModel->updateByIdAndArray($articleId, $updateArray);
      ```

      

    

33. [**Roadiz**](https://github.com/roadiz/roadiz)

    * Read Model

      ```php
      //src/Roadiz/Core/Repositories/LoginAttemptRepository.php
      $qb->select('COUNT(la)')
      ->andWhere($qb->expr()->gte('la.blocksLoginUntil', ':now'))
      ->andWhere($qb->expr()->eq('la.username', ':username'))
      ->getQuery()
      ->setParameters([
                      'now' =>  new \DateTime('now'),
                      'username' => $username,
                     ])
      ```

      

    * Write Model

      none

      

34. [**Serendipity**](https://github.com/s9y/Serendipity)

    * Read Model

      ```php
      //include/functions_config.inc.php
      $r=serendipity_db_query("SELECT $nameFROM{$serendipity['dbPrefix']} authors WHERE authorid=".(int)$authorid,true);
      ```

    

    * Write Model

      ```php
      //include/functions_config.inc.php
      serendipity_db_query("UPDATE{$serendipity['dbPrefix']} authors SET $name='".serendipity_db_escape_string($val)."'WHERE 		  authorid=".(int)$authorid);
      ```

      

35. [**SilverStripe**](https://github.com/silverstripe/silverstripe-framework)

    * Read Model

      ```php
      //code/Reports/RecentlyEditedReport.php
      SiteTree::get()
      ->filter('LastEdited:GreaterThan',date("Y-m-dH:i:s",$threshold))
      ->sort("\"$tableName\".\"LastEdited\"DESC");
      ```

      

    * Write Model

      ```php
      //code/Search/ContentControllerSearchExtension.php
      FieldList::create(TextField::create('Search',false,$searchText)
      ->setAttribute('placeholder',$placeholder)
      ```

      

36. [**Textpattern CMS**](https://github.com/textpattern/textpattern)

    * Read Model

      ```php
      //textpattern/lib/txplib_db.php 
      $q = "SELECT $col FROM ".safe_pfx($table)." WHERE `$key` = $val LIMIT 1";
      ```

      

    * Write Model

      ```php
      //textpattern/lib/txplib_db.php 
      $res = safe_insert($tbl, "title = '$title', lft = $at, rgt = $at+1, type = '$type', name = '$name', parent = '$parent'");
      ```

      

37. [**Thelia**](https://github.com/thelia/thelia)

    * Read Model

      ```php
      //core/lib/Thelia/Install/Database.php
      $result = $this->execute('SELECT * FROM `' . $table . '`');
      ```

    

    * Write Model

      ```php
      //core/lib/Thelia/Command/Install.php 
      $sql = "UPDATE `config` SET `value`=? WHERE `name`='form.secret'";
       $database->execute($sql, [$secret]);
      ```

      

38. [**Twill**](https://github.com/area17/twill)

    * Read Model

      ```php
      //src/Http/Controllers/Admin/ResetPasswordController.php
      DB::table($this->config->get('auth.passwords.twill_users.table','twill_password_resets'))->get()
      ```

    * Write Model

      ```php
      $user = User::create([
              'name' => "Admin",
              'email' => $email,
              'role' => 'SUPERADMIN',
              'published' => true,
              ]);
      $user->save();
      ```

      

39. [**TypiCMS**](https://github.com/TypiCMS/Base)

    * Read Model

      none

    * Write Model

      none

      

40. [**TYPO3**](https://github.com/TYPO3/TYPO3.CMS)

    * Read Model

      ```php
      // Controller/PageInformationController.php 
      $row = $queryBuilder
      ->select('*')
      ->from('pages')
      ->where(
               $queryBuilder->expr()->eq('uid', $queryBuilder->createNamedParameter($id, \PDO::PARAM_INT)),
               $this->getBackendUser()->getPagePermsClause(Permission::PAGE_SHOW)
             )
      ->execute()
      ->fetch();
      ```

    

    * Write Model

      ```php
      //Controller/MaintenanceController.php
      GeneralUtility::makeInstance(ConnectionPool::class)
      ->getQueryBuilderForTable('be_users')
      ->update('be_users')
      ->set('uc', '')
      ->execute();
      ```

      

41. [**Unite CMS**](https://github.com/unite-cms/unite-cms)

    * Read Model

    ​       none

    * Write Model

      none

42. [**Winter CMS**](https://github.com/wintercms/winter)

    * Read Model

      none

    * Write Model

      none

      

43. [**WonderCMS**](https://github.com/robiso/WonderCMS)

    * Read Model

      none

    * Write Model

      none

      

44. [**WordPress**](https://github.com/WordPress/WordPress)

    * Read Model

      ```php
      //wp-includes/class-wp-user.php
      $caps = get_user_meta( $this->ID, $this->cap_key, true );
      ```

      

    * Write Model

      ```php
      //wp-includes/class-wp-user.php
      update_user_meta( $this->ID, $this->cap_key, $this->caps );
      ```

      

45. [**XOOPS**](https://github.com/XOOPS/XoopsCore)

    * Read Model

      ```php
      //xoops_lib/Xoops/Core/Kernel/Handlers/XoopsMemberHandler.php
      $qb ->select('DISTINCT ' . ($asobject ? 'u.*' : 'u.uid'))
      ->fromPrefix('system_user', 'u')
      ->leftJoinPrefix('u', 'system_usergroup', 'm', 'm.uid = u.uid');
      ```

      

    * Write Model

      ```php
      //htdocs/include/checklogin.php
      $member_handler->insertUser($user)
      ```




