# Wordpress API

First make sure you have installed wordpress on your server. If you need to see how to install wordpress, click here.

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
