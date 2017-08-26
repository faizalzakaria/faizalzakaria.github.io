require "rubygems"
require "tmpdir"

require "bundler/setup"
require "jekyll"

GITHUB_REPONAME = "faizalzakaria/faizalzakaria.github.io"

namespace :site do
  desc "Generate blog files"
  task :generate do
    Jekyll::Site.new(Jekyll.configuration({
      "source"      => ".",
      "destination" => "_site"
    })).process
  end

  desc "Generate and publish blog to CodeGarage.co"
  task :publish => [:generate] do
    system 'git checkout master'
    system 'git branch'
    Dir.chdir '_site'
    system "git add ."
    message = "Site updated at #{Time.now.utc}"
    system "git commit -m #{message.inspect}"
    system "git remote add origin git@github.com:#{GITHUB_REPONAME}.git"
    system "git push origin master:refs/heads/master --force"
    system 'git branch'
    system 'git checkout source'
  end
end
