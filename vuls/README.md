# Vulnerability Scan

The results of Splendor's vulnerability discovery are shown here. 
At first, thanks to the ability of static analysis batch scanning, Splendor discovered 17 stored XSS 0day vulnerabilities in this process.
(CVE-2022-2050, CVE-2022-2114, CVE-2022-2194, CVE-2022-2384, CVE-2022-4042, CVE-2022-4110, CVE-2022-4113, CVE-2022-4115, CVE-2022-4119, CVE-2022-4142,
CVE-2022-4200, CVE-2022-4199, CVE-2022-4242, CVE-2022-4243, CVE-2022-4256, CVE-2022-4260, CVE-2022-4330).<br>
Then we show the result of vulnerabilities found in the paper's test cases.


## osCommerce2

  | Tainted Columns                                         | Write Paths                                                  | Read Paths                                                   |
  | ------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | user(user_name)                                         | catalog/admin/administrators.php:102->124<br>catalog/admin/login.php:104->108 | catalog/admin/administrators.php:262->292<br>catalog/admin/administrators.php:262->327 |
  | language(name, code, directory)                         | catalog/admin/languages.php:(73,75,76)->79<br>catalog/admin/languages.php:(20,22,23)->26<br><br> | catalog/admin/languages.php:143->153<br>catalog/admin/languages.php:143->180<br>catalog/admin/languages.php:143->244 |
  | geo_zones(geo_zone_name, geo_zone_description)          | catalog/admin/geo_zones.php:(54,55)->67                      | catalog/admin/tax_rates.php:76->92                           |
  | manufacturers(manufactureers_name, manufacturers_image) | catalog/admin/manufacturers.php:41->45                       | catalog/admin/manufacturers.php:127->163                     |
  | tax_class(tax_class_title, tax_class_description)       | catalog/admin/tax_rates.php:(22,23)->26                      | catalog/admin/tax_rates.php:76->85<br>catalog/admin/tax_rates.php:76->169 |
  | tax_rates(tax_description)                              | catalog/admin/tax_rates.php:(34,35)->38                      | catalog/admin/tax_rates.php:76->85<br>catalog/admin/tax_rates.php:76->169 |
  | product(product_name, product_description)              | catalog/admin/categories.php:347->349<br>                    | catalog/admin/specials.php:157->169<br>catalog/admin/reviews.php:66->144<br>catalog/admin/reviews.php:66->291<br>catalog/admin/reviews.php:66->88 |
  

## catfishCMS

  | Tainted Columns                                      | Write Paths                                                  | Read Paths                                                   |
  | ---------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | users(user_email)                                    | catfish_cpg/application/user/controller/Index.php:56->57     | catfish_cpg/application/admin/controller/Index.php:2666->2669 |
  | users(avatar)                                        | catfish_cpg/application/admin/controller/Index.php:1638->1639 | catfish_cpg/application/index/controller/Index.php:1211->1249<br>catfish_cpg/application/index/controller/Index.php:1211->1247<br>catfish_cpg/application/index/controller/Common.php:562->580<br>catfish_cpg/application/index/controller/Common.php:502->514<br>catfish_cpg/application/index/controller/Common.php:519->536<br>catfish_cpg/application/index/controller/Index.php:157->168<br>catfish_cpg/application/index/controller/Common.php:541->558<br>catfish_cpg/application/admin/controller/Index.php:2663->2669<br>catfish_cpg/application/index/controller/Index.php:419->592<br>catfish_cpg/application/index/controller/Common.php:485->498 |
  | slide(slide_pic)                                     | catfish_cpg/application/admin/controller/Index.php:1215->1217 | catfish_cpg/application/index/controller/Common.php:954->957 |
  | posts(target, href)                                  | catfish_cpg/application/admin/controller/Index.php:654->655  | catfish_cpg/application/index/controller/Index.php:1272->1284 |
  | (links) link_limit, link_target                      | catfish_cpg/application/admin/controller/Index.php:1409->1410 | catfish_cpg/application/index/controller/Index.php:183<br>catfish_cpg/application/index/controller/Common.php:1264<br>catfish_cpg/application/index/controller/Common.php:1257 |
  | (posts) zouzhe, bianji, thumbnail, fujian, fujianurl | catfish_cpg/application/admin/controller/Index.php:654->655  | catfish_cpg/application/index/controller/Index.php:705->745<br>catfish_cpg/application/admin/controller/Index.php:572->586<br>catfish_cpg/application/index/controller/Index.php:1211->1249<br>catfish_cpg/application/index/controller/Index.php:1211->1247<br>catfish_cpg/application/index/controller/Common.php:502->514<br>catfish_cpg/application/index/controller/Common.php:519->536<br>catfish_cpg/application/index/controller/Common.php:596->607<br>catfish_cpg/application/index/controller/Index.php:746->786<br>catfish_cpg/application/index/controller/Index.php:157->168<br>catfish_cpg/application/index/controller/Common.php:541->558<br>catfish_cpg/application/admin/controller/Index.php:572->586<br>catfish_cpg/application/index/controller/Index.php:419->592<br>catfish_cpg/application/index/controller/Common.php:485->498<br>catfish_cpg/application/index/controller/Common.php:485->497<br>catfish_cpg/application/admin/controller/Index.php:1081->1092<br>catfish_cpg/application/index/controller/Index.php:1432->1441 |
  | (links)tuibiao, link_target                          | catfish_cpg/application/admin/controller/Index.php:1467->1468 | catfish_cpg/application/index/controller/Index.php:172->183<br>catfish_cpg/application/index/controller/Common.php:1261->1264<br>catfish_cpg/application/index/controller/Common.php:1245->1257 |
  | posts(target, href)                                  | catfish_cpg/application/admin/controller/Index.php:987->988  | catfish_cpg/application/index/controller/Index.php:705->745<br>catfish_cpg/application/admin/controller/Index.php:572->586<br>catfish_cpg/application/index/controller/Index.php:1211->1249<br>catfish_cpg/application/index/controller/Index.php:1211->1247<br>catfish_cpg/application/admin/controller/Index.php:2093->2102<br>catfish_cpg/application/index/controller/Common.php:502->514<br>catfish_cpg/application/index/controller/Common.php:519->536<br>catfish_cpg/application/index/controller/Common.php:596->607<br>catfish_cpg/application/index/controller/Index.php:746->786<br>catfish_cpg/application/index/controller/Index.php:157->168<br>catfish_cpg/application/index/controller/Common.php:541->558<br>catfish_cpg/application/admin/controller/Index.php:(557,572)->586<br>catfish_cpg/application/index/controller/Index.php:419->592<br>catfish_cpg/application/index/controller/Common.php:485->498<br>catfish_cpg/application/index/controller/Common.php:485->497<br>catfish_cpg/application/admin/controller/Index.php:1081->1092<br>catfish_cpg/application/index/controller/Index.php:1432->1441 |


## punBB

 | Tainted Columns | Source Paths                                                 | Sink Paths                                                   |
  | --------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | posts(message)  | include/functions.php:2307->2316<br>include/functions.php:2075->2108 | delete.php:31->204<br>post.php:566->273<br>moderate.php:504->606<br>extern.php:335->387<br> |
