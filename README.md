WP Nester
=========

When running WordPress as a network with multiple sites, you are given two options for URL's for those sites: subdomains or subdirectories. 

### Subdomains

* mysite.com – main site
* subsite.mysite.com 
* another.mysite.com
* etc.mysite.com


### Subdirectories

* mysite.com - main site
* mysite.com/subsite
* mysite.com/another
* mysite.com/etc

You can nest the subdomains if you like (sub.subsite.mysite.com), but you can't nest this subdirectories. Sometimes you have a nested subdirectory URL structure which is desired for information architecure reasons. In this case, we need a solution.

This project is an exploration of whether it's possible to nest the sites in the subdirectory mode. There is little documentation available, but there is one [report of nesting subdirectory sites](http://maisonbisson.com/post/14052/wordpress-hacks-nested-paths-for-wpmu-blogs/). We will use that article as a jumping board and determine whether the code can be updated to work with the latest version of WordPress and whether it can be made to work efficiently in a high-performance environment.


Where to begin?
--------------

You need to start with a working installation of WordPress, [configured to have multiple sites](http://codex.wordpress.org/Create_A_Network) (a.k.a. 'network').

You will then paste this code into a `sunrise.php` file.


