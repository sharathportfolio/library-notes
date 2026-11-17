# Next.js Library – Important Features

## What is Next.js?

Next.js is a React framework used to build full-stack web applications. It provides routing, navigation, server-side rendering, API handling, image optimization, and many other features.

### Installation

```bash
npx create-next-app@latest my-app
```

## 1. `next/link`

Used for navigation between pages without a full browser page reload.

```jsx
import Link from 'next/link';

function Home() {
    return (
        <div>
            <Link href="/about">About</Link>
        </div>
    );
}

export default Home;
```

**Purpose:** Navigate between pages in a Next.js application.

## 2. `next/router`

Used to access routing information and navigate programmatically in the Pages Router.

```jsx
import { useRouter } from 'next/router';

function Home() {
    const router = useRouter();

    return (
        <button onClick={() => router.push('/about')}>
            Go to About
        </button>
    );
}

export default Home;
```

**Purpose:** Navigate between pages, access route parameters, and manage routing.

**Note:** `next/router` is used in the Pages Router. For the App Router, use `next/navigation`.

## 3. `next/navigation`

Used for navigation and accessing route information in the App Router (`app/` directory).

```jsx
'use client';

import { useRouter } from 'next/navigation';

function Home() {
    const router = useRouter();

    return (
        <button onClick={() => router.push('/about')}>
            Go to About
        </button>
    );
}

export default Home;
```

**Purpose:** Navigate between pages, go back, refresh pages, and manage routes.

Other useful functions:

- `usePathname()` – Get the current URL path.
- `useSearchParams()` – Get URL query parameters.
- `useParams()` – Get dynamic route parameters.
- `redirect()` – Redirect to another page.
- `notFound()` – Display the not-found page.

## 4. `next/image`

Used to optimize images automatically.

```jsx
import Image from 'next/image';

function Home() {
    return (
        <Image
            src="/profile.png"
            alt="Profile"
            width={200}
            height={200}
        />
    );
}

export default Home;
```

**Purpose:** Image optimization, resizing, and better loading performance.

## 5. `next/head`

Used to add SEO-related information and HTML head elements in the Pages Router.

```jsx
import Head from 'next/head';

function Home() {
    return (
        <>
            <Head>
                <title>My Website</title>
                <meta
                    name="description"
                    content="My Next.js website"
                />
            </Head>

            <h1>Welcome</h1>
        </>
    );
}

export default Home;
```

**Purpose:** Manage page titles, descriptions, and metadata.

**Note:** In the App Router, use the Metadata API instead of `next/head`.

## 6. `next/script`

Used to load external JavaScript scripts efficiently.

```jsx
import Script from 'next/script';

function Home() {
    return (
        <>
            <h1>Welcome</h1>

            <Script
                src="https://example.com/script.js"
                strategy="lazyOnload"
            />
        </>
    );
}

export default Home;
```

**Purpose:** Load third-party scripts such as analytics and external libraries.

## 7. `next/font`

Used to optimize and load fonts in Next.js.

```jsx
import { Inter } from 'next/font/google';

const inter = Inter({
    subsets: ['latin']
});

export default function Home() {
    return (
        <h1 className={inter.className}>
            Hello Next.js
        </h1>
    );
}
```

**Purpose:** Improve font loading and performance.

## 8. `next/dynamic`

Used to dynamically import components when they are needed.

```jsx
import dynamic from 'next/dynamic';

const Dashboard = dynamic(
    () => import('./Dashboard')
);

function Home() {
    return <Dashboard />;
}

export default Home;
```

**Purpose:** Reduce initial JavaScript loading by splitting code into smaller chunks.

## 9. `next/headers`

Used to access request headers and cookies in the App Router.

```jsx
import { cookies, headers } from 'next/headers';

export default async function Home() {
    const cookieStore = await cookies();
    const headerStore = await headers();

    return <h1>Welcome</h1>;
}
```

**Purpose:** Access cookies and request headers on the server.

## 10. `next/server`

Used to work with server-side requests, responses, and middleware/proxy functionality.

```javascript
import { NextResponse } from 'next/server';

export function middleware(request) {
    return NextResponse.next();
}
```

**Purpose:** Handle requests, redirects, rewrites, and response processing.

## 11. `next/cache`

Used to manage caching and revalidation in Next.js.

```javascript
import { revalidatePath } from 'next/cache';

revalidatePath('/products');
```

**Purpose:** Refresh cached data or pages when application data changes.

## 12. Other Important Next.js Features

| Feature | Purpose |
|---|---|
| File-based Routing | Automatically creates routes based on folders and files |
| Dynamic Routing | Creates routes using dynamic parameters |
| API Routes | Create backend API endpoints |
| Server Components | Render components on the server |
| Client Components | Handle browser interactions and React hooks |
| SSR | Server-Side Rendering |
| SSG | Static Site Generation |
| ISR | Incremental Static Regeneration |
| Middleware / Proxy | Process requests before they reach route handlers |
| Metadata API | Manage SEO titles and descriptions |
| Route Handlers | Create API endpoints using `route.js` or `route.ts` |
| Loading UI | Display loading screens while content loads |
| Error Handling | Handle application errors |
| Layouts | Share UI across multiple pages |

## 13. Pages Router vs App Router

Next.js supports two routing systems.

| Pages Router | App Router |
|---|---|
| `pages/` directory | `app/` directory |
| `next/router` | `next/navigation` |
| `next/head` | Metadata API |
| API Routes | Route Handlers |
| `_app.js` | `layout.js` |
| `_document.js` | Custom document handling is generally unnecessary |

## Conclusion

Next.js provides many built-in features to develop modern web applications.

The most commonly used features are:

1. `next/link` – Page navigation.
2. `next/navigation` – Routing and navigation.
3. `next/image` – Image optimization.
4. `next/script` – Script loading.
5. `next/font` – Font optimization.
6. `next/dynamic` – Dynamic component imports.
7. `next/headers` – Access cookies and headers.
8. `next/server` – Server-side request handling.
9. `next/cache` – Caching and revalidation.

**Important:** These are built-in Next.js modules and features. You don't need to install each one separately. They are available through the `next` package.