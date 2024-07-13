# Create a professional blog app using React.js and Tailwind CSS
![image](https://github.com/user-attachments/assets/a5e1e9c5-eb92-4ffa-a761-4d00d1999c0c)

## To create a professional blog app using React.js and Tailwind CSS that loads data from a JSON file and displays post details when a link is clicked, follow these steps:

### 1. Setting Up the Project

We first set up a new React project using `create-react-app` and installed Tailwind CSS for styling.

#### Creating the React Project
```bash
npx create-react-app blog-app
cd blog-app
```

#### Installing and Configuring Tailwind CSS
```bash
npm install -D tailwindcss
npx tailwindcss init
```
- Configured `tailwind.config.js` to include our source files.
- Created `src/index.css` to import Tailwind's base, components, and utilities styles.
- Imported `index.css` in `src/index.js` to apply Tailwind styles throughout the app.

### 2. Creating the JSON File

We created a `data.json` file in the `public` folder to store our blog post data. This JSON file includes an array of blog posts, each with an `id`, `title`, `url`, `content`, and `category`.

#### `public/data.json`
```json
[
  {
    "id": "1",
    "title": "Tech News Blog Post",
    "url": "tech-news-blog-post",
    "content": "This is the content of the tech news blog post.",
    "category": "Tech"
  },
  {
    "id": "2",
    "title": "Lifestyle Blog Post",
    "url": "lifestyle-blog-post",
    "content": "This is the content of the Lifestyle blog post.",
    "category": "Lifestyle"
  }
]

```
- Note: You can add posts and categories as you wish. exmaple-
```json
 ,{
    "id": "3",
    "title": "Mobile Blog Post",
    "url": "mobile-blog-post",
    "content": "This is the content of the mobail price blog post.",
    "category": "Mobile"
  }
```

### 3. Creating Components

#### `Navbar.js`
A simple navigation bar with links to the home page and category pages.
```javascript
import React from 'react';
import { Link } from 'react-router-dom';

const Navbar = () => {
  return (
    <nav className="bg-blue-500 p-4">
      <ul className="flex space-x-4">
        <li><Link className="text-white" to="/">Home</Link></li>
        <li><Link className="text-white" to="/category/tech">Tech</Link></li>
        <li><Link className="text-white" to="/category/lifestyle">Lifestyle</Link></li>
      </ul>
    </nav>
  );
}

export default Navbar;
```
- Note: You can add categories as you wish. Example-
```jsx
<li><Link className="text-white" to="/category/mobile">Mobile</Link></li>
``` 

#### `PostList.js`
Displays a list of blog post titles as links. When a link is clicked, it navigates to the detailed view of that post.
```javascript
import React from 'react';
import { Link, useParams } from 'react-router-dom';

const PostList = ({ posts }) => {
  const { category } = useParams();
  const filteredPosts = category ? posts.filter(post => post.category.toLowerCase() === category.toLowerCase()) : posts;

  return (
    <div className="p-4">
      {filteredPosts.map(post => (
        <div key={post.id} className="border-b mb-4 pb-4">
          <h2 className="text-2xl font-bold">
            <Link to={`/post/${post.url}`}>{post.title}</Link>
          </h2>
        </div>
      ))}
    </div>
  );
}

export default PostList;
```
- `useParams` is used to get the category from the URL.
- Filters posts based on the category if provided.

#### `PostDetail.js`
Displays the details of a single post based on the URL parameter.
```javascript
import React from 'react';
import { useParams } from 'react-router-dom';

const PostDetail = ({ posts }) => {
  const { url } = useParams();
  const post = posts.find(p => p.url === url);

  if (!post) {
    return <div>Post not found</div>;
  }

  return (
    <div className="p-4">
      <h1 className="text-4xl font-bold mb-4">{post.title}</h1>
      <div>{post.content}</div>
    </div>
  );
}

export default PostDetail;
```
- Uses `useParams` to get the `url` parameter from the route.
- Finds and displays the post that matches the URL.

### 4. Setting Up Routing

#### `App.js`
The main component that sets up routing for the application.
```javascript
import React, { useState, useEffect } from 'react';
import { BrowserRouter as Router, Route, Routes } from 'react-router-dom';
import Navbar from './components/Navbar';
import PostList from './components/PostList';
import PostDetail from './components/PostDetail';

const App = () => {
  const [posts, setPosts] = useState([]);

  useEffect(() => {
    fetch('/data.json')
      .then(response => response.json())
      .then(data => setPosts(data));
  }, []);

  return (
    <Router>
      <Navbar />
      <Routes>
        <Route path="/" element={<PostList posts={posts} />} />
        <Route path="/category/:category" element={<PostList posts={posts} />} />
        <Route path="/post/:url" element={<PostDetail posts={posts} />} />
      </Routes>
    </Router>
  );
}

export default App;
```
- `useState` to manage the posts data.
- `useEffect` to fetch the JSON data when the component mounts.
- `BrowserRouter` wraps the app to enable routing.
- `Routes` and `Route` define the different paths and their corresponding components.

### Summary

- **Navbar Component**: A simple navigation bar with links.
- **PostList Component**: Displays a list of blog post titles as links and filters posts by category.
- **PostDetail Component**: Displays the details of a single post based on the URL.
- **App Component**: Fetches data from `data.json`, sets up routing, and renders the Navbar and appropriate components based on the route.

This structure provides a basic blog application with navigation, category filtering, and detailed post views. You can further expand and style the app as needed.

![image](https://github.com/user-attachments/assets/689a7847-46e4-4a1e-9ddc-7ba38989b184)
![image](https://github.com/user-attachments/assets/7cd2a7f4-e312-4319-bbcb-aa9357258a55)
![image](https://github.com/user-attachments/assets/b2ff0dda-d5d8-404a-9724-f67f7fd08dd3)
![image](https://github.com/user-attachments/assets/b6a88241-dc1c-4d58-9a62-ecff6436e27f)




