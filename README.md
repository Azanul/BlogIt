# BlogIt

![Screenshot_20230214_104709](https://user-images.githubusercontent.com/42029519/218647696-d9ae254f-f43a-4a50-9718-d3038a5dd56c.png)

## How to use

1. Star this repo 😉 
1. Go to your repository
1. Add the following section to your **README.md** file, you can give whatever title you want. Just make sure that you use `<!-- BLOG-POST-LIST:START --><!-- BLOG-POST-LIST:END -->` in your readme. The workflow will replace this comment with the actual blog post list: 
    ```markdown
    ## 📘 Latest Blogs
    <!-- blogs starts -->
    <!-- blogs ends -->
    ```
1. Create a folder named `.github` and create a `workflows` folder inside it, if it doesn't exist.
1. Create a new file named `blog-it.yml` with the following contents inside the workflows folder:
    ```yaml
    name: Blog It workflow
    on:
      schedule: # Run workflow automatically
        - cron: '0 * * * *' # Runs every hour, on the hour
      workflow_dispatch: # Run workflow manually (without waiting for the cron to be called), through the GitHub Actions Workflow page directly
    permissions:
      contents: write # To write the generated contents to the readme
    
    jobs:
      update-readme-with-blog:
        name: Update this repo's README with latest blog posts
        runs-on: ubuntu-latest
        steps:
          - name: Blog_It
            uses: Azanul/BlogIt@v1
            with:
              url: https://blog.azanulhaque.tech/rss.xml
    ```
1. Replace the above URL list with your own RSS feed URLs. See [popular-sources](#popular-sources) for a list of common RSS feed urls.
1. Commit and wait for it to run automatically, or you can also trigger it manually to see the result instantly.
