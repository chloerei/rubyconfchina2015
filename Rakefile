task :default => :build

desc "prepare"
task :prepare do
  mkdir_p "build/reveal.js"
  cp_r Dir["vendor/reveal.js/{css,js,lib,plugin}"], "build/reveal.js"
  cp_r "images", "build"
end

desc "Build presentation"
task :build => [:clean, :prepare] do
  sh "bundle exec asciidoctor -T vendor/asciidoctor-reveal.js/templates/slim/ -D build index.adoc"
end

desc "Clean build"
task :clean do
  rm_r Dir["build/*"]
end

desc "Deploy to github pages"
task :deploy => :build do
  repo_url = `git config --get remote.origin.url`

  if repo_url.empty?
    raise "Unknow git remote origin url"
  end

  chdir "build" do
    rm_rf ".git"
    sh "git init"
    sh "git add ."
    sh "git commit -m 'Deploy'"
    sh "git remote add origin #{repo_url}"
    sh "git push -f origin master:gh-pages"
  end
end
