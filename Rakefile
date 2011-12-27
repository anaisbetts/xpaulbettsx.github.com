require 'rubygems'
require 'rake'
require 'fileutils'

RootDir = File.dirname(__FILE__)

desc "Draft a new post"
task :new do
  puts "What should we call this post for now?"
  name = STDIN.gets.chomp
  FileUtils.touch("drafts/#{name}.md")

  open("drafts/#{name}.md", 'a') do |f|
    f.puts "---"
    f.puts "layout: post"
    f.puts "title: \"DRAFT: #{name}\""
    f.puts "---"
  end
end

desc "Startup Jekyll"
task :start do
  sh "jekyll --server --pygments"
end

task :check do
  sh "jekyll --no-server --no-auto"
end

task :deploy do
  sh "rm -rf #{RootDir}/.deploy && mkdir #{RootDir}/.deploy"
  sh "jekyll #{RootDir}/.deploy --no-server --no-auto --pygments"
  sh "rm -rf #{RootDir}/.deploy_prod"
  sh "git clone git@github.com:xpaulbettsx/xpaulbettsx.github.com.git #{RootDir}/.deploy_prod"
  sh "rsync -avlp --delete --exclude=.git #{RootDir}/.deploy/ #{RootDir}/.deploy_prod"
  sh "cd #{RootDir}/.deploy_prod && git add . && git ci -m \"Publish on `date`\" && git push"
end

task :default => :start
