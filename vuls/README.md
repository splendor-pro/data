# Vulnerability Scan
The results of Splendor's vulnerability discovery are shown here. 
At first, thanks to the ability of static analysis batch scanning, Splendor discovered 17 stored XSS 0day vulnerabilities in this process.
(CVE-2022-2050, CVE-2022-2114, CVE-2022-2194, CVE-2022-2384, CVE-2022-4042, CVE-2022-4110, CVE-2022-4113, CVE-2022-4115, CVE-2022-4119, CVE-2022-4142,
CVE-2022-4200, CVE-2022-4199, CVE-2022-4242, CVE-2022-4243, CVE-2022-4256, CVE-2022-4260, CVE-2022-4330).<br>
Then we show the result of vulnerabilities found in the paper's test cases.

## osCommerce2-2.3.4.1


  | Tainted Columns                                         | Write Locs                                                   | Read Locs                                                    |
  | ------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | user(user_name)                                         | catalog/admin/administrators.php:287<br>catalog/admin/login.php:108 | catalog/admin/administrators.php:287<br>catalog/admin/administrators.php:368 |
  | language(name, code, directory)                         | catalog/admin/languages.php:79<br>catalog/admin/languages.php:26<br><br> | catalog/admin/languages.php:153<br>catalog/admin/languages.php:180<br>catalog/admin/languages.php:244 |
  | geo_zones(geo_zone_name, geo_zone_description)          | catalog/admin/geo_zones.php:67                               | catalog/admin/tax_rates.php:92                               |
  | manufacturers(manufactureers_name, manufacturers_image) | catalog/admin/manufacturers.php:45                           | catalog/admin/manufacturers.php:163<br>catalog/admin/manufacturers.php:163 |
  | tax_class(tax_class_title, tax_class_description)       | catalog/admin/tax_rates.php:26<br>                           | catalog/admin/tax_rates.php:85<br>catalog/admin/tax_rates.php:169 |
  | tax_rates(tax_description)                              | catalog/admin/tax_rates.php:38                               | catalog/admin/tax_rates.php:85<br>catalog/admin/tax_rates.php:169 |
  | product(product_name, product_description)              | catalog/admin/categories.php:320<br>                         | catalog/admin/specials.php:169<br>catalog/admin/reviews.php:144<br>catalog/admin/reviews.php:291<br>catalog/admin/reviews.php:88 |
