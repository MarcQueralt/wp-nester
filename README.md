WP Nester
=========

This WordPress plugin makes it possible to nest sites under other sites
in a WordPress network with subdirectory sites. 

For example, by using this plugin, all of the following can be valid 
WordPress sites in the `example.com` WordPress network.

* mysite.com
* mysite.com/first
* mysite.com/first/second/
* mysite.com/first/second/third
* mysite.com/fourth

Installation
------------

You must have [installed WordPress](http://wordpress.org/download/) and [created a network](http://codex.wordpress.org/Create_A_Network).

1. Move the `wp-nester` folder into `mu-plugins`.
2. Move `sunrise.php` into the root of your `wp-content` folder. 
   If `sunrise.php` is already present there, then merge in the contents.
3. Edit `wp-config.php` and uncomment or add the `SUNRISE` definition line. If it does not exist, paste the following on the line above the last `require_once` command. 

        define( 'SUNRISE', 'on' );

4. Update your the `.htaccess` file in the root of your WordPress installation 
	to contain the following. 

		# BEGIN WordPress
		<IfModule mod_rewrite.c>
		RewriteEngine On
		RewriteBase /wordpress/
		RewriteRule ^index\.php$ - [L]

		# add a trailing slash to /wp-admin
		RewriteRule ^([_0-9a-zA-Z-]+/)?wp-admin$ $1wp-admin/ [R=301,L]

		RewriteCond %{REQUEST_FILENAME} -f [OR]
		RewriteCond %{REQUEST_FILENAME} -d
		RewriteRule ^ - [L]
		RewriteRule ^([_0-9a-zA-Z-]+/)+(wp-(content|admin|includes).*) $2 [L]
		RewriteRule ^([_0-9a-zA-Z-]+/)?(.*\.php)$ $2 [L]
		RewriteRule . index.php [L]
		</IfModule>

		# END WordPress


Creating Nested Sites
---------------------

Unfortunately, there is a snag when creating sites. We are looking for ways
around it, but it's impossible without editing the WordPress core. 
So you have two options: 

1. Apply the the diff file `site-new.diff`. If you view source you'll see 
   that we only need to add one character, but it's crucial. You could use 
   something like this command in your WordPress install folder.

   		patch -p1 </path/to/wp-nester/site-new.diff 

    OR

2. Create sites first with an un-nested URL such as `example-site`, and then 
   edit them afterwards to be nested, like `subsite/example-site`. This avoids the error
   that you'll receive if you attempt to create a site with a nested URL
   initially. 



Versions
--------

Currently only tested with WordPress 3.6 and 3.8.1.


Acknowledgements
----------------

Our work is based heavily on the code represented in the following 
post and comments.

* [WordPress Hacks: Nested Paths For WPMU Blogs](http://maisonbisson.com/post/14052/wordpress-hacks-nested-paths-for-wpmu-blogs/)


