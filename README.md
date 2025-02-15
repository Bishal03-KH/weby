git init
   git add .
   git commit -m "Initial commit"
   git remote add origin <your-github-repo-url>
   git push -u origin main
   ```

2. Deploy to Vercel:
   1. Go to [Vercel](https://vercel.com) and sign up/login with your GitHub account
   2. Click "Import Project" or "New Project"
   3. Choose "Import Git Repository" and select your GitHub repository
   4. Configure the project:
      - Framework Preset: Other
      - Root Directory: ./
      - Build Command: `npm run build`
      - Output Directory: `dist/public`
   5. Environment Variables:
      - Add your `DATABASE_URL` in the project settings
      - This should be your production database URL
   6. Click "Deploy"

3. After Deployment:
   - Vercel will provide you with a production URL (example: your-app.vercel.app)
   - Each push to the main branch will trigger automatic deployments
   - You can add a custom domain in project settings

## Development

1. Clone the repository:
   ```bash
   git clone <your-repo-url>
   cd <repo-name>
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Create a `.env` file in the root directory and add:
   ```
   DATABASE_URL=your_postgresql_database_url
   ```

4. Start the development server:
   ```bash
   npm run dev
   ```

The app will be available at `http://localhost:5000`

## Project Structure

```
├── client/           # Frontend React application
├── server/           # Backend Express server
├── shared/           # Shared types and utilities
└── public/           # Static assets
```

## Features
- 🎨 Modern and clean design
- 🌓 Dark/Light mode
- 📱 Fully responsive
- ⚡ Fast and optimized
- 💌 Contact form
- 🎭 Beautiful animations

## Local Development

1. Clone the repository:
   ```bash
   git clone <your-repo-url>
   cd <repo-name>
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Create a `.env` file in the root directory and add your database URL:
   ```
   DATABASE_URL=your_postgresql_database_url
   ```

4. Push the database schema:
   ```bash
   npm run db:push
   ```

5. Start the development server:
   ```bash
   npm run dev
   ```

The app will be available at `http://localhost:5000`.


## Deploying to GitHub Pages
1. Update `vite.config.ts` to include your repository name as the base URL if you're deploying to GitHub Pages:
   ```ts
   base: '/your-repo-name/'
   ```

2. Create `.github/workflows/deploy.yml` with the following content:
   ```yaml
   name: Deploy to GitHub Pages

   on:
     push:
       branches: [ main ]

   jobs:
     build-and-deploy:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v2
         - name: Install Dependencies
           run: npm install
         - name: Build
           run: npm run build
         - name: Deploy to GitHub Pages
           uses: JamesIves/github-pages-deploy-action@4.1.5
           with:
             branch: gh-pages
             folder: dist