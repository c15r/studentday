# Student Day
Cloud solutions are much like cooking: you need the right ingredients and the expertise to combine them perfectly. With our Cloud Services, we offer both to our customers. Be it as Private Cloud Solutions in our own datacenters or on the Global Public Clouds together with our partners Amazon Web Services (AWS) and Microsoft Azure. In this workshop, you can make your own first steps towards the Cloud by starting your personal blog and right away deploy it to AWS.


# Your personal blog
Alright, let's get started. In the step by step guide below, you will create your first static site based on [hugo](https://gohugo.io/), push it to [GitHub](https://github.com/), and deploy it with [AWS Amplify](https://aws.amazon.com/amplify/).


## Step 1: Setup Hugo

Install Hugo using the guide for your platform (macOS, Windows, Linux, ...)

https://gohugo.io/getting-started/installing

```bash
# Test if everything is alright
$ hugo version

# Example output
hugo v0.96.0-2fd4a7d3d6845e75f8b8ae3a2a7bd91438967bbb+extended linux/amd64 BuildDate=2022-03-26T09:15:58Z VendorInfo=gohugoio
```


## Step 2: Start you first site

After you have successfully installed Hugo, we can use the handy `hug new site` command to start our personal blog project.
Go to a directory you want to work on and simply type the below commands. Replace *yourblog* with your personal project name.

```bash
# Initialize your site
$ hugo new site yourblog

# Change to the newly created directory
$ cd yourblog
```


## Step 3: Choose and configure your theme

In the current workshop we will work with the [hugo-coder](https://github.com/luizdepra/hugo-coder) theme.
However, there are many more themes at https://themes.gohugo.io.
```bash
# Initialize a new git repository
$ git init

# Configure your theme. Find more themes on https://themes.gohugo.io/
git submodule add https://github.com/luizdepra/hugo-coder.git themes/hugo-coder
```

Configure your theme by opening `config.toml` file in the root directory of our site.
Start based on the config below and customize the params.

Note: the config below is dependant on the chosen theme. In case you've chosen another theme than hugo-coder, you will have to adapt parts of the config.

```toml
baseURL = "http://www.swisscom.com"
languageCode = "en-us"
title = "Swisscom Student Day"
theme = "hugo-coder"

paginate = 20
enableEmoji = true

pygmentsStyle = "monokai"
pygmentsCodeFences = true
pygmentsCodeFencesGuessSyntax = true

[taxonomies]
  category = "categories"
  series = "series"
  tag = "tags"
  author = "authors"

[params]
  author = "Swisscom Student Day 2022"
  info = "Deploy yourself to the Cloud!"
  description = "Example hugo site for the Cloud workshop"
  keywords = "blog,developer,personal"
  avatarurl = "images/avatar.png"
  since = 2022  
  colorScheme = "auto"
  hidecolorschemetoggle = false

# Social links
[[params.social]]
  name = "Github"
  icon = "fa fa-github fa-2x"
  weight = 1
  url = "https://github.com/swisscom"
[[params.social]]
  name = "Twitter"
  icon = "fa fa-twitter fa-2x"
  weight = 3
  url = "https://twitter.com/swisscom"

# Menu links
[[menu.main]]
  name = "Blog"
  weight = 1
  url  = "posts/"
[[menu.main]]
  name = "About"
  weight = 2
  url = "about/"
```


## Step 4: Create your first content

Use the `hugo new` command to create your first pages.

```bash
# Create your first post and add some content
$ hugo new posts/my-first-post.md
$ echo "# My First Post" >> content/posts/my-first-post.md

# Create a simple static page 
$ hugo new about.md
$ echo "# About Me" >> content/about.md
```

Note: the echo commands are meant as example. Use your favorite editor or IDE to edit the newly created markdown files.
Learn more about Markdown in the [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) or the [Markdown Guide](https://www.markdownguide.org/).


# Step 5: See how things look so far

Now that you've done the basic configurations and initialized your first pages, it's time to run the site.
Simply start a local webserver using the built in `hugo serve` command.

```bash
$ hugo serve -D
Start building sites …
...
Built in 69 ms
....
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

Open a browser and check out how things look like using the url listed as output.


## Step 6: Push your site to GitHub

Now it's time to push your blog project to 

1. Go to https://github.com and login with your personal user
   - In case you don't have a GitHub account yet, this is the time to create one :wink:
2. Create a new repository for your project: https://github.com/new
3. Just give it a name and leave the `README`, `.gitignore`, and `LICENSE` options empty

Manually create a .gitignore file in your project based on the following template:
```bash
# Generated files by hugo
/public/
/resources/_gen/
/assets/jsconfig.json
hugo_stats.json

# Executable may be added to repository
hugo.exe
hugo.darwin
hugo.linux

# Temporary lock file while building
/.hugo_build.lock
```

After you have initialized a `.gitignore` file, continue publishing your project:

```bash
# Add the .gitignore file
$ git add .gitignore

# Add all the other files you've created and commit them
$ git add .
$ git commit -m "My new blog project based on Hugo"

# Do some cosmetics, add the upstream repo, and push it remotely
$ git branch -M main
$ git remote add origin https://github.com/<your-user>/<your-repo>.git
$ git push -u origin main
```

## Step 7: Deploy to the Cloud with AWS Amplify

1. Go to https://aws.amazon.com
   - Either click on _Sign In_ and login with your personal AWS account
   - Or click on _Create an AWS Account_ and follow the wizzard
2. Navigate to the _AWS Amplify_ console or simply open https://eu-central-1.console.aws.amazon.com/amplify/home?region=eu-central-1&#/create
3. Choose _Host web app_
4. Add repository branch
   - Choose the in step 6 newly created repository
   - Select `main` as your branch
   - Click on _Next_
5. Configure build settings
   - Choose a suitable _App name_ for your project
   - The _Build and test settings_ should be autodetect. If not, use the settings below
     ```yaml
      version: 1
      frontend:
        phases:
          build:
            commands:
              - hugo
        artifacts:
          baseDirectory: public
          files:
            - '**/*'
        cache:
          paths: []
      ```
   - Unfold the _Advanced settings_ and click on _Add package version override_ in the _Live package updates_ section
   - Choose _Hugo_ and ensure that as _Version_ the value **latest** is set
   - Click on _Next_
5. Review your configuration and hit _Save and deploy_
6. Wait for the deployment pipeline to finish (Provision, Build, Deploy, Verify)
7. Click on the _URL_ shown in the Amplify console
8. Enjoy :smile:
