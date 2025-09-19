VitePress
This guide will walk you through how to integrate Decap CMS with VitePress. If you are using VuePress you can also the VuePress template.

To use the vite-plugin-decap-cms plugin, follow the plugin setup instructions. The plugin will simplify the configuration for you.

Setting up VitePress
See the VitePress prerequisites for the minimum Node version supported.

Install VitePress using the package manager of your choice:

npm install --save-dev vitepress
Follow the VitePress documentation to configure VitePress or use the setup wizard:

npx vitepress init
Setting up Decap CMS
In the public directory, create a new directory /admin/. Inside that directory, you will have to create two files, config.yml and index.html. For this guide you can use the example index.html from the Decap CMS installation:

<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Content Manager</title>
    <!-- Include the script that enables Netlify Identity on this page. -->
    <script src="https://identity.netlify.com/v1/netlify-identity-widget.js"></script>
  </head>
  <body>
    <!-- Include the script that builds the page and powers Decap CMS -->
    <script src="https://unpkg.com/decap-cms@^3.0.0/dist/decap-cms.js"></script>
  </body>
</html>
For your config.yml file, you can put in a starter config:

backend:
  name: git-gateway
  branch: main # Branch to update (optional; defaults to master)

media_folder: public/img
public_folder: /img

collections:
  - name: 'guide'
    label: 'Guide'
    folder: 'guide'
    create: true
    slug: '{{slug}}'
    editor:
      preview: false
    fields:
      - { label: 'Title', name: 'title', widget: 'string' }
      - { label: 'Description', name: 'description', widget: 'string' }
      - { label: 'Body', name: 'body', widget: 'markdown' }
This example only includes the frontmatter included in all themes. You can visit the default theme reference for all frontmatter keys for the default theme.

For VitePress you will need to add {target="_self"} to all admin links since the Decap CMS page is a non-VitePress page.

Pushing to GitHub
It's now time to commit your changes and push to GitHub.

git init
git add .
git commit -m "Initial Commit"
git remote add origin https://github.com/YOUR_USERNAME/NEW_REPO_NAME.git
git push -u origin main
Deploying with Netlify
Go to Netlify and select 'New Site from Git'. Select GitHub and the repository you just pushed to. Click Configure Netlify on GitHub and give access to your repository. Finish the setup by clicking Deploy Site. Netlify will begin reading your repository and starting building your project.
