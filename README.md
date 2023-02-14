# BlogIt

![Screenshot_20230214_104709](https://user-images.githubusercontent.com/42029519/218647696-d9ae254f-f43a-4a50-9718-d3038a5dd56c.png)

## How to use

1. Star this repo 🌟 
1. Go to your repository
1. Add the following section to your **README.md** file, you can give whatever title you want. Just make sure that you use `<!-- blogs starts --><!-- blogs ends -->` in your readme. The workflow will replace this comment with the actual blog post list: 
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
      workflow_dispatch: # Run workflow manually through the GitHub Actions Workflow page directly
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

## Popular Sources 
<details>
  <summary>Some popular blogging platforms and their RSS feed URLs (Click to expand)</summary>

| Name                                                       | Feed URL                                                          | Comments                                                                                                                                                         | Example                                                                                                                           |
|------------------------------------------------------------|-------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| [Dev.to](https://dev.to/)                                  | `https://dev.to/feed/username`                                    | Replace username with your own username                                                                                                                          | https://dev.to/feed/gautamkrishnar                                                                                                |
| [Wordpress](https://wordpress.org/)                        | `https://www.example.com/feed/`                                   | Replace with your own blog url                                                                                                                                   | https://www.gautamkrishnar.com/feed/                                                                                              |
| [Medium](https://medium.com/)                              | `https://medium.com/feed/@username`                               | Replace username with your Medium username                                                                                                                       | https://medium.com/feed/@khaosdoctor                                                                                              |
| [Medium (Sub Domain)](https://medium.com/)                 | `https://username.medium.com/feed`                                | Replace username with your Medium username                                                                                                                       | https://timsneath.medium.com/feed                                                                                                 |
| [Stackoverflow](https://stackoverflow.com/)                | `https://stackoverflow.com/feeds/user/userid`                     | Replace with your StackOverflow [UserId](https://meta.stackexchange.com/questions/98771/what-is-my-user-id/111130#111130)                                        | https://stackoverflow.com/feeds/user/5283532                                                                                      |
| [StackExchange](https://stackexchange.com/)                | `https://subdomain.stackexchange.com/feeds/user/userid`           | Replace with your StackExchange [UserId](https://meta.stackexchange.com/questions/98771/what-is-my-user-id/111130#111130) and sub-domain                         | https://devops.stackexchange.com/feeds/user/15                                                                                    |
| [Ghost](https://ghost.org/)                                | `https://www.example.com/rss/`                                    | Replace with your own blog url                                                                                                                                   | https://blog.codinghorror.com/rss/                                                                                                |
| [Drupal](https://www.drupal.org/)                          | `https://www.example.com/rss.xml`                                 | Replace with your own blog url                                                                                                                                   | https://www.arsenal.com/rss.xml                                                                                                   |
| [Hugo](https://gohugo.io/)                                 | `https://BASE_URL/post/index.xml`                                  | Replace `BASE_URL`([doc](https://gohugo.io/getting-started/configuration/#baseurl)) with your blog url. Refer to the [official Hugo](https://gohugo.io/templates/rss/) or your theme documentation for more info | https://davidaparicio.gitlab.io/website/fr/post/index.xml
| [Youtube Playlists](https://www.youtube.com)               | `https://www.youtube.com/feeds/videos.xml?playlist_id=playlistId` | Replace `playlistId` with your own Youtube playlist id                                                                                                           | https://www.youtube.com/feeds/videos.xml?playlist_id=PLJNqgDLpd5E69Kc664st4j7727sbzyx0X                                           |
| [Youtube Channel Video list](https://www.youtube.com)      | `https://www.youtube.com/feeds/videos.xml?channel_id=channelId`   | Replace `channelId` with your own Youtube channel id                                                                                                             | https://www.youtube.com/feeds/videos.xml?channel_id=UCDCHcqyeQgJ-jVSd6VJkbCw                                                      |
| [Anchor.fm Podcasts](https://anchor.fm/)                   | `https://anchor.fm/s/podcastId/podcast/rss`                       | You can get the rss feed url of a podcast by following [these](https://help.anchor.fm/hc/en-us/articles/360027712351-Locating-your-Anchor-RSS-feed) instructions | https://anchor.fm/s/1e784a38/podcast/rss                                                                                          |
| [Hashnode](https://hashnode.com/)                          | `https://@username.hashnode.dev/rss.xml`                          | Replace @username with your Hashnode username                                                                                                                    | https://polilluminato.hashnode.dev/rss.xml                                                                                        |
| [Google Podcasts](https://podcasts.google.com/)            | `https://podcasts.google.com/feed/channelId`                      | Replace `channelId` with your Google podcast channel Id                                                                                                          | https://podcasts.google.com/feed/aHR0cHM6Ly9mZWVkcy5zb3VuZGNsb3VkLmNvbS91c2Vycy9zb3VuZGNsb3VkOnVzZXJzOjYyOTIxMTkwL3NvdW5kcy5yc3M= |
| [Reddit](https://www.reddit.com/)                          | `http://www.reddit.com/r/topic/.rss`                              | You can create an RSS feed by adding '.rss' to the end of an existing Reddit URL. Replace `topic` with SubReddit topic that interest you or localized to you.    | http://www.reddit.com/r/news/.rss                                                                                                 |
| [Analytics India Magazine](https://analyticsindiamag.com/) | `https://analyticsindiamag.com/author/author_name/feed/`          | Replace `author_name` with your name                                                                                                                             | https://analyticsindiamag.com/author/kaustubhgupta1828gmail-com/feed/                                                             |
| [Feedburner](https://feedburner.com/)                      | `https://feeds.feedburner.com/feed_address`                       | Replace `feed_address` with your Feedburner feed address                                                                                                         | https://feeds.feedburner.com/darkwood-fr/blog                                                                                     |
| [Tumblr](https://www.tumblr.com)                           | `https://blog_name.tumblr.com/rss` or `https://example.com/rss`   | You can create an RSS feed by adding '/rss' to your main blog page or to your own domain if it is configured. Replace `blog_name` with your blog name            | https://goggledoddle.tumblr.com/rss                                                                                               |
| [Blogger](https://www.blogger.com/)                        | `https://blog_name.blogspot.com/feeds/posts/default`              | Replace `blog_name` with your blog subdomain                                                                                                                     | https://singlebucks.blogspot.com/feeds/posts/default                                                                              |
| [Velog](https://velog.io/)                                 | `https://v2.velog.io/rss/userid`                                  | Replace `userid` with your  user id (without the @ symbol)                                                                                                       | https://v2.velog.io/rss/minnczi                                                                                                   |
| [Shouts.dev](https://shouts.dev/)                          | `https://shouts.dev/feed/username`                                | Replace `username` with your own username                                                                                                                        | https://shouts.dev/feed/obydul                                                                                                    |

</details>

## Options

This workflow has additional options that you can use to customize it for your use case. The following are the list of options available:

| Option                       | Default Value                                                                | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Required |
|------------------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| `url` | `""` | RSS url to fetch events from, eg: `https://example1.com`| Yes |
| `max_number_of_posts` | `5` | Max number of posts to fetch from the RSS feed| No |
| `target_md` | `README.md` | Path to .md file to update| No |
| `gh_token` | your GitHub token with repo scope | Use this to configure the token of the user that commits the workflow result to GitHub 


## Examples 
* [My own GitHub profile readme](https://github.com/Azanul) - [YML File](https://github.com/Azanul/Azanul/blob/master/.github/workflows/blog-it.yml)

## ToDo
- [ ] Catch up with [Blog post workflow](https://github.com/gautamkrishnar/blog-post-workflow)

### 💡 Shoutout to [Gautam krishna R](https://github.com/gautamkrishnar) for creating [Blog post workflow](https://github.com/gautamkrishnar/blog-post-workflow), the inspiration for this action
