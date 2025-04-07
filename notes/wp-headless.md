# API

First make sure you have installed wordpress on your server. If you need to see how to install wordpress, click here.

## Install plugins

In `Dashboard`, Go to `Plugins` and choose `Add New Plugin`.

![alt text](<../img/wp-plugins/Screenshot 2025-04-06 at 10.57.09 AM.jpg>)

### Advanced Custom Fields (ACF)

Advanced Custom Fields is used for creating custom: `Post Types`, `Fields` and `Taxonomies`.

Searh for `Advanced Custom Fields` or `ACF`.

![alt text](<../img/wp-plugins/Screenshot 2025-04-06 at 10.57.31 AM.jpg>)
![alt text](<../img/wp-plugins/Screenshot 2025-04-06 at 10.57.41 AM.jpg>)

Press on `Install Now`.

![alt text](<../img/wp-plugins/Screenshot 2025-04-06 at 10.57.51 AM.jpg>)

Once installed, press on `Activate`.

![alt text](<../img/wp-plugins/Screenshot 2025-04-06 at 10.58.06 AM.jpg>)

Once activated, you will be directed to the Plugins page with a `Plugin activated` message.

![alt text](<../img/wp-plugins/Screenshot 2025-04-06 at 10.58.37 AM.jpg>)

### Meta Field Block (Optional)

Meta Field Blocks are useful for adding meta blocks to wordpress pages.

Search for `Meta Field Block` in Plugins.

![alt text](<../img/wp-plugins/Screenshot 2025-04-06 at 12.59.55 PM.jpg>)
![alt text](<../img/wp-plugins/Screenshot 2025-04-06 at 1.05.34 PM.jpg>)

Install and Activate the plugin. It should show up in the list of activated plugins on the `Plugins` page.

![alt text](<../img/wp-plugins/Screenshot 2025-04-06 at 1.00.15 PM.jpg>)
![alt text](<../img/wp-plugins/Screenshot 2025-04-06 at 1.01.05 PM.jpg>)

## Add Custom Post Types to wordpress

In the `Dashboard`, **select** `Post Types` in `Plugins`.

![alt text](<../img/wp-acf/Screenshot 2025-04-06 at 1.13.28 PM.jpg>)

ACF page will open with `Post Types` open at the top and **click on** `Add New`.

![alt text](<../img/wp-acf/Screenshot 2025-04-06 at 10.59.53 AM.jpg>)
![alt text](<../img/wp-acf/Screenshot 2025-04-06 at 11.00.09 AM.jpg>)

Add details for the type of Post you want to create, **type** 'Movies' in the `Plural Label` 'Movie' and `Singular Label`, the `Post Type Key` will autocomplete for you.

![alt text](<../img/wp-acf/Screenshot 2025-04-06 at 11.01.14 AM.jpg>)

At the top of page next to `Add New Post Type`, **click on** `Save Changes`.

![alt text](<../img/wp-acf/Screenshot 2025-04-06 at 11.01.21 AM.jpg>)

Once added, you will see a success message about the post type is created.

![alt text](<../img/wp-acf/Screenshot 2025-04-06 at 11.02.41 AM.jpg>)

## Add Field Groups (Custom Fields for new types)

Custom fields should be specific to the new post type you create, but not something that categorize it, for that you should use `Taxonomies` (which is next after the fieilds).

In this following example, we will create a group named `Movie Info` to use with our `Movies` post type.

First, **click on** `Add New` next to `Field Groups`.

![alt text](<../img/wp-acf/Screenshot 2025-04-06 at 11.03.04 AM.jpg>)

Add the new group name, in this example, we will use `Movie Info`

![alt text](<../img/wp-acf/Screenshot 2025-04-06 at 11.05.40 AM.jpg>)

You can now set different fields, with the type of data as well as the label (how it appears for users) and the `Field Name` should autocomplete (needs to be in all lowercase).

We will first create a new field. **Type** 'Synopsis' and use the default `Field Type` of `Text`.

![alt text](<../img/wp-acf/Screenshot 2025-04-06 at 11.11.54 AM.jpg>)

**Click on** `Add Field` to add another field.

![alt text](<../img/wp-acf/Screenshot 2025-04-06 at 11.12.13 AM.jpg>)

Next, we want to add a year field to our movies as a second field.

**Select** `Number` in the `Field Type`.

![alt text](<../img/wp-acf/Screenshot 2025-04-06 at 11.04.51 AM.jpg>)

**Type** 'Year' as the `Field Label`, the `Field Name` should autocomplete.

