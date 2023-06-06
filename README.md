# react-vite deploy in github pages

1. Open terminal

2. Create react app using vite:

   `npm create vite@latest react-vite-app --template react`

3. Set the correct `base` in `vite.config.js`

   // For example your repository is at https://kbbaldaniya.github.io/react-vite-demo/,
      then set base to `'/react-vite-demo/'`.

    `base: ‘/react-vite-demo/’`
    
4. Build the app:

   `npm run build`

5. Run app `npm run dev` and Commit the code in github repository.

6. Go to your GitHub Pages configuration in the repository settings page.
    - Choose the source of deployment as `GitHub Actions` this will lead you to `create a workflow` that builds and deploys your project.
    - Create `.yml` file of Simple workflow for deploying static content to GitHub Pages.

```ruby
- yml file

# Simple workflow for deploying static content to GitHub Pages
name: Deploy static content to Pages

on:
  # Runs on pushes targeting the default branch
  push:
    branches: ['main']

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# Sets the GITHUB_TOKEN permissions to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

# Allow one concurrent deployment
concurrency:
  group: 'pages'
  cancel-in-progress: true

jobs:
  # Single deploy job since we're just deploying
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
      - name: Set up Node
        uses: actions/setup-node@v3
        with:
          node-version: 18
          cache: 'npm'
      - name: Install dependencies
        run: npm install
      - name: Build
        run: npm run build
      - name: Setup Pages
        uses: actions/configure-pages@v3
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v1
        with:
          # Upload dist repository
          path: './dist'
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v1
```        
        

# Now Your Website Will Run On Github Pages :thumbsup:
# Take Live URl from `Github Pages` :smile:
        
