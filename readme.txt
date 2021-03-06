=== Linkify Posts ===
Contributors: coffee2code
Donate link: https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=6ARCFJ9TX3522
Tags: posts, post, link, linkify, archives, list, widget, template tag, coffee2code
License: GPLv2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html
Requires at least: 3.3
Tested up to: 4.7
Stable tag: 2.3.1

Turn a string, list, or array of post IDs and/or slugs into a list of links to those posts. Provides a widget and template tag.


== Description ==

The plugin provides a widget called "Linkify Posts" as well as a template tag, `c2c_linkify_posts()`, which allow you to easily specify posts to list and how to list them. Posts are specified by either ID or slug. See other parts of the documentation for example usage and capabilities.

Particularly handy when used in conjunction with the post custom field feature of WordPress. You could define a custom field for "Related Posts" or "Additional Products" and manually list out post IDs, then utilize the function provided by this plugin to display links to those posts in a custom manner.

Links: [Plugin Homepage](http://coffee2code.com/wp-plugins/linkify-posts/) | [Plugin Directory Page](https://wordpress.org/plugins/linkify-posts/) | [Author Homepage](http://coffee2code.com)


== Installation ==

1. Install via the built-in WordPress plugin installer. Or download and unzip `linkify-posts.zip` inside the plugins directory for your site (typically `wp-content/plugins/`)
2. Activate the plugin through the 'Plugins' admin menu in WordPress
3. Optional: Use the `c2c_linkify_posts()` template tag in one of your templates (be sure to pass it at least the first argument indicating what post IDs and/or slugs to linkify -- the argument can be an array, a space-separate list, or a comma-separated list). Other optional arguments are available to customize the output.
4. Optional: Use the "Linkify Posts" widget in one of the sidebar provided by your theme.


== Screenshots ==

1. The plugin's widget configuration.


== Frequently Asked Questions ==

= What happens if I tell it to list something that I have mistyped, haven't created yet, or have deleted? =

If a given ID/slug doesn't match up with an existing post then that item is ignored without error.

= How do I get items to appear as a list (using HTML tags)? =

Whether you use the template tag or the widget, specify the following information for the appropriate fields/arguments:

* Before text: `<ul><li>` (or `<ol><li>`)
* After text: `</li></ul>` (or `</li></ol>`)
* Between posts: `</li><li>`

= Does this plugin include unit tests? =

Yes.


== Template Tags ==

The plugin provides one template tag for use in your theme templates, functions.php, or plugins.

= Functions =

* `<?php c2c_linkify_posts($posts, $before = '', $after = '', $between = ', ', $before_last = '', $none = '') ?>`
Displays links to each of any number of posts specified via post IDs

= Arguments =

* `$posts`
A single post ID/slug, or multiple post IDs/slugs defined via an array, or multiple posts IDs/slugs defined via a comma-separated and/or space-separated string

* `$before`
(optional) To appear before the entire post listing (if posts exist or if 'none' setting is specified)

* `$after`
(optional) To appear after the entire post listing (if posts exist or if 'none' setting is specified)

* `$between`
(optional) To appear between posts

* `$before_last`
(optional) To appear between the second-to-last and last element, if not specified, 'between' value is used

* `$none`
(optional) To appear when no posts have been found. If blank, then the entire function doesn't display anything

= Examples =

* These are all valid calls:

`<?php c2c_linkify_posts(43); ?>`
`<?php c2c_linkify_posts("43"); ?>`
`<?php c2c_linkify_posts("hello-world"); ?>`
`<?php c2c_linkify_posts("43 92 102"); ?>`
`<?php c2c_linkify_posts("hello-world whats-cooking"); ?>`
`<?php c2c_linkify_posts("43,92,102"); ?>`
`<?php c2c_linkify_posts("hello-world, whats-cooking"); ?>`
`<?php c2c_linkify_posts("43, 92, 102"); ?>`
`<?php c2c_linkify_posts("hello-world, 92, whats-cooking"); ?>`
`<?php c2c_linkify_posts(array(43,92,102)); ?>`
`<?php c2c_linkify_posts(array("hello-world", "whats-cooking")); ?>`
`<?php c2c_linkify_posts(array("43","92","102")); ?>`

* `<?php c2c_linkify_posts("43 92"); ?>`

Outputs something like:

`<a href="http://yourblog.com/archive/2008/01/15/some-post">Some Post</a>,
<a href="http://yourblog.com/archive/2008/01/15/another-post">Another Post</a>`

* Assume that you have a custom field with a key of "Related Posts" that happens to have a value of "43 92" defined (and you're in-the-loop).

`<?php c2c_linkify_posts(get_post_meta($post->ID, 'Related Posts', true), "Related posts: "); ?>`

Outputs something like:

`Related posts: <a href="http://yourblog.com/archive/2008/01/15/some-post">Some Post</a>,
<a href="http://yourblog.com/archive/2008/01/15/another-post">Another Post</a>`

* `<ul><?php c2c_linkify_posts("43, 92", "<li>", "</li>", "</li><li>"); ?></ul>`

Outputs something like:

`<ul><li><a href="http://yourblog.com/archive/2008/01/15/some-post">Some Post</a></li>
<li><a href="http://yourblog.com/archive/2008/01/15/another-post">Another Post</a></li></ul>`

* `<?php c2c_linkify_posts(""); // Assume you passed an empty string as the first value ?>`

Displays nothing.

* `<?php c2c_linkify_posts("", "", "", "", "", "No posts found."); // Assume you passed an empty string as the first value ?>`

Outputs:

`No posts found.`


== Filters ==

The plugin exposes one action for hooking.

= c2c_linkify_posts (action) =

The 'c2c_linkify_posts' hook allows you to use an alternative approach to safely invoke `c2c_linkify_posts()` in such a way that if the plugin were to be deactivated or deleted, then your calls to the function won't cause errors in your site.

Arguments:

* same as for `c2c_linkify_posts()`

Example:

Instead of:

`<?php c2c_linkify_posts( "112, 176", 'Posts: ' ); ?>`

Do:

`<?php do_action( 'c2c_linkify_posts', "112, 176", 'Posts: ' ); ?>`


== Changelog ==

= 2.3.1 (2017-02-26) =
* Fix: Fix unit tests by not declaring test class variable as static
* Change: Update unit test bootstrap
    * Default `WP_TESTS_DIR` to `/tmp/wordpress-tests-lib` rather than erroring out if not defined via environment variable
    * Enable more error output for unit tests
* Change: Note compatibility through WP 4.7+
* Change: Minor readme.txt content and formatting tweaks
* Change: Update copyright date (2017)

= 2.3 (2016-03-13) =
* Change: Update widget to 004:
    * Add `register_widget()` and change to calling it when hooking 'admin_init'.
    * Add `version()` to return the widget's version.
    * Reformat config array.
    * Discontinue use of old-style constructor.
    * Add inline docs for class variables.
    * Late-escape attribute values.
    * Reorder some conditional expressions.
* Change: Explicitly declare methods in unit tests as public or protected.
* Change: Fix and simplify unit tests. Add tests for widget.
* New: Add 'Text Domain' to plugin header.
* New: Add LICENSE file.
* New: Add empty index.php to prevent files from being listed if web server has enabled directory listings.
* Change: Use DIRECTORY_SEPARATOR in place of '/' when requiring widget file.
* Change: Note compatibility through WP 4.4+.
* Change: Update copyright date (2016).

= 2.2.3 (2015-08-12) =
* Update: Discontinue use of PHP4-style constructor invocation of WP_Widget to prevent PHP notices in PHP7
* Update: Minor widget header reformatting
* Update: Minor widget file code tweaks (spacing, bracing)
* Update: Minor inline document tweaks (spacing)
* Note compatibility through WP 4.3+

= 2.2.2 (2015-02-11) =
* Note compatibility through WP 4.1+
* Update copyright date (2015)

= 2.2.1 (2014-08-26) =
* Minor plugin header reformatting
* Change donate link
* Change documentation links to wp.org to be https
* Note compatibility through WP 4.0+
* Add plugin icon

= 2.2 (2013-12-20) =
* Validate post is either int or string before handling
* Add unit tests
* Minor code tweaks (spacing, bracing)
* Minor documentation tweaks
* Note compatibility through WP 3.8+
* Update copyright date (2014)
* Change donate link
* Add banner

= 2.1.4 =
* Add check to prevent execution of code if file is directly accessed
* Note compatibility through WP 3.5+
* Update copyright date (2013)
* Create repo's WP.org assets directory
* Move screenshot into repo's assets directory

= 2.1.3 =
* Re-license as GPLv2 or later (from X11)
* Add 'License' and 'License URI' header tags to readme.txt and plugin file
* Remove ending PHP close tag
* Note compatibility through WP 3.4+

= 2.1.2 =
* Note compatibility through WP 3.3+
* Add link to plugin directory page to readme.txt
* Update copyright date (2012)

= 2.1.1 =
* Note compatibility through WP 3.2+
* Minor code formatting changes (spacing)
* Fix plugin homepage and author links in description in readme.txt

= 2.1 =
* Add Linkify Posts widget
* Note compatibility through WP 3.1+
* Add Screenshots and Frequently Asked Questions sections to readme.txt
* Add screenshot of widget admin
* Update copyright date (2011)
* Change tags in readme.txt

= 2.0 =
* Rename plugin from 'Linkify Post IDs' to 'Linkify Posts'
* Rename `linkify_post_ids()` to `c2c_linkify_posts()` (but maintain a deprecated version for backwards compatibility)
* Rename 'linkify_post_ids' filter to 'c2c_linkify_posts' (no backwards compatibility support since v1.5 was never released)
* Allow linkifying posts specified by slug (in addition to existing support for posts specified by ID)
* Change description
* Drop support for version of WP older than 2.8

= 1.5 =
* Add filter 'linkify_post_ids' to respond to the function of the same name so that users can use the do_action() notation for invoking template tags
* Fix to prevent PHP notice
* Wrap function in if(!function_exists()) check
* Reverse order of implode() arguments
* Remove docs from top of plugin file (all that and more are in readme.txt)
* Add package info to top of plugin file
* Add PHPDoc documentation
* Note compatibility with WP 2.8+, 2.9+, 3.0+
* Minor tweaks to code formatting (spacing)
* Add Changelog, Filters, and Upgrade Notice sections to readme.txt
* Update copyright date
* Remove trailing whitespace

= 1.0 =
* Initial release


== Upgrade Notice ==

= 2.3.1 =
Trivial update: fixed some unit tests, noted compatibility through WP 4.7+, updated copyright date

= 2.3 =
Minor update: minor updates to widget code and unit tests; verified compatibility through WP 4.4; updated copyright date (2016).

= 2.2.3 =
Bugfix update: Prevented PHP notice under PHP7+ for widget; noted compatibility through WP 4.3+

= 2.2.2 =
Trivial update: noted compatibility through WP 4.1+ and updated copyright date

= 2.2.1 =
Trivial update: noted compatibility through WP 4.0+; added plugin icon.

= 2.2 =
Moderate update: better validate data received; added unit tests; noted compatibility through WP 3.8+

= 2.1.4 =
Trivial update: noted compatibility through WP 3.5+

= 2.1.3 =
Trivial update: noted compatibility through WP 3.4+; explicitly stated license

= 2.1.2 =
Trivial update: noted compatibility through WP 3.3+ and minor readme.txt tweaks

= 2.1.1 =
Trivial update: noted compatibility through WP 3.2+ and minor code formatting changes (spacing)

= 2.1 =
Feature update: added widget, added Screenshots and FAQ sections to readme, noted compatibility with WP 3.1+, and updated copyright date (2011).

= 2.0 =
Significant update. Highlights: renamed plugin; renamed `linkify_post_ids()` to `c2c_linkify_posts()`; allow specifying post slug as well as ID; dropped compatibility with versions of WP older than 2.8.

= 1.5 =
Minor update. Highlights: added filter to allow alternative safe invocation of function; verified WP 3.0 compatibility.
