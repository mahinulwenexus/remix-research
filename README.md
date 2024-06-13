# remix-research

### What loader does?
Here's a breakdown of what loaders do in the context of Remix:

<br>

* <b>Fetching Data </b>: Loaders are used to fetch data needed by a specific route or component. This data could come from various sources such as a database, an external API, or even from the blockchain in the case of Ethereum DApps.
* <b>Asynchronous Operation:</b> Loaders operate asynchronously, meaning they run in the background while other parts of the application continue to execute. This allows the application to remain responsive while data is being fetched.
* <b>Error Handling:</b> Loaders often handle error conditions gracefully, allowing the application to display appropriate error messages or fallback content if the data cannot be fetched successfully.
* <b>Data Preloading:</b> In some cases, loaders can be used to preload data for routes or components that the user is likely to visit next. This helps improve the perceived performance of the application by reducing loading times when navigating between pages.
* <b>Integration with Rendering:</b> Once the data is successfully loaded, loaders typically pass the fetched data as props to the component or route they are associated with. This allows the component to render with the fetched data.




In the context of Remix, which is primarily focused on server-rendered React applications, loaders are a key feature for fetching data on the server-side before rendering the React components. This ensures that the application's initial render contains all the necessary data, improving performance and SEO (Search Engine Optimization).

<br>
<br>

# What is remix theme?
Certainly! In the context of **Remix**, a **theme** defines consistent styling and design choices for your web application. It includes aspects like fonts, colors, spacing, and component styles. By using themes, you can maintain a cohesive look and feel across your entire app. 🎨✨

<br>

In Remix, themes do not provide predefined styles out of the box. Instead, Remix encourages a co-located styling approach where you define styles alongside your components.


<br>
<br>

# Remix loader 
```javascript
import styles from "./styles.module.css";
import Nav from "../../modules/nav";
import { useLoaderData } from "@remix-run/react";


export async function loader () {
  /**
   * I can create any type of console log 
   * this loader function automatically run when remix renders first time
   * It doesn't have to be called anywhere by myself
   * remix takes this export and automatically import it somewhere 
   * remix run it the first time the render happens
   * it runs again when I hit this route.
   */

  try{
    console.log('running loader')
    const response = await fetch("https://reqres.in/api/users?page=2");
    const data = await response.json();
    console.log(data);  
    // console.log(response)
    return json({data: "hello"});
  }catch(err) {
    console.log(err);
  }
 

  // if (!response.ok) {
  //   throw new Error(`Failed to fetch data: ${response.statusText}`);
  // }

  // console.log(response);
  // return json({data: "hello"});
}

export default function Contact() {
  const data = useLoaderData();
  console.log(data);
  console.log("hello from contact page");
  return(
    <>
    <Nav />
    <h1 className={`${styles.h2} ${styles.customStyles}`}>Contact Page</h1>
    </>
  )

}

```


<br>
<br>

# How to make post request in remix using loader
```javascript
import styles from "./styles.module.css";
import Nav from "../../modules/nav";
import { useLoaderData } from "@remix-run/react";
import { json } from "@remix-run/node";


export async function loader () {
  /**
   * I can create any type of console log 
   * this loader function automatically run when remix renders first time
   * It doesn't have to be called anywhere by myself
   * remix takes this export and automatically import it somewhere 
   * remix run it the first time the render happens
   * it runs again when I hit this route.
   */

  try{

    const inputData = {
      email: "eve.holt@reqres.in",
      password: "pistol"
    }

    console.log('running loader')
    const response = await fetch("https://reqres.in/api/users?page=2", {
      method: 'POST',
      headers : {
        'Content-Type' : 'application/json'  
      },
      body: JSON.stringify()
    });

    const data = await response.json(inputData);
    console.log(data);  
    return json({data: "hello"});

  }

catch(err) {
    console.log(err);
  }
}

export default function Contact() {
  const data = useLoaderData();
  console.log(data);
  console.log("hello from contact page");
  return(
    <>
    <Nav />
    <h1 className={`${styles.h2} ${styles.customStyles}`}>Contact Page</h1>
    </>
  )

}
```

