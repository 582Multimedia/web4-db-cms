# Wordpress Customization - Custom Pages

First make sure you have installed wordpress on your server. If you need to see how to install wordpress, [click here](https://youtube.com/playlist?list=PLe6HRxcu-AsDN4fspmBf-CtLCNLYE_ZHr&si=fHv0sixY27yA-qWe).

Make sure you have added Custom Post Types before doing adding custom pages, if you have not, [click here to add custom post types](/notes/wp-custom-post-type.md).

## Displaying Custom Post Types inside wordpress

Meta Field Blocks are useful for adding meta blocks to wordpress pages.

### Install Meta Field Block

In `Dashboard`, Go to `Plugins` and choose `Add New Plugin`.

![alt text](<../img/wp-plugins/Screenshot 2025-04-06 at 10.57.09 AM.jpg>)

Search for `Meta Field Block` in Plugins.

![alt text](<../img/wp-plugins/Screenshot 2025-04-06 at 12.59.55 PM.jpg>)
![alt text](<../img/wp-plugins/Screenshot 2025-04-06 at 1.05.34 PM.jpg>)

Install and Activate the plugin. It should show up in the list of activated plugins on the `Plugins` page.

![alt text](<../img/wp-plugins/Screenshot 2025-04-06 at 1.00.15 PM.jpg>)
![alt text](<../img/wp-plugins/Screenshot 2025-04-06 at 1.01.05 PM.jpg>)

### Custom Page to display Custom Post Types

To be able to view our custom post type of Movies on our wordpress site, we will have to add custom `Query Loop` and `Meta Field Block`.

We will first make a new page, in the `Dashboard`, under `Pages`, **select** `Add New Page`.

![alt text](<../img/wp-custom-block/Screenshot 2025-04-06 at 12.22.30 PM.jpg>)

**Change the title** to `Movie Listing`.

![alt text](<../img/wp-custom-block/Screenshot 2025-04-06 at 12.22.43 PM.jpg>)

**Type** '/Query' and **choose** 'Query Loop' to use the wordpress core.

![alt text](<../img/wp-custom-block/Screenshot 2025-04-06 at 12.23.26 PM.jpg>)

**Click on** `Choose` in the `Query Loop` block.

![alt text](<../img/wp-custom-block/Screenshot 2025-04-06 at 12.23.37 PM.jpg>)

You will see all the patterns you can pick from.

![alt text](<../img/wp-custom-block/Screenshot 2025-04-06 at 12.23.46 PM.jpg>)

**Choose a pattern**.

For this example, we will chose the `Fullwidth posts with uppercase titles`.

![alt text](<../img/wp-custom-block/Screenshot 2025-04-06 at 12.23.55 PM.jpg>)

Once you have chosen a pattern, on the right side panel, look under post type.

![alt text](<../img/wp-custom-block/Screenshot 2025-04-06 at 12.24.13 PM.jpg>)

**Select** the `Movie` post type.

![alt text](<../img/wp-custom-block/Screenshot 2025-04-06 at 10.55.38 PM.jpg>)

You will now see your chosen custom post type appear.

Select the title and look at the `Settings` on the right.

![alt text](<../img/wp-custom-block/Screenshot 2025-04-06 at 12.28.46 PM.jpg>)

**Disable** the `Make title a link` option.

![alt text](<../img/wp-custom-block/Screenshot 2025-04-06 at 12.29.06 PM.jpg>)

The title is now not clickable as a link.

![alt text](<../img/wp-custom-block/Screenshot 2025-04-06 at 12.28.54 PM.jpg>)

At the top of the edit toolbar, **select** `Document Overview`.

![alt text](<../img/wp-custom-block/Screenshot 2025-04-06 at 12.24.37 PM.jpg>)

Expand the Groups and **click** on `Stack` inside `Post Template`.

![alt text](<../img/wp-custom-block/Screenshot 2025-04-06 at 12.24.46 PM.jpg>)

**Click on** the `+` button to see the list of items.

![alt text](<../img/wp-custom-block/Screenshot 2025-04-06 at 12.26.01 PM.jpg>)

**Type** `meta` in the searchbox for the list of items and **select** `Meta Field Block`.

![alt text](<../img/wp-custom-block/Screenshot 2025-04-06 at 12.25.29 PM.jpg>)

A meta field block will appear under your title.

![alt text](<../img/wp-custom-block/Screenshot 2025-04-06 at 12.26.13 PM.jpg>)

On the right side of your edit panel, **click** on `Field Type` and some options will appear.

![alt text](<../img/wp-custom-block/Screenshot 2025-04-06 at 12.26.19 PM.jpg>)

**Select** `ACF - Advanced Custom Fields`.

![alt text](<../img/wp-custom-block/Screenshot 2025-04-06 at 11.04.30 PM.jpg>)

Once you have clicked on it, you can type in the `Field Name`, this must match one of the field names you have created earlier in the `Feild Groups` (must be in lowercase).

In our case, we will **type** 'year'.

![alt text](<../img/wp-custom-block/Screenshot 2025-04-06 at 12.26.34 PM.jpg>)

We will repeat this process for the synopsis.

**Add** another `Meta Field Block`.

![alt text](<../img/wp-custom-block/Screenshot 2025-04-06 at 12.27.00 PM.jpg>)

**Select** `ACF - Advanced Custom Fields`.

![alt text](<../img/wp-custom-block/Screenshot 2025-04-06 at 12.27.15 PM.jpg>)

This time **type** 'synopsis' to add the synopsis field.

We will also scroll down in the `Prefix and suffix` section and **type** 'synopsis' and you can change the Display Layout if you like, by default it is set to block,

![alt text](<../img/wp-custom-block/Screenshot 2025-04-06 at 12.27.44 PM.jpg>)

Your finished template should look like the following.

![alt text](<../img/wp-custom-block/Screenshot 2025-04-06 at 12.27.58 PM.jpg>)

At the top right of your page, you can now **click** on `Publish`.

![alt text](<../img/wp-custom-block/Screenshot 2025-04-06 at 12.28.05 PM.jpg>)

A confirmation dialog will appear and you can **click** on `Publish` to confirm.

![alt text](<../img/wp-custom-block/Screenshot 2025-04-06 at 12.28.09 PM.jpg>)

Once you have confirmed, the page is now live!

![alt text](<../img/wp-custom-block/Screenshot 2025-04-06 at 12.28.18 PM.jpg>)

You can **click** on the `View Page` button to view the page.
