---
title: "Wordpress to Hugo"
description: "Steps involved migrating from Wordpress to Hugo"
tags: [ "wordpress", "hugo", "s3", "aws", "git" ]
date: "2016-05-28"
categories:
  - "writing"
---

The decision to move away from [Wordpress][3] was easy. It cost too much and the writing interface got in the way. Queue the discovery of [static site][4] generators. [Hugo][5] did what I needed and [AWS S3][6] meant I didn't have to run a server.

So what is Hugo?

> Hugo is a static HTML and CSS website generator written in Go.

The biggest selling point for me was Hugo is single blob with no external dependencies.

Setup was easy. Old posts were converted to markdown files. Some content was cut but the old [wordpress][7] site is still available. [Installation][8] was super quick but there's a few gotchas.

{{< highlight shell >}}
pkg install go
mkdir ~/go
echo 'export GOPATH=$HOME/go' > .zshrc
echo 'export PATH=$PATH:$GOPATH/bin' > .zshrc
go get -v github.com/spf13/hugo
{{< /highlight >}}

With Hugo installed I simply created a new site directory and move my converted posts into $your-blog/content.

{{< highlight shell >}}
hugo new site your-blog
hugo new post/wordpress-to-hugo.md
{{< /highlight >}}

Hugo doesn't ship with a default [theme][9] so you'll need to grab one before generating any content.

{{< highlight shell >}}
mkdir ~/your-blog/themes
cd ~/your-blog/themes
git clone https://github.com/crakjie/hugo-base-theme.git
{{< /highlight >}}

You can serve Hugo sites locally or simply run the command to generate site content.

{{< highlight shell >}}
gibson% hugo server --theme=hugo-base-theme
Started building site
0 of 1 draft rendered
0 future content
10 pages created
0 non-page files copied
1 paginator pages created
7 categories created
7 tags created
in 60 ms
Watching for changes in /home/zerocool/your-site/{data,content,layouts,static,themes}
Serving pages from memory
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
^C
gibson%
gibson% hugo
Started building site
0 of 1 draft rendered
0 future content
10 pages created
0 non-page files copied
1 paginator pages created
7 categories created
7 tags created
in 65 ms
{{< /highlight >}}

There's various hosting options for static sites. I chose S3 because I've already got some AWS services.

Here are the steps to S3 serving static site content.

* Create an [S3 bucket][10] matching your website URL
* Update [permissions][11] to allow access to your website.
* Redirect DNS to the S3 bucket URL.
* Upload your files using the Java GUI or [s3cmd][12].

{{< highlight shell >}}
s3cmd put -P --recursive /home/zerocool/your-blog/public/ s3://your-site-url.com
{{< /highlight >}}

Hugo works for me. The process of writing markdown using vim enjoyable and distraction free. The next challenge is automating the publishing process.

[1]: http://blog.network2501.com/2016/05/28/wordpress-to-hugo/#disqus_thread
[2]: http://blog.network2501.com/categories/writing
[3]: https://wordpress.com
[4]: https://www.staticgen.com/
[5]: https://gohugo.io/
[6]: https://aws.amazon.com/s3
[7]: https://project0x9c5.wordpress.com/
[8]: https://gohugo.io/overview/quickstart/
[9]: http://themes.gohugo.io/
[10]: http://docs.aws.amazon.com/AmazonS3/latest/dev/HowDoIWebsiteConfiguration.html
[11]: http://docs.aws.amazon.com/AmazonS3/latest/dev/WebsiteAccessPermissionsReqd.html
[12]: http://s3tools.org/s3cmd

