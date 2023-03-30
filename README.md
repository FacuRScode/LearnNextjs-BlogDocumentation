This is a starter template for [Learn Next.js](https://nextjs.org/learn).

DAY1

Run the project 
npm run dev
Stop it
ctrl + C


REACT Function
    export default function FirstPost() {
    return <h1>First Post</h1>;
    }

Pages all under the directory "Pages"

Link component, NextJS component for a tag
import Link from 'next/link';

<h1 className="title">
  Read <Link href="/posts/first-post">this page!</Link>
</h1>

Static assets under the public directory
import Image from 'next/image';

const YourComponent = () => (
  <Image
    src="/images/profile.jpg" // Route of the image file
    height={144} // Desired size with correct aspect ratio
    width={144} // Desired size with correct aspect ratio
    alt="Your Name"
  />
);

Metadata
import Head from 'next/head';

export default function FirstPost() {
  return (
    <>
      <Head>
        <title>First Post</title>
      </Head>
      <h1>First Post</h1>
      <h2>
        <Link href="/">← Back to home</Link>
      </h2>
    </>
  );
}

Scripts 
import Script from 'next/script';

<Script
        src="https://connect.facebook.net/en_US/sdk.js"
        strategy="lazyOnload" #strategy controls when the third-party script should load
        onLoad={() =>
          console.log(`script loaded correctly, window.FB has been populated`)
        }
      />

CSS Modules 
scope CSS at the component-level
To use CSS Modules, the CSS file name must end with .module.css

To load global CSS to your application, create a file called pages/_app

export default function App({ Component, pageProps }) {
  return <Component {...pageProps} />;
}

Important: You need to restart the development server

DAY2

Next.js’ pre-rendering feature.

![Alt text](https://nextjs.org/static/images/learn/data-fetching/pre-rendering.png)
![Alt text](https://nextjs.org/static/images/learn/data-fetching/no-pre-rendering.png)

Static Generation is the pre-rendering method that generates the HTML at build time. The pre-rendered HTML is then reused on each request.
![Alt text](https://nextjs.org/static/images/learn/data-fetching/static-generation.png)

Server-side Rendering is the pre-rendering method that generates the HTML on each request.
![Alt text](https://nextjs.org/static/images/learn/data-fetching/server-side-rendering.png)

You can use Static Generation for many types of pages, including:

Marketing pages
Blog posts
E-commerce product listings
Help and documentation
You should ask yourself: "Can I pre-render this page ahead of a user's request?" If the answer is yes, then you should choose Static Generation.

If your page shows frequently updated data, use server-side rendering

Static Generation with Data using getStaticProps

export default function Home(props) { ... }

export async function getStaticProps() {
  // Get external data from the file system, API, DB, etc.
  const data = ...

  // The value of the `props` key will be
  //  passed to the `Home` component
  return {
    props: ...
  }
}
Note: In development mode, getStaticProps runs on each request instead.

Implement getStaticProps
import { getSortedPostsData } from '../lib/posts';

export async function getStaticProps() {
  const allPostsData = getSortedPostsData();
  return {
    props: {
      allPostsData,
    },
  };
}

API
export async function getSortedPostsData() {
  // Instead of the file system,
  // fetch post data from an external API endpoint
  const res = await fetch('..');
  return res.json();
}

Database
import someDatabaseSDK from 'someDatabaseSDK'

const databaseClient = someDatabaseSDK.createClient(...)

export async function getSortedPostsData() {
  // Instead of the file system,
  // fetch post data from a database
  return databaseClient.query('SELECT posts...')
}

Server Side Redndering
export async function getServerSideProps(context) {
  return {
    props: {
      // props for your component
    },
  };
}

The two forms of pre-rendering: Static Generation and Server-side Rendering.
Static Generation with data, and without data.
getStaticProps and how to use it to import external blog data into the index page.
Some useful information on getStaticProps.