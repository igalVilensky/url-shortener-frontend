🌐 URL Shortener Frontend
A sleek and modern frontend for the URL Shortener project, built with Nuxt 3 and Tailwind CSS. It connects to a Node.js + Express + MongoDB Atlas backend hosted on Render.

🚀 Features

🔗 Shorten URLs: Input any long URL to get a compact, shareable link.
📋 Easy Copy: Copy shortened URLs with a single click.
📊 View Stats: Track click statistics for all shortened links.
📱 Responsive Design: Mobile-friendly UI powered by Tailwind CSS.

🛠️ Tech Stack

Technology
Description

Nuxt 3
Vue.js framework for SSR and static sites

Tailwind CSS
Utility-first CSS framework for styling

Backend API
Node.js + Express + MongoDB Atlas on Render

Netlify
Hosting platform for the frontend

⚙️ Project Setup
Prerequisites

Node.js: v16 or higher
npm: Package manager
Git: Version control

Installation

Clone the repository
git clone https://github.com/igalVilensky/url-shortener-frontend.git
cd url-shortener-frontend

Install dependencies
npm install

Configure API URLCreate a .env file in the root directory:
NUXT_PUBLIC_API_URL=https://url-shortener-lzgh.onrender.com

Replace with your actual backend API URL.

Run locally
npm run dev

Open http://localhost:3000 in your browser.

Build for production
npm run build

🌍 Deployment (Netlify)

Push your code to a GitHub repository.
Go to Netlify and select New site from Git.
Connect your GitHub repository.
Configure build settings:
Build command: npm run build
Publish directory: .output/public

Add the environment variable in Netlify:
Key: NUXT_PUBLIC_API_URL
Value: https://url-shortener-lzgh.onrender.com (or your backend URL)

Deploy the site to get a live URL! 🎉

📸 Demo

Backend API: Render Service
Frontend App: Netlify Live Site (Update with your Netlify URL)

📝 License
This project is licensed under the MIT License.
🙌 Contributing
Contributions are welcome! Please open an issue or submit a pull request on GitHub.