![alt text](<../img/wp-acf/Screenshot 2025-04-06 at 11.12.17 AM.jpg>)

Underneath, you should find Settings for this group.

In the `Location Rules` tab, Make sure `Show this field group if` `Post Type` `is equal to`, **select** `Movie`.

![alt text](<../img/wp-acf/Screenshot 2025-04-06 at 8.19.53 PM.jpg>)

And in the `Settings` tab, **enable** `Show in REST API`.

![alt text](<../img/wp-acf/Screenshot 2025-04-06 at 12.51.00 PM.jpg>)

## Taxonomies

Taxonomies are for adding groups or categories of relationships to different post types.

In our example, we will add genre to our movies.

On the `Taxonomies` tab, **click on** `Add New`.

![alt text](<../img/wp-acf/Screenshot 2025-04-06 at 11.13.11 AM.jpg>)

**Type** 'Genres' as the `Plural Label` and 'Genre' as the `Singular Label`, `Taxonomy Key` will autofill in lowercase for you. Make sure you select the `Post Types`, in our case, **select** 'Movies' in the dropdown.

![alt text](<../img/wp-acf/Screenshot 2025-04-06 at 11.13.44 AM.jpg>)

WHen you are done, go up and **click on** `Save Changes`.

![alt text](<../img/wp-acf/Screenshot 2025-04-06 at 11.13.58 AM.jpg>)

A success message will appear for your taxonomy is created.

![alt text](<../img/wp-acf/Screenshot 2025-04-06 at 11.14.08 AM.jpg>)

## Add new Custom Post

Now we can finally add our own objects in the custom post type we created (Movies).

In the `Dashboard`, below `Comments`, you should find `Movies`, **select** `Add New Movie`.

![alt text](<../img/wp-acf/Screenshot 2025-04-06 at 11.14.33 AM.jpg>)

We will use actual movies as reference. In this example, we will use Shawshank Redemption from IMDB. Open this link: [Shawshank Redemption](https://www.imdb.com/title/tt0111161/)  in a new tab or window and have the Window open for your `New Movie`.

**Change the title** on this new Movie and **add details** in the `Synopsis` and `Year` fields below.

![alt text](<../img/wp-acf/Screenshot 2025-04-06 at 11.16.23 AM.jpg>)

On the right side panel, **select** `Movie`.

![alt text](<../img/wp-acf/Screenshot 2025-04-06 at 11.16.41 AM.jpg>)

Go to the `Genres` area.

![alt text](<../img/wp-acf/Screenshot 2025-04-06 at 11.16.58 AM.jpg>)

**Type and add the genres** listed on IMDB, make sure to **seperate each genre by using a comma** (as written under the textarea).

![alt text](<../img/wp-acf/Screenshot 2025-04-06 at 11.17.33 AM.jpg>)

Once you are done, it should look like this:

![alt text](<../img/wp-acf/Screenshot 2025-04-06 at 11.17.47 AM.jpg>)

**Click on** `Publish` at the top and you have now added a `Movie` to your list of `Movies`.

![alt text](<../img/wp-acf/Screenshot 2025-04-06 at 11.17.53 AM.jpg>)

### Practice adding new post from your Custom Type

**Now add 4 more movies to your list of movies and add in all relevant details.**

## Custom Blocks

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

## Wordpress API / Headless Wordpress

In order for us to by pass wordpress theme system and use the data from our site directly through the wordpress API, we have to enable just one setting.

In the `Dashboard`, under `Settings`, **select** `Permalinks`.

![alt text](<../img/wp-headless/Screenshot 2025-04-06 at 11.18.40 AM.jpg>)

The permalinks setting will appear.

![alt text](<../img/wp-headless/Screenshot 2025-04-06 at 11.18.50 AM.jpg>)

Under the list of options in permalink structure, **select** the `Post name` option.

![alt text](<../img/wp-headless/Screenshot 2025-04-06 at 11.18.53 AM.jpg>)

Go to the bottom of the page and **click** on `Save Changes`.

![alt text](<../img/wp-headless/Screenshot 2025-04-06 at 11.18.55 AM.jpg>)

You have now enabled the wordpress javascript API!

To view your wordpress installation's API, you can go to this path:

< wordpress path >/wp-json/wp/v2

where < wordpress path > is the path on your server for wordpress.

For my example, you can visit:

[https://ngy.582mi.com/headless/wp-json/wp/v2](https://ngy.582mi.com/headless/wp-json/wp/v2)
