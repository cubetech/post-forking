# Post Forking #
**Contributors:**   
**Tags:** 
**Requires at least:** 
**Tested up to:**  
**Stable tag:**

WordPress Post Forking allows users to "fork" or create an alternate version of a WordPress content to foster a more collaborative approach to content curation.

## Description ##

WordPress Post Forking allows users to "fork" or create an alternate version of a WordPress content to foster a more collaborative approach to content curation. This can be used, for example, to allow external (such as visitors to your site) or internal (such as other authors) users with the ability to submit proposed revisions. It can even be used on smaller or single-author sites to enable post authors to edit published posts without their changes appearing immediately. If you're familiar with Git, or other decentralized version control systems, you're already familiar with WordPress post forking.

How might you use it?
---------------------
* Allowing users without edit or publish post capabilities to edit and submit changes to content (similar to [GitHub’s pull request system](https://help.github.com/articles/using-pull-requests))
* Collaborative editing (by resolving two users’ conflicted saves – [Wired’s example](http://www.wired.com/wiredenterprise/2012/02/github-revisited/))
* Saving draft changes of already-published content
* Scheduling pending changes to already-published content

How does it work?
-----------------

When a user without the `edit_post` capability attempts to edit a given post, WordPress will automatically create a "fork" or alternate version of the post which they can freely edit. The edit screen will look just like the standard post editing interface that they are used to. When they're done, they simply click "submit for review." At this point, the fork goes into the standard WordPress moderation queue (just like any time an author without the `publish_post` capability submits a post), where an editor can review, and potentially approve the changes for publishing. If the changes can be automatically merged, the original post will be updated, otherwise, the editor will be presented with the ability to resolve the conflicting changes.

Concepts
--------

WordPress Post Forking introduces many of Git's well-established conventions to the WordPress world, and as a result, uses a unique vocabulary to describe what it does:

* **Post** - Any WordPress post that uses the `post_content` field, including posts, pages, and custom post types
* **Fork** - Clone of a post intended for editing without disturbing the parent post
* **Branch** - Parallel versions of the same parent post, owned by the post author
* **Merge** - To push a fork's changes back into its parent post
* **Conflict** - When a post is forked if a given line is changed on the fork, and that same line is subsequently edited on the parent post prior to the merge, the post cannot be automatically merged, and the conflict is presented to the merger to resolve

Under the hood
--------------

** Warning: geek content! **

Forking a post creates a copy of the most recent version of the post as a "fork" custom post type. Certain fields (e.g., `post_content`, `post_title`) are copied over to the new fork. The plugin also stores the revision ID for the revision prior to when the fork was created (see [`includes/revisions.php`](https://github.com/benbalter/post-forking/blob/master/includes/revisions.php#L2) for more information as to why we store the previous revision). 

The fork post type has its own capabilities, allowing a user without the ability to edit or publish on the parent post to edit a fork. Once changes have been made, assuming the user does not have the `publish_fork` capability, the user would submit the fork for review (similar to submitting a Pull Request in GitHub parlance) using the normal WordPress moderation system.

Publishing a fork (either by the fork author, if they have the capability, or my an editor) triggers the merge itself. The post content of the fork undergoes a three way merge with the base revision and current version of the parent post.

A fork can have three post statuses:

1. Draft - The fork is being edited
1. Pending - The fork has been submitted for publication
1. Published - The fork has been merged

Note: No user should have the `edit_published_fork` capability. Once published, the fork post_type simply exists to provide a record of the change and allow the author page, to theoretically list contributions by author.

Future Features (Maybe)
-----------------------

* Ability to fork more than just the post_content (e.g., taxonomies, post meta)
* Appending parent revision history to fork
* Spoofing post_type so metaboxes, etc. appear
* Merge into WordPress core
 
Forking additional fields
-------------------------

As of this version, the only editable portion of the fork is the `post_content` field. The underlying logic has been built to be easily abstracted to accomidate forking of title, post meta, and taxonomies, but the logic for merging additional fields is not as clean. We'd need to create a snapshot of the post meta or taxonomy terms prior to the fork and then write the logic to do a three way merge of the changes. Complicating things further, for post meta, meta can be a single value or an array, furthing complicating a theoretical merge. Last, post_title would affect post_name which would break in the event of a conflict.

Why this plugin?
----------------

* [GitHub for Journalism — What WordPress Post Forking could do to Editorial Workflows
](http://ben.balter.com/2012/02/28/github-for-journalism-what-wordpress-post-forking-could-do-to-editorial-workflows/)

License
-------

The project is licensed under the GNU General Public License v3 or Later

 

## Installation ##

### Automatic Install ###
1. Login to your WordPress site as an Administrator, or if you haven't already, complete the famous [WordPress Five Minute Install](http://codex.wordpress.org/Installing_WordPress)
2. Navigate to Plugins->Add New from the menu on the left
3. Search for Post Forking
4. Click "Install"
5. Click "Activate Now"

### Manual Install ###
1. Download the plugin from the link in the top left corner
2. Unzip the file, and upload the resulting "wp-document-revisions" folder to your "/wp-content/plugins directory" as "/wp-content/plugins/post-forking"
3. Log into your WordPress install as an administrator, and navigate to the plugins screen from the left-hand menu
4. Activate Post Forking

## Frequently Asked Questions ##

Please see (and feel free to contribute to) the [Frequently Asked Questions Wiki](https://github.com/benbalter/WP-Resume/wiki/Frequently-Asked-Questions).

## Screenshots ##

( SCREENSHOTS HERE )

## Changelog ##

### 0.1 ###

## Upgrade Notice ##

Coming soon...

## Frequently Asked Questions ##

Please see (and feel free to contribute to) the [Frequently Asked Questions Wiki](https://github.com/benbalter/WP-Resume/wiki/Frequently-Asked-Questions).

## How To Contribute ##

Post Forking is an open source project and is supported by the efforts of an entire community. We'd love for you to get involved. Whatever your level of skill or however much time you can give, your contribution is greatly appreciated.

( calls to action here )

## Upgrade Notice ##

Coming soon...

## Where To Get Support Or Report An Issue ##

info here