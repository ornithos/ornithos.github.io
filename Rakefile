require "rubygems"
require "tmpdir"

require "bundler/setup"
require "jekyll"


# modified from Octopress script: http://ixti.net/software/2013/01/28/using-jekyll-plugins-on-github-pages.html 
GITHUB_REPONAME = "ornithos/ornithos.github.io"


desc "Generate blog files"
task :generate do
  system("bundle exec jekyll serve")
end


desc "Generate and publish blog to gh-pages"
task :publish => [:generate] do
  Dir.mktmpdir do |tmp|
    cp_r "_site/.", tmp
    
    system "git checkout HEAD -- _site"   # this has been copied to tmpdir / need to revert for checkout.
    system "git checkout master"
    cp_r File.join(tmp, "."), "."
    message = "Site updated at #{Time.now.utc}"
    system "git add ."
    system "git commit -m #{message.inspect}"
    system "git push origin master"
    system "rm -r _site"         # ~ I guess dangerous, but in case jekyll serve is listening and created _site during this process.
    system "git checkout source"
  end
end

