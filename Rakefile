require "rubygems"
require "tmpdir"
require "bundler/setup"
require "jekyll"

# Indiquez le nom de votre dépôt
GITHUB_REPONAME = "aboddeti/aboddeti.github.io"
TMP = "../aboddeti.github.io/"

namespace :site do
  desc "Generating site files"
  task :generate do
    Jekyll::Site.new(Jekyll.configuration({
      "source"      => ".",
      "destination" => "_site"
    })).process
  end

desc "Generation and publication on GitHub"
task :publish => [:generate] do
  cp_r "_site/.", TMP
  pwd = Dir.pwd
  Dir.chdir TMP
  File.open(".nojekyll", "wb") { |f| f.puts("Locallly generated site.") }

    system "git pull"
    system "git add ."
    message = "Site updates on #{Time.now.utc}"
    system "git commit -m #{message.inspect}"
    system "git push -u origin master"
    Dir.chdir pwd
  end
end

