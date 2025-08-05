# Yulistic's Personal Website

This is a personal website built with [Hugo](https://gohugo.io/) and hosted on GitHub Pages.

## Building locally

To work locally with this project, you'll have to follow the steps below:

1. Clone this repository
2. [Install Hugo](https://gohugo.io/installation/)
3. Preview your project: `hugo server`
4. Add content
5. Generate the website: `hugo` (optional)

Read more at Hugo's [documentation](https://gohugo.io/documentation/).

### Preview your site

If you clone this project to your local computer and run `hugo server`,
your site can be accessed under `localhost:1313/`.

## GitHub Pages Deployment

This site is automatically deployed to GitHub Pages using GitHub Actions. The deployment workflow is triggered on every push to the `master` branch.

The workflow:
1. Builds the Hugo site
2. Deploys to GitHub Pages

## Configuration

The site configuration is stored in `config.toml`. Key settings include:

- `baseurl`: Set to your GitHub Pages URL (`https://username.github.io/`)
- `theme`: Currently using the `hyde-y` theme
- Social links and other personal information

## Content Management

- Blog posts are stored in `content/post/`
- Static files (images, PDFs) are in `static/`
- Site data is in `data/`

## Theme

This site uses a customized version of the [Hyde-Y](https://github.com/enten/hyde-y) theme for Hugo.

## License

This project is licensed under the terms specified in the LICENSE file.