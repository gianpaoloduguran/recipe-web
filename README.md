<!-- A recipe web app built using nextjs , tailwind css and pocketbase. -->
<a name="readme-top"></a>

# Recipe Web Project

___
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
        <li><a href="#reason-for">Reason for</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#api-sample">API Sample</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>



## About The Project

This is a simple crud web project that creates, display , edit and delete recipes as well as users (admin only). This web project consists of a mixture of both server side componets and client side components.

Features:

* Create,Read,Update and Delete Recipes.
* Create,Read,Update and Delete Users (Admin Only).
* Login and Registration.
* Basic Authentication.
* Mobile Responsive.

This project is just a simple project designed to have a javascript framework work with a light database like pocketbase.
It is also using the experimental nextjs 13 new app directory where by default all pages are server side unless stated to be client.

Thank you.

<p align="left">(<a href="#readme-top">back to top</a>)</p>

## Built With

This project is built with using the following technologies:

* [![Next][Next.js]][Next-url]
* [![Pocketbase][PocketBase]][Pocketbase-url]
* [![TailwindCSS][Tailwind CSS]][Tailwind CSS-url]

<p align="left">(<a href="#readme-top">back to top</a>)</p>

## Reason for
  
The reason for choosing the technologies mentioned above is that I want to use nextjs a react framework with tailwind css and pocketbase a self host database server to have fast and light project.

<p align="left">(<a href="#readme-top">back to top</a>)</p>
### Prerequisites

The prerequisites for this project:

  ```sh
  Node.js 14.6.0 or higher
  ```

<p align="left">(<a href="#readme-top">back to top</a>)</p>

## Installation

1. Clone the Github repsitory

   ```sh
    git clone https://github.com/Gianik/recipe-web.git
   ```

2. Install NPM packages

   ```sh
   npm install || npm i
   ```

3. Start Pocketbase

   ```sh
   ./pocketbase serve
   ```

4. Enter the Pocketbase link `.env.local`

   ```js
   // only applicable to server side rendered pages
   // client side atm is hard coded
   PB_LINK = 'your pocketbase link'  
   Sample:'http://127.0.0.1:8090'
    ```

5. Start the next dev

   ```js
    npm run dev
    ```
6. Login
 
   ```js
    //You can login using this credentials it has an admin role:
    //Email:test@test.com
    //Password:12345
   ```

<p align="left">(<a href="#readme-top">back to top</a>)</p>

## Usage

Sample Use Cases will be placed here along with a short explanation.

Notes:

* It is not advisable to access the main pages without logging in or there is no data in local storage as it can break the program. 
* Please check the Pocketbase link in the terminal to make sure the api calls will be proper.
* if the images are not displaying properly you can find them in the folder 'readme_images'

![Pocketbase Terminal Screen Shot][terminal-screenshot]


Sample Login and Registration

![Login Screen Shot][login-screenshot]

![Registration Screen Shot][registration-screenshot]

This pages handle the login and registration portion of the system.
After loggin in the user will be redirected to a page with showing a list of the recipes made by the user.

Sample My Recipes

![My Recipes Screen Shot][my-recipes-screenshot]

On the main pages sidebar links are restricted by role admin can access more links that can view,edit and delete all recipes and users.

Sample Admin Sidebar
<br/>
![Sidebar admin Screen Shot][sidebar-admin-screenshot]

Sample User Sidebar

![Sidebar user Screen Shot][sidebar-user-screenshot]
<br/>

Important part of this web app is to create,read,update and delete recipes and a sample of screenshot will be shown.

Sample Recipe Create
<br/>
![Add Recipe 1 Screen Shot][Add-Recipe-1-screenshot]
![Add Recipe 2 Screen Shot][Add-Recipe-2-screenshot]
![Add Recipe 3 Screen Shot][Add-Recipe-3-screenshot]
![Add Recipe 4 Screen Shot][Add-Recipe-4-screenshot]

Sample View Recipe
![View Recipe Screen Shot][View-Recipe-screenshot]

Sample Edit Recipe, In Edit Recipe or User the data will be fetch and populate the input boxes,textarea and select boxes with the current information

![Edit Recipe Screen Shot][Edit-Recipe-screenshot]

Sample Delete Recipe, Before you can delete a recipe a confirmation page where the user needs to confirm to delete the recipe or user or not.

![Delete Recipe Screen Shot][Delete-Recipe-screenshot]

In particular an admin user can see all users and recipes and can add new ones,view,edit and delete existing ones.
<br/>
![All Recipes Screen Shot][All-Recipes-screenshot]
![All Users Screen Shot][All-Users-screenshot]

<p align="left">(<a href="#readme-top">back to top</a>)</p>

## API Sample

Samples of the API used and a short explanation will be provided here.

Note: Some API call link are hard coded as this is due to nextjs rendering on server side by default and cannot access environment variables in the client.The experimental app directory might be a factor on this.

* Sample of a Create API

     ```js
            const pb = new PocketBase('http://127.0.0.1:8090');
            await pb.collection('users').create({
                name: fullName,
                email: email,
                password: password,
                passwordConfirm: confirmPassword,
                role: 'user',
                emailVisibility: true
            })
        // The goal of this api is to create a user this specific api is used
        // in registration and addUsers a variation is used in add recipes. 
        // It does this by creating an instance of Pocketbase with the link and
        // call a function of collection that is create along with the data needed.
    ```

* Sample Auth API
  
    ```js
            const pb = new PocketBase('http://127.0.0.1:8090');
            await pb.collection('users').authWithPassword(
                email,
                password,
            )
            // The goal of this api to authenticate with pocketbase to log in.
            // Again it needs an instance of Pocketbase and it calls one of the
            // available methods of authentication in this case it is
            // authWithPassword with email. It also available with username and
            // password and support for integration with Web.  OAuth2 
    ```

* Samples Get API
  
    ```js
    //Find One record
    const pb = new PocketBase(process.env.PB_LINK);
    const data = await pb.collection('recipes').getOne(`${recipeId}`);

    //get all recipes max 30 record
    const pb = new PocketBase(process.env.PB_LINK);
    const data = await pb.collection('recipes').getFullList(30, {
    });

    // get all recipes filtered by author with max 30 records
    const pb = new PocketBase(process.env.PB_LINK);
    const data = await pb.collection('recipes').getFullList(30, {
      filter: `recipe_author="${authorId}"`
    });

    // This is a sample of a get api with three variations with getOne for
    // details of one, getFullList with a max of 30 and a variation of
    // getFullList with a condition. A max number of records it can return is 
    // required. As usual an instance of Pocketbase is needed and necessary data
    // like the ids.


    ```

* Sample Update API

    ```js
        const pb = new PocketBase('http://127.0.0.1:8090');
        await pb.collection('recipes').update(`${params.params.editrecipeId}`,{
        recipe_name: recipeName,
        recipe_ingredients: ingredientlist ,
        recipe_instructions:  instructionList ,
        })
        // The update API is alike with the Create one but this time you need to
        // pass the id of the record you are going to update along with the new
        // data. Like other API used an instance of Pocketbase is needed to 
        // call the api.
    ```

* Sample Delete API
  
  ```js
    const pb = new PocketBase('http://127.0.0.1:8090');
    await pb.collection('users').delete(`${params.params.userId}`)

    // The delete API is straghtforward you just need to specify the collection
    // and call the delete function along with the id of the record that is to
    // be deleted.
  ```

<p align="left">(<a href="#readme-top">back to top</a>)</p>

## Contacts

My Email: paoloduguran@gmail.com

Project Repository: [https://github.com/Gianik/recipe-web.git](https://github.com/Gianik/recipe-web.git)

<p align="left">(<a href="#readme-top">back to top</a>)</p>

## Acknowledgments

I would like to acknowledge the other minor packages used in the project.

* [![HeadlessUI][Headless UI]][Headless UI-url]
* [Heroicons](https://heroicons.com/)

<p align="left">(<a href="#readme-top">back to top</a>)</p>



<!-- Markdown Links and images -->
[PocketBase]:https://img.shields.io/static/v1?style=for-the-badge&message=PocketBase&color=222222&logo=PocketBase&logoColor=B8DBE4&label=
[PocketBase-url]: https://pocketbase.io/

[Next.js]: https://img.shields.io/badge/next.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white
[Next-url]: https://nextjs.org/

[Tailwind CSS]:https://img.shields.io/static/v1?style=for-the-badge&message=Tailwind+CSS&color=222222&logo=Tailwind+CSS&logoColor=06B6D4&label=
[Tailwind CSS-url]:https://tailwindcss.com/

[Headless UI]:https://img.shields.io/static/v1?style=for-the-badge&message=Headless+UI&color=222222&logo=Headless+UI&logoColor=66E3FF&label=
[Headless UI-url]: https://headlessui.com/

[terminal-screenshot]: readme_images/pocketbase_terminal.PNG
[login-screenshot]: readme_images/Login_Sample.PNG
[registration-screenshot]: readme_images/Register_Sample.PNG
[my-recipes-screenshot]: readme_images/My_Recipes_Sample.png
[sidebar-admin-screenshot]: readme_images/Sidebar_Admin_Sample.PNG
[sidebar-user-screenshot]: readme_images/Sidebar_User_Sample.PNG
[Add-Recipe-1-screenshot]: readme_images/Add_Recipe_Sample_1.PNG
[Add-Recipe-2-screenshot]: readme_images/Add_Recipe_Sample_2.PNG
[Add-Recipe-3-screenshot]: readme_images/Add_Recipe_Sample_3.PNG
[Add-Recipe-4-screenshot]: readme_images/Add_Recipe_Sample_4.PNG
[View-Recipe-screenshot]: readme_images/View_Recipe_Sample.PNG
[Edit-Recipe-screenshot]: readme_images/Edit_Recipe_Sample.PNG
[Delete-Recipe-screenshot]: readme_images/Delete_Confirmation.PNG
[All-Recipes-screenshot]: readme_images/All_Recipes_Sample.PNG
[All-Users-screenshot]: readme_images/All_Users_Sample.PNG