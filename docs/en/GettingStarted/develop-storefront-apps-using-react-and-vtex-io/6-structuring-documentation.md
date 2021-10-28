# 5. Structuring documentation

Now that you have created a component and defined its style, it is time to generate the documentation for the new app!

App documentation is one of the most critical parts when developing a project, as it will explain all the features to future users.

With that in mind, the VTEX IO team provides a *documentation template* to help you in this process:

1. Access your app's `docs` folder.
2. Access the `README.md` file.

In the `README.md` file, you will find structured recommendations you should follow when generating your documentation. Read the file carefully and make changes according to your particular scenario. 

In addition to presenting the theme blocks exported by your app, you also need to describe their properties and list the CSS Handles created in the previous step, as described in the *template*. 

Remember that **documentation is an ongoing process**–whenever a new setting modifies the user experience in your app, the `README.md` file needs to be updated.

>ℹ️ Block properties are the same as the React component that it renders. This means that when you import a React component and link it to a theme block being developed, the theme block automatically inherits the properties of the React component. So, do not forget to access the component's documentation and document the properties available for the block in your app's `README.md` file, clarifying the setting for each one and its default value.
