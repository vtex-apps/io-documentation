
# Creating a Black Friday page from template

You may want to create custom landing pages for big events, such as Black Friday and Cyber Monday, to compose your marketing strategy. 

With that in mind, we created a landing page template for Black Friday following VTEX recommended practices to help your store maximize profits and conversions. 

This guide will show you how to implement the Black Friday landing page template.
 
>ℹ️ You can also base on this template to create a new or refreshed homepage for your store website.

![Black Friday landing page template](https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/templates/blackfriday.gif?raw=true)

## Step by step

### Step 1 - Downloading the template files 

Download the template files available here: [black-friday-template-files 2021.zip](https://drive.google.com/file/d/1sNOehohokdx-GLsvjdr9tRxhm42NWZKy/view). Within it, you'll find the following folders:

- `/assets` - Sample banners.
- `/store/blocks/custom-template-blackfriday-lp` - json blocks.
- `/style/css/custom-template-blackfriday-lp` - Custom page styles.

### Step 2 - Integrating the template files with the store theme

1. Open your store theme project using the code editor of your choice.
2. Open your project's `manifest.json` file and declare the `"assets": "0.x"` builder on the `builders` list:

  ```diff
  "builders": {
  +  "assets": "0.x",
     "styles": "2.x",
     "store": "0.x",
     "sitemap": "0.x"
  }
  ```

3. Copy and paste the code you previously downloaded into the corresponding folders of your store theme project.

>⚠️ If you are running "styles": "1.x", you must copy and paste the CSS code within its corresponding CSS files since this version doesn't allow subfolders for CSS.

4. Check the code comments within the `/store/blocks/custom-template-blackfriday-lp/custom-template-blackfriday-lp.jsonc` file and add your pre-existing shelves accordingly.

![bf-template](https://user-images.githubusercontent.com/60782333/137352422-c8f144bb-750e-4ccf-b339-c921efaf9950.png)

5. Using the terminal, run `vtex link` on your project folder. 
7. Go back to your code and customize the template as you wish.


### Step 3 - Implementing the page at your store

1. On your browser, open the Admin and go to *CMS > Pages*.
2. Click on **Create new** to create a new page.
3. Edit the page title and URL as you wish. At the Templates section, select the `"store.custom#blackfriday-lp"` template.

Note that the `"store.custom#blackfriday-lp"` template is set to be a custom page by default. If you want to apply this template as your main home page, you must first set
`"store.home#blackfriday-lp"` on the `/custom-template-blackfriday-lp.jsonc` template file.



