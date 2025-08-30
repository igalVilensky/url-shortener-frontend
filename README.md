# 🌐 URL Shortener Frontend

A sleek and modern frontend for the **URL Shortener** project, built with **Nuxt 3** and **Tailwind CSS**. It connects to a Node.js + Express + MongoDB Atlas backend hosted on **Render**.

![Nuxt 3](https://img.shields.io/badge/Nuxt_3-00C58E?logo=nuxt.js&style=flat-square)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?logo=tailwind-css&style=flat-square)
![Netlify](https://img.shields.io/badge/Netlify-00C7B7?logo=netlify&style=flat-square)

## 🚀 Features
- 🔗 **Shorten URLs**: Input any long URL to get a compact, shareable link.
- 📋 **Easy Copy**: Copy shortened URLs with a single click.
- 📊 **View Stats**: Track click statistics for all shortened links.
- 📱 **Responsive Design**: Mobile-friendly UI powered by Tailwind CSS.

## 🛠️ Tech Stack
| Technology | Description |
|------------|-------------|
| [Nuxt 3](https://nuxt.com/) | Vue.js framework for SSR and static sites |
| [Tailwind CSS](https://tailwindcss.com/) | Utility-first CSS framework for styling |
| [Backend API](https://www.mongodb.com/atlas) | Node.js + Express + MongoDB Atlas on Render |
| [Netlify](https://www.netlify.com/) | Hosting platform for the frontend |

## ⚙️ Project Setup

### Prerequisites
- **Node.js**: v16 or higher
- **npm**: Package manager
- **Git**: Version control

### Installation
1. **Clone the repository**
   ```bash
   git clone https://github.com/igalVilensky/url-shortener-frontend.git
   cd url-shortener-frontend
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Configure API URL**
   Create a `.env` file in the root directory:
   ```env
   NUXT_PUBLIC_API_URL=https://url-shortener-lzgh.onrender.com
   ```
   Replace with your actual backend API URL.

4. **Run locally**
   ```bash
   npm run dev
   ```
   Open `http://localhost:3000` in your browser.

5. **Build for production**
   ```bash
   npm run build
   ```

## 🌍 Deployment (Netlify)
1. Push your code to a GitHub repository.
2. Go to [Netlify](https://www.netlify.com/) and select **New site from Git**.
3. Connect your GitHub repository.
4. Configure build settings:
   - **Build command**: `npm run build`
   - **Publish directory**: `.output/public`
5. Add the environment variable in Netlify:
   - Key: `NUXT_PUBLIC_API_URL`
   - Value: `https://url-shortener-lzgh.onrender.com` (or your backend URL)
6. Deploy the site to get a live URL! 🎉

## 📸 Demo
- **Backend API**: [Render Service](https://url-shortener-lzgh.onrender.com)
- **Frontend App**: [Netlify Live Site](#) (Update with your Netlify URL)

## 📝 License
This project is licensed under the [MIT License](LICENSE).

## 🙌 Contributing
Contributions are welcome! Please open an issue or submit a pull request on [GitHub](https://github.com/igalVilensky/url-shortener-frontend).