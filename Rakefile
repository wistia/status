# http://mikeferrier.com/2011/04/29/blogging-with-jekyll-haml-sass-and-jammit/
desc "Pre Jekyll rendering stuff"
task :pre_jekyll do
  puts "Doing pre-Jekyll schtuffs ..."

  print "  Compiling the compass ... "
  system "compass compile"
  puts "done."

  print "  Rendering Haml layouts ... "
  system(%{
    cd _layouts/haml &&
    for f in *.haml; do [ -e $f ] && haml $f ../${f%.haml}.html; done
  })
  puts "done."

  print "  Rendering Haml includes ... "
  system(%{
    cd _includes/haml &&
    for f in *.haml; do [ -e $f ] && haml $f ../${f%.haml}.html; done
  })
  puts "done."

  puts "All done."

end

desc "Launch preview environment"
task :preview => :pre_jekyll do
  system "foreman start"
end

desc "Build the site"
task :build => :pre_jekyll do
  system "bundle exec jekyll build"
end

# add a title to a post like np title="Blah this is my title"
desc "Create a new blog post"
task :np do

  content = ENV["content"] || "new update"
  title = ENV["title"] || "new-post"
  slug = title.downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '')

  puts "creating a new post, entitled #{title}"

  path = "_posts/#{ Date.today }-#{ slug }.md"

  if File.exist?(path)
  	puts "[WARN] File exists - skipping create"
  else
    File.open(path, "w") do |post|
      post.puts "---"
      post.puts "layout: post"
      post.puts "title: \"#{ title.gsub(/-/, ' ')}\""
      post.puts "---"
      post.puts content
    end
  end

  exit 1

end
