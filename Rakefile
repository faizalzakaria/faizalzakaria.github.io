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

  desc "Generate and publish blog to s3"
  task :publish => [:generate] do
    puts `aws s3 sync _site s3://blog.codegarage.co --profile codegarage`
  end
end
