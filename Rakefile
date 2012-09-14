require "rubygems"
require "haml"

DESC = "Created by awef."

rule ".svg" => "%{^svg/,src/}X.haml" do |a|
  haml = open(a.prerequisites[0]).read

  html = Haml::Engine.new(haml).render

  File.open a.name, "w+" do |f|
    f.write(html)
  end
end

task :default => [
  :haml_to_svg,
  "index.html"
]

lambda {
  directory "svg"

  list = ["svg"]

  FileList["src/*.haml"].each {|a|
    list.push(a.sub(/^src\//, "svg/").sub(/\.haml$/, ".svg"))
  }

  task :haml_to_svg => list
}.call()

file "index.html" => FileList["svg/*.svg"].include("index.haml") do
  HAML_TEMPLATE = open("index.haml").read

  haml_var = {
    "svg_list" => FileList["svg/*.svg"]
  }

  html = Haml::Engine.new(HAML_TEMPLATE).render(Object.new, haml_var)

  File.open "index.html", "w+" do |f|
    f.write(html)
  end
end
