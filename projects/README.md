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
|  8 | WackoPicko | 2007 |   2510 | paper teset case[7]         |
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
[1] Top 10 Best PHP CMS In 2022: [https://devrims.com/blog/best-php-cms-platforms/](https://www.plesk.com/blog/various/top-10-php-cms-platforms-for-developers-in-2020/)
[2] Dahse, Johannes and Thorsten Holz. “Simulation of Built-in PHP Features for Precise Static Code Analysis.” Network and Distributed System Security Symposium (2014).
[3] Alhuzali, Abeer, Rigel Gjomemo, Birhanu Eshete and Venkat Venkatakrishnan. “NAVEX: Precise and Scalable Exploit Generation for Dynamic Web Applications.” USENIX Security Symposium (2018).
[4] Kassar, Feras Al, Giulia Clerici, Luca Compagna, Davide Balzarotti and Fabian Yamaguchi. “Testability Tarpits: the Impact of Code Patterns on the Security Testing of Web Applications.” Proceedings 2022 Network and Distributed System Security Symposium (2022): n. pag.
[5] Li, Penghui, Wei Meng, Kangjie Lu and Changhua Luo. “On the Feasibility of Automated Built-in Function Modeling for PHP Symbolic Execution.” Proceedings of the Web Conference 2021 (2021): n. pag.
[6] Luo, Changhua, Penghui Li and Wei Meng. “TChecker: Precise Static Inter-Procedural Analysis for Detecting Taint-Style Vulnerabilities in PHP Applications.” Proceedings of the 2022 ACM SIGSAC Conference on Computer and Communications Security (2022): n. pag.
[7] Eriksson, Benjamin, Giancarlo Pellegrino and Andrei Sabelfeld. “Black Widow: Blackbox Data-driven Web Scanning.” 2021 IEEE Symposium on Security and Privacy (SP) (2021): 1125-1142.
[8] phpStan: https://github.com/phpstan/phpstan
[9] Z-Blog: ttps://github.com/zblogcn
[10] ImpressCMS: https://en.wikipedia.org/wiki/ImpressCMS
[11] PunBB: https://en.wikipedia.org/wiki/PunBB

## 2. Awesome-CMS for rebuttal
In order to better illustrate the generality of DAL usage, in the rebuttal we decided to include a new dataset, i.e. to analyze the database query patterns of 45 PHP projects in awesome-cms.
