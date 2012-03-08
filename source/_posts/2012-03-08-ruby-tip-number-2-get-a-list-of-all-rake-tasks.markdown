---
layout: post
title: "Ruby Tip #2: Get a List of All Rake Tasks"
date: 2012-03-08 15:28
comments: true
categories:
- Ruby
- Tip
---

Many people are having trouble remembering all the rake tasks defined
in a particular project's `Rakefile` (especially if they hadn't
authored it). This is quite normal given the fact that Rails's
Rakefile, for instance, defines 39 tasks (as of version
3.2.2). Personally I never memorize anything, but the most basic rake
tasks - for everything else there is the `rake -T` (or `rake --tasks`)
command. Here's the command in action for Octopress's Rakefile:

```bash
$ rake -T
rake clean                 # Clean out caches: .pygments-cache, .gist-cache, .sass-cache
rake copydot[source,dest]  # copy dot files for deployment
rake deploy                # Default deploy task
rake gen_deploy            # Generate website and deploy
rake generate              # Generate jekyll site
rake install[theme]        # Initial setup for Octopress: copies the default theme into the path of Jekyll's generator.
rake integrate             # Move all stashed posts back into the posts directory, ready for site generation.
rake isolate[filename]     # Move all other posts than the one currently being worked on to a temporary stash location (stash) so regenerating the site happens much quicker.
rake list                  # list tasks
rake new_page[filename]    # Create a new page in source/(filename)/index.markdown
rake new_post[title]       # Begin a new post in source/_posts
rake preview               # preview the site in a web browser
rake push                  # deploy public directory to github pages
rake rsync                 # Deploy website via rsync
rake set_root_dir[dir]     # Update configurations to support publishing to root or sub directory
rake setup_github_pages    # Set up _deploy folder and deploy branch for Github Pages deployment
rake update_source[theme]  # Move source to source.old, install source theme updates, replace source/_includes/navigation.html with source.old's navigation
rake update_style[theme]   # Move sass to sass.old, install sass theme updates, replace sass/custom with sass.old/custom
rake watch                 # Watch the site and regenerate when it
changes
```

Not only did you get a list of all the tasks, but nice descriptions of
the tasks as well.
