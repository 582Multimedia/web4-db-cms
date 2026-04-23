# LIA - Final project

Using Vue, you will create an app with a chosen collection of objects that will be saved with custom post types inside Wordpress.

Technical requirements

## Figma

- Must include details of the type of object that makes up your app
- Design your views prior to adding them into your Vue project

## Git

- Project must be committed and uploaded to GitHub per usual
- Commits must not contain tons of changes or else that portion will not be evaluated (0%)

## Vue

- Must be done in Vue3
- There should be minimum 5 views (home page, list / gallery, add, edit, delete)
- One of your components must receive props so you can use it in multiple places
- Must use forms that gets or send data to wordpress via fetch() inside your script
- Components that has forms must have event listeners using Vue
- Make sure loading screens are implemented
- Confirmations before deleting and success messages should be modals

## Wordpress

- Custom post type must be added to your wordpress site using ACF plugin
- Your custom post type must have appropriate fields that matches your figma file
- Must enable REST API to allow read, add, edit and delete of your custom post type
- One of your fields must be an image
- Must have at least one taxonomy to categorize your objects
